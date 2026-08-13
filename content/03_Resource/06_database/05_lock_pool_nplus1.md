---
title: Lock, Connection Pool, N+1
draft: true
tags:
  - database
  - lock
  - connection-pool
  - jpa
---

# Lock, Connection Pool, N+1

## 학습 목표

- Shared Lock과 Exclusive Lock의 차이를 설명할 수 있다.
- Lock Wait와 Deadlock의 차이를 설명할 수 있다.
- Connection Pool이 고갈되었을 때 나타나는 증상을 설명할 수 있다.
- N+1 문제가 무엇이며 어떻게 확인하는지 설명할 수 있다.
- Optimistic Lock과 Pessimistic Lock을 어떤 상황에서 선택하는지 설명할 수 있다.

## Lock

### Shared Lock과 Exclusive Lock

| 구분 | Shared Lock | Exclusive Lock |
| ---- | ----------- | -------------- |
| 목적 |  |  |
| 함께 획득 가능한 Lock |  |  |
| 획득하는 상황 |  |  |

### Lock Wait

<!-- 대기가 발생하는 조건과 Lock Wait Timeout이 동작하는 방식을 기록한다. -->

### Deadlock

<!-- Lock Wait와의 차이, DB가 Deadlock을 감지하고 처리하는 방식을 기록한다. -->

| 구분 | Lock Wait | Deadlock |
| ---- | --------- | -------- |
| 상황 |  |  |
| 해소 방법 |  |  |
| Application이 받는 결과 |  |  |

### Long Transaction과 Lock

<!-- Transaction 유지 시간이 Lock 점유 시간과 어떻게 연결되는지 기록한다. -->

```sql
-- 예: MySQL Lock 대기 확인
SELECT * FROM performance_schema.data_lock_waits;

-- 예: MySQL 최근 Deadlock 확인
SHOW ENGINE INNODB STATUS;

-- 예: PostgreSQL 대기 중인 Query 확인
SELECT pid, wait_event_type, wait_event, state, query FROM pg_stat_activity
WHERE wait_event_type = 'Lock';
```

## Optimistic Lock과 Pessimistic Lock

| 구분 | Optimistic Lock | Pessimistic Lock |
| ---- | --------------- | ---------------- |
| 전제 | 충돌이 드물다 | 충돌이 잦다 |
| 구현 방식 |  |  |
| 충돌 시 동작 |  |  |
| 적합한 상황 |  |  |

<!-- 재고 차감이나 포인트 사용처럼 충돌이 잦은 작업에서 어떤 선택을 할지 기준을 정리한다. -->

## Connection Pool

### Connection Pool이 필요한 이유

<!-- Connection 생성 비용과 DB의 최대 연결 수 제한을 기록한다. -->

### Pool 크기 결정

<!-- Application Thread 수, DB의 max connections, Query 실행 시간의 관계를 기록한다. Pool을 무작정 늘렸을 때 생기는 문제도 함께 정리한다. -->

### Connection Timeout

<!-- Connection 획득 대기 Timeout과 Query Timeout, Socket Timeout을 구분해서 기록한다. -->

| 구분 | 대상 | 초과했을 때의 동작 |
| ---- | ---- | ------------------ |
| Connection 획득 Timeout |  |  |
| Query Timeout |  |  |
| Socket Timeout |  |  |

### Connection Pool Exhaustion

<!-- 고갈 시 나타나는 증상과, Application Thread가 대기 상태로 쌓이는 과정을 기록한다. -->

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

## N+1

### N+1 문제

<!-- 연관 데이터를 조회할 때 Query가 반복 실행되는 구조를 예시와 함께 기록한다. -->

### 확인 방법

<!-- Query 로그, 실행 Query 수 측정, Slow Query Log에서의 특징을 기록한다. -->

### 해결 방법

| 방법 | 동작 | 주의할 점 |
| ---- | ---- | --------- |
| Fetch Join |  |  |
| Batch Size |  |  |
| 별도 조회 후 조합 |  |  |

## 백지복습 질문

- Lock Wait와 Deadlock을 어떻게 구분하는가?
- Connection Pool이 고갈되면 어떤 증상이 나타나는가?
- 요청이 느릴 때 Connection 대기인지 Lock 대기인지 어떻게 판별하는가?

## 참고 자료

- [MySQL 8.4 Reference Manual - InnoDB Locking](https://dev.mysql.com/doc/refman/8.4/en/innodb-locking.html)
- [MySQL 8.4 Reference Manual - Deadlocks in InnoDB](https://dev.mysql.com/doc/refman/8.4/en/innodb-deadlocks.html)
- [PostgreSQL Documentation - Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html)
- [HikariCP - About Pool Sizing](https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing)
- [Hibernate ORM Documentation](https://docs.jboss.org/hibernate/orm/current/userguide/html_single/Hibernate_User_Guide.html)

## 함께 읽기

- [11주차 - Transaction, Isolation Level, MVCC](03_Resource/06_database/01_transaction_isolation_mvcc)
- [Lock과 Connection Pool 트러블슈팅 사례](03_Resource/06_database/06_lock_pool_nplus1_ts)
