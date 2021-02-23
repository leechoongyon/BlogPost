---
title: 2021-02-16 TIL
date: 2021-02-16 21:00:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
 
## ThreadPoolExecutor 설명 
 
#### 개념
- ThreadPoolExecutor 는 ThreadPool 을 관리해주는 역할

#### ThreadPoolExecutor 환경 설정
- corePoolSize : 초기에 corePoolSize 만큼 스레드가 생성되며, 이를 유지함.
- maximumPoolSize : ThreadPool 에서 최대로 유지할 수 있는 Thread 갯수
- workQueue : corePoolSize 초과하는 요청에 대해 큐에 담는다.
    - 예를 들면, corePoolSize : 1 이고, workQueue : 10 이며, 요청 스레드는 10이라 가정하면 corePoolSize 에서 1개 스레드로 처리하고 큐에는 9개 요청이 대기하고 있음.

#### Case 별 ThreadPoolExecutor 동작

###### case1. 요청 스레드가 corePoolSize
- 
 

## reference
- http://wonwoo.ml/index.php/post/2254
