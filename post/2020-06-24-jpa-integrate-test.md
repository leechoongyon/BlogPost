---
title: jpa integrate test (jpa 통합 테스트) 
date: 2020-06-24 22:40:00 +/-TTTT
categories: [jpa]
tags: [jpa]     # TAG names should always be lowercase
---

##  Jpa 통합 테스트 세팅 방법
- Jpa 단독 (repository) 으로 테스트 하고 싶다면, @DataJpaTest 를 사용
- @DataJpaTest 를 사용한다면 단독으로 repository bean 초기화가 일어나고 사용할 수 있음.
- 여기서는 서비스 테스트를 위해 통합 테스트 하는 방법을 설명



## source
- 간략히 설명하면 @SpringBootTest 를 수행하면 @SpringBoot 와 비슷한 과정을 겪게 됨. (Scan, Bean initialize 등)
- 아래와 같이 어노테이션을 설정해두면 빈 초기화가 일어나면서 repository, 서비스 등 빈 초기화가 일어 남.
- 단, 이 때, 주의할 점은 반드시 Bean 에 등록해야한다. 자바 new 로 생성해버리면 빈에 등록이 안돼서 초기화가 안 일어날 수 있다.

```java
@RunWith(SpringRunner.class)  
@SpringBootTest
public class xxxTest {

	@Test
	public void test123() {
			...
			...
	}

}
```