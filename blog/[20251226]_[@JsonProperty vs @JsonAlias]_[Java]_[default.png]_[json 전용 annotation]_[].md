## @JsonProperty vs @JsonAlias

### The difference
In Jackson, the key difference is that @JsonProperty defines the single, logical name used for both serialization (Java object to JSON) and deserialization (JSON to Java object), while @JsonAlias specifies one or more alternative names that are only accepted during deserialization. 

### @JsonProperty vs. @JsonAlias
Feature 	@JsonProperty	@JsonAlias
Primary Use	Defines the primary JSON property name to use when converting between Java objects and JSON.	Defines one or more secondary, alternative names to accept from incoming JSON.
Serialization	The value specified in @JsonProperty is used as the key in the generated JSON output.	Aliases are ignored during serialization; only the actual field name or @JsonProperty name is used.

Deserialization	The field expects a JSON key matching the specified name (or the Java field name if not specified).	The field will also accept any of the names listed in @JsonAlias during the deserialization process.

Flexibility	Offers full control over property visibility and naming for both processes.	Primarily used for backward compatibility or handling JSON from different sources that may use varied naming conventions for the same data.

### Example
Consider a scenario where a Java object needs to handle an incoming JSON field that might be named producer, produced_by, or createdBy, but the Java field is consistently named producerName. 

```java
import com.fasterxml.jackson.annotation.JsonAlias;
import com.fasterxml.jackson.annotation.JsonProperty;

public class Product {
    private int id;

    @JsonProperty("producerName")
    @JsonAlias({"producer", "produced_by", "createdBy"})
    private String producerName;

    // Getters and setters
}
```

Deserialization: Incoming JSON with any of "producerName", "producer", "produced_by", or "createdBy" will successfully map to the producerName field.
Serialization: When this Java Product object is converted to JSON, the output will only use the key "producerName". 
