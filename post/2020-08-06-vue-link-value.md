---
title: vue.js 링크 value 에 마스킹 데이터 세팅 방법
date: 2020-08-06 20:24:00 +/-TTTT
categories: [vue.js]
tags: [vue.js]     # TAG names should always be lowercase
---

## vue.js 링크 value 에 마스킹 데이터 세팅 방법
- html 은 아래와 같이 작성
- backend 에서 데이터 보내줄 때, 마스킹된 데이터와 마스킹 되지 않은 데이터를 같이 보내줌.
- 찍을 때는 마스킹된 데이터를 보내주고, 실제 method 에 데이터를 전해줄 때는 마스킹 안된 데이터를 전해줌.
```html
<el-table-column prop="maskingData" label="마스킹데이터" v-if="false" width="120" align="center"/>
<el-table-column prop="data" label="일반데이터" width="120" align="center">
    <template slot-scope="props">
    <a href='#' @click="clickMethod(props.row.data)" >{{props.row.maskingData}}</a>
    </template>
</el-table-column>

``` 
