---
title: "[Error][Spring] Port 8080 was already in use."
excerpt:
categories:
  - Spring
  - Spring_Error
tags:

date: 2022-08-01
last_modified_at: 2022-08-01
sidebar_main: true
---

## Tomcat Error : Port 8080 was already in use.

![image](https://user-images.githubusercontent.com/31675698/182081717-68f03de6-0399-44ca-b52c-e3a2f0db38ee.png)

분명 스프링 종료하고 껐는데 스프링 실행 시 8080포트를 쓰고 있다고 에러가 났다.

<br/>

### 해결 방법

8080 포트를 쓰고 있는 프로그램을 찾아서 강제로 종료시키면 된다.

![스크린샷 2022-07-31 오후 5 28 34](https://user-images.githubusercontent.com/31675698/182171820-d31bc7fb-2d6a-4783-9f9d-7440bc5c5080.png)

실행중인 스프링부트를 종료하니 오류없이 다시 잘 실행되었다!

참고 : [stackoverflow.com/questions/](https://stackoverflow.com/questions/34253779/tomcat-server-error-port-8080-already-in-use)
