---
title: 2021-03-21 TIL
date: 2021-03-21 10:00:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 

## Generic, WildCard 정리

## Generic 
#### 개념
- 입력한 객체 타입을 보장하기 위해 사용
#### 매개변수
- E: Element, 컬렉션의 요소를 표시할 때 사용
- K: Key, V: Value, T: Class Type
#### Example
- 아래 예시를 보면 Key, Value 형태로 매개변수가 설정된 Generic 이다.
- String 으로 Key, Value 를 초기화했으며, key, value 는 String 만 올 수 있다.
- 만약, 다른 타입을 입력하면 컴파일 단계에서 에러가 발생한다.
    - 이렇게 하는 목적은 다른 값이 들어오는 것을 컴파일 단계에서부터 체크하겠다는 것.

```java
public interface Map<K,V> {
		V put(K key, V value);
}
Map<String, String> map = new HashMap<>();
```

## WildCard
#### 배경 & 개념
- Generic 은 정해진 타입만 사용할 수 있다. 유연하게 사용할 수 없다. 유연하게 사용하고 싶은 요구사항이 있기에 WildCard 가 나왔다.

#### 종류
- Unbound WildCard
    - Collection<?> 로 정의되어질 수 있으며, 모든 타입이 올 수 있음. 내부적으로 Object 로 정의 되서 사용
    - 주로 List 에서 쓰임. List 는 어떤 타입이든 올 수 있으니.
- Upper Bound WildCard
    - Collection<? extends Test> 와 같은 형태로 사용되며, Test 클래스의 자식 클래스만을 타입으로 받겠다는 것.
    - 자식 클래스 어떤 것이 와도 되지만 기능은 Test 선언된 것만 사용 가능.
    - 딱히 이거다 하는 사용 예시가 떠오르지는 않음.
- Lower Bound WildCard
    - Collection<? super Test> 와 같은 형태로 사용되며, Test 클래스의 부모 클래스만을 타입으로 받겠다는 것
    - Test 클래스에 선언된 메소드들을 사용 가능.
    - 딱히 이거다 하는 예시가 떠오르지 않음.
## 차이점
- 정리하면 Generic 은 타입을 한 번 정하면 계속 그 타입을 써야한다. 만약 다른 타입을 쓰면 컴파일 시 에러가 난다.
- WildCard 는 Generic 에 비해 유연한 구조를 가지고 있다.

## Reference
- [https://velog.io/@eversong/Java-Generic-WildCard에-대해서](https://velog.io/@eversong/Java-Generic-WildCard%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)