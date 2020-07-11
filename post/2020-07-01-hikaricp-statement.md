---
title: HikariCP 는 Statement Cache 를 사용하지 않는다. 
date: 2020-07-01 22:01:00 +/-TTTT
categories: [database, hikaricp]
tags: [hikaricp]     # TAG names should always be lowercase
---

#### 결론부터 얘기하면 HikariCP 는 Statement Cache 를 사용하지 않는다.
- PreparedStatement Caching 은 connection 하나당 캐시가 이루어진다.
- 어플리케이션이 100개의 실행된 쿼리와 10개의 connection pool 을 가지고 있다면 데이터베이스는 1000개의 실행 계획을 holding 하고 있다. 또한, 이 풀은 많은 preparedStatement 를 caching 하고 있다.
- 대부분의 JDBC 드라이버들은 Statement cache 를 가지고 있다. ex) Oracle, MySQL, DB2 등
- 이런 드라이버들의 특징 중 하나는 실행 계획을 커넥션 간 공유하는 기능이 있는 것이다.
- 위에서 얘기한 1000개의 실행 계획을 hoding 하는 것보다 데이터베이스 내에 100개의 쿼리를 캐싱하는 것이 낫다는 것이다. 이것은 성능 향상을 의미한다.


#### Reference
- [https://github.com/brettwooldridge/HikariCP](https://github.com/brettwooldridge/HikariCP)