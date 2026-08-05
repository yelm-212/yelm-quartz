---
title: OS
draft: true
tags:
  - os
---

# OS

운영체제의 동작 원리를 학습하고, 공개된 장애 사례를 바탕으로 문제를 역추론한 기록입니다.

> 전체 일정과 진행 방식은 [[01_Project/12_week_cs_study|12주 CS 학습 계획]]에서 관리합니다.

## 학습 원칙

- 트러블슈팅 사례는 실제 공개 사례를 우선 사용한다.
- 개인 경험은 학습한 개념과 자연스럽게 연결되는 경우에만 사용한다.
- 장애 사례는 증상을 먼저 살펴본 뒤 가설을 세우고 실제 원인과 비교한다.
- OS 면접 질문 전체가 아니라, 백엔드 서버에서 발생할 수 있는 문제를 OS 개념과 연결하는 것을 목표로 한다.

## 학습 목차

### 5주차

- 학습내용: [[03_Resource/05_os/01_process_thread_cpu|Process, Thread와 CPU Scheduling]]
- 트러블슈팅: [[03_Resource/05_os/02_process_thread_cpu_ts|CPU와 Thread 트러블슈팅 사례]]

### 6주차

- 학습내용: [[03_Resource/05_os/03_virtual_memory|Virtual Memory와 Memory 문제]]
- 트러블슈팅: [[03_Resource/05_os/04_virtual_memory_ts|Memory 트러블슈팅 사례]]

### 7주차

- 학습내용: [[03_Resource/05_os/05_concurrency_io|동시성과 I/O]]
- 트러블슈팅: [[03_Resource/05_os/06_concurrency_io_ts|동시성과 I/O 트러블슈팅 사례]]

### 8주차

- 학습내용: [[03_Resource/05_os/07_os_linux_summary|OS와 Linux 진단 종합]]
- 트러블슈팅: [[03_Resource/05_os/08_os_linux_summary_ts|File Descriptor 고갈 트러블슈팅 사례]]

## 4주 완료 목표

```text
요청 지연 또는 서버 이상
→ Process / Thread
→ CPU / Scheduling
→ Virtual Memory / Memory
→ Lock / I/O
→ File Descriptor
→ System Call
```
