---
title: 2021-03-05 TIL
date: 2021-03-05 21:37:00 +/-TTTT
categories: [TIL]
tags: [til]     # TAG names should always be lowercase
---
 
 
## [Spring] ResponseEntity 란?
- HttpBody, HttpHeader, HttpStatus 을 담고 있음.
- 해당 데이터들을 response 로 넘겨줄 수 있음.

- 아래 소스를 보면, getMember 를 호출하면 member 데이터 (JSON) 와 HttpStatus.OK (200) 을 클라이언트에서 받게 됨.

```java

@RestController
public class MemberController {
    
    @GetMapping("/member/{id}")
    public ResponseEntity getMember(@PathVariable("id") String id) {
            
        ...
        ...

        return new ResponseEntity(member, HttpStatus.OK);
    }
}
```

## Reference
- https://devlog-wjdrbs96.tistory.com/182 