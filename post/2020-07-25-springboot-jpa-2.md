---
title: spring boot, jpa n+1 문제
date: 2020-07-25 09:55:00 +/-TTTT
categories: [spring, jpa]
tags: [jpa]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## n+1 문제
- Lazy Loading 으로 설정된 엔티티를 추후 조회할 때, 추가로 쿼리가 실행될 수 있는 것을 n+1 문제라고 한다.
- 예를 들면, 상위 엔티티 안에 하위 엔티티가 있다고 가정했을 때, 하위 엔티티를 Lazy 로딩으로 설정했다고 가정.
- 상위 엔티티를 조회했을 때, select 쿼리가 1번 발생하고 뒤에 비즈니스 로직에서 하위 엔티티를 조회할 때 추가로 select 쿼리가 발생.
- 이것을 n+1 문제라고 함.

## 해결방안
- Entity Graph
- join fetch

## 주의사항
- Entity Graph 의 경우 outer join.
- Join Fetch 의 경우 inner join.
- 또한, 둘 다 카타시안 곱으로 처리하기에 하위 엔티티 갯수만큼 상위 엔티티가 나올 수 있음.
- 해결하기 위해 DISTINCT 을 이용해 처리.

## source
- https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-jpa-example
- CategoryRepositoryTest.java 참고

## reference
- https://jojoldu.tistory.com/165