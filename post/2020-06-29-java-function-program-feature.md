---
title: 자바 함수형 프로그래밍 특징 (java function program feature)
date: 2020-06-29 21:45:00 +/-TTTT
categories: [java, function]
tags: [java]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  

## 함수형 프로그래밍
- 함수를 이용하여 사이드 이펙트 없이 구현하는 프로그래밍 언어
- y = f(x) 처럼 x 값이 같으면 y 값이 같아야 한다. 
- 아래의 특징들을 사용해 프로그램 복잡도를 낮춘다.

## 1급 객체
- 함수를 변수나 데이터 구조 안에 담을 수 있다.
- 함수를 파라미터로 전달할 수 있다.
- 함수를 반환 값으로 사용할 수 있다.
- 위와 같은 특징들을 통해 사이드 이펙트를 고려 안해도 됨. 
```java
Func func = new Func() {
    xxx
    xxx     
};

```

## 불변성 
- 함수형 프로그래밍에서는 데이터가 변할 수 없는데, 이를 불변성 데이터라고 한다.
- 데이터 변경이 필요한 경우, 원본 데이터 구조를 변경하지 않고 그 데이터를 복사본을 만들어 그 일부를 변경하고, 변경한 복사본을 사용해 작업을 진행한다.
- 원본 데이터가 바뀔 경우 고려해야할 것이 많기에 데이터 복사본을 만들어 처리. 
```java

    int count = 0;
    new Thread(() -> {
        System.out.println(count); // compile 가능
    }
    )   

    
    int count = 0;
    new Thread(() -> {  
        count++; // compile error
    
        int tmp = count;
        tmp++; // compile O
    
    }
    )  


```

## 고차 함수 
- 함수에 함수를 파라미터로 전달할 수 있다.
- 함수의 반환 값으로 함수를 사용할 수 있다.
```java
public void func(FunctionXXX xxx) {
    xxx
    xxx
}
```


## 순수 함수 
- 동일한 입력에는 항상 같은 값을 반환해야 한다.
- 함수의 실행은 프로그램의 실행에 영향을 미치지 않아야 한다.


## reference
-  https://medium.com/@soeunlee/javascript%EC%97%90%EC%84%9C-%EC%99%9C-%ED%95%A8%EC%88%98%EA%B0%80-1%EA%B8%89-%EA%B0%9D%EC%B2%B4%EC%9D%BC%EA%B9%8C%EC%9A%94-cc6bd2a9ecac