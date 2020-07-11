---
title: tomcat, apache web server get client ip (톰캣, 아파치 웹서버 환경에서 client ip 가져오기) 
date: 2020-06-24 19:40:00 +/-TTTT
categories: [infra, tomcat]
tags: [tomcat]     # TAG names should always be lowercase
---

## 톰캣, 아파치 웹서버 환경에서 client ip 가져오기
- 기존에 다음과 같이 가져왔는데 localhost ip 만 가져오는 현상이 발생.
```java
public void xxxMethod (HttpServletRequest request) {
    String addr = request.getRemoteAddr();
}
```

- 인터넷 찾아보다 다음과 같은 소스로 변경했더니 정상적으로 가져오기 시작.

{% gist leechoongyon/5f3d02c31f3149a9f14c6049f52c65ad %}


## Reference
- https://stackoverflow.com/questions/16558869/getting-ip-address-of-client