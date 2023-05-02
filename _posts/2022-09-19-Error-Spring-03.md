---
title: "[Error][Spring] org.mariadb.jdbc.Driver 오류"
excerpt:
categories:
  - Spring
  - Spring_Error
tags:

date: 2022-09-19
last_modified_at: 2022-09-19
sidebar_main: true
---

`application.properies`에서 driver 부분이 인식을 못하고 빨간색으로 되어 있었고, 스프링부트 실행하면 오류가 떴다.

`application.properies`

```
spring.datasource.driver-class-name=org.mariadb.jdbc.Driver
```

에러 메세지

```
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'dataSourceScriptDatabaseInitializer' defined
```

<br/>

### 해결 방법

1. `application.properies`에서 문장 끝 Driver 뒤에 공백이 있는 지 확인
2. 라이브러리가 아직 인식이 안된 경우 gradle refresh 하기

<img width="598" alt="image" src="https://user-images.githubusercontent.com/31675698/190979104-0cec2cb8-d4a0-4130-b3a3-271f92f28840.png">

<br/>

참고 : [https://www.inflearn.com/questions/94737](https://www.inflearn.com/questions/94737)
