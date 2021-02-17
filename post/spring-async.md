---
title: 2021-02-14 TIL
date: 2021-02-14 19:00:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
`오늘부터 날짜 별로 TIL 이 아니라 깊게 공부하고 내 생각을 많이 담자.`


## Spring Async 처리
- sync 란 호출 후 응답을 기다리는거고, async 는 호출 후 응답을 기다리지 않는 것입니다.
- Spring 에서 @Async annotation 을 설정해두면 호출하는 스레드는 즉시 리턴하고, Spring TaskExecutor 에서 Thread 처리를 수행합니다.
- @Async 라고 선언된 annotation 이 spring aop 에 의해서 감지되서 수행 됩니다.

## spring Async 활용 source
#### AsyncConfig
- AsyncConfig 를 통해 Spring 에서 Async 설정을 어떻게 할지 알려줍니다.
- AsyncConfig 에 @EnableAsync 를 선언함으로써 관련 설정을 수행합니다.
- getAsyncExecutor 에 Bean 명을 선언한 이유는 또 다른 AsyncExecutor 를 만들수도 있을 것 같아서 설정했습니다.

```java

@Configuration
@EnableAsync
public class AsyncConfig implements AsyncConfigurer {

    @Bean(name = "asyncTestExecutor")
    @Override
    public Executor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(2);     
        executor.setMaxPoolSize(5);
        executor.setQueueCapacity(10);
        executor.setBeanName("asyncTestExecutor");
        executor.initialize();
        return executor;
    }
}


```

#### AsyncTestController
- GetMapping 을 받아서 sync, async 테스트를 하고자 아래와 같이 소스를 구현했습니다.  

```java
import lombok.extern.slf4j.Slf4j;
import org.example.online.service.AsyncTestService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@Slf4j
@RestController
public class AsyncTestController {

    @Autowired
    private AsyncTestService asyncTestService;

    @GetMapping("/test/async")
    public String asyncTest() {
        asyncTestService.asyncTest();
        return "asyncTest...";
    }

    @GetMapping("/test/sync")
    public String syncTest() {
        asyncTestService.syncTest();
        return "syncTest...";
    }
}
```

#### AsyncTestService
- 5초 간 sleep 한 후에 메소드를 종료합니다.

```java
import lombok.extern.slf4j.Slf4j;
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Slf4j
@Service
public class AsyncTestService {

    @Async("asyncTestExecutor")
    public void asyncTest() {
        try {
            log.info("before sleep...");
            Thread.sleep(5000);
            log.info("after sleep, asyncTest");
        } catch (InterruptedException e) {
            log.error(e.getMessage(), e);
            throw new RuntimeException(e);
        }
    }

    public void syncTest() {
        try {
            log.info("before sleep...");
            Thread.sleep(5000);
            log.info("after sleep, syncTest...");
        } catch (InterruptedException e) {
            log.error(e.getMessage(), e);
            throw new RuntimeException(e);
        }
    }
}
```

## localhost 실행방법 (get 방식)
- 위와 같이 소스를 작성하고 application 을 실행시킨 후, 브라우저에서 localhost:8080/test/async, localhost:8080/test/sync 를 호출하면 됩니다.
- sync 는 5초 후에 결과를 반환할테고, async 는 즉시 반환합니다.

## ThreadPoolExecutor 와 spring 과의 관계 정리
- 아래 reference 읽어보면 나옴.
- 어떻게 spring 이 ThreadPoolExecutor 를 만들어서 저장하고, 실행하는지. aop 관련

## spring async 를 어떠한 경우에 사용하면 좋은가?
- api 연동을 하는데 해당 api 가 시간이 오래 걸릴경우 사용하면 좋다.
    - 단 api 연동을 통해 받은 response 값이 필요없을 경우이다.
    - 필요하다면 sync 처리를 하거나 다른 방안을 강구해야 한다.

## Reference
- https://pakss328.medium.com/spring-async-annotation%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-thread-%EA%B5%AC%ED%98%84-f5b4766d49c5
- https://brunch.co.kr/@springboot/401