---
layout: post
title:  "Everytime Scraper"
description: "Everything of Everytime. Anytime."
categories: data_collecting
read_minutes: 10
is_project_page: true
show_downloads: false
linux_compatible: false
---

# **Table of Contents**

1. **Introduction**
  - Why do I come up with this project?
  - Objective
2. **Planning**
3. **Execution**
  - Scarver
  - Database
  - Server
4. **Concluding Remark**

- **Troubleshooting Footnotes**

* * *

## **1. Introduction**
> #### **Why do I come up with this project?**

　4년동안 에브리타임을 써 오면서 불편한 점: 글이 자주 삭제된다. 질문글 기능이 있지만 쓰는 사람이 1/10이 되려나..?<sup>[t1](#ftn_1)</sup>

　졸업할 때가 되기는 했지만 에브리타임에 올라오는 글을 아카이브로 저장해두는 것이 매우 유용할 것으로 생각해서 만들게 됐다.

> #### **Objective**

　삭제 걱정 없이 Data Collectiong 가능. 정보(Data)를 누군가 독식하고 삭제하는 것을 방지. 

　집에 리눅스 서버가 있지만  AWS 클라우드에 올려 누구나 서버 걱정 없이 사용하게 만들고자 함.

　이것으로 추후 여러 분석도 가능할 것으로 기대함. ex) Text mining을 해 대학생의 말투를 패턴화하면 에브리타임 계정을 사고 들어온 40대 진보 아저씨를 구별할 수 있지 않을까?

　ex2) 예전에 교수님한테 들었던 말인데 서울 상위권 대학과 중위권 대학의 학벌 차이는 그렇게 크지 않고, 자신감 차이가 크다고 말했다. 대학 별로 Sentiment Analysis를 한다면 이 말을 증명할 수 있지 않을까?

* * *

## **2. Planning**
> #### **Keep it Simple, Stupid.**

　쉽고 간단하게 만들자는 것이 개발 철칙. 필요한 기능만 만들고자 했다.

1. 10분 단위로 에브리타임의 게시글을 가져와서 데이터베이스에 저장
2. 게시판 한정 & 검색
3. 기존 게시글에 덧글이 추가되면 자동으로 업데이트
4. 서버는 클라우드로 이용

　Planning을 그렇게 거창하게 하지 않는 성격이라서 개략적으로만 머리 속에 두고 바로 본 페이지로 넘어감

　다만 예상되는 문제점은 짚고 넘어가는 것은 좋다고 생각.
1. 로그인 기능
2. 덧글 추가 위한 기존 데이터와 대조
3. 

* * *

## **3. Execution**
> #### **Scraper**

　이 프로젝트 이전에도 여러 토이 프로젝트를 진행했는데, 개발 과정에서 선택이 정말 중요하다는 생각이 들었다. 

　Scraper는 `selenium` 패키지를 사용할 것이다. `requests`와 `beautifulsoup`을 사용해서 만든 적이 있었는데 자바스크립스를 사용한 페이지에서의 scraping activity가 많이 제한

```python
def os_selection():
    if os.name == 'posix':	# Selenium on Ubuntu
		# some code...
    elif os.name == 'nt':    # Selenium on Windows
		# some code...
    return browser
```

[CSS Diner]:https://flukeout.github.io/
여기서 CSS Selector를 직관적으로 배울 수 있었다.
[Pandas Index]:https://gooopy.tistory.com/92

AWS websites
[Pandas Index]:https://gooopy.tistory.com/92
[Putty]:https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/putty.html
[Amazon EC2  Putty username ==> ec2-user]:t.ly/mYNz
[AWS Putty 인바운드 규칙]:t.ly/txtL
[Python scripts on an AWS EC2]:t.ly/lIfs
[Python version change in AWS EC2]:t.ly/OpRJ

* * *

## **4. Concluding Remarks**


* * *


## **Troubleshooting Footnotes**

<a name="ftn_1">t1</a>: 주석에 관한 설명을 이곳에...

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

<img src = "https://www.dropbox.com/s/yz0mymrk6lpxwe1/1.png?raw=1" style = "width:100%; object-fit: contain">
![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Definition lists can be used with HTML syntax.
<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>