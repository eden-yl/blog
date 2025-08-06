# JPA Entity IdClass 지정 방법

* IdClass?


```Java

@Getter
@Entity
public class EmployeeEntity {

    @Id
    @Column(name = "ID")
    private Long id;

    @Column(name = "EMP_NO")
    private Long empNo;

    @Column(name = "DEPT_ID")
    private String deptId;

    // 생략...
}

```

