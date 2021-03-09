---
title: 2021-02-22 TIL
date: 2021-02-22 22:15:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
## aop spring architecture
- Spring 에서 aop 를 사용할 때는 proxy 패턴을 사용한다.

## aop 란?
- 기본개념은 https://insanelysimple.tistory.com/223 참고

## Proxy 패턴이란?
#### 개념
- 실제 객체를 직접 호출하는 것이 아니라 가상의 객체 안에 실제 객체를 선언하여 가상 객체를 호출하는 방식

#### 장점
- 실제 객체 앞뒤로 내가 원하는 추가 기능을 넣을 수 있음. 즉, 원본 객체를 변경하지 않아도 됨.
- 실제 객체를 숨길 수 있다. 인터페이스만 노출시켜서.

#### 단점
- 소스 유지 보수가 힘들다. 소스를 작정하고 은퍠시키면 찾기가 힘들다.

#### 예시
- source 작성 (JavaExample 에 있음)
- Main Class 에서 ProxyObject 를 호출하고, ProxyObject 에서는 RealObject 를 호출하는게 핵심 
 
```java

public interface RealInterface {
    public void helloWorld();
}


@Slf4j
public class RealObject implements RealInterface {
    @Override
    public void helloWorld() {
        log.info("Hello World...");
    }
}

@Slf4j
public class ProxyObject implements RealInterface {

    private RealInterface realInterface;

    @Override
    public void helloWorld() {
        realInterface = new RealObject();

        log.info("before call helloWorld");
        realInterface.helloWorld();
        log.info("after call helloWorld");
    }
}


public class Main {
    public static void main(String[] args) {
        RealInterface realInterface = new ProxyObject();
        realInterface.helloWorld();
    }
}


```

 

## reference
- https://sabarada.tistory.com/20
- https://bamdule.tistory.com/154