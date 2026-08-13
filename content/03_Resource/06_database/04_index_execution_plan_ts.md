---
title: Slow Query 트러블슈팅 사례
draft: true
tags:
  - database
  - index
  - query
  - troubleshooting
---

# Slow Query 트러블슈팅 사례

<!-- 사례를 정하면 제목을 증상을 요약한 문장으로 바꾼다. -->

<!-- 사례 후보: Slow Query, 잘못된 Query 배포, Index 미사용, 잘못된 Composite Index -->

## 문제 상황

## 시스템 구성

```text
요청
→ Application
→ Query
→ Optimizer와 Execution Plan
→ Index 또는 Full Scan
→ 데이터
```

<!-- 테이블 규모와 데이터 증가 추이도 함께 적는다. -->

## 관측한 증상

- 느려진 Query와 실행 시간:
- 실행 횟수:
- 느려지기 시작한 시점:
- 직전 배포나 데이터 변화:

## 당시 가설

1.
2.
3.

## 진단 과정

- Slow Query Log나 실행 통계에서 대상 Query 좁히기
- 실행계획 확인 (접근 방식, 사용된 Index, 예상 행 수와 실제 행 수)
- Index 존재 여부와 실제 사용 여부 구분
- 대상 컬럼의 데이터 분포와 Cardinality 확인
- 통계 정보 갱신 시점 확인

## 실제 원인

## 해결

## 당시 몰랐던 개념

<!-- 예: Index가 있어도 Optimizer가 선택하지 않는 조건, 예상 행 수와 실제 행 수 차이가 뜻하는 것 -->

## 추가로 공부한 개념

## 지금 다시 대응한다면

```text
Query 자체가 느린가?
→ Full Scan인가?
→ Index가 있는가?
→ Index를 사용하는가?
→ Execution Plan은?
→ 데이터 분포는?
```

순서로 확인한다. Index를 추가하기 전에 실행계획부터 본다.

## 재발 방지 체크리스트

## 함께 읽기

- [12주차 - Index와 Execution Plan](03_Resource/06_database/03_index_execution_plan)
