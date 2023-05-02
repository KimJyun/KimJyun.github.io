---
title: "[Algorithm][Python] 프로그래머스 탐욕법(Greedy) > 체육복 (Level 1)"
excerpt: 프로그래머스 체육복 Python
categories:
  - Algorithms
tags:
  - [Algorithms, Python, Programmers]

date: 2023-05-02
last_modified_at: 2023-05-02
---

**문제 설명**

점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 전체 학생의 수는 2명 이상 30명 이하입니다.
- 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
- 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

**입출력 예**

<img width="270" alt="image" src="https://user-images.githubusercontent.com/31675698/235613676-1d65a570-5f68-46f1-924f-7e1b514b047a.png">

<hr>

### 풀이

1. lost와 reserve에 모두 들어있다면, lost, reserve 에서 모두 제거
2. lost를 돌면서, reserve에 앞뒤 숫자가 있다면, 앞->뒤의 우선순위로 제거
3. ```n(전체 학생 수) - len(lost)```가 체육복이 있는 학생 수(answer)

**1차 코드(실패)** 
```python
def solution(n, lost, reserve):
    for l in lost[:]:
        if l in reserve:
            reserve.remove(l)
            lost.remove(l)
        
        if l-1 in reserve:
            lost.remove(l)
            reserve.remove(l-1)
        elif l+1 in reserve:
            lost.remove(l)
            reserve.remove(l+1)
        
    return n-len(lost)
```

**문제**

1. ```for l in lost: lost.remove(l)``` 로 구현했을 때, for문을 도는 l이 전체를 돌지 않고, 중간이 씹히는 현상이 있었다. 
이 경우 list에서 해당 항목이 지워지면서, 인덱스가 앞으로 당겨져 모든 list를 돌지 않아 생기는 문제이다.<br/>
따라서, **list를 복사해서 돌려야한다.(list[:])**

2. lost와 reserve에 동시에 있는 요소를 지우기 위해 for문을 사용한 것을 ```SET```으로 바꾸어 구현했다. <br/>
차집합을 ```-```로 간단하게 구현할 수 있다.

3. 나는 반복문을 lost를 기준으로 돌렸는데, 이렇게 되면,
    - lost의 항목을 지우면서 오류가 생길 수 있고,
    - lost도 지우고, reserve 도 함께 지워줘야 한다.

    그래서, **reserve 로 반복문을 돌아**, reserve의 원소마다 한번씩만 사용할 수 있게 했다.

<br/>

**변경 후 코드(정답)**
```python
def solution(n, lost, reserve):
    set_lost = set(lost) - set(reserve)
    set_reserve = set(reserve) - set(lost)
    for r in set_reserve:
        if r-1 in set_lost:
            set_lost.remove(r-1)
        elif r+1 in set_lost:
            set_lost.remove(r+1)
        
    return n-len(set_lost)
````
