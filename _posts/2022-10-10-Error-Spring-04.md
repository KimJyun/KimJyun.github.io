---
title: "[Error][Spring] @BeforeAll @AfterAll 사용시 JUnitException"
excerpt:
categories:
  - Spring
  - Spring_Error
tags:

date: 2022-10-10
last_modified_at: 2022-10-10
sidebar_main: true
---

테스트 코드에 @BeforeAll, @AfterAll 어노테이션을 썼는데, 아래와 같은 오류가 났다.

```
org.junit.platform.commons.JUnitException: @AfterAll method '...' must be static unless the test class is annotated with @TestInstance(Lifecycle.PER_CLASS).
```

### 해결방안

`static` 이나 `@TestInstance(Lifecycle.PER_CLASS)` 를 붙이면 된다.

- 각 해당 메서드에 `static` 을 붙인다.
- class Test 위에 `@TestInstance(Lifecycle.PER_CLASS)` 을 붙인다.

~~각 메서드 위에 `@TestInstance` 를 붙여서 오류가 났다.ㅋㅋㅋ~~
