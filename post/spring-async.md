---
title: 2021-02-14 TIL
date: 2021-02-14 19:00:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
`오늘부터 날짜 별로 TIL 이 아니라 깊게 공부하고 내 생각을 많이 담자.`


## Spring Async 처리
- Spring 에서 @Async annotation 을 설정해두면 호출하는 스레드는 즉시 리턴하고, Spring TaskExecutor 에서 Thread 처리를 수행함.


## Spring TaskExecutor
- Executor 는 스레드 풀로서 스레드를 관리하는 개념
- 아래 소스와 같이 Runnable 을 받아서 실행하는 인터페이스. 

```java
@FunctionalInterface
public interface TaskExecutor extends Executor {

	/**
	 * Execute the given {@code task}.
	 * <p>The call might return immediately if the implementation uses
	 * an asynchronous execution strategy, or might block in the case
	 * of synchronous execution.
	 * @param task the {@code Runnable} to execute (never {@code null})
	 * @throws TaskRejectedException if the given task was not accepted
	 */
	@Override
	void execute(Runnable task);

}
```


## Reference
- https://pakss328.medium.com/spring-async-annotation%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-thread-%EA%B5%AC%ED%98%84-f5b4766d49c5