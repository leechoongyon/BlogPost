---
title: Spring Batch ORA-08177
date: 2020-08-18 20:21:00 +/-TTTT
categories: [spring-batch]
tags: [spring-batch]     # TAG names should always be lowercase
---

## Spring Batch ORA-08177 발생 원인
- spring batch 테이블 접근 시 isolation level 이 serialize 로 걸려있을 때 위 에러가 발생.
- 즉, BATCH_JOB_INSTANCE, BATCH_JOB_EXECUTION 테이블 들에 동시 접근할 때 위 에러가 발생.

## 재연 방법
- 같은 배치를 몇십개씩 백그라운드로 돌리면 나옴.
- sh xxxxxx & 

## 해결방안
```java
@Configuration
public class JobConfiguration extends DefaultBatchConfigurer {

    @Autowired
    private DataSource dataSource;

    @Override
    protected JobRepository createJobRepository() throws Exception {
        JobRepositoryFactoryBean factory = new JobRepositoryFactoryBean();
        factory.setDataSource(dataSource);
        factory.setTablePrefix("BATCH_");
        factory.setTransactionManager(new DataSourceTransactionManager(dataSource));
        factory.setIsolationLevelForCreate("ISOLATION_READ_COMMITTED");
        factory.afterPropertiesSet();
        return factory.getObject();
    }
}
```


## reference
- https://okky.kr/article/573766