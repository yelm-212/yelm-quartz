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

## 사례 선정 기준

- CPU 사용률 급증, 특정 Process 또는 Thread의 CPU 과점유, Context Switching 증가, CPU는 낮지만 Load Average가 높은 문제 중 하나와 관련된 공개 사례를 선택한다.
- 장애를 겪은 조직이 직접 공개한 기술 블로그, 발표 자료, 사후 분석 문서를 우선 사용한다.
- 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자가 경험한 현상과 최초로 관찰된 로그 및 메트릭만 기록한다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 변경 사항을 정리한다. -->

## 2. CPU와 Thread 관점에서 원인 가설 설정

```text
CPU 사용률
→ Load Average
→ Process
→ Thread
→ Process State
→ CPU Bound / I/O Bound
→ Context Switching
```

| 우선순위 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ----------- | ------------------ |
| 1        |      |             |                    |
| 2        |      |             |                    |
| 3        |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### 로그

<!-- 요청 처리 시간, 배포 이력, GC 로그 등 확인할 로그와 판단 기준을 기록한다. -->

### 메트릭

<!-- user/system/iowait CPU, Load Average, Run Queue 길이, Thread 수, Context Switch 수를 기록한다. -->

### 명령어

```bash
# 예: CPU 사용률과 Load Average 확인
top

# 예: CPU를 많이 사용하는 thread 확인
top -H -p <pid>

# 예: process 상태와 CPU 사용률 정렬
ps -eLo pid,tid,stat,pcpu,comm --sort=-pcpu | head

# 예: run queue 길이, context switch, iowait 확인
vmstat 1
```

<!-- 명령어 출력에서 무엇을 확인할지 함께 설명한다. 운영 환경에서 사용할 때의 권한과 부하도 확인한다. -->

### CPU 사용률과 Load Average 구분

<!-- CPU가 낮은데 Load Average가 높다면 무엇을 의심할지, 반대의 경우는 어떤지 기준을 정리한다. -->

## 4. 실제 원인 확인

<!-- 공개 사례가 밝힌 직접 원인과 근본 원인, 이를 뒷받침한 증거를 기록한다. -->

## 5. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

<!-- 즉시 조치와 장기 개선을 구분해서 기록한다. -->

## 개인 경험과의 연결

<!-- 개념과 자연스럽게 연결되는 경험이 있을 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 같은 증상이 발생했을 때 재사용할 수 있는 판단 기준을 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 공식 문서를 기록한다. -->

## 함께 읽기

- [[03_Resource/05_os/01_process_thread_cpu|5주차 - Process, Thread와 CPU Scheduling]]
