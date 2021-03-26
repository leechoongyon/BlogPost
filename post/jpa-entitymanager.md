---
title: 2021-03-26 TIL
date: 2021-03-26 22:15:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 

# Entity
- 테이블과 매칭되는 개념
- ORM 을 이루는 기반 개념 중 하나. 객체와 RDB 간 연결시켜주는 존재

# EntityManager
- 엔티티를 관리하는 역할을 한다.
- 엔티티 매니저 내부에는 영속성 컨텍스트가 있으며, 이를 통해 엔티티 관리.
    - 잠깐 영속성 컨텍스트의 개념을 짚고 넘어가면 엔티티를 영구히 저장하는 공간
- 여러 엔티티 매니저가 하나의 영속성 컨텍스트를 공유 가능
- EntityManager 는 Thread-Safe 를 보장해야 한다. 동일한 EntityManager 를 가지고 멀티 스레드 환경에서 호출한다면 데이터가 어떻게 변경될지 모름.

# Reference

- [https://perfectacle.github.io/2018/01/14/jpa-entity-manager-factory/](https://perfectacle.github.io/2018/01/14/jpa-entity-manager-factory/)
- [https://medium.com/@SlackBeck/spring-container는-jpa-entitymanager의-thread-safety를-어떻게-보장할까-1650473eeb64](https://medium.com/@SlackBeck/spring-container%EB%8A%94-jpa-entitymanager%EC%9D%98-thread-safety%EB%A5%BC-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%B3%B4%EC%9E%A5%ED%95%A0%EA%B9%8C-1650473eeb64)