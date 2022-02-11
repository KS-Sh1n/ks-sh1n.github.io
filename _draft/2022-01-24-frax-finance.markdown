---
layout: post
title:  "Junior Economist's Perspective on Frax Finance. "
description: "How innovative does it? Is it a really worthwhile move?"
categories: blockchain
read_minutes: 10
is_project_page: false
show_downloads: false
linux_compatible: false
---

* * *

https://medium.com/@hasufly/maker-dai-stable-but-not-scalable-3107ba730484
https://thelonelyghost.substack.com/p/what-the-frax
https://medium.com/kokoa-finance/how-stablecoin-ecosystem-grows-a3f9aa32f346

　가상화폐를 공부한 사람이라면, 스테이블코인(Stablecoin)의 존재를 모르는 사람은 없을 것입니다. 스테이블코인이란, 가상화폐 한 단위의 가치가 $1와 연결되도록(pegging) 설계한 가상화폐입니다. 우리가 매일같이 쓰는 USDT, USDC, DAI 등이 모두 스테이블코인으로 가상화폐 시장의 안전자산과 기둥과 같습니다.

　스테이블코인은 한 마리의 백조와 같습니다. 겉으로 보면 달러 대신 사용할 수 있는 매우 우아한 가상화폐지만, 그 안에는 최대한 효율적이고 신뢰성 있는 스테이블코인을 만들기 위한 개발자들의 노력의 발장구가 담겨 있습니다. 그리고 본 내용에 들어가기 전에 그 작동 원리를 잠깐 설명하고자 합니다.

　스테이블코인은 크게 2가지의 기반에서 설계됩니다. 하나는 담보 기반, 다른 하나는 알고리즘 기반입니다. 

# **담보 기반 스테이블코인**

### **● 핵심**
　유통하는 스테이블코인 $1당 최소 $1 이상의 담보를 다른 자산으로 가지고 있습니다. 예를 들어, MakerDAO에서 유동하는 DAI는 스테이블코인과 이더리움같은 다른 가상화폐를, USDC는 실제 달러 자산(현금 + 단기 채권)을 스테이블코인의 담보로 가지고 있습니다.

<img src = "https://www.dropbox.com/s/zsr1trhosl1l1cy/20.png?dl=0" style = "width:100%; object-fit: contain">

#### **● 장점**
  - 신뢰성

　담보 자산의 가치가 폭락하지 않는 이상 투자자는 언제나 시장에 유통되는 스테이블코인을 $1과 교환할 수 있다는 확신을 가질 수 있습니다. 또한, 유통되는 모든 스테이블코인이 담보로 보증되어 있기 때문에 뱅크런과 같은 리스크를 걱정할 필요도 없습니다. 이는 스테이블코인 가격을 유지하기 위한 신뢰에 매우 중요합니다.

  - 가격 안정성

　스테이블코인의 가치를 보증하는 담보의 존재는 스테이블코인의 가치를 $1로 유지하는 것을 훨씬 쉽게 만듭니다. 쉽게 신뢰를 얻고 가격을 유지할 수 있다는 점 때문에 대부분의 스테이블코인 프로젝트가 담보 기반 스테이블코인을 채택하고 있습니다.

#### **● 단점**
  - 비효율성

　담보가 있다는 것은, $1의 스테이블코인을 유통하기 위해 적어도 $1 이상을 금고에 가지고 있어야 한다는 의미입니다. 추가적으로 담보로 가지고 있는 가상화폐의 본질적으로 높은 변동성에서 오는 리스크를 충당하려면 더 많은 담보를 가질 인센티브가 생깁니다.  예를 들어, DAI는 유통하는 DAI보다 훨씬 많은 양의 가상화폐를 담보로 가지고 있습니다.

  - 더 높은 기회비용

　담보를 많이 보유할수록 담보를 스테이킹 등에 활용하지 못하는 데에서 오는 기회비용이 증가합니다. 프로젝트 개발자는 이러한 기회비용을 충당하기 위해 스테이블코인의 대출 이자는 높게, 예치 이자는 낮게 설정할 인센티브를 가질 것입니다. 다량의 자산을 보관하는 데서 오는 고유위험(custodial risk)도 무시할 수 없을 것입니다.

# **알고리즘 기반 스테이블코인**

### **● 핵심**
　스테이블코인 한 단위의 가격을 $1로 유지하는 조정 알고리즘을 도입하는 것입니다. 담보는 유동하는 스테이블코인의 일부만 두기도 하고 아예 두지 않기도 합니다. 가장 대표적인 알고리즘 기반 스테이블코인은 테라 생테계에서 사용되는 스테이블코인 UST입니다.

#### **● 장점**
  - 효율성(Capital Efficiency)

　알고리즘 기반 스테이블코인은 가격에 따른 상대적인 공급량을 조절해 $1을 유지합니다. 이는 스테이블코인 가격을 유지하는 데 담보를 이용할 필요가 없어진다는 의미입니다. 담보의 부재는 담보 기반 스테이블코인 프로젝트보다 더 낮은 대출 이자, 더 높은 예치 이자를 달성할 수 있게 만듭니다.

#### **● 단점**

  - 어려움

