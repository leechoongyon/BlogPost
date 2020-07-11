---
title: java factorial 구현 (recursion, forloop 비교)
date: 2020-07-04 10:07:00 +/-TTTT
categories: [coding]
tags: [coding]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## java factorial 구현 (recursion, forloop 비교)


###### 1. long 으로 구현
- 숫자가 커질수록 long 의 범위를 넘어서기에 안됨.

###### 2. BigInteger Recursion 구현
- 숫자가 커질수록 Stack 에 데이터를 계속 쌓아두기에 StackOverFlow 가 발생

###### 3. BigInteger fooLoop 구현
- 숫자가 커져도 처리 가능

###### source
{% gist leechoongyon/abe7d9384082e6a7d65d82f2063d5d7e %}