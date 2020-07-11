---
title: apache-commons-email 첨부파일 명에 한글 포함될 경우 깨지는 현상
date: 2020-06-14 21:05:00 +/-TTTT
categories: [opensource, apache-email]
tags: [apache-email]     # TAG names should always be lowercase
---

#### Issue
- Apache-common-email API 를 사용 중 첨부 파일명에 한글 명이 들어갈 경우 첨부파일 명이 깨지는 현상

#### Environment
- apache-common-email.1.5.jar
- javax.mail-api.1.6.1.jar

#### 원인 분석
- javax.mail-api.1.6.1 jar 를 사용해서 첨부 파일을 보내면 깨지지 않고 정상적으로 보내 짐.
- 관련하여 Apache-email 소스를 분석한 결과 MultiPartEmail 쪽의 fileName 을 MimeUtility.encodeText(...) 를 사용하지 않을 경우 정상적으로 동작. 테스트 했을 경우, pdf, jpg, text, zip 등 사용하고 있는 파일 확장자에 대해 정상적으로 출력 됨.
- commons-email 에서 fileName 을 encode 해서 base64 로 filename 이 encoding 됐는데, javax.mail-api 에서 base64 로 인코딩된 fileName 을 한 번 더 handling 하는 과정에 첨부파일 명에 delimiter 가 추가 됨. 첨부파일 명에 delimiter 가 붙음으로 인해 SMTP 서버에서 첨부파일명을 해석하지 못함.
#### 이슈 제기
- apache-common jira 에 이슈 등록 
	- MultiPartEmail 소스를 수정해도 되는지에 대해 
- stackoverflow 에 이슈 등록
	- [https://stackoverflow.com/questions/57388873/why-attachment-file-name-broken-when-using-the-apache-email-library]
	- commons-email Encoding 안해도 된다는 답변 받음.