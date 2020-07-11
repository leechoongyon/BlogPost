---
title: spring boot + jpa + querydsl 설정
date: 2020-06-25 22:40:00 +/-TTTT
categories: [jpa, querydsl]
tags: [querydsl]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  
 
## spring boot + jpa + querydsl 설정
- 아래 블로그에 나온 내용대로 했을 때, BasicTest 로 돌렸더니 cannot find symbol 에러가 남.
- QAcademy 가 classpath 에 걸려있는데 왜 못찾는지 헤매다가 github source 보고 고침.
- 실습 예제는 reference 참고

{% gist leechoongyon/a65d8b6914b7306d6c5b254d0eff9c15 %}



## reference
- https://jojoldu.tistory.com/372 