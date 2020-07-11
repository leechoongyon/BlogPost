---
title: spring-boot, gradle test 환경 구성 정리
date: 2020-07-10 23:11:00 +/-TTTT
categories: [gradle]
tags: [gradle]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## spring-boot, gradle test 환경 구성 정리
- build.gradle 파일
```java
// build.gradle 
compile('org.springframework.boot:spring-boot-starter')
testCompile('org.springframework.boot:spring-boot-starter-test')
```

- 그런 뒤, gradle build 나 gradle test 를 하면 @Test 등록된 것들이 실행된다.

## 주의사항
- Test package 와 src package 가 같아야 한다.
- src/main/java/com/example 이라면
- test/java/com/example 밑에 테스트 파일이 존재해야 한다.