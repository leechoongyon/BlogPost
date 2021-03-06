---
title: jpa concept (jpa 개념) 
date: 2020-06-24 21:40:00 +/-TTTT
categories: [jpa]
tags: [jpa]     # TAG names should always be lowercase
---


## Jpa 란? 
- Java Persistence API 
- 자바 ORM 기술에 대한 API 표준 명세
- ORM 사용을 위한 인터페이스를 모아둔 것


## ORM 이란? 
- Object Releational Mapping
- 객체와 관계형 데이터베이스를 맵핑
- 패러다임의 불일치 문제 및 SQL 생성을 해줌.
    - Object 와 RDB 를 맵핑해줌으로써 기존의 DB 접근 방식에 대한 개선

## Jpa 의 편리함
- 코드 간결성
    - 먼저 한 예시를 보겠다. JDBC 를 이용해서 insert, update 를 한다고 가정하자.
    - update, insert 를 개발했는데 update, insert 에 컬럼을 추가하는  요구사항이 발생했다. 그럼 update, insert 에 사용되는 객체에 컬럼을 추가하고, update, insert 에 사용되는 쿼리에 컬럼을 추가해줘야 한다.
    - Jpa 는 이러한 것을 Entity 만 수정해주고 저장하면 나머지를 알아서 해준다.
- 코드 명확함
    - SQL 을 보는 것보다 코드만 보고 어떻게 동작할지 쉽게 짐작이 감.

## Jpa 단점
- learning cost 높음.
- 구조를 모르면 내가 예상치 못하게 동작함.

## 왜 Jpa 를 사용하는가?
- 반복되는 작업을 줄여줌.
- 운영 및 추가 개발 (유지보수)
- 패러다임 불일치 해결 = 즉, 반복되는 작업 줄여 줌.
    - 상속
    - 비교
    - 연관관계
    - 그래프 탐색
- 성능 (JDBC 와 프로그램 간 중간에 JPA 가 위치하고 있기에 이 이점을 이용해 성능 개선 가능)
    - Context 영역
- 데이터 접근 추상화 및 독립성

## Jpa 와 MyBatis 비교
- Jpa 는 객체와 관계형 데이터베이스 간 맵핑을 해주는 개념이며, MyBatis 는 SQL 맵퍼이며, 객체와 SQL 과의 맵핑을 담당.

## 패러다임 불일치

#### 1. 상속
- 객체는 상속이 가능하지만, 관계형 데이터베이스는 상속이 없다.
- 그렇기에 상속 관계의 객체를 관계형 데이터베이스에 집어넣기 위해서는 각각의 객체를 가져와 테이블에 넣어줘야 한다.

```text
INSERT INTO PARENT(xxx) ;
INSERT INTO CHILD(xxx) ;
```

- 이러한 이유는 객체와 RDB 가 사용하는 용도가 다르기 때문이다. 객체 지향 언어는 객체 간의 통신을 통해 현실세계의 복잡함을 푸는 언어고, 상속, 추상화, 다형성을 통해 구현한다.
- 그에 비해 RDB 는 데이터 중심으로 구조화 되어있다. 이러한 용도와 목적의 차이를 패러다임의 불일치라고 하고, 이 때문에 불편함이 발생한다. 
- Jpa 에서는 위와 같은 것을 해결하기 위해 다음과 같이 처리한다.

```java
public class Parent {
    Child child;
    
    ...
    ...
}

jpa.persist(parent);
```

- 위와 같이 하면 저 위에 것처럼 쿼리를 여러 번 날릴 필요 없이 Jpa 내부에서 자동으로 처리해준다.
- 즉, 상속의 경우 객체 안에 객체를 정의해놓음으로써 JPA 가 자동으로 이를 연결시켜줌.

#### 2. 연관 관계
- 객체는 참조를 통해 연관된 객체를 조회한다.
- 반면 RDB 테이블은 외래키를 사용해서 테이블 간 연관관계를 맺는다.
- 이러한 패러다임 불일치로 인해 발생되는 문제점은 다음과 같다.


```java
public class Parent {
    Child child;
  
    public Child getChild() {
      return child;
    }
}


// 위와 같을 때, Parent 를 가지고 저장할려면, Child 의 key 를 가져와야 한다.
// 가져온 Child key 를 가지고, 테이블에 저장을 해야할테고.
parent.getChild().getId();
insert (parent xxx);
insert (child xxx);

// Jpa 에서는 다음과 같이 처리한다.
// 자동으로 연관관계를 맺어 처리해준다.
parent.setChild(child);
jpa.persist(parent);
```

- 이런 문제를 해결하기 위해 JPA 에서는 객체를 참조할 때 자동으로 외래키를 조회해서 다른 객체를 조회해온다.

#### 3. 객체 그래프 탐색
- 객체의 참조를 통해 계속해서 탐색하는 것을 의미
- 객체만으로는 객체 그래프 탐색이 어디까지 이루어질 수 있는지 확인할려면 SQL 을 직접확인해야 한다.
- JPA 는 이 문제를 지연로딩으로 해결했다.
- 참조되는 객체를 실제로 호출할 때, 해당 데이터를 읽어오는 것으로.

#### 4. 비교
- RDB 는 기본키의 값으로 로우를 비교.
- 객체는 '==', 'equals' 사용. (== 주소 비교, equals 값 비교)
- 이런 패러다임의 문제를 해결하기 위해 JPA 는 같은 트랜잭션일 떄, 같은 키로 조회하면 같은 객체가 조회되는 것을 보장.

## Reference
- 자바 ORM 표준 JPA 프로그래밍