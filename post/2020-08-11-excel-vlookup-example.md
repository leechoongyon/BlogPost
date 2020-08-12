---
title: excel vlookup 을 활용하여 두 리스트 중 같은 값 찾기.
date: 2020-08-11 18:30:00 +/-TTTT
categories: [excel]
tags: [excel]     # TAG names should always be lowercase
---

## excel vlookup 을 활용하여 두 리스트 중 같은 값 찾기.
- a 열, b 열에 가격이 있으며, a 열의 값이 b 열에 존재하는지를 찾는 엑셀
- 아래 내용을 설명하면, a1 의 값이 b1~b100 안에 있는지 확인하고, 값이 일치한다면 (false) 첫번째 행(1) 을 반환한다.
  
```text

=vlookup(a1, $b$1:$b$100, 1, false)

``` 