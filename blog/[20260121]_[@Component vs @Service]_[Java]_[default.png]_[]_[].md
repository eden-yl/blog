 ### Can @Component and @Service are interchangeable?
 
 Yes — it will work. Both register a Spring bean and can be injected the same way, but they differ semantically.

- `@Component`  
  - Generic stereotype. Any Spring-managed component can use it.  
  - No special runtime behavior beyond bean registration.

- `@Service`  
  - Specialized stereotype that is itself a `@Component`.  
  - Communicates intent: this bean is part of the service layer.  
  - Useful for readability, documentation and for any tooling/AOP pointcuts that specifically target service beans.

- Related note: `@Repository` adds exception translation for persistence exceptions; `@Transactional` is unrelated and can be applied to any stereotype.

Recommendation: using `@Component` is fine technically. Prefer `@Service` when the class represents business/service logic (for clearer intent and possible pointcut/tooling matches).