---
title: StockPrice (프로그래머스)
date: 2020-06-14 20:15:00 +/-TTTT
categories: [coding, programmers]
tags: [programmers]     # TAG names should always be lowercase
---

#### 문제 설명 
- https://programmers.co.kr/learn/courses/30/lessons/42584 참고
--- 

#### 풀이
- Stack 이용
- for 문 돌리면서 스택에 한개 씩 넣기.
- 스택에 넣는 조건은 스택에 있는 top 보다 작을 경우 넣는다.
- 스택에서 빼낸 것은 계산을 해준다.
- 위에처럼 돌리고 마지막까지 스택에 남아있는 것은 뒤에 있는 것들이 작다는 것이니 stack 에서 빼서 계산.
- 시간복잡도가 최악의 경우 O(n제곱) 이 나올 수 있는건가? 나올 수 있음. 구조상
- 일단 최선의 경우 O(n) 이 나옴.
- 최악의 경우 O(n) < x < O(n제곱) 사이에 있을거 같음.

#### source code
{% gist leechoongyon/4c34fdabcb95721e40bba9b1512624d9 %}
