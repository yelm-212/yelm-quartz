---
title: Index와 Execution Plan
draft: true
tags:
  - database
  - index
  - execution-plan
  - query
---

# Index와 Execution Plan

## 학습 목표

- B+Tree가 Database Index에 적합한 이유를 설명할 수 있다.
- Clustered Index와 Non-Clustered Index의 차이를 설명할 수 있다.
- Composite Index의 컬럼 순서가 중요한 이유를 설명할 수 있다.
- Covering Index를 설명할 수 있다.
- Selectivity와 Cardinality가 Index 선택에 미치는 영향을 설명할 수 있다.
- Execution Plan에서 확인해야 할 주요 항목을 설명할 수 있다.
- Optimizer와 CBO가 실행계획을 선택하는 방식을 설명할 수 있다.
- EXPLAIN과 EXPLAIN ANALYZE의 차이를 설명할 수 있다.
- Nested Loop Join과 Hash Join의 동작 방식과 선택 조건을 설명할 수 있다.

## Index

### B+Tree

<!-- Disk 기반 저장 구조에서 B+Tree가 선택되는 이유를 Height, Node 크기, Range Scan 관점에서 기록한다. -->

### Index의 기본 동작

<!-- Index를 통해 행을 찾는 과정과 Index 유지 비용을 기록한다. -->

### Clustered Index

<!-- 데이터가 Index 순서로 저장되는 구조와 Secondary Index가 이를 참조하는 방식을 기록한다. -->

| 구분 | Clustered Index | Non-Clustered Index |
| ---- | --------------- | ------------------- |
| 저장 구조 |  |  |
| 개수 제한 |  |  |
| 조회 경로 |  |  |

### Composite Index

<!-- 왼쪽 접두어 규칙과 컬럼 순서가 사용 가능 여부를 바꾸는 이유를 기록한다. -->

### Covering Index

<!-- Index만으로 Query를 처리할 수 있는 조건과 이점을 기록한다. -->

### Selectivity와 Cardinality

<!-- 두 지표의 정의와, 값이 낮을 때 Optimizer가 Index를 선택하지 않는 이유를 기록한다. -->

### Index가 사용되지 않는 경우

<!-- 컬럼 가공, 타입 불일치, 넓은 범위 조회, 통계 정보 문제 등을 기록한다. -->

| 상황 | Index를 사용하지 못하는 이유 | 대안 |
| ---- | ---------------------------- | ---- |
|  |  |  |

## Execution Plan

### Optimizer와 CBO

<!-- 통계 정보를 기반으로 비용을 추정해 실행계획을 선택하는 과정을 기록한다. 통계가 실제와 어긋날 때 생기는 문제도 함께 정리한다. -->

### EXPLAIN과 EXPLAIN ANALYZE

| 구분 | 실행 여부 | 확인할 수 있는 것 |
| ---- | --------- | ----------------- |
| EXPLAIN |  |  |
| EXPLAIN ANALYZE |  |  |

### 확인해야 할 주요 항목

<!-- 접근 방식, 사용된 Index, 예상 행 수와 실제 행 수의 차이, Join 순서와 방식, 정렬과 임시 테이블 사용 여부를 기록한다. -->

### Full Table Scan과 Index Scan

<!-- 각각이 유리한 상황과, Full Scan이 항상 문제는 아닌 이유를 기록한다. -->

### Join

| 방식 | 동작 | 유리한 상황 |
| ---- | ---- | ----------- |
| Nested Loop Join |  |  |
| Hash Join |  |  |

## 실습

직접 테스트 테이블과 데이터를 만들어 실행계획을 비교한다.

```text
Index 없음
→ Single Column Index
→ Composite Index
→ Composite Index 컬럼 순서 변경
```

### 실습 환경

<!-- DBMS 버전, 테이블 정의, 데이터 건수, 데이터 분포를 기록한다. -->

```sql
-- 예: 테스트 테이블
CREATE TABLE orders (
  id BIGINT PRIMARY KEY,
  user_id BIGINT NOT NULL,
  status VARCHAR(20) NOT NULL,
  created_at DATETIME NOT NULL
);
```

### 실행계획 비교

| 조건 | 사용된 Index | 접근 방식 | 예상 행 수 | 실제 행 수 | 실행 시간 |
| ---- | ------------ | --------- | ---------- | ---------- | --------- |
| Index 없음 |  |  |  |  |  |
| Single Column Index |  |  |  |  |  |
| Composite Index |  |  |  |  |  |
| 컬럼 순서 변경 |  |  |  |  |  |

<!-- 각 단계에서 실행계획이 달라진 이유를 함께 기록한다. -->

## 백지복습 질문

- Composite Index의 컬럼 순서는 왜 중요한가?
- Index가 있는데도 사용되지 않는 경우는 언제인가?
- Execution Plan에서 가장 먼저 확인해야 할 항목은 무엇인가?

## 참고 자료

- [MySQL 8.4 Reference Manual - Optimization and Indexes](https://dev.mysql.com/doc/refman/8.4/en/optimization-indexes.html)
- [MySQL 8.4 Reference Manual - EXPLAIN Statement](https://dev.mysql.com/doc/refman/8.4/en/explain.html)
- [MySQL 8.4 Reference Manual - Nested-Loop Join Algorithms](https://dev.mysql.com/doc/refman/8.4/en/nested-loop-joins.html)
- [PostgreSQL Documentation - Indexes](https://www.postgresql.org/docs/current/indexes.html)
- [PostgreSQL Documentation - Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)
- [PostgreSQL Documentation - Planner Statistics](https://www.postgresql.org/docs/current/planner-stats.html)

## 함께 읽기

- [Slow Query 트러블슈팅 사례](03_Resource/06_database/04_index_execution_plan_ts)
