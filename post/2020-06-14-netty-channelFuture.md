---
title: netty ChannelFuture
date: 2020-06-14 22:50:00 +/-TTTT
categories: [netty]
tags: [netty]     # TAG names should always be lowercase
---


#### netty ChannelFuture
```text
The result of an asynchronous Channel I/O operation.
All I/O operations in Netty are asynchronous. It means any I/O calls will return immediately with no guarantee that the requested I/O operation has been completed at the end of the call. Instead, you will be returned with a ChannelFuture instance which gives you the information about the result or status of the I/O operation.

A ChannelFuture is either uncompleted or completed. When an I/O operation begins, a new future object is created. The new future is uncompleted initially - it is neither succeeded, failed, nor cancelled because the I/O operation is not finished yet. If the I/O operation is finished either successfully, with failure, or by cancellation, the future is marked as completed with more specific information, such as the cause of the failure. Please note that even failure and cancellation belong to the completed state.
```
- netty 공식 설명에는 다음과 같이 나와있음.
- 비동기 채널 I/O 작업의 결과물. 상태와 결과를 알려주는 객체라 생각하면 될듯
- 이 부분이 자바의 future 패턴임.
    - 작업이 오래 걸리는 것에 대해 비동기 처리한 후, 뒤에서 처리될 동안 다른 작업을 하겠다라는 패턴


#### Reference
- https://netty.io/4.0/api/io/netty/channel/ChannelFuture.html