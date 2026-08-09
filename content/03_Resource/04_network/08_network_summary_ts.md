---
title: Network 종합 트러블슈팅 사례
draft: true
tags:
  - network
  - troubleshooting
---

# Network 종합 트러블슈팅 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: 하나의 요청이 사용자에게 도달하기까지 여러 계층이 함께 영향을 준 공개 사례 -->

## 문제 상황

## 시스템 구성

```text
Client
→ DNS
→ TCP 또는 QUIC
→ TLS
→ CDN, WAF, Load Balancer, Reverse Proxy
→ Application
```

<!-- 실제 사례의 구성으로 바꿔 적는다. 없는 hop은 지운다. -->

## 관측한 증상

- 사용자에게 보인 오류:
- 오류율과 응답 시간:
- 영향 범위 (특정 지역, 특정 client, 전체):

## 당시 가설

1.
2.
3.

## 진단 과정

- DNS 조회 결과와 응답한 resolver
- 단계별 소요 시간 분해 (`curl -w`로 dns, connect, tls, ttfb)
- TLS 인증서와 ALPN
- Load Balancer target health와 오류 응답이 어디서 생성됐는지
- Application 로그와 의존 서비스 상태

## 실제 원인

## 해결

## 당시 몰랐던 개념

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
DNS
→ TCP 또는 QUIC
→ TLS
→ HTTP
→ Proxy와 Load Balancer
→ Application
```

순서로 각 hop의 입력과 출력을 비교한다. 어느 hop까지 정상이었는지를 먼저 확정한다.

## 장애 확산 경로

<!-- 최초 원인이 어떤 경로로 다른 계층에 영향을 주었는지 적는다. -->

## 재발 방지 체크리스트

## 함께 읽기

- [4주차 - Network 종합](03_Resource/04_network/07_network_summary)
