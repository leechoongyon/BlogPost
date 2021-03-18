---
title: 2021-03-13 TIL
date: 2021-03-13 22:10:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---


## jpa fetch join
- jpa 에서 여러 Entity 와 관계를 맺을 때, 여러 번의 쿼리가 발생할 수 있음.
- 이를 막기 위해 fetch join 으로 한 번에 가져오도록 할 있음. 쿼리 수 줄어듬.

#### jpa fetch join paging 문제점 
- fetch join 의 문제점은 컬렉션이 페이징이 안됨.
    - 페이징이 안되는 경우는 다음과 같음.
    - A 와 B 가 1:n 관계이고, A 데이터가 3개, B 데이터가 7개 있다고 가정.
    - A 를 기준으로 B 데이터를 가져오면 총 21개의 row 가 생김.
    - 이 때, 내가 원하는건 A 를 기준으로 페이징을 하고 싶은데 JPA 입장에서는 어떤 기준을 가지고 Paging 을 해야하는지를 모름.
    - 그렇기에 컬렉션이 페이징이 안됨.
#### jpa fetch join paging 해결방안
- 위 문제를 해결하기 xxxToOne 관계는 fetch 조인으로 가져온다.
    - A, B 가 ManyToOne, OneToOne 관계이면 데이터를 가져올 떄 A 개수만큼 가져오기에 페이징으로 가져올 수 있음.
- 문제는 xxxToMany 관계인데. 이걸 해결하기 위해 지연로딩과 properties 로 처리.
    - 여기서 말하는 proeprteis 는 hibernate.default_batch_fetch_size 또는 @BatchSize 임.
    - 이 옵션은 데이터를 가져올 때 한 번에 가져오는 옵션인데. 예시를 들어 설명
- [예시] A 를 기준으로 B,C,D 테이블 데이터를 가져와야 함. 
    - A:B 는 OneToOne, A:C 는 ManyToOne, A:D 는 OneToMany 라고 가정.
    - 우선 A,B,C 는 fetch join 으로 다 가져옴. 이럴 경우 데이터가 A 를 기준으로 증가하기에 페이징이 됨.
    - 문제는 A:D 인데 A:D 의 경우 지연로딩을 해놓고 hibernate.default_batch_fetch_size = 100 이라고 옵션을 설정해놓으면 A 에서 D 를 List 로 가져올 때, InQuery 로 가져옴.
    - 즉, select * from D where xx in (xxx); 이런식으로 100개만큼을 한 번에 가져오게 됨. 
    - hibernate.default_batch_fetch_size 갯수는 100~1000 이며, 1000은 DBMS 마다 InQuery 를 제한하는 경우가 있으니 이렇게 설정.
    
## reference
- 인프런 강의 스프링부트-JPA-API개발-성능최적화