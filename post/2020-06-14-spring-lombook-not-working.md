---
title: SpringBoot Intellij lombok 적용이 안될 때
date: 2020-06-14 21:03:00 +/-TTTT
categories: [spring, setup]
tags: [spring]     # TAG names should always be lowercase
---

* 정리 목적으로 글 작성

#### SpringBoot Intellij 사용 시 lombok 적용 안될 때 상황
- build 또는 application 을 실행했을 때, cannot find symbol 과 같은 에러가 발생할 때
- 환경 : Intellij, gradle, spring-boot

#### 해결 방안
* 1번 해결방안
	* Intellij --> preference --> Build,Execution,Deployment --> Compiler --> Annotation Processors 들어가서 Enable annotation processing 체크
	* lombok 플러그인 설치 (Intellij preference --> plugin 에서 lombok 검색)
* 2번 해결방안 : File > Invalidate Caches / Restart > Invalidate and Restart
* 3번 해결방안 : build.gradle 에 다음과 같이 설정
	- 아래의 annotionProcessor 는 Compile 수행 시 annotation 에 대한 스캔 및 롬복 관련 설정을 해주는 것이다. (Getter, Setter, Builder)

```groovy
compileOnly 'org.projectlombok:lombok'  
annotationProcessor 'org.projectlombok:lombok'
```