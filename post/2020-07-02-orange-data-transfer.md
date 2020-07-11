---
title: orange 툴 data transfer 방법     
date: 2020-07-02 19:00 +/-TTTT
categories: [tool]
tags: [tool]     # TAG names should always be lowercase
---

> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## orange tool data transfer 방법
- 운영 DB 에 있는 데이터를 개발로 가져오고 싶을 때
- Orange 메뉴에 보면 Tools/Unload Tool, Load Tool 이 있음.
- Unload Tool 은 테이블 데이터를 로컬에 내리는 것이고, Load 는 DB 에 저장하는 것임.
- 전체적인 순서는 Unload Tool 을 통해 운영 DB 데이터를 로컬에 파일로 저장하고, 해당 파일을 가지고 개발 디비 가서 Load 하면 된다. 