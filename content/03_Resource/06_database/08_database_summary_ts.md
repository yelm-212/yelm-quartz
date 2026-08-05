---
title: Database 종합 장애 사례
draft: true
tags:
  - database
  - troubleshooting
---

# Database 종합 장애 사례

## 사례 선정 기준

- Database의 여러 요소가 동시에 영향을 준 실제 장애 사례를 선택한다.
- 다음 요소가 두 개 이상 얽혀 있는 사례를 우선 사용한다.

| 요소 | 이 사례에서의 관련 여부 |
| ---- | ----------------------- |
| Connection Capacity 증가 |  |
| Query Contention |  |
| Lock |  |
| Traffic 증가 |  |
| Schema Migration |  |
| Timeout |  |
| Replication 영향 |  |

> 하나의 원인만 찾는 것이 아니라 장애가 어떤 연쇄 과정을 거쳐 확대되었는지 분석한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자가 경험한 현상과 최초로 관찰된 로그 및 메트릭만 기록한다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 배포와 마이그레이션 여부를 정리한다. -->

## 2. 원인 가설 설정

```text
Connection Pool
→ Slow Query
→ Execution Plan과 Index
→ Lock과 Transaction
→ Replication 상태
```

| 우선순위 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ----------- | ------------------ |
| 1        |      |             |                    |
| 2        |      |             |                    |
| 3        |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### 로그

<!-- Application 오류 로그, Slow Query Log, DB 오류 로그, 배포와 마이그레이션 이력을 기록한다. -->

### 메트릭

<!-- 연결 수, Active Transaction 수, Lock 대기, Query 처리량, Replication Lag, 응답 시간 분포를 기록한다. -->

### Query

```sql
-- 예: 현재 실행 중인 Query와 상태 확인
SHOW FULL PROCESSLIST;

-- 예: 연결 수와 상한 확인
SHOW STATUS LIKE 'Threads_connected';
SHOW VARIABLES LIKE 'max_connections';

-- 예: PostgreSQL 활동 중인 세션 확인
SELECT pid, state, wait_event_type, xact_start, query FROM pg_stat_activity;
```

## 4. 실제 원인 확인

<!-- 공개 사례가 밝힌 직접 원인과 근본 원인, 이를 뒷받침한 증거를 기록한다. -->

## 5. 장애 확산 경로

<!-- 최초 원인이 어떤 순서로 다른 요소에 영향을 주었는지 시간 순으로 정리한다. -->

```text
최초 원인
→ 1차 영향
→ 2차 영향
→ 장애 확대
→ 사용자 영향
```

| 시각 | 발생한 일 | 영향을 받은 구간 | 관찰된 신호 |
| ---- | --------- | ---------------- | ----------- |
|  |  |  |  |

### 증폭 요인

<!-- Retry, Timeout 설정, Connection 재시도, Auto Scaling 등 장애를 키운 요인을 기록한다. -->

## 6. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

<!-- 즉시 조치와 장기 개선을 구분해서 기록한다. 어느 지점에서 연쇄를 끊을 수 있었는지도 함께 정리한다. -->

## 개인 경험과의 연결

<!-- 개념과 자연스럽게 연결되는 경험이 있을 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 12주 학습 전체를 돌아보며, 장애 상황에서 어떤 계층을 어떤 순서로 확인할지 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 공식 문서를 기록한다. -->

- [Google Cloud Architecture Framework - Reliability](https://cloud.google.com/architecture/framework/reliability)

## 함께 읽기

- [[03_Resource/06_database/07_database_summary|12주차 - Database 종합]]
