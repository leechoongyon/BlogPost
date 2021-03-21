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

```java
public interface Map<K,V> {
		V put(K key, V value);
}

Map<String, String> map = new HashMap<>();
```

## Reference

- [https://velog.io/@eversong/Java-Generic-WildCard에-대해서](https://velog.io/@eversong/Java-Generic-WildCard%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)