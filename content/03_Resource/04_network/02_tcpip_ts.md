---
title: TCP 연결 장애 트러블슈팅 사례
draft: true
tags:
  - network
  - tcp
  - troubleshooting
---

# TCP 연결 장애 트러블슈팅 사례

<!-- 사례를 정하면 제목을 "Endpoint가 정상인데 Ingress에서 503이 발생한 이유"처럼 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: TCP 연결 실패, Connection Storm, Local Port 고갈, TIME_WAIT 증가 -->

## 문제 상황

<!-- 어떤 시스템에서 언제 발생했는지 3~4줄로 적는다. 공개 사례라면 원문 링크를 남긴다. -->

## 시스템 구성

<!-- 요청이 거치는 경로를 hop 단위로 나열한다. -->

```text
Client
→ DNS
→ 대상 IP:Port
→ TCP 연결
→ Server
```

## 관측한 증상

<!-- 실제로 확인한 값만 적는다. 이 시점에 원인은 적지 않는다. -->

- 오류 메시지:
- 연결 실패율:
- Socket state 분포:

## 당시 가설

<!-- 증상만 보고 세운 가설을 나열한다. 나중에 틀린 것으로 밝혀져도 그대로 남긴다. -->

1.
2.
3.

## 진단 과정

<!-- 확인한 순서대로 나열한다. 각 단계에서 무엇을 보고 다음으로 넘어갔는지 드러나게 적는다. -->

- 연결 실패 지점 확인 (timeout / refused / reset 구분)
- Socket state 집계 (`ss -tan`)
- Local port 사용량과 ephemeral port 범위
- TIME_WAIT 수
- Server accept queue와 SYN 재전송 (`ss -ltn`, `netstat -s`)

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 이 사례를 이해하는 데 필요했는데 몰랐던 것을 적는다. -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
연결 시도
→ 대상 IP와 Port
→ TCP 연결 수립
→ Socket State
→ Local Port 사용량
→ TIME_WAIT
→ Server Accept Queue
```

순서로 각 단계의 입력과 출력을 비교한다.

## 재발 방지 체크리스트

## 함께 읽기

- [[03_Resource/04_network/01_tcp|1주차 - TCP/IP와 연결]]
