---
title: CPU와 Thread 트러블슈팅 사례
draft: true
tags:
  - os
  - cpu
  - thread
  - troubleshooting
---

# CPU와 Thread 트러블슈팅 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: CPU 사용률 급증, 특정 Process 또는 Thread의 CPU 과점유, Context Switching 증가, CPU는 낮지만 Load Average가 높은 문제 -->

## 문제 상황

## 시스템 구성

```text
요청
→ Application Process
→ Thread Pool
→ CPU
```

<!-- 실제 사례의 구성으로 바꿔 적는다. 인스턴스 수와 코어 수도 함께 남긴다. -->

## 관측한 증상

- CPU 사용률 (user, system, iowait):
- Load Average:
- 응답 시간과 처리량:
- 영향 범위:

## 당시 가설

1.
2.
3.

## 진단 과정

- CPU 사용률과 Load Average 비교 (연산 부하인지 대기인지 구분)
- CPU를 점유하는 Process 확인
- 해당 Process 안에서 어떤 Thread가 점유하는지 확인 (`top -H -p`)
- Thread State 분포 확인
- Context switch 수와 run queue 길이 확인 (`vmstat`)

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 예: Load Average에 포함되는 상태, voluntary와 involuntary context switch의 차이 -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
CPU 사용률
→ Load Average
→ Process
→ Thread
→ Process State
→ CPU Bound와 I/O Bound
→ Context Switching
```

순서로 확인한다. CPU가 높은 상황과 대기가 쌓인 상황을 먼저 구분한다.

## 재발 방지 체크리스트

## 함께 읽기

- [5주차 - Process, Thread와 CPU Scheduling](03_Resource/05_os/01_process_thread_cpu)
