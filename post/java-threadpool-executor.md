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

###### case1. 요청 스레드가 10개, corePoolSize 1개, WorkQueue 10개, maximumPoolSize : 5
- 초기에 corePoolSize 만큼 스레드가 생성되고 1개 스레드를 처리.
- 9개 요청은 큐에 담겨져 있어서. 요청을 처리할 때마다 큐에서 1개씩 빼서 처리.

###### case2. 요청 스레드가 10개, corePoolSize 1개, workQueue 5개, maximumPoolSize : 5개
- 초기에 corePoolSize 만큼 스레드가 생성되고 1개 스레드를 처리.
- 큐에 5개 쌓이고, 요청 스레드가 4개 남음.
- ThreadPool 이 maximumPoolSize (5개) 만큼 스레드를 생성해 나머지 요청 스레드를 처리함.
- 요청 스레드를 처리하고, ThreadPool 은 일정시간이 흐른 후, corePoolSize 를 유지.
 
###### case3. 요청 스레드가 10개, corePoolSize 1개, workQueue 5개, maximumPoolSize : 2개
- 초기에 corePoolSize 만큼 스레드가 생성되고 1개 스레드를 처리.
- 큐에 5개가 쌓이고, 요청 스레드가 4개 남음. 
- ThreadPool 에서 thread 를 maximumPoolSize (2개) 까지 늘림. 
- 그래도 요청 스레드가 3개 남음. 요청 스레드를 처리할 스레드가 없다고 에러 남. 

#### ThreadPool 과 OS core 관계
- 좀 다른 주제일 수 있지만 생각나는 김에 적어 봤음.
- 하나의 JVM 은 하나의 프로세스에서 동작한다. 하나의 프로세스 안에는 여러개의 스레드가 동작한다.
- 수십개의 요청이 들어와서 ThreadPool 에서 스레드를 하나씩 꺼내서 처리한다고 가정해보자.
- 이 때, 이 스레드들은 하나의 core 에서 동작할까? 정답은 멀티 core 에서 동작한다는 것이다.
- 하나의 JVM 은 하나의 프로세스에서 동작한다면, 하나의 core 에서만 스레드가 동작할 것이라 생각되지만.
- 요즘 OS 시스템은 스레드 단위로 스케줄링을 처리할 수 있다.
- 즉, JVM 내에서 스레드를 할당해 요청을 처리해도 OS System 에서 여러 core 에 스케줄링해서 멀티 core 로 처리할 수 있다.    

## reference
- http://wonwoo.ml/index.php/post/2254
- https://insanelysimple.tistory.com/226