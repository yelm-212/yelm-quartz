---
title: 동시성과 I/O 트러블슈팅 사례
draft: true
tags:
  - os
  - concurrency
  - io
  - troubleshooting
---

# 동시성과 I/O 트러블슈팅 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: Blocking I/O로 인한 요청 적체, Thread Pool Exhaustion, Lock 대기 또는 Deadlock, Event Loop에서 Blocking 작업 실행 -->

## 문제 상황

## 시스템 구성

```text
요청
→ Thread Pool
→ 처리 Thread
→ Lock 또는 외부 I/O
→ 응답
```

## 관측한 증상

- 요청 적체와 응답 시간:
- CPU 사용률:
- Active Thread 수와 Queue 길이:
- Timeout 발생 여부:

## 당시 가설

1.
2.
3.

## 진단 과정

- CPU 사용률과 iowait 확인 (연산 부하가 아닌 것부터 확인)
- 실행 중인 Thread 수와 Thread State 확인
- 각 Thread가 어디서 대기하는지 확인 (`ps -eLo wchan`, thread dump)
- Lock 대기와 I/O 대기 구분
- Thread Pool의 Active 수, Queue 길이, 획득 대기 시간 확인

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 예: Blocking 호출 하나가 Pool 전체를 묶는 과정, Lock 대기와 I/O 대기가 지표에서 비슷하게 보이는 이유 -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
요청이 적체됨
→ CPU 사용률 확인
→ 실행 중인 Thread 수 확인
→ Thread State 확인
→ I/O 대기인가?
→ Lock 대기인가?
→ Thread Pool이 고갈됐는가?
```

순서로 확인한다. Thread를 늘리기 전에 어디서 대기하는지부터 확정한다.

## 재발 방지 체크리스트

## 함께 읽기

- [[03_Resource/05_os/05_concurrency_io|7주차 - 동시성과 I/O]]
