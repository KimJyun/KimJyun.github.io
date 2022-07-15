---
title: "[Crawling][Scrapy] 공부하며 정리하기 - 01"
excerpt:
categories:
  - Crawling
  - Scrapy

tags:
  - Crawling
  - Scrapy

date: 2022-07-14
last_modified_at: 2022-07-14
---

# [Crawling] Scrapy 정리 01

## Scrapy 프로젝트의 기본 구조

```
scrapy.cfg
myproject/
    __init__.py
    items.py
    middlewares.py
    pipelines.py
    settings.py
    spiders/
        __init__.py
        spider1.py
        spider2.py
        ...
```

- 프로젝트 루트 디렉토리 : `scrapy.cfg` 파일이 있는 디렉토리
  > 프로젝트 설정을 정의하는 python 모듈의 이름이 포함된다.

```
[settings]
default = myproject.settings
```

## 프로젝트 만들기

```
scrapy startproject <myproject> [project_dir]
```

명령어를 입력하면 `project_dir`디렉토리 아래에 `myproject`라는 이름으로 scrapy 프로젝트가 생성된다.
<br/><br/>
다음으로 새 프로젝트 디렉토리로 이동한다.

```
cd [project_dir]
```

여기에서 `scrapy`명령을 사용하여 프로젝트를 관리하고 제어가 가능하다.
<br/><br/>

## 프로젝트 제어

- 새 spider 만들기

```
scrapy genspider <name> <domain or URL>
```

### 📎 crawl

```
scrapy crawl <spider>
```

- 프로젝트 필요

spider를 사용하여 크롤링을 시작한다.

### 📎 fetch

```
scrapy fetch <url>
```

- 프로젝트 필요 없음

Scrapy Downloader를 사용하여 주어진 url을 다운로드하고 내용을 표준 출력에 쓴다.
<br/><br/>

지원되는 옵션 :

- `spider=SPIDER` : spider 자동 감지 우회 및 특정 스파이더 강제 사용
- `--headers` : request의 body 대신 request의 HTTP Header를 출력
- `no-redirect` : HTTP 3xx redirects을 따르지 않음(default : redirects 따름)

사용 예시 :

```
$ scrapy fetch --nolog http://www.example.com/some/page.html
[ ... html content here ... ]

$ scrapy fetch --nolog --headers http://www.example.com/
{'Accept-Ranges': ['bytes'],
 'Age': ['1263   '],
 'Connection': ['close     '],
 'Content-Length': ['596'],
 'Content-Type': ['text/html; charset=UTF-8'],
 'Date': ['Wed, 18 Aug 2010 23:59:46 GMT'],
 'Etag': ['"573c1-254-48c9c87349680"'],
 'Last-Modified': ['Fri, 30 Jul 2010 15:30:18 GMT'],
 'Server': ['Apache/2.2.3 (CentOS)']}
```

### 📎 view

```
scrapy view <url>
```

- 프로젝트 필요 없음

Scrapy spider 가 보는 것처럼 브라우저에서 주어진 URL을 연다. 가끔 spider가 보는 페이지가 우리가 보는 것과 다를 수 있기 때문에 예상한 내용인지 확인하기 위해 사용할 수 있다.

사용 예 :

```
$ scrapy view http://www.example.com/some/page.html
[ ... browser starts ... ]
```

### 📎 Shell

```
scrapy shell [url]
```

- 프로젝트 필요 없음

주어진 URL에 대해 Scrapy shell을 실행하거나 URL이 제공되지 않은 경우는 비어 있다. <br/>
또한, `./`, `../` 같은 절대 파일 경로인 UNIX 스타일 의 로컬 파일 경로를 지원한다.

지원되는 옵션 :

- `-c code` : shell에서 코드를 평가하고 결과를 출력하고 종료

사용 예 :

```
$ scrapy shell http://www.example.com/some/page.html
[ ... scrapy shell starts ... ]

$ scrapy shell --nolog http://www.example.com/ -c '(response.status, response.url)'
(200, 'http://www.example.com/')

# shell follows HTTP redirects by default
$ scrapy shell --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)'
(200, 'http://example.com/')

# you can disable this with --no-redirect
# (only for the URL passed as command line argument)
$ scrapy shell --no-redirect --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)'
(302, 'http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F')
```

### 📎 Parse

```
scrapy parse <url> [options]
```

- 프로젝트 필요

`--callback` 옵션과 함께 전달된 메서드를 사용하거나 지정되지 않은 경우 지정된 URL을 가져와 이를 처리하는 spider로 분석한다.

지원되는 옵션 :

- `--spider==SPIDER` : 스파이더 자동 감지 우회 및 특정 스파이더 강제 사용
- `--a NAME=VALUE` : 스파이더 인수 설정(반복 가능)
- `--callback` 또는 `-c` : 응답 구문 분석을 위한 콜백으로 사용할 스파이더 메서드
- `--meta` 또는 `-m` : 콜백 요청에 전달할 추가 요청 메타. 유효햔 JSON 문자열이어야 한다. 예) `cbkwargs='{"foo":"bar"}'`
- `--cbkwargs` : 콜백에 전달될 추가 키워드 인수. 유효한 JSON 문자열이어야 한다. 예) `'cbkwargs='{"foo":"bar"}'`
- `--pipelines` : 파이프라인을 통해 항목을 처리
- `--rules` 또는 `-r` : `CrawlSpider` 응답을 구분 분석하는 데 사용할 콜백
- `--noitems` : 스크랩한 항목을 표시하지 않음
- `--nolinks` : 추출된 링크를 표시하지 않음
- `--nocolour` : 출력물을 채색하기 위해 안료를 사용하지 마라.
- `--depth` 또는 `-d` : 요청을 재귀적으로 따라야 하는 깊이 수준(default : 1)
- `--verbose` 또는 `-v` : 각 깊이 수준에 대한 정보 표시
- `--output` 또는 `-o` : 스크랩한 항목을 파일에 덤프

사용 예 :

```
$ scrapy parse http://www.example.com/ -c parse_item
[ ... scrapy log lines crawling example.com spider ... ]

>>> STATUS DEPTH LEVEL 1 <<<
# Scraped Items  ------------------------------------------------------------
[{'name': 'Example item',
 'category': 'Furniture',
 'length': '12 cm'}]

# Requests  -----------------------------------------------------------------
[]
```

### 📎 Runspider

```
scrapy runspider <spider_file.py>
```

- 프로젝트 필요 없음

프로젝트를 만들 필요 없이 Python 파일에 자체 포함된 spider를 실행한다.

사용 예 :

```
$ scrapy runspider myspider.py
[ ... spider starts crawling ... ]
```
