---
title: "[Error][Spring] 빌드 시 java 버전에 의한 오류 및 해결"
excerpt:
categories:
  - Spring
  - Spring_Error
tags:

date: 2022-10-18
last_modified_at: 2022-10-18
sidebar_main: true
---

에러 메시지

```
Caused by: java.lang.UnsupportedClassVersionError
Java Runtime only recognizes class file versions up to 52.0
```

빌드 시 자바 버전이 맞지 않아 생긴 오류이다.

<br/>

## 해결방안

로컬 pc의 버전을 보니 `openjdk 17` 버전이다. <br/>
따라서 openjdk 17버전으로 다시 설치해 해결했다. <br/>

### 자바 버전 확인을 위한 명령어

```
$ java -version
```

### openjdk 17 버전 설치

```
wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.rpm

sudo rpm -ivh jdk-17_linux-x64_bin.rpm

sudo alternatives --config java

java -version

```

<br/><br/>

참고 : [https://binux.tistory.com/m/122](https://binux.tistory.com/m/122)
