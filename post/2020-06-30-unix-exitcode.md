---
title: unix exit code description (exit code 설명)
date: 2020-06-30 19:30:00 +/-TTTT
categories: [unix, shell]
tags: [shell]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  

## EXIT CODE 이란?
- UNIX 의 종료 코드
- 0 인 경우 정상. 0이외의 것은 비정상

## EXIT CODE 를 어디다 사용하는가?
- 프로그램을 수행했을 때, EXIT_CODE 를 받아서 분기 처리를 해준다.  
- 아래 예제를 참조

## code example

{% gist leechoongyon/7f49f356e367ef85af9e89af45a95dac %}
