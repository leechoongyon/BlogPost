---
title: 2021-03-26 TIL
date: 2021-03-26 22:15:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
## Entity
- 테이블과 매칭되는 개념
- ORM 을 이루는 기반 개념 중 하나. 객체와 RDB 간 연결시켜주는 존재

## EntityManager
- 엔티티를 관리하는 역할을 한다.
- 엔티티 매니저 내부에는 영속성 컨텍스트가 있으며, 이를 통해 엔티티 관리.
- 여러 엔티티 매니저가 하나의 영속성 컨텍스트를 공유 가능
- EntityManager 는 Thread-Safe 를 보장해야 한다. 동일한 EntityManager 를 가지고 멀티 스레드 환경에서 호출한다면 데이터가 어떻게 변경될지 모름.

## 영속성 컨텍스트, dirty checking
- 잠깐 영속성 컨텍스트의 개념을 짚고 넘어가면 엔티티를 영구히 저장하는 공간
- 영속성 컨텍스트는 관리하고 있는 엔티티의 변화를 추적하고, 한 트랜잭션 내에서 변화가 일어나면 엔티티에 마킹한다. 그리고 트랜잭션이 끝나는 시점에 마킹한 것을 DB 에 반영해준다. 
    - 이를 dirty checking 이라 한다.
- 이렇게 dirty checking 을 함으로써 여러 이점이 있겠지만 영속성 컨텍스트가 중간에서 쿼리들을 모았다가 한 번에 반영해주니 리소스 감소가 있음.
    - 이를 쓰기 지연이라 함.
- 단, 영속성 컨텍스트 에서 관리 하지 않는 Entity 일 경우 위 동작을 안하겠지

## Spring 환경에서 동일 Transaction 에서의 EntityManager 와 다른 Transaction 에서의 EntityManager
- 동일 Transaction 에서 EntityManager 를 여러 번 호출해서 처리하면 같은 영속성 컨텍스트 에서 처리된다.
- 다른 Transaction 이라면 다른 영속성 컨텍스트에서 처리된다.
- 아래 예시를 보면 쉽게 알 수 있음. test 메소드를 보면 처음 findAll 을 한 뒤에, member 를 한 번 저장하고, 다시 findAll 을 하는 것이다.
    - test 메소드에 @Transactional 이 걸려있으면, 같은 영속성 컨텍스트에서 처리되기에 save 한 멤버가 조회가 된다.
    - test 메소드에 @Transactional 이 안걸려있으면, 같은 영속성 컨텍스트가 아니기에 save 한 멤버가 조회가 안된다.
- 결론을 얘기하면 Spring 에서 여러 EntityManager 가 같은 트랜잭션일 경우 같은 영속성 컨텍스트에 접근한다.  

```java
    // MemberService.java
    public List<Member> test() {
        List<Member> members = memberRepository2.findAll();
        members.forEach(member -> {
            log.info("before member : {}, order.size : {}", member, member.getOrders().size());
        });

        Long id = saveMember(Member.builder().name("test").build());

        members = memberRepository2.findAll();
        members.forEach(member -> {
            log.info("after member : {}, order.size : {}", member, member.getOrders().size());
        });

        return members;
    }   

    // MemberRepository2.java
    private final EntityManager em;

    public void save(Member member) {
        em.persist(member);
    }

    public Member findOne(Long id) {
        return em.find(Member.class, id);
    }

    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class)
                .getResultList();
    }

```

## Spring 환경 에서 EntityManager 는 Thread-Safe 한가?
- 아래 블로그 내용 결론만 정리하면 Spring 에서는 EntityManager 를 Proxy 를 통해 감싸며, EntityManager 메소드를 호출할 때마다 Proxy 를 통해 EntityManager 를 생성한다. 즉, Thread-Safe 하다.

```java
    // Create a new EntityManager for use within the current transaction.
		logger.debug("Opening JPA EntityManager");
		EntityManager em = null;

		// Sync 를 맞출 필요 없는 Transaction 이라면 EntityManager 를 UNSYNC 하게 만듬.  
		if (!synchronizedWithTransaction) {
			try {
				em = emf.createEntityManager(SynchronizationType.UNSYNCHRONIZED, properties);
			}
			catch (AbstractMethodError err) {
				// JPA 2.1 API available but method not actually implemented in persistence provider:
				// falling back to regular createEntityManager method.
			}
		}

		// Sync 처리해서 Transaction 을 만듬.
		if (em == null) {
			em = (!CollectionUtils.isEmpty(properties) ? emf.createEntityManager(properties) : emf.createEntityManager());
		}

		try {
			// Use same EntityManager for further JPA operations within the transaction.
			// Thread-bound object will get removed by synchronization at transaction completion.
			emHolder = new EntityManagerHolder(em);
			if (synchronizedWithTransaction) {
				Object transactionData = prepareTransaction(em, emf);
				TransactionSynchronizationManager.registerSynchronization(
						new TransactionalEntityManagerSynchronization(emHolder, emf, transactionData, true));
				emHolder.setSynchronizedWithTransaction(true);
			}
			else {
				// Unsynchronized - just scope it for the transaction, as demanded by the JPA 2.1 spec...
				TransactionSynchronizationManager.registerSynchronization(
						new TransactionScopedEntityManagerSynchronization(emHolder, emf));
			}
			TransactionSynchronizationManager.bindResource(emf, emHolder);
		}
		catch (RuntimeException ex) {
			// Unexpected exception from external delegation call -> close EntityManager and rethrow.
			closeEntityManager(em);
			throw ex;
		}
```

## EntityManagerFactory
- EntityManager 를 만드는 것이며, 스레드 간에 공유가 안되게 돼있음. 싱글톤 방식임.

## Reference

- [https://perfectacle.github.io/2018/01/14/jpa-entity-manager-factory/](https://perfectacle.github.io/2018/01/14/jpa-entity-manager-factory/)
- [https://medium.com/@SlackBeck/spring-container는-jpa-entitymanager의-thread-safety를-어떻게-보장할까-1650473eeb64](https://medium.com/@SlackBeck/spring-container%EB%8A%94-jpa-entitymanager%EC%9D%98-thread-safety%EB%A5%BC-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%B3%B4%EC%9E%A5%ED%95%A0%EA%B9%8C-1650473eeb64)