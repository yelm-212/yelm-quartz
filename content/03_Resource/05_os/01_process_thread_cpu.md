---
title: Process, Thread와 CPU Scheduling
draft: true
tags:
  - os
  - process
  - thread
  - cpu
  - scheduling
---

# Process, Thread와 CPU Scheduling

## 학습 목표

- Program, Process, Thread의 차이를 설명할 수 있다.
- Process의 주요 상태와 상태 전이를 설명할 수 있다.
- PCB가 어떤 정보를 관리하는지 개략적으로 설명할 수 있다.
- Process의 주요 Memory 영역을 설명할 수 있다.
- Context Switching이 발생하는 이유와 비용을 설명할 수 있다.
- CPU Bound와 I/O Bound 작업을 구분할 수 있다.
- CPU Scheduling이 필요한 이유를 설명할 수 있다.
- FCFS와 Round Robin의 기본 동작과 차이를 설명할 수 있다.
- 동시성과 병렬성을 구분할 수 있다.

## Process와 Thread

### Program과 Process

<!-- 디스크에 있는 실행 파일과 실행 중인 인스턴스의 차이를 기록한다. -->

### Thread

<!-- Process 안에서 Thread가 공유하는 자원과 각자 갖는 자원을 구분해서 기록한다. -->

| 구분 | Process | Thread |
| ---- | ------- | ------ |
| 공유 자원 |  |  |
| 고유 자원 |  |  |
| 생성 비용 |  |  |
| 격리 수준 |  |  |

### Process State

<!-- New, Ready, Running, Waiting, Terminated의 의미와 상태 전이가 일어나는 조건을 기록한다. -->

```text
New → Ready → Running → Terminated
              ↕
            Waiting
```

### PCB

<!-- PID, Process State, Program Counter, Register, Memory 정보, File Descriptor Table 등 PCB가 관리하는 정보를 기록한다. -->

## Process Memory

### Memory 영역

| 영역 | 저장되는 것 | 크기 결정 시점 | 증가 방향 |
| ---- | ----------- | -------------- | --------- |
| Code |  |  |  |
| Data |  |  |  |
| BSS |  |  |  |
| Heap |  |  |  |
| Stack |  |  |  |

### Thread별 Stack

<!-- Thread마다 Stack이 분리되는 이유와 Heap을 공유할 때 발생하는 문제를 기록한다. -->

## CPU와 Scheduling

### CPU Bound와 I/O Bound

<!-- 두 작업의 실행 패턴 차이와, 이 구분이 Thread 수 결정에 어떤 영향을 주는지 기록한다. -->

### CPU Scheduling의 목적

<!-- CPU 활용률, 응답 시간, 처리량, 공평성 등 서로 충돌할 수 있는 목표를 기록한다. -->

### FCFS

<!-- 동작 방식과 Convoy Effect를 기록한다. -->

### Round Robin과 Time Slice

<!-- Time Slice 크기가 응답 시간과 Context Switching 비용에 미치는 영향을 기록한다. -->

| 알고리즘 | 선점 여부 | 장점 | 단점 |
| -------- | --------- | ---- | ---- |
| FCFS |  |  |  |
| Round Robin |  |  |  |

## Context Switching

### Context Switching이 필요한 이유

<!-- 어떤 사건이 Context Switching을 유발하는지 기록한다. -->

### Process와 Thread의 Context Switching 차이

<!-- Address Space 전환과 TLB, Cache에 미치는 영향을 중심으로 기록한다. -->

### Context Switching 비용

<!-- 직접 비용과 Cache 무효화 같은 간접 비용을 구분해서 기록한다. 확인 방법도 함께 정리한다. -->

```bash
# 예: 초당 context switch 수와 interrupt 수 확인
vmstat 1

# 예: 특정 process의 context switch 통계 확인
cat /proc/<pid>/status | grep ctxt_switches
```

## 동시성과 병렬성

<!-- 단일 코어와 다중 코어에서 어떻게 달라지는지 예시와 함께 기록한다. -->

## 연관 학습

<!-- JVM이나 Thread 구현을 깊게 파는 것이 목적은 아니다. 다음 정도만 확인한다. -->

- JVM은 OS 관점에서 하나의 Process인가?
- Java Thread와 OS Thread는 어떤 관계인가?
- Spring 서버는 요청을 어떤 Thread에서 처리하는가?

## 백지복습 질문

- Process와 Thread는 무엇이 다른가?
- CPU가 높은 상황과 Thread가 대기 중인 상황을 어떻게 구분할 것인가?
- Context Switching이 많아지면 어떤 증상이 나타나는가?

## 참고 자료

- [OSTEP - Virtualization: Processes](https://pages.cs.wisc.edu/~remzi/OSTEP/#book-chapters)
- [Linux man-pages - proc(5)](https://man7.org/linux/man-pages/man5/proc.5.html)
- [Linux man-pages - sched(7)](https://man7.org/linux/man-pages/man7/sched.7.html)
- [Linux man-pages - pthreads(7)](https://man7.org/linux/man-pages/man7/pthreads.7.html)
- [Linux Kernel Documentation - Scheduler](https://docs.kernel.org/scheduler/index.html)

## 함께 읽기

- [[03_Resource/05_os/02_process_thread_cpu_ts|CPU와 Thread 트러블슈팅 사례]]
