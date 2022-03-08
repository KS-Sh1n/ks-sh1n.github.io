---
layout: post
title:  "DeFi Series 1: Aperture Finance"
description: "디파이 산업에 델타 헤징을 가져오다."
categories: defi
read_minutes: 6
is_project_page: false
show_downloads: false
linux_compatible: false
---

# **●Table of Contents**
### 　　　**1. [About](#about)**<br>
### 　　　**2. [Experience](#experience)**<br>
### 　　　**3. [Team and VCs](#teamvc)**<br>
### 　　　**4. [Verdict](#verdict)**<br>

* * *
　DeFi 프로젝트 분석 아티클입니다. 체인 상관 없이 근본 프로젝트 또는 재미있어 보이는 프로젝트 위주로 들여올 생각입니다.

　**이번 분석 대상은 델타 헤징이 main selling point인 DeFi `Aperture Finance`입니다.**

## **1. About**<a name="about">
> ### **Aperture Finance Summary**

- Cross-Chain 지향 & 서로 다른 DeFi 네트워크를 seamless하게 연결
- 현재는 테라 기반. 추후에 다른 체인으로 확장 예정 (?)
- 실물 or 가상자산을 매개로 하는 Delta-Neutural 전략 제공
- Delta-Neutral 전략은 smart contract으로 자동화됨

> ### **Delta-Neutral?**
Delta-Neutural을 잘 아는 분이라면 이 부분은 넘어가셔도 됩니다.

　Delta-Neutural을 처음 들어보는 사람이 많을 것입니다. 한 마디로 요약하면 **파생상품을 적절히 조합해 가격 변동(Delta)이 0인 상품을 만드는 투자 전략**입니다. 가장 간단한 예로, 비트코인 선물의 롱 포지션과 숏 포지션을 동시에 사는 것도 Delta-Neutral 투자 전략입니다.

　가격 변동이 없다면 Delta-Neutural 전략은 왜 쓰는 걸까요? 현실 금융에는 훨씬 더 다양한 사용처가 있지만, 가상화폐 환경에서는 주로 **이자를 주면서 가격 변동성이 있는 토큰의 가격 변동성 헤징**을 위해 사용됩니다.

　예를 들어, LooksRare NFT Marketplace는 홈페이지에서 `$LOOKS`를 예치한 홀더들에게 NFT 거래 수수료의 일부분을 이더리움을 나누어줍니다. 이 이자 수익(APR)은 현재 약 200% 대로, 매우 매력적으로 보입니다. 하지만, 이자 수익을 얻기 위해 `$LOOKS`를 예치하면 `$LOOKS`의 변동성에 그대로 노출되는 문제가 생깁니다.

　<img src = "https://www.dropbox.com/s/arqf1m8170pbhd9/2022-03-07-aperture-2.png?raw=1" style = "width:100%; object-fit: contain">
###### Source: [Coinmarketcap - #LOOKS](https://coinmarketcap.com/currencies/looksrare/)

　최근 한 달 `$LOOKS`의 가격입니다. `$LOOKS`를 예치만 한 상태였다면 200%대의 APR로도 충당이 불가능한 손실이 났을 것입니다. 여기서 우리는 `FTX`의 선물 거래소를 볼 필요가 있습니다. **`FTX`의 `LOOKS-PREP`에서 숏 포지션을 가져감으로써 우리는 `$LOOKS`의 가격 변동성을 제거하고 안전하게 이자만 챙길 수 있습니다.**(보통 이렇게 변동성 리스크를 제거하는 것을 헤징이라고 부릅니다.)

