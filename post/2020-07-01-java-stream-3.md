---
title: java stream 예제 - List 안에 List 의 값에서 특정 조건을 만족하는 값을 찾는 것  
date: 2020-07-01 22:02:00 +/-TTTT
categories: [java, stream]
tags: [java]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## List 안에 List 의 값에서 특정 조건을 만족하는 값을 찾는 것
- 소스를 간단히 설명하면, List 안에 List 가 있다.
- A List 안에는 B List 값이 있다.
- 여기서 B List 의 num 값이 특정 조건을 만족하는 List 를 찾고 싶다.
- map 을 통해 특정 List 를 가져오고, flatMap 을 통해 B List 의 값을 flat 으로 평평하게 만든다.
- flat 으로 평평하게 만든 값을 filter 를 이용하여 조건을 건다.


```java
public class LambdaTest {  
    public static void main(String[] args) {  
        A a = new A(10000);  
        A a1 = new A(20000);  
        A a2 = new A(30000);  
        A a3 = new A(40000);  
        A a4 = new A(50000);  
  
        List<A> aList = new ArrayList<>();  
        aList.add(a);  
        aList.add(a1);  
        aList.add(a2);  
        B b = new B();  
        b.setList(aList);  
  
        List<A> aList1 = new ArrayList<>();  
        aList1.add(a);  
        aList1.add(a1);  
        aList1.add(a2);  
        aList1.add(a3);  
        aList1.add(a4);  
        B b1 = new B();  
        b1.setList(aList1);  
  
        List<B> list = new ArrayList<>();  
        list.add(b);  
        list.add(b1);  
  
  
        /** 특정 숫자를 초과하는 대상을 추출해라. */  
  List<A> tmp = list.stream().map(s -> s.getList())  
                .flatMap(List::stream)  
                .filter(bb -> bb.getNum() > 10000)  
                .collect(Collectors.toList());  
        tmp.forEach(i -> System.out.println("num : " + i.getNum()));  
    }  
  
  
    public static class B {  
        private List<A> list;  
  
        public void setList(List<A> list) {  
            this.list = list;  
        }  
  
        public List<A> getList() {  
            return list;  
        }  
    }  
  
    public static class A {  
        private int num;  
  
        public A(int num) {  
            this.num = num;  
        }  
  
        public int getNum() {  
            return num;  
        }  
    }  
}
```