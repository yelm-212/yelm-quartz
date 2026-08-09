---
title: Transaction, Isolation Level, MVCC
draft: true
tags:
  - database
  - transaction
  - isolation-level
  - mvcc
---

# Transaction, Isolation Level, MVCC

## 학습 목표

- Transaction과 ACID를 설명할 수 있다.
- Transaction 범위를 잘못 잡았을 때 발생할 수 있는 문제를 설명할 수 있다.
- Isolation Level별 차이를 설명할 수 있다.
- MVCC가 무엇이며 왜 사용하는지 설명할 수 있다.
- Undo, Redo, WAL이 Transaction의 Rollback과 장애 복구에 어떻게 사용되는지 설명할 수 있다.

## Transaction

### Transaction

<!-- 하나의 논리적 작업 단위가 필요한 이유를 예시와 함께 기록한다. -->

### ACID

| 속성 | 의미 | 보장 방법 |
| ---- | ---- | --------- |
| Atomicity |  |  |
| Consistency |  |  |
| Isolation |  |  |
| Durability |  |  |

### Commit과 Rollback

<!-- 두 명령이 실행될 때 저장 구조에서 어떤 일이 일어나는지 기록한다. -->

### Transaction 범위

<!-- Transaction이 시작되고 종료되는 시점, 범위가 넓어질 때 Lock과 Connection 점유에 미치는 영향을 기록한다. -->

```text
Transaction 시작
→ Query 실행
→ 외부 호출이나 대기가 포함되는가?
→ Lock 유지 시간
→ Transaction 종료
```

## Isolation Level

### 동시성 이상 현상

| 현상 | 설명 | 발생 조건 |
| ---- | ---- | --------- |
| Dirty Read |  |  |
| Non-Repeatable Read |  |  |
| Phantom Read |  |  |

### Isolation Level 비교

| Level | Dirty Read | Non-Repeatable Read | Phantom Read |
| ----- | ---------- | ------------------- | ------------ |
| READ UNCOMMITTED |  |  |  |
| READ COMMITTED |  |  |  |
| REPEATABLE READ |  |  |  |
| SERIALIZABLE |  |  |  |

<!-- 표준 정의와 실제 DBMS 구현의 차이도 함께 기록한다. -->

### 사용 중인 DB의 기본 Level

<!-- MySQL(InnoDB)과 PostgreSQL의 기본 Level과 그 선택의 의미를 기록한다. -->

## MVCC

### MVCC가 필요한 이유

<!-- 읽기와 쓰기가 서로를 차단하지 않도록 만드는 방식과 그 이점을 기록한다. -->

### 동작 방식

<!-- 버전 관리, Snapshot, 오래된 버전 정리 과정을 개략적으로 기록한다. -->

```text
Transaction 시작
→ Snapshot 확보
→ 각 행의 버전 중 볼 수 있는 버전 선택
→ 변경 시 새 버전 생성
→ 더 이상 참조되지 않는 버전 정리
```

### Long Transaction과 MVCC

<!-- 오래 열린 Transaction이 오래된 버전 정리를 막아 발생시키는 문제를 기록한다. -->

## Undo, Redo, WAL

| 구분 | 저장하는 내용 | 사용되는 상황 |
| ---- | ------------- | ------------- |
| Undo |  |  |
| Redo |  |  |
| WAL |  |  |

<!-- Rollback과 장애 복구에서 각각 어떤 역할을 하는지 구분해서 기록한다. -->

## 연관 학습

<!-- Spring 환경에서 다음 정도를 연결한다. -->

### `@Transactional`

<!-- Proxy 기반 동작, 적용되지 않는 경우, 전파 속성 정도를 기록한다. -->

### Transaction Boundary

<!-- Transaction 안에 외부 API 호출이나 긴 작업이 포함될 때의 문제를 기록한다. -->

### Long Transaction

<!-- 확인 방법과 영향을 기록한다. -->

```sql
-- 예: MySQL 실행 중인 transaction 확인
SELECT * FROM information_schema.innodb_trx;

-- 예: PostgreSQL 오래 열린 transaction 확인
SELECT pid, state, xact_start, query FROM pg_stat_activity
WHERE xact_start IS NOT NULL ORDER BY xact_start;
```

## 백지복습 질문

- Transaction 범위를 잘못 잡으면 어떤 문제가 생기는가?
- Isolation Level을 올리면 무엇을 얻고 무엇을 잃는가?
- MVCC를 사용하는 DB에서 Long Transaction이 왜 위험한가?

## 참고 자료

- [MySQL 8.4 Reference Manual - InnoDB Transaction Model](https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-model.html)
- [MySQL 8.4 Reference Manual - Transaction Isolation Levels](https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html)
- [PostgreSQL Documentation - Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
- [PostgreSQL Documentation - Write-Ahead Logging](https://www.postgresql.org/docs/current/wal-intro.html)
- [Spring Framework - Transaction Management](https://docs.spring.io/spring-framework/reference/data-access/transaction.html)

## 함께 읽기

- [Transaction 트러블슈팅 사례](03_Resource/06_database/02_transaction_isolation_mvcc_ts)
