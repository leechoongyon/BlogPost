---
title: 2020-11-02 TIL
date: 2020-11-02 20:18:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
## 2020-11-02 TIL 


#### AOP 설명

-   AOP ( Aspect Oriented Programming )
-   AOP 의 개념은 핵심 관심만 집중할 수 있도록, 중복 해서 작성해야 하는 핵심 이외의 코드들은 외부로 빼놔서 일괄적용시키는 것
-   AOP 방식의 가장 큰 장점은 핵심 부분을 건드리지 않으면서 중복 코드를 제거 가능
    - 비슷한 자바 패턴이 strategy 패턴이 있음.

#### AOP 용어


###### aspect
-   

###### Pointcut
-   어느 부분( Where )에 횡단 관심 모듈을 삽입 할 것인지 정의
-   자바 프로그래밍은 메서드의 호출로 실행되기 때문에 메서드에 횡단 관심 모듈을 삽입
-   Execution 에 명시해서 어떤 메소드에서 실행될지 결정
-   예를 들면, @Around("execution(\* _..aoptest._.\*(..))")
-   Execution 을 통해 어떤 메소드에서 실행할지 결정

###### Joinpoint
-   joinpoint는 언제( When ) 횡단 관심 모듈을 삽입할지를 정의
-   joinpoint의 몇 가지 종류
    -   before : 메서드 실행 전
    -   after : 메서드 실행 후
    -   around : 메서드 실행 전, 후
-   예를 들면, @Around("execution(\* _..aoptest._.\*(..))")
    -   @Around 가 Joinpoint 임.
-   합류하는 지점. 즉, 어디서 적용할 것인지.  

###### Advice
-   advice는 핵심 관심 모듈에 삽입 될 횡단 관심 모듈 자체( What )를 정의
-   JoinPoint 와 PointCut 이 적용된 메소드 자체 내용을 의미함.
    -   Public ~ method () { … advice 내용 }
    
###### weaving
-   aspect 가 대상에 적용되어 지는 과정들을 뜻함.
-   PointCut으로 설정된 JoinPoint 에 Advice 내용이 적용되어 대상(메소드,클래스) 호출 시 AOP Proxy가 만들어지는 과정입니다.

## reference
- https://sabarada.tistory.com/94?category=803157