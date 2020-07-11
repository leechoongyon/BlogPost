---
title: logback-spring.xml 설정
date: 2020-06-15 20:50:00 +/-TTTT
categories: [logback]
tags: [logback]     # TAG names should always be lowercase
---



#### logback-spring.xml 설정 
- spring boot 기준으로 src/main/resources 밑에다 두면 자동으로 classpath 잡히며, 읽는다.
- spring starter 를 dependency 로 설정한다면 logback 관련 라이브러리 들은 사용할 수 있다.
- Intellij 의 경우 annotation Processor 를 등록해줘야 source 에서 @Slf4j 를 사용할 수 있다.



- 아래 소스에서 LOG_DIR 은 export LOG_DIR=/tmp/logs 와 같이 설정해줘야 먹힘.
- springProfile 은 적절한 것을 선택해주면 된다.
{% gist leechoongyon/2b6afdb45f33ba0a07515c0fb4c9faa9 %}




 