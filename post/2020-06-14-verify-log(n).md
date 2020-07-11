---
title: verify log(n) (log(n) 시간 복잡도 증명) 
date: 2020-06-14 20:15:00 +/-TTTT
categories: [algorithm]
tags: [algorithm]     # TAG names should always be lowercase
---


#### logN 의 시간복잡도 증명
- logN 의 시간복잡도가 어떻게 나오는지 증명

#### 증명
- n 의 크기를 반씩 줄이는 걸 가정
1.  n 이 반씩 줄다보면 k 단계에서  최종적으로 1이 된다 가정하자.
2.  단계별로 n --> n/2 --> n/4 --> n/2의k 승 진행
3.  n = 2 의 k 승
4. 양쪽에 로그 붙이면 logN = k 가 됨.

#### 예시
- 아래와 같은 예시가 있을 때, 몇 번 실행되는가?
- n = 16 이라 가정하면, 16 --> 8 --> 4 --> 2 --> 1 이고, 이는 logN 의 시간복잡도를 가지게 됨. 실행 횟수는 log(16) = 4 가 된다.
- Quick Sort 나 Merge Sort 에서 O(n*logn) 이 나오는 이유는 O(n) 은 각 레이어별로 수행되는 비교횟수이고, logn 은 레이어가 몇 개 있냐를 뜻한다. 즉, 하나의 레이어의 비교횟수 * 레이어 횟수가 최종 비교 횟수이다.
```prettyprint
for (int i = n ; i > 0 ; i /= 2) {

}
```   

#### Reference
- https://riptutorial.com/ko/algorithm/example/26648/o--log-n--%EC%9C%A0%ED%98%95%EC%9D%98-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98