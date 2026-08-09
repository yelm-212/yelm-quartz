---
title: File Descriptor 고갈 트러블슈팅 사례
draft: true
tags:
  - os
  - linux
  - file-descriptor
  - troubleshooting
---

# Jenkins에서 Too many open files가 발생한 이유

<!-- 실제 내용을 채우면서 제목을 사례에 맞게 다듬는다. -->

## 문제 상황

- Jenkins 실행 환경과 담당하던 작업
- 발생 시점과 영향 범위
- 공개할 수 없는 식별 정보는 일반화해서 적는다

## 시스템 구성

```text
Jenkins Process
→ File Descriptor Table
→ File, Socket, Pipe
→ Process Limit (nofile)
→ 시스템 전체 File Handle Limit
```

## 관측한 증상

- 오류 메시지: `Too many open files`
- 실패한 작업:
- 발생 주기:
- 재시작 후 동작:

## 당시 가설

1.
2.
3.

## 진단 과정

- 대상 Process가 연 FD 수 확인 (`ls /proc/<pid>/fd | wc -l`)
- FD 종류별 분포 확인 (`lsof -p <pid>`)
- Process에 적용된 Soft와 Hard Limit 확인 (`prlimit`, `/proc/<pid>/limits`)
- 시스템 전체 file handle 사용량 확인 (`/proc/sys/fs/file-nr`)
- 사용량이 계속 증가하는지, 특정 시점에만 급증하는지 확인

## 실제 원인

## 해결

<!-- Limit 상향과 누수 해결을 구분해서 적는다. Limit만 올렸다면 무엇이 남았는지도 적는다. -->

## 당시 몰랐던 개념

- File Descriptor가 파일뿐 아니라 Socket과 Pipe도 가리킨다는 점
- Soft Limit과 Hard Limit의 차이
- 실행 중인 Process에 실제로 적용된 Limit을 확인하는 방법

## 추가로 공부한 개념

- Process별 FD Table과 시스템 전체 File Handle Limit의 구분
- User Mode와 Kernel Mode, System Call
- 어떤 문제에 어떤 진단 도구를 쓰는지의 구분

## 비교한 공개 사례

<!-- 같은 증상이 다른 원인에서 나온 공개 사례를 하나 골라 원인이 갈린 지점만 짧게 적는다. -->

| 구분 | Jenkins 사례 | 공개 사례 |
| ---- | ------------ | --------- |
| 증상 |  |  |
| 실제 원인 |  |  |
| 판별 지점 |  |  |

## 지금 다시 대응한다면

```text
Too many open files
→ 어떤 Process인가?
→ 열려 있는 FD의 종류는?
→ 파일인가 Socket인가?
→ 사용량이 증가만 하는가?
→ Limit이 낮은가, 누수인가?
```

순서로 확인한다. Limit을 올리기 전에 누수 여부부터 판단한다.

## 재발 방지 체크리스트

## 함께 읽기

- [8주차 - OS와 Linux 진단 종합](03_Resource/05_os/07_os_linux_summary)
