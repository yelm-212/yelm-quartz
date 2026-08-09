---
title: 동시성과 I/O
draft: true
tags:
  - os
  - concurrency
  - lock
  - thread-pool
  - io
---

# 동시성과 I/O

## 학습 목표

- Race Condition과 Critical Section을 설명할 수 있다.
- Mutex와 Semaphore의 차이를 설명할 수 있다.
- Deadlock의 네 가지 발생 조건을 설명할 수 있다.
- Thread Safe의 의미를 설명할 수 있다.
- Thread Pool을 사용하는 이유를 설명할 수 있다.
- CPU Bound와 I/O Bound 작업에 따라 Thread Pool 크기 기준이 달라지는 이유를 설명할 수 있다.
- Thread Pool이 고갈되었을 때 나타나는 증상을 설명할 수 있다.
- Blocking과 Non-Blocking, Synchronous와 Asynchronous를 구분할 수 있다.
- I/O Multiplexing이 필요한 이유를 설명할 수 있다.
- epoll이 다수의 연결을 처리하는 데 유리한 이유를 개략적으로 설명할 수 있다.

## 동시성 제어

### Race Condition

<!-- 공유 자원에 대한 접근 순서에 따라 결과가 달라지는 상황을 예시와 함께 기록한다. -->

### Critical Section

<!-- 상호 배제, 진행, 한정 대기 조건을 기록한다. -->

### Mutex와 Semaphore

| 구분 | Mutex | Semaphore |
| ---- | ----- | --------- |
| 목적 |  |  |
| 소유 개념 |  |  |
| 값의 범위 |  |  |
| 대표적인 사용 상황 |  |  |

### Deadlock

<!-- 발생 조건 네 가지와 각 조건을 깨뜨리는 방법을 기록한다. -->

| 조건 | 의미 | 깨뜨리는 방법 |
| ---- | ---- | ------------- |
| Mutual Exclusion |  |  |
| Hold and Wait |  |  |
| No Preemption |  |  |
| Circular Wait |  |  |

### Thread Safe

<!-- 어떤 코드가 Thread Safe한지 판단하는 기준과 대표적인 확보 방법을 기록한다. -->

## Thread 관리

### Thread Pool을 사용하는 이유

<!-- Thread 생성 비용과 무제한 생성이 만드는 문제를 기록한다. -->

### Thread 수 결정 시 고려 사항

<!-- CPU Bound와 I/O Bound에서 기준이 달라지는 이유, 대기 시간 비중, Queue 정책을 기록한다. -->

| 작업 유형 | Thread 수 기준 | 근거 |
| --------- | -------------- | ---- |
| CPU Bound |  |  |
| I/O Bound |  |  |

### Thread Pool Exhaustion

<!-- 고갈 시 나타나는 증상과 Queue 대기, Timeout, 요청 적체로 이어지는 과정을 기록한다. -->

## I/O Model

### Blocking과 Non-Blocking

<!-- 호출이 반환되는 시점을 기준으로 정리한다. -->

### Synchronous와 Asynchronous

<!-- 결과를 누가 어떻게 확인하는지를 기준으로 정리한다. -->

| 구분 | Blocking | Non-Blocking |
| ---- | -------- | ------------ |
| Synchronous |  |  |
| Asynchronous |  |  |

### I/O Multiplexing

<!-- 하나의 Thread가 다수의 FD를 감시해야 하는 이유를 기록한다. -->

### select, poll, epoll

<!-- 내부 구현을 자세히 비교하기보다 기존 방식의 한계와 epoll이 필요한 이유를 중심으로 기록한다. -->

| 방식 | 감시 대상 전달 방식 | 이벤트 확인 비용 | 한계 |
| ---- | ------------------- | ---------------- | ---- |
| select |  |  |  |
| poll |  |  |  |
| epoll |  |  |  |

## 연관 학습

- CPU Bound 작업과 Thread Pool
- I/O Bound 작업과 Thread Pool
- Lock 대기와 I/O 대기의 차이

<!-- Lock 대기와 I/O 대기는 증상이 비슷해 보일 수 있으므로 구분 기준을 명확히 정리한다. -->

> IPC, Spin Lock, Lock-Free, Wait-Free는 필수 범위에서 제외한다.

## 백지복습 질문

- Race Condition과 Deadlock은 무엇인가?
- Blocking과 Non-Blocking, Sync와 Async는 어떻게 다른가?
- Thread Pool이 고갈되면 어떤 현상이 나타나는가?

## 참고 자료

- [OSTEP - Concurrency](https://pages.cs.wisc.edu/~remzi/OSTEP/#book-chapters)
- [Linux man-pages - epoll(7)](https://man7.org/linux/man-pages/man7/epoll.7.html)
- [Linux man-pages - select(2)](https://man7.org/linux/man-pages/man2/select.2.html)
- [Linux man-pages - poll(2)](https://man7.org/linux/man-pages/man2/poll.2.html)
- [Linux man-pages - pthread_mutex_lock(3p)](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html)
- [Linux man-pages - sem_overview(7)](https://man7.org/linux/man-pages/man7/sem_overview.7.html)

## 함께 읽기

- [5주차 - Process, Thread와 CPU Scheduling](03_Resource/05_os/01_process_thread_cpu)
- [동시성과 I/O 트러블슈팅 사례](03_Resource/05_os/06_concurrency_io_ts)
