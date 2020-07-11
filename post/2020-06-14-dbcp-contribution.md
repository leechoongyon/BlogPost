---
title: apache-dbcp connectionFactory 개선사항 정리
date: 2020-06-14 21:03:00 +/-TTTT
categories: [opensource, dbcp]
tags: [dbcp]     # TAG names should always be lowercase
---


- dbcp 관련 개선사항을 정리. 추후 관련 내용을 다시 봤을 때 기억이 안날 것을 대비해 적어놓음.

#### 내용
- MyBatis 에서 dbcp 를 통해 connection 을 가져올 때마다 connection 관련 추가적으로 해야 할 요건이 있음. 추가적인 요건을 A라 가정. 그런데 connection 을 가져올 때 마다 A를 수행하다 보니 기존에 이미 A 를 수행했던 Connection 이 또 다시 A 를 수행하니 오버헤드가 발생 됨.
- 그렇기에 dbcp 내에서 connection 을 생성할 때, 한 번만 해당 로직을 수행하도록 진행할려고 했음.
- 하지만 dbcp 내에 connection 을 생성할 때, 해당 로직을 실행할 수 있는 interface 가 없음.
- dbcp 쪽에 해당 이슈를 개선사항으로 제기하고, github 에 PR 을 제공하여 dbcp 2.7 버전에 위 사항을 반영 함.
- 관련 issue ticket : [https://issues.apache.org/jira/browse/DBCP-547?filter=-2]