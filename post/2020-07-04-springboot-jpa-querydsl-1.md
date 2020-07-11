---
title: spring boot, jpa, querydsl 정리 - 1편 환경 구성 (spring boot, jpa, querydsl, gradle, multi project)
date: 2020-07-03 21:33:00 +/-TTTT
categories: [spring, jpa]
tags: [jpa]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


# 목차

- ### [spring boot, jpa, querydsl 정리 - 1편 환경 구성 (spring boot, jpa, querydsl, gradle, multi project)](https://leechoongyon.github.io/posts/springboot-jpa-querydsl-1)




## 환경 
- Intellij
- Spring boot
- jpa
- querydsl
- gradle (multi project) 

###### github source
- [spring-boot-jpa-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-jpa-example) 참고

###### 1. 프로젝트 전체적인 구성
- RootProject : spring-boot-example
- SubProject : spring-boot-jpa-example

###### 2. 프로젝트 구성 방법
- [Intellij multi project 만드는 법](https://leechoongyon.github.io/posts/intellij-gradle-multi-project) 참고

- root build.gradle
{% gist leechoongyon/5354a9575492739a98cc048378d2f0b4 %}

- jpa sub build.gradle
{% gist leechoongyon/d8295d1623f2c29fe484ce16d410336a %}


