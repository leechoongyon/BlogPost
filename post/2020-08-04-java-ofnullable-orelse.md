---
title: 자바 ofNullable, ofElse, ofElseGet
date: 2020-08-04 20:29:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

## 자바 ofNullable
- Optional.ofNullable(value)
- value 가 null 인지 확신할 수 없을 때 사용.
- null 이면 비어있는 Optional 객체를 넘겨준다.


## ofElse, ofElseGet
- 둘 다 null 일 때 동작하는 것이다.
- 단, 차이점은 ofElse 는 null 이 아니여도 동작한다는 점.
- 아래 orElse 는 Hello World 가 찍힘.
- orElseGet 은 Hello World 가 안찍힘. 
- 둘의 차이점을 이해하고 쓰기.
 
```java

xxx.orElse(test())

public static String test() {
    
    System.out.println("Hello World");
    return "test";
}


xxx.orElseGet(test());


```