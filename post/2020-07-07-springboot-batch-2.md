---
title: spring boot, spring batch 정리 - 2편 partitioner 예제
date: 2020-07-07 19:57:00 +/-TTTT
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
## partitioner 기능 및 장단점 정리
###### partitioner 개념
- partitioner 는 하나의 jvm 내에서 멀티 스레드로 처리하는 방법이다.
- partitioner 에서 데이터를 나누고 각 스텝에 분배를 하며, 스텝에서는 분배받은 데이터를 가지고 프로그램을 수행한다.

###### 장단점
- partitioner 의 장점은 데이터를 분배하고 멀티 스레드로 처리하기에 속도가 대개 잘나온다.
    - 하지만 속도가 반드시 잘나오는 경우는 아니다. 실제 현실 세계에서 partitioner 를 썼을 때, 비슷하거나 오히려 덜 나오는 경우도 봤다.   
- partitioner 의 단점은 로그가 뒤섞여서 나오기에 로그 찾기가 힘들다. 또한, partitioner 는 멀티 스레드 환경에서 수행되기에 1개의 스레드가 장애가 발생 시 다른 스레드에 영향을 미치기에 실제 상용에서 쓰기에 문제점을 갖고 있다.
    - Job 을 병렬로 돌려서 처리하는게 안정성 측면 + 속도 측면에서 더 낫다고 생각합니다.

## partitioner 예제
###### Partitioner.java
- 데이터를 분배하는 Partitioner
{% gist leechoongyon/be98e698629e5a51d2e66970756b5765 %} 

###### JobConfiguration.java
- partitioner 구성 java source
- gridSize 는 3이며, gridSize 는 분할할 step 개수 (각 step 은 TaskExecutor 를 통해 수행)

{% gist leechoongyon/03916d65443485c9374db8c89e24b86e %}

## 전체 source
- [spring-boot-batch-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-batch-example) 참고


## reference
- https://howtodoinjava.com/spring-batch/spring-batch-step-partitioning/