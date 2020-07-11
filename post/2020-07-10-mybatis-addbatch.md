---
title: MyBatis AddBatch 처리 방법
date: 2020-07-10 00:28:00 +/-TTTT
categories: [mybatis]
tags: [mybatis]     # TAG names should always be lowercase
---

#### MyBatis AddBatch 처리 방법
```java
SqlSession sqlSession = xxx().getSqlSession().openSession(ExecutorType.Batch, false);
```
- 위와 같이 설정하고 사용 시, AddBatch 처럼 작동 됨.

#### 주의사항
- CUD 를 수십, 수백, 수천을 실행하고 release 안하면 ora-01000 cursor 초과 에러가 발생함.
- 오라클 세션에 정해진 cursor 개수가 있는데, 그걸 초과해버리면 에러가 난다. 그렇기에 commitCount 를 잡아서 처리해줘야 위 에러가 발생 안한다.
- sqlSession.flushStatements 를 호출하면 statement close 가 이루어짐.