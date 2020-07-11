---
title: 정규화 & 비정규화 (Normalized Denormalized)
date: 2020-06-27 20:45:00 +/-TTTT
categories: [database, concept]
tags: [database]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  

## 정규화
- RDB 설계에서 중복을 최소화하게 데이터를 구조화하는 프로세스를 정규화 라고 함.
- RDB 정규화의 목표는 이상이 있는 관계를 작고 잘 조직된 관계를 생성하는 것에 있음.
- 위와 같이 정규화를 통해 테이블을 정비하고 이를 통해 RDB 나머지 부분들로 전파되게 하는 것이 목표

#### 정규화 - 1NF
- 하나의 컬럼에 중복이 없어야 함.
- 해결 방법은 중복이 있는 컬럼을 분리 시킨다. 테이블을 분리
- ID 1개에 PHONE_NO 가 여러개면 ID 를 관리하는 테이블 1개, PHONE_NO 를 관리하는 테이블 2개로 분리.

#### 정규화 - 2NF
- 테이블에 후보키 A, 후보키가 아닌 것 B 가 존재할 때, B를 결정하기 위해 A 전체를 참조해야하는 경우 2NF 이다. 
- 예를 들면, name, age, 수강 subject 이 있으면, name, subject 이 기본키 인데, age 는 name 에만 종속 돼있음.
- 이를 해결하기 위해 테이블 2개로 분리.

#### 정규화 - 3NF
- 기본키 이외의 다른 컬럼이 그 외 다른 컬럼을 결정할 수 없는 것.
- Student_id, Student_name, Street, city, State, Zip 이 있으면, 기본키는 Student_id 가 됨. 이 때, Zip 컬럼의 값이 정해지면, Street, City, State 값도 자동으로 정해 짐.
- 테이블 쪼개는게 해결책. Student 테이블, Address 테이블

#### 정규화 - BCNF
- 3차 정규형을 만족하면서 모든 결정자가 후보키 집합에 속한 정규형
- 결정자란 하나의 컬럼이 다른 컬럼을 결정한다는 것


## 비정규화
- 정규화 후, 조회 성능을 향상시키기 위해 데이터를 중복하거나 그룹핑하는 과정
- 비정규화의 예로는 그룹에 대한 합계를 테이블에 저장 or 자주 조인하여 사용하는 컬럼을 테이블안에 중복해서 넣어놓는 것

## reference
- https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94