---
title: OS와 Linux 진단 종합
draft: true
tags:
  - os
  - linux
  - system-call
  - file-descriptor
---

# OS와 Linux 진단 종합

## 학습 목표

- User Mode와 Kernel Mode를 구분하는 이유를 설명할 수 있다.
- System Call이 Application과 Kernel을 연결하는 방식을 설명할 수 있다.
- File Descriptor가 무엇인지 설명할 수 있다.
- 일반 파일뿐 아니라 Socket과 Pipe도 FD로 관리되는 이유를 설명할 수 있다.
- Process별 FD Limit과 시스템 전체 File Handle Limit을 구분할 수 있다.
- File Descriptor가 고갈되었을 때 나타나는 증상을 설명할 수 있다.
- CPU, Memory, Disk I/O, Network, FD 문제를 어떤 도구로 확인할지 설명할 수 있다.

## Kernel Interface

### User Mode와 Kernel Mode

<!-- 두 모드를 구분하는 이유와 전환이 발생하는 시점을 기록한다. -->

### System Call

<!-- Application이 Kernel 기능을 요청하는 경로와 Library Function과의 차이를 기록한다. -->

```text
Application의 함수 호출
→ Library
→ System Call
→ Mode 전환
→ Kernel 처리
→ 결과 반환
```

### Application과 Kernel의 관계

<!-- 파일, 네트워크, 메모리 요청이 결국 Kernel을 거치는 이유를 정리한다. -->

## File Descriptor

### File Descriptor

<!-- Process가 열어 둔 자원을 가리키는 정수 식별자의 의미를 기록한다. -->

### Process별 File Descriptor Table

<!-- FD Table, Open File Table, Inode의 관계를 개략적으로 기록한다. -->

### File, Socket, Pipe와의 관계

<!-- 서로 다른 자원이 같은 인터페이스로 다뤄지는 이유를 기록한다. -->

### Limit

| 구분 | 확인 방법 | 적용 범위 |
| ---- | --------- | --------- |
| Soft Limit |  |  |
| Hard Limit |  |  |
| Process별 `nofile` |  |  |
| 시스템 전체 File Handle Limit |  |  |

```bash
# 예: 현재 shell의 limit 확인
ulimit -Sn
ulimit -Hn

# 예: 실행 중인 process의 limit 확인
prlimit --pid <pid>
cat /proc/<pid>/limits

# 예: 시스템 전체 file handle 사용량 확인
cat /proc/sys/fs/file-nr

# 예: process가 연 FD 수 확인
ls /proc/<pid>/fd | wc -l
```

### File Descriptor 고갈

<!-- `Too many open files`가 발생했을 때 나타나는 증상과, 파일뿐 아니라 네트워크 연결도 함께 실패하는 이유를 기록한다. -->

## 주요 진단 도구

<!-- 명령어의 모든 옵션을 외우기보다 어떤 문제에 어떤 도구를 쓸지 구분하는 데 집중한다. -->

| 확인 대상 | 도구 | 확인할 항목 |
| --------- | ---- | ----------- |
| CPU | `top`, `ps`, `vmstat` |  |
| Memory와 Swap | `free`, `vmstat`, `/proc` |  |
| Disk I/O | `iostat`, `vmstat` |  |
| Network Socket | `ss` |  |
| File Descriptor | `lsof`, `prlimit`, `/proc` |  |
| 대기 중인 System Call | `strace` |  |

## 종합 질문

> 서버의 CPU 또는 Memory 사용량이 급증하거나 요청 처리가 지연될 때 어떤 순서로 원인을 확인할 것인가?

```text
증상과 영향 범위 확인
→ Process 확인
→ CPU와 Thread 상태 확인
→ Memory와 Swap 확인
→ Disk / Network I/O 확인
→ File Descriptor 확인
→ 필요 시 System Call 추적
```

<!-- 각 단계에서 어떤 결과가 나오면 다음 단계로 넘어갈지, 어떤 결과면 그 단계에서 원인을 확정할지 기준을 정리한다. -->

## OS 4주 정리

<!-- 5~8주차 내용을 하나의 흐름으로 연결한다. -->

```text
요청 지연 또는 서버 이상
→ Process / Thread
→ CPU / Scheduling
→ Virtual Memory / Memory
→ Lock / I/O
→ File Descriptor
→ System Call
```

## 백지복습 질문

- User Mode와 Kernel Mode를 구분하는 이유는 무엇인가?
- File Descriptor가 고갈되면 왜 파일과 Network 연결을 새로 열 수 없는가?
- CPU, Memory, I/O, FD 문제를 어떤 순서와 도구로 확인할 것인가?

## 참고 자료

- [Linux man-pages - syscalls(2)](https://man7.org/linux/man-pages/man2/syscalls.2.html)
- [Linux man-pages - open(2)](https://man7.org/linux/man-pages/man2/open.2.html)
- [Linux man-pages - getrlimit(2)](https://man7.org/linux/man-pages/man2/getrlimit.2.html)
- [Linux man-pages - proc(5)](https://man7.org/linux/man-pages/man5/proc.5.html)
- [Linux man-pages - lsof(8)](https://man7.org/linux/man-pages/man8/lsof.8.html)
- [Linux man-pages - ss(8)](https://man7.org/linux/man-pages/man8/ss.8.html)
- [Linux man-pages - strace(1)](https://man7.org/linux/man-pages/man1/strace.1.html)
- [Linux Kernel Documentation](https://docs.kernel.org/)

## 함께 읽기

- [[03_Resource/05_os/01_process_thread_cpu|5주차 - Process, Thread와 CPU Scheduling]]
- [[03_Resource/05_os/03_virtual_memory|6주차 - Virtual Memory와 Memory 문제]]
- [[03_Resource/05_os/05_concurrency_io|7주차 - 동시성과 I/O]]
- [[03_Resource/05_os/08_os_linux_summary_ts|File Descriptor 고갈 트러블슈팅 사례]]
