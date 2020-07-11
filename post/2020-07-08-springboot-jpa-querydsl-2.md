---
title: spring boot, jpa, querydsl 정리 - 2편 조인 예제 (연관관계 없음)
date: 2020-07-08 21:56:00 +/-TTTT
categories: [spring, jpa]
tags: [jpa]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


# 목차

- ### [spring boot, jpa, querydsl 정리 - 1편 환경 구성 (spring boot, jpa, querydsl, gradle, multi project)](https://leechoongyon.github.io/posts/springboot-jpa-querydsl-1)
- ### [spring boot, jpa, querydsl 정리 - 2편 조인 예제 (연관관계 없음)](https://leechoongyon.github.io/posts/springboot-jpa-querydsl-2)




---
## 조인 예제 (연관관계 없음)
- 서로 다른 두 테이블을 조인하는 예제. 조인해서 member id 로 조회.
- member 와 address 가 있으며, 둘은 1:1 라 가정.
 
###### Entity source
```java

public interface MemberRepositoryCustom {
    List<Member> findByTelNo(String telNo);
    MemberInfo findMemberInfo(String id);
}


@RequiredArgsConstructor
public class MemberRepositoryImpl implements MemberRepositoryCustom {

    private final JPAQueryFactory queryFactory;

    @Override
    public MemberInfo findMemberInfo(String id) {
        return queryFactory.select(Projections.bean(MemberInfo.class
                , member.as("member"), address.as("address")))
                .from(member)
                .join(address).on(member.addrId.eq(address.addrId))
                .where(member.id.eq(id))
                .fetchOne();
    }
}




@Entity
@NoArgsConstructor
@Getter
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private String id;

    @Column
    private String name;

    @Column
    private String telNo;

    @Column
    private int age;

    String addrId;

    @Builder
    public Member(String name, String telNo, int age, String addrId) {
        this.name = name;
        this.telNo = telNo;
        this.age = age;
        this.addrId = addrId;
    }
}

----------------

@Entity
@Getter
@Setter
@NoArgsConstructor
public class Address {
    @Id
    private String addrId;

    @Column
    private String addr;

    @Builder
    public Address(String addrId, String addr) {
        this.addrId = addrId;
        this.addr = addr;
    }
}




@RunWith(SpringRunner.class)
@SpringBootTest
public class MemberRepositoryTest {

    @Autowired
    private MemberRepository memberRepository;

    @Autowired
    private AddressRepository addressRepository;

    @Test
    public void findMemberInfoTest() {
        String addrId = "11111";
        Member member = Member.builder()
                .telNo("010-1234-5678")
                .addrId(addrId)
                .age(20)
                .name("홍길동")
                .build();
        member = memberRepository.save(member);
        String memberId = member.getId();
        Address address = Address.builder()
                .addr("주소")
                .addrId(addrId).build();

        addressRepository.save(address);

        MemberInfo memberInfo = memberRepository.findMemberInfo(memberId);
        Assert.assertEquals(memberInfo.getMember().getId(), memberId);
        Assert.assertEquals(memberInfo.getMember().getAddrId(), memberInfo.getAddress().getAddrId());
    }
}

```


## 전체 source
- [spring-boot-jpa-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-jpa-example) 참고