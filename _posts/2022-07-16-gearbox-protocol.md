---
layout: post
title:  "Gearbox Protocol"
description: "Use leverage in popular DeFi protocols"
author: "bemodest.eth"
categories: defi
tags: [defi]
image: ../assets/img/0716_1.png
---

### *취미생활방 서포터즈 활동으로 작성된 게시글입니다.

## 🔎 개요
- 이더리움 네트워크의 파생상품 프로토콜
- 레버리지 포지션을 구축하고 여러 DeFi 프로토콜에서 이를 활용
- [TVL: 1230만 달러(7월 14일 기준)](https://defillama.com/protocol/gearbox)

## 🔎 Lenders and Borrowers
- [Lenders](https://docs.gearbox.finance/liquidity-providers/pools-and-apy): Borrower가 빌릴 수 있는 유동성을 제공
- [Borrowers](https://docs.gearbox.finance/traders-and-farmers/how-to-open-account): 담보금을 넣고 Lender의 유동성을 추가로 빌려 레버리지 포지션을 구축
- 담보금의 최대 3배까지 대출 가능 (최대 4x 레버리지)
- 지원 자산: BTC / ETH / DAI / USDC

# 🔎 [Allowlist](https://docs.gearbox.finance/overview/credit-account/allowedlist-policy)
- Gearbox의 레버리지는 프로토콜의 Credit Account에서 관리
- [Gearbox 거버넌스](https://gov.gearbox.fi/)가 승인한 컨트랙트와 토큰에서만 레버리지 활용 가능
- **현재 승인한 컨트랙트: Curve 3pool, Uniswap, Yearn(DAI, USDC), Sushiswap**

# 🔎 [$GEAR](https://docs.gearbox.finance/gear-token/gear-overview)
- Gearbox Protocol의 유틸리티 / 거버넌스 토큰
- 다른 사람에게 토큰 전송 불가능. 투표권 delegate는 가능
- 전송 여부는 DAO 투표에 따라 바뀔 수 있음

## 💡 [$GEAR 토큰 분배](https://medium.com/gearbox-protocol/gear-token-not-yet-live-and-governance-reverse-voting-escrow-75f367985397)
- **총 물량: 100억 개**
- 51%: DAO 다중서명 지갑이 관리
- 20%: Initial Core Members (팀) 물량 | 12개월 락업 + 18개월 베스팅 
- 9.20%: Initial Contributor(투자자) 물량 | 12개월 락업 + 18개월 베스팅
- 11.52%: 회사 물량 | 12개월 락업 + 18개월 베스팅
- 나머지: 여러 방식으로 커뮤니티에 분배

- Reverse ve Model: 팀 물량과 투자자 물량은 시간이 갈수록 토큰의 voting power가 감소

## 🔎 정리 & 의견
Gearbox가 Aave와 Compound와 비교했을 때 가지는 가장 큰 장점은 낮은 이자율과 더 적은 담보로 더 큰 레버리지 포지션을 취할 수 있다는 점이다. 그리고 DAI와 USDC 같은 스테이블코인을 빌리면 더 적은 리스크로 더 효율적인 DeFi 파밍이 가능하다.

그러나 여러 제약도 있다. 레버리지를 Allowlist에 있는 DeFi에만 활용할 수 있다. 그리고 대출 이자가 낮은 이유는 공급된 유동성 대비 대출금이 매우 적기 때문이다. 더 많은 유저가 Gearbox에서 돈을 빌려 레버리지 포지션을 구축한다면 Gearbox의 대출 이자율은 증가할 것이다.

그리고 Allowlist로 프로젝트를 가려도 내재적인 컨트랙트 리스크는 존재한다. Allowlist 내에 있는 DeFi가 아닌 Gearbox 자체가 표적이 될 수도 있다.

Gearboxs는 Allowlist를 통해 무분별한 레버리지 성장을 막고 있다. 그래서 아직 프로젝트는 작아 보이지만 Gearbox의 잠재력은 무궁무진하다. Alchemix, Abracadabra와 같은 DeFi 프로토콜이 추가되고 지원 자산이 늘어난다면 DeFi 생태계에서 새로운 가치를 창출할 수 있을 것이다.