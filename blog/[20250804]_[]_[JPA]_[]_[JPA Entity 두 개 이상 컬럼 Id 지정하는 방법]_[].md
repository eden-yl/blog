# JPA Entity IdClass 지정 방법

* IdClass?

일반적인 Long 타입 id로 key를 지정하는 엔티티 예시

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

