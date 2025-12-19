## Method invoked

### Example code
```java
import java.lang.reflect.Method;

public class ReflectionExample {
    public void targetMethod(String param1, int param2) {
        System.out.println("Method invoked with: " + param1 + " and " + param2);
    }

    public static void main(String[] args) throws Exception {
        // 1. Get the Class object
        Class<?> clazz = ReflectionExample.class;
        // Or Class.forName("ReflectionExample");

        // 2. Get the Method object by name and parameter types
        // The parameters are the class types of the arguments (String.class, int.class)
        Method method = clazz.getMethod("targetMethod", String.class, int.class);

        // 3. Create an instance of the class to invoke the method on
        Object instance = clazz.getDeclaredConstructor().newInstance();

        // 4. Invoke the method with the instance and arguments
        Object result = method.invoke(instance, "Hello", 123);
        
        // If the method has a return value, it can be cast from the result object
        // Object result = method.invoke(instance, "Hello", 123);
    }
}


```