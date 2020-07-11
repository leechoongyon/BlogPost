---
title: jpa transaction 묶음
date: 2020-06-25 00:20:00 +/-TTTT
categories: [jpa]
tags: [jpa]     # TAG names should always be lowercase
---

 
## 시행 착오
- Spring, Spring Boot 의 시작점을 통해 시작하지 않는다면, @Transactional 어노테이션이 안먹는거 같음.
- 이를 통해 트랜잭션 매니저가 제대로 설정 안되면 위 @Transactional 이 적용안된 것을 알 수 있었음.
- 처음 내가 의도한 바는 repository interface 를 통해 @Transactional 로 묶는거였음. 근데 안묶임. WebService 만들 때는 잘 묶였는데 jpa 만 떼어다가 쓸려니 안먹힘.
- 추후 왜 @Transactional 이 안먹히는지 원인 파악 해보기.

## source
- EntityManager 생성은 spring-boot 의 AutoConfiguration 을 이용했고, EntityManagerFactory 를 가져와서 EntityManager 를 가져오도록 함.

```java
@Autowired
private EntityManagerFactory emf;

...
...

EntityManager em = emf.createEntityManager();
/** 트랜잭션 시작 */
em.getTransaction.begin();

... (1)
... (2)
... (3)

/** (1), (2), (3) 트랜잭션 묶임. */
em.getTransaction.commit();

```