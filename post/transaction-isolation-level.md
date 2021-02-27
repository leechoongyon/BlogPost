---
title: 2021-02-22 TIL
date: 2021-02-22 22:15:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
## transaction isolation level 설명 
 
###### Read Uncommitted (레벨 0) - 거의 안씀
- 데이터를 읽을 때, 커밋되지 않는 데이터를 읽는다. 즉, 동시성 제어를 안한다.

###### Read Committed (레벨 1)
- 커밋이 완료된 데이터만 읽을 수 있다.
- Dirty Read 보장
    - A, B 트랜잭션이 있고, A 에서 데이터를 변경하고 커밋 전에 B 가 해당 데이터를 읽을 경우 변경된 데이터를 읽을 수 없음.
- Non-Repeatable Read 현상 발생할 수 있음.
    - 한 트랜잭션 내에서 같은 쿼리 2번 실행시켰는데, 1번 실행 후, 데이터가 다른 곳에서 변경돼서 커밋됐으면 다시 조회할 때 값이 달라질 수 있음.

###### Repeatable Read (레벨 2)
- 선행 트랜잭션이 읽은 데이터는 트랜잭션이 종료될 때까지 후행 트랜잭션이 갱신하거나 삭제하는 것을 불허함으로써 같은 데이터를 두 번 쿼리했을 때 일관성 있는 결과를 리턴 하는 것을 말한다.
- Non-Repeatable Read 현상 X
- Phantom Read 현상은 여전히 발생한다.
    - 한 트랜잭션 내에서 반복 데이터를 2번 읽을 때 발생하는 현상은 없어지나, 한 트랜잭션 내에서 동일한 쿼리를 2번 실행할 때, 처음에 없던 데이터가 2번째 쿼리에서 발생할 수 있는 현상을 의미함.

###### Serializable (레벨 3)
- 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능.
- Phantom Read 현상 X 
- 이 Level에서는 INSERT 작업도 허용하지 않습니다.

###### 요약
 - 레벨이 높아질수록 Concurrency 는 높아지고 속도는 느려짐.
 - MySQL 은 REPEATABLE-READ, Oracle 은 READ-COMMITED 가 기본 임.
