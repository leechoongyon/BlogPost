---
title: java volatile
date: 2020-06-15 22:05:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

#### Volatile
- 멀티스레드 환경에서 동시성을 제어하기 위해 나온 기법 중 한개.
- 기본적으로 메모리에 올려져있는 데이터를 읽을 때, Main Memory --> Cpu Cache 에 복제해놓고, 스레드 별로 Cpu Cache 에 접근해서 읽는다.
- 위와 같은 상황에서 여러 멀티 스레드가 다른 CPU 를 사용하고 있다면 동시에 접근할 때, 값이 달라질 수 있다.
- Volatile 은 Cpu Cache 를 읽는게 아니라 Main Memory 에서 데이터를 직접 읽는다.
- 주로 쓰이는 곳은 하나의 스레드는 쓰고, 여러 쓰레드가 read 할 때 쓰인다.
