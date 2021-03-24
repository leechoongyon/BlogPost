---
title: jpa n+1 정리
date: 2020-07-21 22:16:00 +/-TTTT
categories: [jpa]
tags: [jpa]     # TAG names should always be lowercase
---

 
## Jpa n+1 문제 
#### 개념 
- A와 B 테이블이 있다고 가정하고 OneToMany 관계라 가정하자.
- A 데이터는 2개, B 데이터는 4개. 
- A 데이터를 전체 조회한 후, Jpa 를 통해 B 데이터를 접근해서 가져올려고 한다.
- 그럼 A 데이터를 전체 조회하는 쿼리 1개. A 데이터 각각이 B 를 조회하는 쿼리 2개. 총 3개가 실행 됨.
- 이것을 n + 1 이라 한다.
- fetch type 이 Lazy, Eager 에 관계 없음. 


## reference

-   [https://jojoldu.tistory.com/165](https://jojoldu.tistory.com/165)