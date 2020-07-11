---
title: spring boot, spring batch 정리 - 1편 환경 구성 (spring boot, spring batch, gradle, multi project)
date: 2020-07-03 21:33:00 +/-TTTT
categories: [spring, batch]
tags: [spring-batch]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


# 목차

- ### [spring boot, spring batch 정리 - 1편 환경 구성 (spring boot, spring batch, gradle, multi project)](https://leechoongyon.github.io/posts/springboot-batch-1)
- ### [spring boot, spring batch 정리 - 2편 partitioner 예제](https://leechoongyon.github.io/posts/springboot-batch-2)
- ### [spring boot, spring batch 정리 - 3편 repeat step 예제 (파라미터만 변경해서 실행 )](https://leechoongyon.github.io/posts/springboot-batch-3)
- ### [spring boot, spring batch 정리 - 4편 JdbcCursorItemReader NamedParameter 사용 예제 ](https://leechoongyon.github.io/posts/springboot-batch-4)
- ### [spring boot, spring batch 정리 - 5편 대용량, low latency 를 위해 어떤 ItemReader 가 좋은가? (spring-batch 병렬 처리) ](https://leechoongyon.github.io/posts/springboot-batch-5)

---
## 환경 구성
- spring boot
- spring batch
- jpa
- querydsl
- gradle (multi project)


###### github source
- [spring-boot-batch-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-batch-example) 참고


###### 1. 프로젝트 전체적인 구성
- RootProject : spring-boot-example
- SubProject : spring-boot-batch-example


###### 2. 프로젝트 구성 방법
- [Intellij multi project 만드는 법](https://leechoongyon.github.io/posts/intellij-gradle-multi-project) 참고

- root build.gradle
{% gist leechoongyon/5354a9575492739a98cc048378d2f0b4 %}

- spring-boot-batch-example build.gradle
{% gist leechoongyon/d8295d1623f2c29fe484ce16d410336a %}

###### 3. 구성 시 주의사항
- SpringBoot 2.3.1 과 JPA 를 같이 사용하면 배치 프로그램 수행 시, ShutdownHook 가 걸리는거 같음.
- 프로그램 종료가 바로 안되고, 1분 정도 대기하다 프로그램이 종료 됨.
- 해당 기능을 끌려고 찾아봤는데 안보여서 boot version 2.2.1 로 수정


