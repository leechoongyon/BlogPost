---
title: java heap, stack, static 설명    
date: 2020-07-01 22:12:00 +/-TTTT
categories: [java, memory]
tags: [java]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## Stack
- 각 스레드마다 하나의 Stack 이 존재.
- 원시타입의 데이터 값을 저장.
- Heap 영역의 데이터 참조 값이 저장.
    - 예를 들면, List<String> list = new ArrayList<>(); 라면 list 참조 값은 stack 에 있고, 데이터는 Heap 에 있음.
    
## Heap
- new 로 생성된 모든 데이터가 저장.
    - 위 예를 들면 new ArrayList<>(); 의 데이터는 Heap 에 저장.

## static
- 필드 부분에서 선언된 변수(전역변수)와 정적 멤버변수(static이 붙은 자료형) Static 영역에 데이터를 저장한다. 
- Static 영역의 데이터는 프로그램의 시작부터 종료가 될 때까지 메모리에 남아있게 된다. 



## Reference
- https://yaboong.github.io/java/2018/05/26/java-memory-management/