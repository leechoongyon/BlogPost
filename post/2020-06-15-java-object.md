---
title: java object
date: 2020-06-15 22:15:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

#### object
- 자바의 모든 클래스는 Object 를 상속받고 있다.
- 그 이유는 모든 클래스가 공통의 기능을 제공하기 위함이다.

#### object 제공 메소드
1. toString
- 클래스를 표현하는 방법
- overriding 가능

2. equals
- 두 객체의 내용이 같은지 확인
- equals 를 재정의하면 hashcode 도 재정의 하는 것이 좋음.
- equals 의 기본 동작은 주소를 비교하는 것이며, override 해야 값 비교가 가능.

3. hashcode
- 두 객체가 같은 객체인지 확인
- collection 에서 hashcode 를 사용해 값을 가져오거나 넣는다. 

4. clone
- 복제

5. finalize
- 객체 소멸 시 호출
  