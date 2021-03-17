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