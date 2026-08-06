---
title: Memory 트러블슈팅 사례
draft: true
tags:
  - os
  - memory
  - troubleshooting
---

# Memory 트러블슈팅 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: Memory Leak, Swap 증가, Thrashing, OOM, OOM Killer에 의한 Process 종료 -->

## 문제 상황

## 시스템 구성

```text
Application Process
→ Heap / Native Memory
→ Process Memory (RSS)
→ 시스템 Memory
→ Swap
```

<!-- 컨테이너라면 cgroup memory limit도 함께 적는다. -->

## 관측한 증상

- Memory 사용량 추이:
- Swap 사용량:
- 응답 시간 변화:
- Process 종료 여부:

## 당시 가설

1.
2.
3.

## 진단 과정

- 시스템 Memory와 Swap 사용량 확인 (`free`, `vmstat`)
- Process별 RSS 추이 확인
- Application이 보고하는 Heap 사용량과 RSS 비교
- Major page fault와 swap in/out 추이 확인
- OOM Killer 동작 여부 확인 (`dmesg`)

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 예: Heap이 여유로워도 RSS가 늘 수 있는 이유, Page Cache가 사용량에 포함되는 방식 -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
Memory 사용량 증가
→ Process Memory
→ Heap / Native Memory
→ RSS
→ Page Cache
→ Swap
→ Page Fault
→ OOM Killer
```

순서로 확인한다. 트래픽에 따른 정상 증가와 반환되지 않는 누수를 먼저 구분한다.

## 재발 방지 체크리스트

## 함께 읽기

- [[03_Resource/05_os/03_virtual_memory|6주차 - Virtual Memory와 Memory 문제]]
