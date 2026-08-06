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
- 처음 관찰된 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자 영향, 오류 메시지, 최초 로그와 메트릭만 기록한다. 실제 원인과 해결 방법은 아직 적지 않는다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 배포와 트래픽 변화를 정리한다. -->

| 확인 항목             | 관찰 결과 |
| --------------------- | --------- |
| 사용자 영향           |           |
| 영향 범위             |           |
| 시작 시점과 지속 시간 |           |
| 재현 조건             |           |
| 최근 변경 사항        |           |

## 2. 구간별 원인 가설 설정

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

<!-- 어느 구간에서 대기하는지 구분하는 데 집중한다. 각 구간에서 대기할 때 나타나는 증상의 차이를 먼저 정리한다. -->

| 대기 구간          | 대표 증상 | 확인 방법 |
| ------------------ | --------- | --------- |
| Application Thread |           |           |
| Connection Pool    |           |           |
| Transaction        |           |           |
| Query              |           |           |
| Lock               |           |           |

| 우선순위 | 구간 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ---- | ----------- | ------------------ |
| 1        |      |      |             |                    |
| 2        |      |      |             |                    |
| 3        |      |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### Connection Pool

<!-- Active/Idle Connection 수, Pending Thread 수, 획득 대기 시간, 획득 실패 로그를 확인한다. -->

```sql
SHOW STATUS LIKE 'Threads_connected';
SHOW VARIABLES LIKE 'max_connections';
```

### Lock 대기

<!-- 어떤 Query가 어떤 Lock을 기다리는지, 대기의 원인이 되는 Transaction은 무엇인지 확인한다. -->

```sql
-- MySQL Lock 대기
SELECT * FROM performance_schema.data_lock_waits;

-- PostgreSQL Lock 대기
SELECT pid, wait_event_type, wait_event, state, query
FROM pg_stat_activity WHERE wait_event_type = 'Lock';
```

### Deadlock

<!-- 최근 Deadlock의 발생 빈도와 관련된 Query를 확인한다. -->

```sql
SHOW ENGINE INNODB STATUS;
```

### Application 로그

<!-- Connection 획득 실패, Lock Wait Timeout, Query Timeout 로그와 판단 기준을 기록한다. -->

| 구간             | 로그·메트릭·명령어 | 판단 기준 | 관찰 결과 |
| ---------------- | ------------------ | --------- | --------- |
| Application Thread |                  |           |           |
| Connection Pool  |                    |           |           |
| DB Connection    |                    |           |           |
| Transaction      |                    |           |           |
| Query            |                    |           |           |
| Lock             |                    |           |           |

<!-- 운영 환경에서 조회할 때 필요한 권한과 부하, 민감 정보 노출 가능성을 확인한다. -->

## 4. 조사 과정

<!-- 실제 사례의 조사 순서를 시간순으로 재구성한다. 각 단계에서 무엇을 관찰했고 어떤 가설을 배제하거나 강화했는지 기록한다. -->

| 순서 | 확인한 내용 | 관찰 결과 | 가설에 미친 영향 | 다음 행동 |
| ---- | ----------- | --------- | ---------------- | --------- |
| 1    |             |           |                  |           |
| 2    |             |           |                  |           |
| 3    |             |           |                  |           |

## 5. 실제 원인 확인

### 직접 원인

### 근본 원인

### 원인을 뒷받침한 증거

## 6. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

### 즉시 조치

<!-- 서비스 복구를 위해 수행한 조치와 선택 이유를 기록한다. -->

### 장기 개선

<!-- Transaction 범위 조정, Lock 획득 순서 정리, Pool 크기와 timeout 설정, monitoring과 alert 중 사례에 해당하는 내용을 기록한다. Pool 크기 상향이 근본 해결이 아닌 경우도 함께 정리한다. -->

| 개선 항목 | 방지하거나 줄이는 위험 | 검증 방법 |
| --------- | ---------------------- | --------- |
|           |                        |           |

## 개인 경험과의 연결

<!-- 개념과 자연스럽게 연결되는 경험이 있을 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 같은 증상이 발생했을 때 재사용할 수 있는 판단 기준과 조사 순서를 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 공식 문서를 기록한다. -->

## 함께 읽기

- [[03_Resource/06_database/05_lock_pool_nplus1|11주차 - Lock, Connection Pool, N+1]]
