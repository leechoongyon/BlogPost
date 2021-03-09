---
title: 자바 스트레지트 패턴
date: 2020-08-01 10:21:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

## 자바 스트레지트 패턴
- 스트레지트 패턴이란 인터페이스의 구현체를 달리 줘서 유연하게 변경할 수 있는 패턴
- 알고리즘 전략을 유연하게 변경할 수 있는 패턴
- 쉽게 설명하면, 변경이 일어나는 부분을 따로 찾아내서 그 부분만 캡슐화 
- 또다른 설명으로는 객체가 할 수 있는 행위들 각각을 전략으로 만들어서, 동적으로 행위를 변경하고자 할 때, 생성자를 달리 줘서 행위를 다르게 하는 패턴이다.

## source
```java
package pattern.strategy;

public class StrategyPatternTest {
    public static void main(String[] args) {
        Player player = new Player(new BaseballPlay());
        player.play();
    }
}



package pattern.strategy;


public interface Strategy {
    public void play();
}



package pattern.strategy;

public class SoccerPlay implements Strategy {
    @Override
    public void play() {
        System.out.println("SoccerPlay...");
    }
}


package pattern.strategy;

public class Player {
    private Strategy strategy;
    public Player(Strategy strategy) {
        this.strategy = strategy;
    }
    public void play() {
        strategy.play();
    }
}


package pattern.strategy;

public class BaseballPlay implements Strategy {
    @Override
    public void play() {
        System.out.println("Baseball play...");
    }
}
```



#### 스테이트 패턴
- 행위와 관련된 패턴이며. 다음과 같음.
- 1번째 행위 후 2번째 행위를 수행. 이 때, 상태를 ready --> start --> done 이런식으로 자연스럽게 변경해나가는거지.
- hadoop 에서 이런 소스가 많이 보임.
- 다시 정리하면 행위를 수행할 때마다 상태가 변경되고. 행위를 실행 하기 전 상태 체크가 들어가면 오류를 줄일 수 있겠지.


## reference
- https://niceman.tistory.com/133