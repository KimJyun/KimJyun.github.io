---
title: "[Error][Scrapy] HTTP status code is not handled or not allowed"
excerpt:
categories:
  - Scrapy
  - Error
tags:

date: 2022-07-14
last_modified_at: 2022-07-14
---

```
INFO: Ignoring response <404 url>: HTTP status code is not handled or not allowed
```

`Scrapy`를 사용하여 웹 페이지를 크롤링할 때 페이지의 http 코드가 404인 경우 scrapy는 이를 무시하지만, <br/>
크롤러에서 http 코드에 대한 특수 처리를 수행하려는 경우에는 수행되지 않는다고 한다.

### 해결 방법

`settings.py`에 추가하기 <br/>
`HTTPERROR_ALLOWED_CODES = [404]`
