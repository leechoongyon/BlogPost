---
title: java string concat 
date: 2020-06-23 21:00:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

## java string concat
1. String + String
- 위와 같은 경우 String concat 을 + 로만 수행한다면 concat 을 할 때마다 AbstractStringBuilder 를 생성함.
- 즉, 새로운 인스턴스를 생성하기에 성능 저하를 불러 일으킨다.

2. StringBuilder
- String 연산을 할 때, 새로운 인스턴스를 생성하는게 아니라 기존 인스턴스로 처리하기에 성능 저하 없음.

3. StringBuffer
- 위에 StringBuilder 를 thread-safe 하게 구현.


## java literal & new
- 추가로 string 을 literal 로 지정할 경우 String constant Pool 영역에 저장.
- 문자열이 같을 경우 constant pool 에서 가져오기에 주소 값이 같음.
- new String("aaa); 와 같이 생성하면 heap 에 생성 됨.