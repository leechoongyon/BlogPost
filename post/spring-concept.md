---
title: 2021-03-09 TIL
date: 2021-03-09 21:12:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 

## [Spring] Spring IOC, DI, PSA

#### IOC
###### 배경
- 자바 플랫폼이 어플리케이션 개발에 관련된 풍부한 기능을 제공하더라도 기본적으로 이러한 기능들을 하나의 큰 구조로 만드는 기능은 부족하다. 
- 스프링 프레임워크 제어의 역전 (IoC) 컴포넌트는 이러한 관심사에 접근한다. 
- 즉, 서로 다른 기능들을 하나의 커다란 프레임워크로서 관리하는 것에 초점을 두고 있다.

###### 개념
- 인스턴스 생성의 제어를 개발자 본인이 아닌 다른 누군가 처리. 
- 즉 IOC 란 인스턴스의 생성부터 소멸까지 개발자가 아닌 컨테이너가 대신 관리해준 다는 것이다.
- POJO (bean) 을 관리
    - POJO 란 컴포넌트 등의 의존성이 없는 자바 오브젝트 객체를 말한다.
- IOC Container 는 BeanFactory, ApplicationContext 를 말한다.
- 정확히는 BeanFactory 내부에서 ResourceLoader 를 가지고 있고, 이를 getBean 등을 통해서 접근할 수 있다.

#### DI
- DI는 Dependency Injection(의존성 주입)의 약자로, 객체들 간의 의존성을 줄이기 위해 사용되는 Spring IOC 컨테이너의 구체적인 구현 방식이다. 
- 설정 파일을 통해 객체간의 의존관계를 설정함으로써 Ioc Container 가 객체간의 의존 관계를 정의

#### PSA
- Portable Service Abstraction
- 환경의 변화에 상관없이 일관된 방식으로의 접근 방식 제공
- 예를 들면, MyBatis 나 Jpa 를 단독 모듈로 사용할 때랑, 스프링에서 사용할 때 사용 방식에 큰 차이가 없는 것이 한 예시임.
- 이것이 Spring 이 지향하는 사상이며, 그렇게 하기 위해 중간 interface 에서 조절하는거지.
