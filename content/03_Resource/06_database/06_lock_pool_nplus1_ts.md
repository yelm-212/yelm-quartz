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

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: Lock Contention, Deadlock, Connection Pool Exhaustion, Long Transaction으로 인한 요청 지연 -->

## 문제 상황

## 시스템 구성

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

<!-- Pool 크기와 DB의 max connections를 함께 적는다. -->

## 관측한 증상

- 응답 지연 또는 오류 메시지:
- Active와 Idle Connection 수:
- Lock 대기와 Deadlock 발생 여부:
- 영향 범위:

## 당시 가설

1.
2.
3.

## 진단 과정

- 어느 구간에서 대기하는지부터 확정 (Thread, Pool, Transaction, Query, Lock)
- Connection 획득 대기 시간과 실패 로그 확인
- Lock 대기 중인 Query와 대기를 유발한 Transaction 확인
- Deadlock 발생 이력 확인
- Query 실행 시간과 Transaction 유지 시간 비교

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 예: Pool 고갈과 Lock 대기가 Application 로그에서 비슷하게 보이는 이유, Pool을 늘려도 해결되지 않는 경우 -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

순서로 각 구간의 대기 여부를 확인한다. Pool 크기를 올리기 전에 대기 구간을 확정한다.

## 재발 방지 체크리스트

## 함께 읽기

- [13주차 - Lock, Connection Pool, N+1](03_Resource/06_database/05_lock_pool_nplus1)
