---
title: mybatis where 조건에 array 를 이용해서 in 조건 사용하기.
date: 2020-06-14 18:45:00 +/-TTTT
categories: [mybatis]
tags: [mybatis]     # TAG names should always be lowercase
---


* mybatis where 조건에 array 를 이용해서 in 조건 사용하기.
---

```java
Map<String, Object> daoIn = new HashMap<>();
daoIn.put("arr", new String[]{"aaa", "bbb"});
```

```xml
<!-- xxx.xml -->
<foreach collection="arr" item="item" index="index" open="(" close=")" separator=",">  
   #{item}  
</foreach>
```

```

