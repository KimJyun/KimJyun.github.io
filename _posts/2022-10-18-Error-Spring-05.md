---
title: "[Error][Spring][AWS] java.sql.SQLException: No database selected "
excerpt:
categories:
  - Spring
  - Error
tags:

date: 2022-10-18
last_modified_at: 2022-10-18
---

로컬 DB 사용하다가 AWS RDS로 바꾸고 배포 하려고 하는데 오류가 났다.

```
java.sql.SQLException: No database selected
```

<br/>

### 해결방안

DB의 데이터베이스명이 선택되지 않아 생긴 에러이다.

`application.yml`

```
spring:
  datasource:
    url: jdbc:mysql://{rds 엔드포인트}:3306/{database명}
    username:
    password:
```

rds 엔드포인트 뒤에 : 3306/{database명} 을 추가하면 해결된다.
