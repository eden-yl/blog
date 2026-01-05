● SAP/WMS Integration Module Analysis

  Package Structure

  com.slp.module.ifs.sap
  ├── api/                          # REST API layer
  │   ├── common/dto/              # Response DTOs
  │   ├── common/error/            # Error mapping & classification
  │   ├── config/advice/           # Exception & response interceptors
  │   ├── config/filter/           # Auth & logging filters
  │   ├── domain/ddus/             # DDUS (WMS) domain controllers
  │   ├── domain/ddhq/             # DDHQ (Headquarters) domain
  │   ├── domain/obd/              # OBD (Outbound Delivery) domain
  │   ├── log/                     # Request/response logging
  │   └── mapper/                  # MyBatis mappers for logging
  ├── domain/obd/                  # Business logic layer
  │   ├── service/                 # OBD business services
  │   ├── mapper/                  # MyBatis mappers
  │   └── dto/                     # Domain DTOs
  ├── dto/                         # Shared DTOs
  ├── enums/                       # Shared enumerations
  └── utils/                       # Utility functions

  Total: ~54 Java files in a layered architecture

  ---
  Key Process Flows

  1. OBD Cancellation (SAP → WMS)

  DdusSapApiController → ObdCancelRequestService.validateRequest()
    → insertReceiveRows() (IFT_SAP_RECEIVE_OBD_CANCEL_REQUEST)
    → processBusiness() (query WMT_OB_OUTB_HR, update ORDER_DEL_SCD)
    → updateSuccess/updateError()

  2. OBD Validation During Shipping

  OutbOrderValidationService.validateIfNeeded()
    → Check system config USE_SAP_ORDER_VALID_CHECKER
    → Call SAP API based on order type (STO/OBD)
    → Validate line counts, products, quantities
    → Update ORDER_VALID_STATUS

  3. OBD Deletion (WMS → SAP)

  OutbOrderDeleteIfService.sendObdDelete()
    → Validate ORDER_DEL_SCD state
    → Call SAP delete API
    → Update status (SAP_DELETE_COMPLETED/FAILED)

  4. Request/Response Processing

  RestApiBasicAuthFilter (auth validation)
    → RestApiLoggingFilter (log req/res)
    → Controller execution
    → RestApiExceptionAdvice / RestApiSuccessAdvice (response wrapping)

  ---
  ⚠️ Identified Issues and Vulnerabilities

  CRITICAL

  | Issue               | Location                        | Risk                                      |
  |---------------------|---------------------------------|-------------------------------------------|
  | Plaintext passwords | RestApiProperties.java:37       | Credentials stored in config as plaintext |
  | Hardcoded user ID   | ObdReceiveController.java:32-33 | "hm_MIG" used for all audit trails        |

  HIGH

  | Issue                  | Location                              | Risk                                               |
  |------------------------|---------------------------------------|----------------------------------------------------|
  | Null pointer risk      | OutbOrderDeleteIfService.java:180-181 | SAP response structure changes = silent failures   |
  | OData injection        | SapUtils.java:9-10                    | wrapWithQuotes() doesn't escape special chars      |
  | Unchecked type casting | SapStoService.java:74-75              | @SuppressWarnings("unchecked") without validation  |
  | Raw body logging       | RestApiLoggingFilter.java:188         | If storeAuthorizationRaw: true, credentials logged |

  MEDIUM

  | Issue                        | Location                                | Risk                                     |
  |------------------------------|-----------------------------------------|------------------------------------------|
  | ThreadLocal leak             | RestApiLogContext.java:21               | Async processing may not clean up        |
  | Silent API errors            | OutbOrderValidationService.java:164-170 | safeFetchSap() swallows exceptions       |
  | Guard bypass                 | OutbOrderGuard.java:35                  | Config can disable guard without logging |
  | Loose exception handling     | IfErrorMapper.java:105-114              | Reflection errors silently ignored       |
  | Map.get() without null check | ObdCancelRequestService.java:180-181    | NPE risk on missing columns              |

  LOW

  | Issue               | Location                            | Risk                                    |
  |---------------------|-------------------------------------|-----------------------------------------|
  | Stub endpoints      | DdhqSapApiController.java           | Unimplemented functionality returns 200 |
  | TODO comments       | Multiple files                      | Production code with known issues       |
  | Magic strings       | OutbOrderValidationService.java:183 | Undocumented regex for normalization    |
  | No input validation | ObdReceiveController.java:27        | Raw body inserted without size check    |

  ---
  Recommendations (Priority Order)

  1. Immediate: Move passwords to secure vault (HashiCorp Vault, AWS Secrets Manager)
  2. High: Add null safety checks in SAP response parsing
  3. High: Implement proper OData parameter escaping in SapUtils
  4. Medium: Add audit logging for guard/feature flag bypasses
  5. Medium: Replace @SuppressWarnings("unchecked") with runtime type validation
  6. Low: Remove or implement stub endpoints in DdhqSapApiController