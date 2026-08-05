---
title: Database
draft: true
tags:
  - database
---

# Database

Database의 동작 원리를 학습하고, 공개된 장애 사례를 바탕으로 문제를 역추론한 기록입니다.

> 전체 일정과 진행 방식은 [[01_Project/12_week_cs_study|12주 CS 학습 계획]]에서 관리합니다.

## 학습 원칙

- 트러블슈팅 사례는 실제 공개 사례를 우선 사용한다.
- 개인 경험은 학습한 개념과 자연스럽게 연결되는 경우에만 사용한다.
- 장애 사례는 증상을 먼저 살펴본 뒤 가설을 세우고 실제 원인과 비교한다.
- API가 느리다는 현상에서 바로 Index를 추가하지 않고 병목 구간을 먼저 좁힌다.

## 학습 목차

### 9주차

- 학습내용: [[03_Resource/06_database/01_transaction_isolation_mvcc|Transaction, Isolation Level, MVCC]]
- 트러블슈팅: [[03_Resource/06_database/02_transaction_isolation_mvcc_ts|Transaction 트러블슈팅 사례]]

### 10주차

- 학습내용: [[03_Resource/06_database/03_index_execution_plan|Index와 Execution Plan]]
- 트러블슈팅: [[03_Resource/06_database/04_index_execution_plan_ts|Slow Query 트러블슈팅 사례]]

### 11주차

- 학습내용: [[03_Resource/06_database/05_lock_pool_nplus1|Lock, Connection Pool, N+1]]
- 트러블슈팅: [[03_Resource/06_database/06_lock_pool_nplus1_ts|Lock과 Connection Pool 트러블슈팅 사례]]

### 12주차

- 학습내용: [[03_Resource/06_database/07_database_summary|Database 종합]]
- 트러블슈팅: [[03_Resource/06_database/08_database_summary_ts|Database 종합 장애 사례]]

## 4주 완료 목표

```text
Connection Pool
→ Query
→ Execution Plan
→ Index
→ Transaction
→ Lock
→ Replication
```
