---
title: Virtual Memory와 Memory 문제
draft: true
tags:
  - os
  - memory
  - virtual-memory
  - paging
---

# Virtual Memory와 Memory 문제

## 학습 목표

- Virtual Memory가 필요한 이유를 설명할 수 있다.
- Page와 Frame의 차이를 설명할 수 있다.
- Paging과 Page Table의 역할을 설명할 수 있다.
- MMU와 TLB가 필요한 이유를 설명할 수 있다.
- Page Fault가 발생했을 때 어떤 일이 일어나는지 설명할 수 있다.
- Swap이 증가하면 성능이 저하될 수 있는 이유를 설명할 수 있다.
- Thrashing이 무엇인지 설명할 수 있다.
- Process Memory와 JVM Heap의 차이를 설명할 수 있다.
- OOM과 OOM Killer의 기본적인 동작을 설명할 수 있다.

## Virtual Memory

### Virtual Memory가 필요한 이유

<!-- 격리, 물리 메모리보다 큰 주소 공간, 배치의 유연성 등 어떤 문제를 해결하는지 기록한다. -->

### Virtual Address와 Physical Address

<!-- 두 주소 공간의 관계와 Process마다 주소 공간이 분리되는 의미를 기록한다. -->

### Page와 Frame

| 구분 | 대상 | 크기 | 설명 |
| ---- | ---- | ---- | ---- |
| Page |  |  |  |
| Frame |  |  |  |

### Paging과 Page Table

<!-- Page Table이 매핑을 관리하는 방식과 Multi-level Page Table이 필요한 이유를 기록한다. -->

### Page Fault

<!-- Minor Fault와 Major Fault를 구분하고, Fault 발생 시 Kernel이 수행하는 처리 흐름을 기록한다. -->

```text
Virtual Address 접근
→ Page Table 확인
→ 매핑 없음 또는 Frame 미적재
→ Page Fault
→ Kernel이 Frame 확보
→ 필요 시 Disk에서 적재
→ Page Table 갱신
→ 명령어 재실행
```

## 주소 변환

### MMU

<!-- 하드웨어가 주소 변환을 담당하는 이유를 기록한다. -->

### TLB

<!-- Page Table 접근 비용과 TLB Hit과 Miss가 성능에 미치는 영향을 기록한다. -->

### 변환 흐름

```text
CPU의 Virtual Address 참조
→ TLB 조회
→ TLB Miss 시 Page Table 조회
→ Physical Address 확보
→ Memory 접근
```

## Memory 문제

### Swap

<!-- Swap이 동작하는 조건과 Swap In과 Out이 지연에 미치는 영향을 기록한다. -->

### Thrashing

<!-- Page Fault와 Swap이 서로를 악화시키는 과정을 기록한다. -->

### OOM과 OOM Killer

<!-- 할당 실패와 OOM Killer에 의한 종료를 구분하고, 어떤 기준으로 종료 대상이 선정되는지 기록한다. 컨테이너 환경의 memory limit도 함께 확인한다. -->

```bash
# 예: 메모리와 swap 사용량 확인
free -m

# 예: swap in과 out, page fault 확인
vmstat 1

# 예: process별 RSS 확인
ps -eo pid,rss,vsz,comm --sort=-rss | head

# 예: OOM Killer 동작 여부 확인
dmesg -T | grep -i -E 'oom|killed process'
```

## 연관 학습

### Heap과 Process Memory

<!-- Application이 말하는 Heap과 OS가 보는 Process Memory의 범위 차이를 기록한다. -->

### JVM Heap과 실제 Process Memory

<!-- Heap 외에 Metaspace, Thread Stack, Native Memory, GC 구조가 차지하는 영역을 기록한다. Heap은 여유로운데 RSS가 계속 증가하는 상황을 어떻게 해석할지 정리한다. -->

### RSS

<!-- RSS와 VSZ의 차이, 공유 페이지가 포함되는 방식을 기록한다. -->

### Paging과 Segmentation

<!-- Paging과 비교하기 위한 개념 수준으로만 정리한다. -->

### 내부 단편화와 외부 단편화

<!-- 각 방식에서 어떤 단편화가 발생하는지 정리한다. -->

> Page Replacement Algorithm과 LRU 구현은 필수 범위에서 제외한다.

## 백지복습 질문

- Virtual Memory와 Paging은 왜 필요한가?
- Page Fault와 Swap은 성능에 어떤 영향을 주는가?
- JVM Heap은 여유로운데 Process가 OOM Killer에 의해 종료될 수 있는 이유는 무엇인가?

## 참고 자료

- [OSTEP - Virtualization: Memory](https://pages.cs.wisc.edu/~remzi/OSTEP/#book-chapters)
- [Linux Kernel Documentation - Memory Management](https://docs.kernel.org/mm/index.html)
- [Linux man-pages - proc(5)](https://man7.org/linux/man-pages/man5/proc.5.html)
- [Linux man-pages - free(1)](https://man7.org/linux/man-pages/man1/free.1.html)
- [Linux Kernel Documentation - Control Group v2 (Memory)](https://docs.kernel.org/admin-guide/cgroup-v2.html#memory)

## 함께 읽기

- [5주차 - Process, Thread와 CPU Scheduling](03_Resource/05_os/01_process_thread_cpu)
- [Memory 트러블슈팅 사례](03_Resource/05_os/04_virtual_memory_ts)
