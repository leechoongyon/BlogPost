---
title: java stream 예제 - list 안의 list 안의 map 에 대해서 filter 걸기    
date: 2020-07-01 23:04:00 +/-TTTT
categories: [java, stream]
tags: [java]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## list 안의 list 안의 map 에 대해서 filter 걸기
- 아래 소스를 설명하면, ListA 에는 list 가 있는데 해당 list 안에는 Map<String, String> 이 있다.
- 구하고자 하는 것은 Map 안의 value 중에서 val1 로 시작하는 value 를 구하는 것이다.
- flatMap 은 map 과는 다르게 단일원소 스트림으로 변환시켜주는 메소드.


```java
public class LambdaTest {  
    public static void main(String[] args) {  
        Map<String, String> map = new HashMap<>();  
        map.put("val", "val1");  
  
        Map<String, String> map1 = new HashMap<>();  
        map1.put("val", "val11");  
  
        Map<String, String> map2 = new HashMap<>();  
        map2.put("val", "val111");  
  
        List<Map<String, String>> list = new ArrayList<>();  
        list.add(map);  
        list.add(map1);  
        list.add(map2);  
  
        List<A> listA = new ArrayList<>();  
        A a = new A();  
        a.setList(list);  
        listA.add(a);  
  
        Map result = listA.stream().map(i -> i.getList())
                    .flatMap(List::stream)
                    .filter(i -> i.get("val").equals("val1")).findAny().get();  
        log.debug("result : {}", result);  
  }  
    
  public static class A {  
        @Getter
        private List<Map<String, String>> list;
  }  
}
```