---
title: Database 종합
draft: true
tags:
  - database
  - replication
  - sharding
  - normalization
---

# Database 종합

## 학습 목표

- RDB와 NoSQL의 데이터 모델과 선택 기준을 설명할 수 있다.
- Replication, Sharding, Partitioning의 목적과 차이를 설명할 수 있다.
- Replication Lag이 읽기 일관성과 장애 전환에 미치는 영향을 설명할 수 있다.

## RDB와 NoSQL

| 구분 | RDB | NoSQL |
| ---- | --- | ----- |
| 데이터 모델 |  |  |
| 스키마 |  |  |
| 일관성 |  |  |
| 확장 방식 |  |  |
| 적합한 상황 |  |  |

<!-- 어떤 요구사항이 있을 때 어느 쪽을 선택할지 기준을 기록한다. -->

## Replication

### Replication의 목적

<!-- 가용성, 읽기 확장, 백업 관점에서 목적을 기록한다. -->

### 동작 방식

<!-- 로그 기반 복제 흐름과 동기 및 비동기 복제의 차이를 기록한다. -->

### Replication Lag

<!-- Lag이 발생하는 원인과 읽기 요청을 Replica로 보낼 때 생기는 일관성 문제를 기록한다. 장애 전환 시 데이터 유실 가능성도 함께 정리한다. -->

```sql
-- 예: MySQL replica 상태와 지연 확인
SHOW REPLICA STATUS;

-- 예: PostgreSQL 복제 지연 확인
SELECT client_addr, state, sent_lsn, replay_lsn FROM pg_stat_replication;
```

## Sharding과 Partitioning

| 구분 | Partitioning | Sharding |
| ---- | ------------ | -------- |
| 분할 범위 |  |  |
| 목적 |  |  |
| 운영 난이도 |  |  |
| 주의할 점 |  |  |

<!-- Shard Key 선택이 잘못됐을 때 생기는 문제도 함께 기록한다. -->

## Backup과 Recovery

<!-- 전체 백업과 증분 백업, Point-in-Time Recovery의 개념, RPO와 RTO를 기록한다. -->

## Normalization과 Denormalization

<!-- 정규화가 해결하는 문제와, 조회 성능을 위해 비정규화를 선택할 때의 트레이드오프를 기록한다. -->

## 종합 질문

> 평소 정상적으로 동작하던 API가 느려졌을 때 Database 관점에서 무엇을 어떤 순서로 확인할 것인가?

```text
Connection Pool
→ Slow Query
→ Execution Plan과 Index
→ Lock과 Transaction
→ Replication 상태
```

<!-- 각 단계에서 어떤 결과가 나오면 다음 단계로 넘어갈지 기준을 정리한다. -->

| 단계 | 확인할 것 | 문제일 때의 신호 | 다음 단계로 넘어가는 조건 |
| ---- | --------- | ---------------- | ------------------------- |
| Connection Pool |  |  |  |
| Slow Query |  |  |  |
| Execution Plan과 Index |  |  |  |
| Lock과 Transaction |  |  |  |
| Replication |  |  |  |

## Database 4주 정리

<!-- 9~12주차 내용을 하나의 흐름으로 연결한다. -->

```text
Connection Pool
→ Query
→ Execution Plan
→ Index
→ Transaction
→ Lock
→ Replication
```

## 백지복습 질문

- Replication, Sharding, Partitioning은 각각 무엇을 해결하는가?
- Replica에서 읽을 때 어떤 문제가 생길 수 있는가?
- API가 느려졌을 때 Index 추가 전에 무엇을 먼저 확인해야 하는가?

## 참고 자료

- [MySQL 8.4 Reference Manual - Replication](https://dev.mysql.com/doc/refman/8.4/en/replication.html)
- [MySQL 8.4 Reference Manual - Partitioning](https://dev.mysql.com/doc/refman/8.4/en/partitioning.html)
- [PostgreSQL Documentation - High Availability, Load Balancing, and Replication](https://www.postgresql.org/docs/current/high-availability.html)
- [PostgreSQL Documentation - Table Partitioning](https://www.postgresql.org/docs/current/ddl-partitioning.html)
- [PostgreSQL Documentation - Backup and Restore](https://www.postgresql.org/docs/current/backup.html)

## 함께 읽기

- [9주차 - Transaction, Isolation Level, MVCC](03_Resource/06_database/01_transaction_isolation_mvcc)
- [10주차 - Index와 Execution Plan](03_Resource/06_database/03_index_execution_plan)
- [11주차 - Lock, Connection Pool, N+1](03_Resource/06_database/05_lock_pool_nplus1)
- [Database 종합 장애 사례](03_Resource/06_database/08_database_summary_ts)
