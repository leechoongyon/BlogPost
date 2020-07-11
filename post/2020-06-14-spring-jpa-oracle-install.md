---
title: SpringBoot, Jpa, Oracle 설정하기 
date: 2020-06-14 20:57:00 +/-TTTT
categories: [spring, setup]
tags: [spring]     # TAG names should always be lowercase
---

- SpringBoot 설정 시 Jpa, Oracle 을 어떻게 세팅해야하는지에 대한 것을 정리. 세팅 정보만 기술하고, 추후 테스트 코드 까지 같이 넣기.

---
- 아래와 같이 application.yml 을 통해 설정하는 방법과 프로그래밍 적으로 제어하는 방법이 있음. 여기서는 application.yml 을 통해 설정하는 방법을 정리
- boot 2.0 이상에서는 url, username, password 를 spring.datasource 레벨에 기술
-  application.yml
```yaml
spring:
  datasource:
    driver-class-name: oracle.jdbc.driver.OracleDriver
    url: 
    username: 
    password: 
      hikari:
        maximum-pool-size: 5
        minimum-idle: 1
        pool-name: hikari

  jpa:
    hibernate:
      ddl-auto: create
    show-sql: true
    database-platform: org.hibernate.dialect.Oracle10gDialect
```

- build.gradle
```groovy

implementation 'org.springframework.boot:spring-boot-starter-jdbc'  
implementation("ojdbc... xxx")
compile('org.springframework.boot:spring-boot-starter-data-jpa')

```
