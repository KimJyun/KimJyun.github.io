---
title: "[IntelliJ] Indent Issue : 적용한 Indent가 작동 안됨"
excerpt:
categories:
  - IntelliJ
  - Error

tags:

date: 2022-09-04
last_modified_at: 2022-09-04
---

# [IntelliJ]: Indent Issue : 적용한 Indent가 작동 안되는 이슈

naver의 java 컨벤션을 사용하고 있었는데, Indent가 제대로 작동되지 않는 이슈가 생겼다.

저번에도 같은 이슈가 있었는데, 또 발생했다. 그래서 해결방법을 기록해두려고 한다.

컨벤션 : [네이버 컨벤션](https://naver.github.io/hackday-conventions-java/#_intellij)

<br/>

### 해결방법

- File > Settings > Editor > Code Style > Java 메뉴로 이동한다.

- Tabs and Indents 탭으로 이동해서 아래 항목을 입력한다.

- `Use tab charactor` : 미선택
