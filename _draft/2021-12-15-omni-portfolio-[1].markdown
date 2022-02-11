---
layout: post
title:  "Optimal Crypto Portfolio"
description: "1. Securing Alpha in a Highly Volatile Market"
categories: finance
read_minutes: ?
is_project_page: false
show_downloads: false
linux_compatible: false
---

# **Table of Contents**

1. Introduction
  - Why do I come up with this project?
  - Objective
2. Drafts & Plans
  - Idea
  - Data
  - Algorithm
  - Important Factors
3. What can I learn
4. References

* * *

### 문단 복사 붙여넣기용
<p>　</p>

## **1. Introduction**
> ### **Why do I come up with this project?**

<p>　가상화폐로 돈복사한 사람도 많지만, 그 이면에는 잘못된 투자로 인해 큰 돈을 잃은 사람도 훨씬 많을 것이다. 역사에는 승자의 기록만 존재한다고 하지 않나. 무지성 상승장에는 모든 사람이 돈을 벌겠지만, 그런 장이 다시 온자는 보장도 없을 것이다.</p>
<p>　가상화폐 시장은 크게 두 가지 측면으로 활용될 수 있다고 생각한다. 첫째, 큰 리스크를 가져가면서 성공하면 대박을 보는 것. 둘째, 적은 리스크를 가져가면서도 다른 포트폴리오보다 높은 수익률을 얻을 수 있는 것. 여기서는 두 번째 측면으로 가상화폐를 활용하고자 한다.</p>
<p>　투기용으로 가상화폐가 주로 사용되는 것을 뉴스에서 볼 수 있지만, 나는 투기와 헤징을 동시에 활용하고자 한다. </p>
<p>　그리고 제약 조건 내에서 optimization이라는 논리는 경제학과 데이터 분석을 통한 인사이트 발견이 가장 잘 맞아떨어지는 구간이라고 생각한다. </p>

> ### **Objective**

<p>　가상화폐를 포함한 포트폴리오를 통해서 얻고자 하는 것은 동일하다. Max Profit & Min Risk. 그리고 Same risk 대비 얻을 수 있는 Profit이 일반 포트폴리오 대비 훨씬 높을 것으로 기대한다.</p>
<p>　과거 시장 Asset의 가격을 기반으로. Max Profit과 Min Risk를 가져다주는 Portfolio 조합을 추천하는 것까지는 기존과 동일하다. 그러나, 여기서 추가하고자 하는 것은 Defi protocol의 도입이다. Defi LP staking 또는 farming을 통해서 얻을 수 있는 이익을 포트폴리오 profit과 risk에 도입하는 것이다. 모델은 복잡해지겠지만 더 높은 profit을 가지는 모델을 얻을 수 있을 것으로 기대한다.</p>

* * *

## **2. Drafts & Plans**
> ### **Idea**

<p>　구현하고자 하는 기본적인 아이디어는 다음과 같다.</p>

  - 선물, 옵선 가격, 편비를 감안해 최적의 Portfolio 비율을 능동적으로 조정.
  - Portfolio 비율을 능동적으로 조정해 내가 원하는 APR이나 Risk tolerance를 맞추기
  - 포트폴리오의 과거 out-of sample 수익률과 실시간 수익률을 그리프로 시각화
  - DCA를 반영해 Portfolio 불어나게 만들기
  - 다양한 투자 옵션 (선물, 옵션 포함)까지 포함해서 최적의 수익률을 낼 수 있는 포트폴리오 조합을 만들기. Thinking about every possible combination.

> ### **Data**
<p>　필요한 데이터를 다음과 같이 정리할 수 있을 것이다.</p>

  - 과거 / 실시간 가상화폐 데이터
  - 파생상품 / Defi 데이터
  - Benchmark 용 S&P 500 데이터

> ### **Algorithm**
<p>　일단 필요한거 붙여넣어보기</p>

  - Mean-Variance Optimization (MVO)
<p>　solve a multi-objective optimization problem subject to basic constraints imposed on the portfolio.</p>

  - Max Sharpe Ratio
<p>　Alternative:  Sortino Ratio and Treynor Ratio</p>

  - Constrained Portfolio Optimization

  - Recommendation Algorithm
<p>　현재 시점에서의 최적의 Spot & Derivative의 조합을 찾아주는 데 추천 시스템이 요긴하게 쓰일 수 있을 것.</p>


<p>　분석 순서</p>

1. 포트폴리오를 정하기
2. Optimization
3. Benchmark(S&P 500)과의 비교
4. 또는 Benchmark와 비교하지 않고 APR과 Risk에 점수를 매겨 가장 높은 점수부터 나열하게 하기?

> ### **Important Factors**
<p>　분석에 중요하게 봐야 할 요소들</p>

  - Risk-Return Tradeoff
  - Which crypto dataset to use?

* * *

## **3. What can I learn**
  - linear scalarization
<p>　Transformation of bi-criterion objective function into single-criterion function</p>



* * *

## **4. References**

[Python implementation of portfolio optimization]

```python
# Python Sample Code
# Remind that code snipset doesn't wrap!
a = "hello, world!"
print(a)
```

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

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

[Python implementation of portfolio optimization]: https://www.kaggle.com/vijipai/notebooks