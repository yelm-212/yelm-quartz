---
title: Transaction 트러블슈팅 사례
draft: true
tags:
  - database
  - transaction
  - troubleshooting
---

# Transaction 트러블슈팅 사례

## 사례 선정 기준

- Long Transaction, Transaction Contention, 잘못된 Transaction 범위 중 하나와 관련된 공개 사례를 선택한다.
- 장애를 겪은 조직이 직접 공개한 기술 블로그, 발표 자료, 사후 분석 문서를 우선 사용한다.
- 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자가 경험한 현상과 최초로 관찰된 로그 및 메트릭만 기록한다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 변경 사항을 정리한다. -->

## 2. Transaction 관점에서 원인 가설 설정

```text
Transaction 시작 시점
→ Transaction 종료 시점
→ Transaction 유지 시간
→ Lock 유지 여부
→ 다른 요청에 미치는 영향
```

| 우선순위 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ----------- | ------------------ |
| 1        |      |             |                    |
| 2        |      |             |                    |
| 3        |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### 로그

<!-- Application의 Transaction 경계 로그, Timeout, Rollback 로그와 판단 기준을 기록한다. -->

### 메트릭

<!-- 활성 Transaction 수, 최장 Transaction 유지 시간, Lock 대기 수, Rollback 비율을 기록한다. -->

### Query

```sql
-- 예: MySQL 실행 중인 transaction과 시작 시각 확인
SELECT trx_id, trx_state, trx_started, trx_query
FROM information_schema.innodb_trx ORDER BY trx_started;

-- 예: PostgreSQL 오래 열린 transaction 확인
SELECT pid, state, xact_start, now() - xact_start AS duration, query
FROM pg_stat_activity WHERE xact_start IS NOT NULL ORDER BY xact_start;
```

<!-- 각 결과에서 무엇을 확인할지 함께 설명한다. 운영 환경에서 실행할 때의 권한과 부하도 확인한다. -->

### Transaction 유지 시간과 Query 실행 시간 구분

<!-- Query 자체는 빠른데 Transaction이 오래 열려 있는 상황을 어떻게 판별할지 정리한다. -->

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

- [[03_Resource/06_database/01_transaction_isolation_mvcc|9주차 - Transaction, Isolation Level, MVCC]]
