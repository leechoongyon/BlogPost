---
title: java stream 예제 - List 안에 List 의 값에서 특정 조건을 만족하는 값을 찾는 것  
date: 2020-07-01 22:02:00 +/-TTTT
categories: [java, stream]
tags: [java]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## List 안에 List 의 값에서 특정 조건을 만족하는 값을 찾는 것
- 소스를 간단히 설명하면, List 안에 List 가 있다.
- A List 안에는 B List 값이 있다.
- 여기서 B List 의 num 값이 특정 조건을 만족하는 List 를 찾고 싶다.
- map 을 통해 특정 List 를 가져오고, flatMap 을 통해 B List 의 값을 flat 으로 평평하게 만든다.
- flat 으로 평평하게 만든 값을 filter 를 이용하여 조건을 건다.

{% gist leechoongyon/275cc3705f640b07264749724a27f197 %}