　'제대로 작동하는 알고리즘'을 만드는 것이 매우 어렵습니다. 알고리즘을 조금이라도 잘못 설계하면 알고리즘이 역방향으로 작동해 $1을 유지할 수 없어지기 때문입니다. 알고리즘 기반 스테이블코인의 문제점에 대해 더 자세히 알고 싶다면 [코코아 파이낸스의 글](https://medium.com/kokoa-finance/kokoa-finance-fixing-stablecoin-designs-kr-3c99a17d0e9f) 을 참고하면 좋을 것 같습니다.

### 알고리즘 기반 스테이블코인
- 장점 : 수요와 공급에 의한 알고리즘에 따라 발행량을 결정하므로 1달러 페깅이 쉬움
- 단점 : 발행된 스테이블 코인을 뒷받침하는 담보가 없으므로 믿음이 깨지면 시스템이 붕괴함

  - 초기 생존의 어려움

　스테이블코인이 100% 담보로 뒷받침되지 않는다는 것은 '신뢰 기반'의 부재를 의미합니다. 그리고 이는 초기 프로젝트의 안정성에 큰 영향을 미칩니다. 스테이블코인의 시장 규모가 작은 프로젝트 초기에 스테이블코인을 뒷받침하는 담보가 100%가 아니거나 아예 없다면, 작은 변화에도 사람들이 민감하게 반응할 것이고, 스테이블코인의 주 목적인 가격 유지 기능을 달성하기가 어려워집니다.

# Frax Finance의 등장

　'제대로 작동하는 알고리즘'을 만드는 것의 매우 어렵기 때문에 알고리즘 기반 스테이블코인 프로젝트 대부분은 실패로 끝났습니다. 그럼에도 시도는 계속되었고, 여기서 Frax Finance가 등장합니다. Frax는 

Frax는 담보의 신뢰성과 알고리즘의 효율성을 합치자는 생각을 했디. 그리고 결론부터 말하자면, Frax는 성공했다. 알고리즘 방식으로 조정되는 스테이블코인 메커니즘을 채택하면서도, 오랫동안 살아남았기 때문이다.

# Frax Finance는 어떻게 성공했을까?
먼저, Frax는 기존의 담보 기반 스테이블코인 메커니즘에서 시작한다. Frax Finance의 스테이블코인, FRAX를 $1만큼 빌리기 위해 $1만큼의 스테이블코인 담보를 맡아두는 것이다. 

그러나 Frax Finance의 핵심은, $1 만큼의 FRAX를 빌리기 위해 반드시 $1만큼의 담보가 필요한 것이 아니라는 관념을 깨는 것에서 시작합니다. Frax Finance는 담보 비율이라는 개념을 도입했습니다. 예를 들어, 담보 비율이 50%라면, $1 만큼의 FRAX가 $0.5 만큼의 달러로 보증이 된다는 의미입니다. 그리고 담보로 보증되지 않는 부분은 알고리즘을 통해 FRAX의 가격 안정성을 조정합니다.

Frax Finance는 최적의 담보 비율을 정하는 방법을 시장에 물어봄으로써 해결했습니다.

FRAX의 가격이 $1보다 높다면, 이는 시장이 FRAX에 더 많은 수요를 보이고 FRAX에 대해 충분한 신뢰를 보이고 있다는 신호입니다. 기존의 스테이블코인 프로토콜은 시장 참가자의 무위험 수익 (Arbitrage Opportunity) 인센티브를 이용해 올라간 가격을 $1로 맞추려고 합니다.

그러나 FRAX는 내재된 프로토콜을 통해 담보 비율을 낮춤으로써 가격 상승에 대응합니다. 담보 비율이 낮아지면, $1 만큼의 FRAX를 얻기 위해 지불해야 하는 보증

반대로 FRAX의 가격이 $1보다 낮다면, 시장이 FRAX에 대해 충분한 신뢰를 보이지 않다는 신호다. 그러면 FRAX는 내재된 프로토콜을 통해 담보 비율을 높인다.

시장에게 "너는 얼마만큼의 담보를 맡기고 싶어?"를 물어봄으로써 효율성을 유지할 수 있었다? 이에 맞게 담보 비율을 조정한다.

스테이블코인에 담보를 둔다는 것은 달러의 가치를 인정한다는 뜻이라고 생각함.
스테이블코인의 탈담보 움직임은 달러에서 벗어나려는 시도라고 볼수도 있을듯.

# Frax가 나아가는 방향
Frax finance는 부분 담보 기반 스테이블코인이라는 새로운 분야를 개척했습니다. 그러나, Frax의 목표는 담보 기반 스테이블코인에서 시작해 완전히 알고리즘을 기반으로 하는 스테이블코인을 만드는 것입니다.

FPI에 대한 설명
Frax's **end vision is to build the first crypto native version of the CPI called the Frax Price Index (FPI)** governed by FXS holders (and other protocol tokens). FRAX is currently pegged to USD but aspires to become the first decentralized, permissionless native unit of account which holds standard of living stable.

# **Final Thought**
담보 기반 스테이블도 진화하고 있습니다. 맡아놓은 담보를 리스크가 낮은 곳에 스테이킹함으로써 비효율성 문제를 해결하고 있습니다. 그러나, 안정성이 가장 우선되는 Core level의 담보 기반 스테이블코인(DAI, USDC)은 이러한 전략을 펼치기가 어려울 것입니다. 수많은 알고리즘 기반 스테이블코인 프로젝트들이 Core level의 스테이블코인 위치를 차지하기 위해 지금도 노력하고 있습니다.

스테이블코인의 가장 중요한 요소는 $1을 얼마나 잘 유지하는가라고 생각합니다. 

그 신뢰를 초반에는 담보로 잡고 이후에는 프로젝트 운영으로 쌓인 신뢰로 대신한다는 생각은 좋은 것 같다.

과도기적인 상황이지 않을까?

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