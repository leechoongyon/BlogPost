---
title: checked, unchecked exception
date: 2020-08-09 10:00:00 +/-TTTT
categories: [java]
tags: [java]     # TAG names should always be lowercase
---

## Check Exception

-   꼭 처리해야만 함. Try catch 명시적
-   Exception 밑에 RuntimeException 을 제외한 모든 Exception
-   컴파일 단계에 확인
-   Rollback 하지 않음 (트랜잭션). 왜냐하면 Checked Exception 이라는건 사용자가 알고 있는 Exception 이니.

## Unchecked Exception

-   명시적으로 처리 X
-   실행단계에 확인
-   Rollback 함. (트랜잭션). 예상치 못한 Exceptio 이 발생했으니.

## 언제 어디에 써야하는가?

-   Checked Exception 의 의도는 명확하다. Exception 이 발생하면 그 Exception 에 대해 인지하고 있어라. 그러니 Exception 에 대한 대처 방법을 명시해라.
-   UnCheckedException 의 의도도 명확하다. Exception 을 명시적으로 체크하지 않는다는 의미이지.
-   CheckedException 을 써야하는지 UnCheckedException 을 써야하는지 위 내용과 관련하여 검색을 해봤는데 마땅히 답은 없음.
-   내 생각은 UnCheckedException 을 쓰는게 맞는거 같음. try catch 가 붙음으로써 소스 가독성이 떨어지고 반드시 Check 해야 하는 Exception 이라는건 변할 수도 있다고 생각 됨. 그러기에 UnCheckedException 을 쓰는게 맞는거 같음.