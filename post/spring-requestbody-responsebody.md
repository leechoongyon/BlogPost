---
title: 2021-03-05 TIL
date: 2021-03-05 21:45:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
 
## [Spring] @RequestBody, @ResponseBody 란?
- Client 으ㅏ Http Body 데이터를 Controller 에서 받을 때, 자바 객체로 데이터를 변환해주는 역할은 한다.
- ReqeustBody 의 경우 HttpBody 요청을 자바 객체로 변경해주고.
- ResponseBody 의 경우 자바 객체를 HttpBody 데이터로 변환을 해주는 것
- 요약하면 Client 의 xml, json 데이터를 받아 오브젝트 형태로 변환해주는 역할이 RequestBody
- 오브젝트 형태인 데이터를 Xml, json 데이터로 직렬화시키는 것이 ResponseBody

## Marshal, unmarshal
- 보통 오브젝트를 직렬화 (일렬로 쭉 세우는 것) 를 마샬링이라 하고. (ResponseBody)
- 직렬화된 것을 오브젝트로 변환하는 것을 unmarshal 이라고 함. (RequestBody)

## RestController
- 위 설명과 별개로 Controller 와 ResponseBody 를 합친게 RestController 이다.
- RestController 를 선언하면 별도 ResponseBody 는 필요없음.

## Reference
- https://devbox.tistory.com/entry/Spring-RequestBody-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%EA%B3%BC-ReponseBody-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%EC%9D%98-%EC%82%AC%EC%9A%A9 