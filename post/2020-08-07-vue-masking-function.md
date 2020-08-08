---
title: vue.js 마스킹 function
date: 2020-08-07 20:52:00 +/-TTTT
categories: [vue.js]
tags: [vue.js]     # TAG names should always be lowercase
---

## vue.js 마스킹 function
- email 마스킹
- @ 뒤에 글자를 전부 마스킹 한다. 

```html
export function masking(value, type) {
  let val = '';
  var str = value.toString();
  if (type == 'email') {
    if (str.includes("@")) {
      val = str.substring(0, str.indexOf("@")) + "*".repeat(str.length - str.indexOf("@")); 
    } else {
      val = str;
    }
  } else {
      returnVal = value;
  }

  return returnVal;
}


```