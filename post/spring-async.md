---
title: 2021-02-14 TIL
date: 2021-02-14 19:00:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
`오늘부터 날짜 별로 TIL 이 아니라 깊게 공부하고 내 생각을 많이 담자.`


## Spring Async 처리
- sync 란 호출 후 응답을 기다리는거고, async 는 호출 후 응답을 기다리지 않는 것이다.
- Spring 에서 @Async annotation 을 설정해두면 호출하는 스레드는 즉시 리턴하고, Spring TaskExecutor 에서 Thread 처리를 수행함.
- @Async 라고 선언된 annotation 이 spring aop 에 의해서 감지되서 수행 됨.

## spring Async 활용 source
```java
@Configuration
@EnableAsync
public class AsyncConfig implements AsyncConfigurer {

    @Bean(name = "asyncTestExecutor")
    @Override
    public Executor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(2);    // 
        executor.setMaxPoolSize(5);
        executor.setQueueCapacity(10);
        executor.setBeanName("asyncTestExecutor");
        executor.initialize();
        return executor;
    }
}
```

- corePoolSize : 최조 생성되는 스레드 사이즈이며, 해당 사이즈로 스레드 풀은 스레드 개수를 유지한다.
- maximumPoolSize : ThreadPool 에 최대로 유지할 수 있는 개수.
- queueCapacity : 


## Spring TaskExecutor
- Executor 는 스레드 풀로서 스레드를 관리하는 개념
- TaskExecutor interface 는 다음과 같이 Runnable 을 받아서 실행. 

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


## spring async 의 스레드 구조 파악
- 호출하는게 메인스레드라고 하면, 내부에서 TaskExecutor 가 별도로 있을 거임.

## spring async 를 어떠한 경우에 사용하면 좋은가?

## Reference
- https://pakss328.medium.com/spring-async-annotation%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-thread-%EA%B5%AC%ED%98%84-f5b4766d49c5
- https://brunch.co.kr/@springboot/401