　**물론 변동성 제거는 무료가 아닙니다.** 무기한 선물 상품 특성상 [편비](https://academy.binance.com/ko/articles/what-are-perpetual-futures-contracts)로 돈이 빠져나가고, 헤징을 위해 숏 포지션을 들어간 만큼 유동성이 묶이게 됩니다. 만약 전략에 포함된 자산 중 페어 자산이 있다면 [비영구적 손실](https://academy.binance.com/ko/articles/impermanent-loss-explained)도 고려해야 합니다. 그럼에도 Delta-Neutural 전략은 변동성을 제거하면서 동시에 수익성을 챙길 수 있는 좋은 전략 중 하나입니다.

> ### **Delta-Neutral in Aperture Finance**

　<img src = "https://www.dropbox.com/s/s1au8036prcdx5t/2022-03-07-aperture-1.png?raw=1" style = "width:100%; object-fit: contain">
###### Source: [Aperture Finance](https://medium.com/@aperturefinance/the-delta-neutral-strategy-on-synthetic-tokens-4b3e6428486d)
　`Aperture Finance`의 Delta-Neutural 전략은 `Anchor`와 `Mirror`를 이용합니다. 이자를 얻는 방법은 총 3가지입니다.
1. `Anchor`에 `$UST` 예치
2. 1을 담보로 `Mirror`의 합성자산 숏 포지션 예치
3. `Mirror`의 합정자산 롱 포지션 + 2에서 남은 담보로 `Terraswap`에서 롱 포지션-`$UST` 페어 예치

　여기의 2번 과정에서 청산 위험이 발생합니다. 기반 자산의 가격이 오르면 담보 대비 빌린 자산의 비율이 높아지므로 지정된 담보 비율보다 낮아지고, 청산이 발생합니다. 

## **2. Experience**<a name="experience">
　현재 `Aperture Finance`는 private beta를 진행 중이며, 오딧이 마무리되는 대로 public launch를 진행한다고 합니다. 저도 Private beta에 참가했습니다.

　숏 포지션으로 들어가는 합성자산의 양이 많을수록(= 담보 비율이 낮을수록), Delta-Neutural 전략의 수익률도 증가합니다. 기본적으로 Delta-Neutural이지만, 약간의 risk-return tradeoff를 조정할 수 있습니다.

## **3. Team and VCs**<a name="teamvc">
　추가 예정

## **4. Verdict**<a name="verdict">
> ### **기대되는 점**
- `Anchor`보다 더 높은 수익 제공
- 초기 유동성 걱정 없음

　기본적으로 `Anchor`를 기반으로 `Mirror`의 롱 포지션과 숏 포지션을 들어가는 전략입니다. 때문에 `Mirror`의 합성자산 예치 수익이 웬만큼 낮지 않은 이상 항상 `Anchor`보다 높을 것입니다.

　유동성 문제는 생각보다 큰 장점입니다. 대부분의 DeFi 프로젝트는 초기 유동성 부족으로 인한 극심한 가격 변동성을 버티지 못하고 실패합니다. `Aperture Finance`의 전략은 자체 토큰이 없고, 유동성이 이미 충분히 많은 `Anchor`와 `Mirror`를 기반으로 하기 때문에 해당 문제에서 자유롭습니다. 또한, 합성자산의 롱 포지션과 숏 포지션을 같은 양으로 들어가기 때문에, 포지션 간 유동성 불균형으로 인해 문제가 생길 가능성도 없습니다.

> ### **우려되는 점**
- `Anchor`의 지속 가능성
- 경우에 따라 `Anchor`보다 수익이 낮을 수도 있음
- 기반자산 가격의 상승으로 인한 청산 위험
- 컨트랙 자체의 리스크

　`Anchor`를 기반으로 한다는 것은, `Anchor`와 단점을 공유한다는 뜻이기도 합니다. 미래에 `Anchor`의 수익이 낮아지면, Delta-Neutural 전략의 수익도 같이 낮아질 것입니다. 그래도 `Anchor` 측에서도 `Anchor`의 지속 가능성에 대해 고려하고 있는 것처럼 보이기 때문에 `Anchor`로 인해 전략 자체가 박살나는 경우는 없을 것 같습니다.

　제가 여기서 우려하는 것은 두 번째입니다. **앞서 언급한 것처럼 자산의 변동성 제거는 무료가 아닙니다.** `Aperture Finance`에 많은 유동성이 몰려 `Mirror` 합성자산에도 많은 유동성이 몰립니다. 예치 보상이 그대로인 상태에서 유동성이 몰리면 `Mirror`의 예치 수익이 감소합니다. **그 결과 경우에 따라 수익이 `Anchor`보다 낮아질 가능성도 있다고 봅니다.**

*(비슷한 사례로 일부 페어가 마이너스 수익을 기록한 적이 있었던 클레이스왑 플러스 예치가 있습니다. 그러나, `Aperture Finance`는 구조상 마이너스 수익으로는 가지 않을 것입니다.)*

　`Aperture Finance`의 Delta-Neutural 전략은 기반자산의 숏 포지션에서 청산 리스크가 존재합니다. 사이트에서 해당 기반자산의 가격이 얼마나 올라야 청산이 되는지 알려주니 그에 따라서 잘 대처하시면 될 것 같습니다. 그리고 이는 반대로 **합성자산의 가격 하락으로 인한 청산 걱정이 없다**는 뜻이기도 합니다. 즉, 미래 전망이 어두운 합성자산을 기반으로 하는 곳에 투자하는 것도 괜찮아 보입니다.

　그리고 당연한 이야기지만, 위의 모든 전략은 `Aperture Finance`가 컨트랙을 잘 작성했다는 것을 전제로 합니다. 컨트랙 리스크는 어느 DeFi 프로젝트에나 존재하지만, Delta-Neutural 전략같이 컨트랙이 복잡해질수록 취약점이 발생할 확률은 높아질 것입니다.

> ### **총평**

　2월 초에 베타를 시작했을 때부터 기대하고 있었던 프로젝트입니다. 적다 보니 우려되는 점이 기대되는 점보다 많아졌지만, 그럼에도 매우 가능성 있는 프로젝트라고 생각하고 있습니다.

* * *
### **● 참고 자료**
○ [What Is Aperture?](https://medium.com/@aperturefinance/what-is-aperture-e823c939d667)
<br>
○ [The Delta-neutral Strategy on Synthetic Tokens on Terra](https://medium.com/@aperturefinance/the-delta-neutral-strategy-on-synthetic-tokens-4b3e6428486d)
<br>
○ [Mirror V2-What's new, Walkthrough and Advanced Farming Strategies.](https://medium.com/coinmonks/mirror-v2-whats-new-walkthrough-and-advanced-farming-strategies-6e48a0b1eff2)
<br>
