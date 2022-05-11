---
title: "[SpringBoot] ./gradlew.bat build : command not found"
excerpt : 
categories:
  - SpringBoot
  - Error
tags:


date: 2022-05-07
last_modified_at: 2022-05-07
---

# [SpringBoot] Window : ./gradlew.bat build error

## Gradle 빌드하기
1. [Window] Git Bash 실행 or cmd에 wsl 입력
2. 프로젝트 경로로 이동
3. [Window] : ./gradlew.bat build <br>
[macOS] : ./gradlew build <br/><br/>
이 과정에서 오류가 났다.
![image](https://user-images.githubusercontent.com/31675698/167251975-05d19c4c-06b6-4018-a243-2c6644221a5c.png)

>시도
>- gradlew clean build 해봤는데 해결 못함
>- cmd에 wsl로 사용하다가 git bash로 바꿔서 `gradlew.bat build` 하니까 해결 ~~....왜??~~
![image](https://user-images.githubusercontent.com/31675698/167252239-6c8a59e4-9fa2-4962-bae2-1700ff1f4e05.png)
4. `cd build/libs`
5. `java -jar hello-spring-0.0.1-SNAPSHOT.jar`
6. 실행 확인
![image](https://user-images.githubusercontent.com/31675698/167252331-ed1f603d-1de1-4e5d-ae10-eec88ea8f41d.png)

얏호~~ 성공