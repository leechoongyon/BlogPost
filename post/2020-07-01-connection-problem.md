---
title: Connection 통신 중 실패 시 벌어지는 상황과 해결 방안 
date: 2020-07-01 22:00:00 +/-TTTT
categories: [database, connection]
tags: [database]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  

---
###### 장애 상황 1
- Connection 통신 시 TCP 통신이 이루어 짐.
- TCP 통신을 잠깐 설명하고 넘어가면 동기 통신이며, 메시지를 주고 받는 안전한 통신 프로토콜이다.
- 클라이언트와 서버가 TCP 통신 중 장애가 발생했다고 가정하면, 클라이언트나 서버는 응답을 기다리는 상황이 발생할 수 있음.
- 위와 같이 장애가 발생하면 OS 의 TCP Timeout 이 발생할 때까지 '대기' 상태가 됨.

---
###### 장애 상황 1 해결 방안
- Driver-Level 에서의 Socket timeout 을 설정 함.
- 여러 드라이버들이 위와 같은 Socket timeout을 설정하며, HikariCP 또한 지원 함.

---
###### 장애 상황 2
- JVM 또는 OS 에 의해 DNS Caching 이 생기는게 또 다른 문제 상황이라고 설명하고 있음. 
- Database 에 장애가 발생해 Recovery 하고 있는데, Database 의 hostname 이 여전히 고정 값인데, 데이터베이스 IP 바껴버리면 Caching 된 데이터베이스 정보가 남아있기에 Recovery 에 영향을 미침.

---
###### 장애 상황 2 해결 방안
- 위 상황을 해결하기에 JVM 의 TTL 을 설정하면 된다고 함. 캐시 Expire 시간을 설정함.
- 참고 : [https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-jvm-ttl.html](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-jvm-ttl.html)



---
Reference : [https://github.com/brettwooldridge/HikariCP/wiki/Rapid-Recovery](https://github.com/brettwooldridge/HikariCP/wiki/Rapid-Recovery)