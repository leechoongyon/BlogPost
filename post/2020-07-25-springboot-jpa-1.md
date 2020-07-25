---
title: spring boot, jpa save 동작 원리
date: 2020-07-25 09:40:00 +/-TTTT
categories: [spring, jpa]
tags: [jpa]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## spring-data-jpa 에서 save 동작 원리
- source 부터 살펴보기.
- 아래 소스를 살펴보면 entity 가 이미 영속성에 등록돼있으면 merge 를 없으면 persist 를 실행하게 돼있다.
- merge 는 해당 ID 가 영속성에 존재하면 update 를 수행. 없으면 INSERT 를 수행한다.
    - 여기서 주의할 점은 ID 가 없을 경우 SELECT 를 시도하는 경우가 있을 수 있다는 것.
    - 기본키 생성 전략이 없을 경우 (애플리케이션에서 생성) SELECT 를 수행한 후, INSERT 를 실행하기에 쿼리가 2배로 실행됨.
- persist 의 경우 INSERT 쿼리만 실행 됨.
- 즉, 정리하면 merge 는 기존의 객체가 존재할 경우 사용하면 좋고, persist 는 새로운 객체를 생성할 때 좋음.
    
```java
	@Transactional
	@Override
	public <S extends T> S save(S entity) {
		if (entityInformation.isNew(entity)) {
			em.persist(entity);
			return entity;
		} else {
			S result = em.merge(entity);
			return result;
//			return em.merge(entity);
		}
	}
```