---
title: Database 종합 장애 사례
draft: true
tags:
  - database
  - troubleshooting
---

# Database 종합 장애 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: Connection Capacity 증가, Query Contention, Lock, Traffic 증가, Schema Migration, Timeout, Replication 영향이 두 개 이상 얽힌 공개 사례 -->

## 문제 상황

## 시스템 구성

```text
Application
→ Connection Pool
→ Primary DB
→ Replica
```

## 관측한 증상

- 사용자에게 보인 오류와 지연:
- 연결 수와 Slow Query 추이:
- Lock 대기와 Replication Lag:
- 직전 배포 또는 스키마 변경:

## 당시 가설

1.
2.
3.

## 진단 과정

- 연결 수와 상한, 세션 상태 분포 확인
- Slow Query와 Lock 대기 확인
- 오래 열린 Transaction 확인
- Replication Lag 확인
- 배포와 마이그레이션 이력을 장애 시각과 대조

## 실제 원인

## 장애 확산 경로

<!-- 하나의 원인만 찾는 것이 아니라 어떤 순서로 확대됐는지 적는다. -->

```text
최초 원인
→ 1차 영향
→ 2차 영향
→ 사용자 영향
```

<!-- Retry, Timeout 설정, Connection 재시도 등 장애를 키운 증폭 요인도 함께 적는다. -->

## 해결

## 당시 몰랐던 개념

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
Connection Pool
→ Slow Query
→ Execution Plan과 Index
→ Lock과 Transaction
→ Replication 상태
```

순서로 확인한다. 어느 것이 원인이고 어느 것이 결과인지 먼저 구분한다.

## 재발 방지 체크리스트

## 함께 읽기

- [12주차 - Database 종합](03_Resource/06_database/07_database_summary)
