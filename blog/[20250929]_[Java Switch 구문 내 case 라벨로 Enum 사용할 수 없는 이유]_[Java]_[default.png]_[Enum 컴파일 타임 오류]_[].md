# Using Enum at compile time

### 자바 예시 코드
```Java
package com.slp.module.ifs.outbound.sender;

public enum ResultEnum {

    WAIT("W"),
    READY("R"),
    SUCCESS("S"),
    FAIL("F"),

    STATE("state"),
    ERROR("error"),
    MESSAGE("message"),
    SUCCESS_MSG("success"),
    FAIL_MSG("fail");

    private final String value;

    ResultEnum(String value) {
        this.value = value;
    }

    public String code() {
        return value;
    }

    public Integer parseInt() {
        return Integer.parseInt(value);
    }

}

```


You cannot use ResultEnum.STATE.code() directly in a case label because case labels require constant expressions known at compile time. Method calls like .code() are not compile-time constants, even if they return a String. Only string literals or static final constants are allowed in case labels.

Switch 구문의 case 라벨의 경우 컴파일 시점에 알 수 있는 constant를 요구한다. 그러나 Enum 내부에 선언한 code() 메서드의 경우 컴파일 시점에 알 수 없으므로 case 라벨에 직접 사용 불가능.

