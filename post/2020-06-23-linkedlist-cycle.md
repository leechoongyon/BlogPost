---
title: linkedlist cycle (링크드리스트 순환 체크) 
date: 2020-06-23 21:33:00 +/-TTTT
categories: [datastructure, linkedlist]
tags: [linkedlist]     # TAG names should always be lowercase
---


## source
- linkedList 순환 확인
- 시간복잡도 O(n). while 문만 확인하면 되니.
- 공간복잡도 O(node 갯수). 최대 node 개수만큼 set 에 공간을 차지함.  
- 참고로 LinkedList 와 array 의 차이는 데이터를 CUD 하는 것과 Search 하는 것의 시간복잡도 차이가 있음.
- 배열의 경우 찾는데 O(1), LinkedList 의 경우 최악의 경우 O(n).
- 데이터 넣을 때는 배열의 경우 데이터 갯수만큼 성능이 떨어짐. 링크드리스트는 O(1)

{% gist leechoongyon/f628f8aea3744a11ece1eee14835c744 %}
