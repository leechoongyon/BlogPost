---
title: spring boot, spring batch 정리 - 4편 JdbcCursorItemReader NamedParameter 사용 예제 
date: 2020-07-09 22:35:00 +/-TTTT
categories: [spring, batch]
tags: [spring-batch]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


# 목차

- ### [spring boot, spring batch 정리 - 1편 환경 구성 (spring boot, spring batch, gradle, multi project)](https://leechoongyon.github.io/posts/springboot-batch-1)
- ### [spring boot, spring batch 정리 - 2편 partitioner 예제](https://leechoongyon.github.io/posts/springboot-batch-2)
- ### [spring boot, spring batch 정리 - 3편 repeat step 예제 (파라미터만 변경해서 실행 )](https://leechoongyon.github.io/posts/springboot-batch-3)
- ### [spring boot, spring batch 정리 - 4편 JdbcCursorItemReader NamedParameter 사용 예제 ](https://leechoongyon.github.io/posts/springboot-batch-4)
- ### [spring boot, spring batch 정리 - 5편 대용량, low latency 를 위해 어떤 ItemReader 가 좋은가? (spring-batch 병렬 처리) ](https://leechoongyon.github.io/posts/springboot-batch-5)

## source
- [spring-boot-batch-example source](https://github.com/leechoongyon/spring-boot-example/tree/master/spring-boot-batch-example) 참고

## JdbcCursorItemReader NamedParameter 사용 예제
- 핵심은 Sql 에 NamedParameterUtils 을 사용해서 named parameter 를 변환.
```java
@Bean
public JdbcCursorItemReader<Person> itemReader() {
    String sql = "select * from person where id = :id and name = :name";
    Map<String, Object> namedParameters = new HashMap<String, Object>() {{
        put("id", 1);
        put("name", "foo");
    }};
    return new JdbcCursorItemReaderBuilder<Person>()
            .name("personItemReader")
            .dataSource(dataSource())
            .rowMapper(new BeanPropertyRowMapper<>(Person.class))
            .sql(NamedParameterUtils.substituteNamedParameters(sql, new MapSqlParameterSource(namedParameters)))
            .preparedStatementSetter(new ListPreparedStatementSetter(Arrays.asList(NamedParameterUtils.buildValueArray(sql, namedParameters))))
            .build();
}
```


## JdbcCurItemReader 간략히 설명
- 배치 프로그램에서 데이터를 한 번에 읽어서 메모리에 올리면 OOM (Out Of Memory) 가 발생할 수 있다.
- 이를 해결하기 위해 데이터를 select 해오기 위해 Connection 을 계속해서 맺은 상태에서 데이터를 계속해서 streaming 방식으로 끌어오는 것.
- 쉽게 설명하면 ResultSet 에서 next() 를 생각하면 됨.

## reference
- https://github.com/spring-projects/spring-batch/issues/1081