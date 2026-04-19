---
title: Transformer Self-Attention
sources:
- https://youtu.be/kCc8FmEb1nY
- (internal source)
tags:
- '#topic/attention'
- '#depth/read'
created: 2026-04-19
updated: 2026-04-19
---

# Transformer Self-Attention

## 한 문장 요약
Self-attention은 각 토큰이 Q·K·V 세 projection을 통해 시퀀스 내 다른 모든 토큰과의 관련도를 계산하고, 그 가중 평균으로 출력을 만드는 메커니즘이다.

## 왜 중요한가
RNN처럼 순서에 의존하지 않고 시퀀스 내 임의 위치 간 의존성을 직접 모델링할 수 있어 Transformer 계열 언어 모델의 핵심 구성 요소가 된다.

## 핵심 개념
- **Q (Query)**: "내가 뭘 찾고 있나" — 각 토큰이 다른 토큰에게 던지는 질문
- **K (Key)**: "나는 어떤 정보를 갖고 있나" — 각 토큰의 라벨
- **V (Value)**: "내가 실제로 내놓을 값" — attention 가중치에 따라 전달되는 정보
- Q·K·V는 모두 동일한 입력 x에 서로 다른 linear projection을 적용한 것

## 직접 확인한 것
Karpathy zero-to-hero 강의(출처: https://youtu.be/kCc8FmEb1nY)를 통해 아래 수식을 확인:

```
attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V
```

- `QK^T`: 토큰 i와 토큰 j 사이의 dot product → 호환성 점수
- `/ sqrt(d_k)`: 차원이 커질수록 dot product 값이 커져 softmax가 지나치게 sharp해지는 것을 방지하기 위한 스케일 보정
- `softmax(...)`: 각 토큰이 다른 토큰에 얼마나 attend할지 확률 분포로 변환
- `... V`: 확률 분포로 가중 평균한 value가 각 위치의 최종 출력

## 미해결 / 다음에 볼 것
- **Multi-head attention의 직관**: `d_model / num_heads`로 쪼개는 이유 — "각 head가 서로 다른 관계를 학습"한다는 설명을 봤으나, concat 후 linear를 거치므로 수학적으로 단일 큰 head와 등가처럼 보이는 부분이 아직 불명확
- **Causal mask 직접 구현**: 상삼각 `-inf` 채우는 것을 PyTorch로 scratch 구현해볼 것
- "Attention Is All You Need" 원 논문 Section 3.2 (Scaled Dot-Product Attention) 재독
- nanoGPT의 `CausalSelfAttention` 구현 읽기

## 관련 페이지
- [[transformer]]
- [[multi-head-attention]]