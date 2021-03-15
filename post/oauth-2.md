---
title: 2021-03-15 TIL
date: 2021-03-15 20:55:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
## Oauth 배경
- 내가 서비스를 운영중인데 회원가입, 로그인 기능을 만들어야하는데 다른 서비스를 (네이버, 카카오) 통해 회원가입, 로그인을 처리하고 싶다. (고객의 편의를 위해)
- 하지만 다른 서비스의 ID,PW 를 본인이 운영하는 서비스에서 가지고 있을 수는 없다.
- 그렇기에 Oauth 가 나왔다.

## Oauth 개념
- 내가 운영하는 서비스가 A, 다른 서비스를 B 라 한다면 A 에서 로그인을 위해 B 서비스의 회원정보를 이용하고 싶다고 가정해보자.
- 그럼 내가 운영하는 서비스에서 B 서비스의 로그인 창을 띄워서 ID, PW 를 입력하게 하고 회원이 맞다면 A 서비스로 Access Token 을 넘겨주고 화면을 리다이렉트 시켜줄 것이다.
- 이 Access Token 으로 B 서비스의 정보를 이용할 수 있다.
- 이것이 oauth 의 개념

## Reference
- [https://velog.io/@undefcat/OAuth-2.0-간단정리](https://velog.io/@undefcat/OAuth-2.0-%EA%B0%84%EB%8B%A8%EC%A0%95%EB%A6%AC)
