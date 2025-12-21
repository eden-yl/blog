## flushCache 옵션

### Example code
```XML
<!-- This insert statement will flush the cache after execution (default behavior for inserts) -->
<insert id="insertUser" ... flushCache="true">
    ...
</insert>

<!-- This select statement will flush the cache every time it is called -->
<select id="selectLatestData" resultType="map" flushCache="true">
    ...
</select>

<!-- Default for select: flushCache="false" and useCache="true" (if 2nd level cache is enabled) -->
<select id="selectUserData" resultType="User">
    ...
</select>

```

```java
import org.apache.ibatis.annotations.Options;
import org.apache.ibatis.annotations.Select;

public interface MyMapper {

    @Select("SELECT * FROM users WHERE id = #{id}")
    @Options(flushCache = true)
    User selectUserAndFlushCache(int id);
}

```

### Key Points
Cache Levels: It affects both the local session cache (scoped to a single SqlSession) and the second-level cache (scoped to the entire SqlSessionFactory).

Purpose: It is essential when you need to ensure that subsequent queries retrieve the absolute latest data from the database, bypassing any stale cache entries.

Default Behavior: Update, insert, and delete operations inherently flush the cache to maintain data consistency. Select operations do not, by default.

Alternative Control: You can also control the local cache scope by setting the localCacheScope in the MyBatis configuration to STATEMENT, which effectively disables the local cache for the duration of the statement. 
