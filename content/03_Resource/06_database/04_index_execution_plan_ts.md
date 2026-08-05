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

## 사례 선정 기준

- Slow Query, 잘못된 Query 배포, Index 미사용, 잘못된 Composite Index 중 하나와 관련된 공개 사례를 선택한다.
- 장애를 겪은 조직이 직접 공개한 기술 블로그, 발표 자료, 사후 분석 문서를 우선 사용한다.
- 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자가 경험한 현상과 최초로 관찰된 로그 및 메트릭만 기록한다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 배포와 데이터 증가 여부를 정리한다. -->

## 2. Query 관점에서 원인 가설 설정

```text
Query 자체가 느린가?
→ Full Scan인가?
→ Index가 있는가?
→ Index를 사용하는가?
→ Execution Plan은?
→ 데이터 분포는?
```

| 우선순위 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ----------- | ------------------ |
| 1        |      |             |                    |
| 2        |      |             |                    |
| 3        |      |             |                    |

## 3. 확인할 로그, 메트릭, 명령어 정의

### 로그

<!-- Slow Query Log, Application의 Query 실행 시간 로그, 배포 이력과 판단 기준을 기록한다. -->

### 메트릭

<!-- Query 실행 시간 분포, 실행 횟수, 스캔한 행 수, 반환한 행 수, Buffer Pool Hit 비율을 기록한다. -->

### Query

```sql
-- 예: 실행계획 확인
EXPLAIN SELECT ...;

-- 예: 실제 실행 통계까지 확인
EXPLAIN ANALYZE SELECT ...;

-- 예: MySQL Slow Query Log 설정 확인
SHOW VARIABLES LIKE 'slow_query%';
SHOW VARIABLES LIKE 'long_query_time';

-- 예: PostgreSQL 실행 통계 상위 Query 확인
SELECT query, calls, mean_exec_time, rows
FROM pg_stat_statements ORDER BY mean_exec_time DESC LIMIT 10;
```

<!-- 각 결과에서 무엇을 확인할지 함께 설명한다. 운영 환경에서 `EXPLAIN ANALYZE`를 실행할 때의 부하도 확인한다. -->

### 갑자기 느려진 이유 구분

<!-- Query는 그대로인데 느려진 경우 데이터 증가, 통계 정보 변화, 실행계획 변경 중 무엇을 먼저 확인할지 정리한다. -->

## 4. 실제 원인 확인

<!-- 공개 사례가 밝힌 직접 원인과 근본 원인, 이를 뒷받침한 증거를 기록한다. -->

## 5. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

<!-- 즉시 조치와 장기 개선을 구분해서 기록한다. Index 추가가 만드는 쓰기 비용도 함께 정리한다. -->

## 개인 경험과의 연결

<!-- 개념과 자연스럽게 연결되는 경험이 있을 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 같은 증상이 발생했을 때 재사용할 수 있는 판단 기준을 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 공식 문서를 기록한다. -->

## 함께 읽기

- [[03_Resource/06_database/03_index_execution_plan|10주차 - Index와 Execution Plan]]
