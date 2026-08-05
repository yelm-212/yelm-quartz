---
title: Lock과 Connection Pool 트러블슈팅 사례
draft: true
tags:
  - database
  - lock
  - connection-pool
  - troubleshooting
---

# Lock과 Connection Pool 트러블슈팅 사례

## 사례 선정 기준

- Lock Contention, Deadlock, Connection Pool Exhaustion, Long Transaction으로 인한 요청 지연 중 하나와 관련된 공개 사례를 선택한다.
- 장애를 겪은 조직이 직접 공개한 기술 블로그, 발표 자료, 사후 분석 문서를 우선 사용한다.
- 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자가 경험한 현상과 최초로 관찰된 로그 및 메트릭만 기록한다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 변경 사항을 정리한다. -->

## 2. 어느 구간에서 대기하는지 구분

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

<!-- 어느 구간에서 대기하는지 구분하는 데 집중한다. 각 구간에서 대기할 때 나타나는 증상의 차이를 먼저 정리한다. -->

| 대기 구간 | 대표 증상 | 확인 방법 |
| --------- | --------- | --------- |
| Application Thread |  |  |
| Connection Pool |  |  |
| Transaction |  |  |
| Query |  |  |
| Lock |  |  |

### 원인 가설

| 우선순위 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ----------- | ------------------ |
| 1        |      |             |                    |
| 2        |      |             |                    |
| 3        |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### 로그

<!-- Connection 획득 실패, Lock Wait Timeout, Deadlock, Query Timeout 로그와 판단 기준을 기록한다. -->

### 메트릭

<!-- Active/Idle Connection 수, Pending Thread 수, Connection 획득 대기 시간, Lock 대기 수를 기록한다. -->

### Query

```sql
-- 예: MySQL Lock 대기 확인
SELECT * FROM performance_schema.data_lock_waits;

-- 예: MySQL 최근 Deadlock 확인
SHOW ENGINE INNODB STATUS;

-- 예: MySQL 연결 수 확인
SHOW STATUS LIKE 'Threads_connected';
SHOW VARIABLES LIKE 'max_connections';

-- 예: PostgreSQL Lock 대기 확인
SELECT pid, wait_event_type, wait_event, state, query
FROM pg_stat_activity WHERE wait_event_type = 'Lock';
```

<!-- 각 결과에서 무엇을 확인할지 함께 설명한다. 운영 환경에서 실행할 때의 권한과 부하도 확인한다. -->

## 4. 실제 원인 확인

<!-- 공개 사례가 밝힌 직접 원인과 근본 원인, 이를 뒷받침한 증거를 기록한다. -->

## 5. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

<!-- 즉시 조치와 장기 개선을 구분해서 기록한다. Pool 크기 상향이 근본 해결이 아닌 경우도 함께 정리한다. -->

## 개인 경험과의 연결

<!-- 개념과 자연스럽게 연결되는 경험이 있을 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 같은 증상이 발생했을 때 재사용할 수 있는 판단 기준을 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 공식 문서를 기록한다. -->

## 함께 읽기

- [[03_Resource/06_database/05_lock_pool_nplus1|11주차 - Lock, Connection Pool, N+1]]
