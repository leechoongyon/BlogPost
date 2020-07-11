---
title: spring boot, spring batch 정리 - 3편 repeat step 예제 (파라미터만 변경해서 실행)
date: 2020-07-08 20:57:00 +/-TTTT
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


## repeat step 예제 (파라미터만 변경해서 실행)
- 동일한 step 을 파라미터만 변경해서 반복해서 실행
- 반복되는 횟수는 동적으로 제어.


###### 반복 횟수 job configuration
- 아래 내용 중 중요한 것은 COMPLETED 와 FAILED 에 따라 step 이 계속실행될지 종료될지를 결정하는 것.

{% gist leechoongyon/abe76918615f534b0d03999e480b955e %}

## source
- [spring-boot-batch-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-batch-example) 참고

## reference
- https://jojoldu.tistory.com/328 참고