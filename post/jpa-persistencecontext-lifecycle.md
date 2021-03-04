---
title: 2021-02-23 TIL
date: 2021-02-23 20:41:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 

## Jpa 란 무엇인가? 
- 자바 ORM 기술에 대한 API 표준 명세
- ORM 이란 객체와 RDB 를 맵핑한다는 말
- 즉 객체를 통해 RDB 데이터를 가져오겠다는 것

## Jpa 라이프사이클

#### 비영속
- Persistence Context 에서 관리하지 않는 상태

#### 영속
- Persistence Context 에서 관리하는 상태
- find 를 통해 데이터를 검색했거나, persist 메소드를 통해 저장한 경우 영속성 상태가 됨.

#### 삭제
- 관리되고 있는 객체를 removed 메소드를 통해 삭제했을 때, 실제 DB 에 삭제가 된다.
- 이 상태가 삭제 상태이다.

#### 준영속
- 트랜잭션이 commit 되었거나 clear, flush 메소드가 실행된 경우 준영속 상태가 된다.
- 즉, DB 와 더 이상 동기화 하지 않는다.
 
## 영속성 컨텍스트 관계
- 아래 reference 참고해서 적기.

## jpa 준영속 상태
- https://insanelysimple.tistory.com/265

## jpa update 변경감지 vs merge 어떤 것이 더 나은가?

## reference
- https://insanelysimple.tistory.com/235
- https://insanelysimple.tistory.com/236
- https://blog.woniper.net/266