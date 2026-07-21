---
title: 12주 CS 학습 계획
draft: false
tags:
  - project
  - cs
  - network
  - os
  - database
---

# 12주 CS 학습 계획

## 전체 구성

- 1~4주차: Network
- 5~8주차: OS
- 9~12주차: Database

## 매주 진행할 일

- 해당 주차 핵심 개념 학습 및 백지복습
- 실제 트러블슈팅 사례 1개 역추론
- 일요일까지 PR 제출
- 팀원 PR 1개 이상 리뷰

트러블슈팅 사례는 **실제 공개 사례를 우선 사용**한다. 내가 겪은 경험 중 해당 개념과 유관한 경험이 존재하는 경우에만 관련 내용을 작성한다.

## 학습 기록

| 주차 | 주제 | 학습 내용 | 트러블슈팅 |
| --- | --- | --- | --- |
| 1주차  | TCP/IP와 연결                      | [TCP IP와 연결](03_Resource/04_network/01_tcp) | [[03_Resource/04_network/01_tcp/troubleshooting|TCP 연결 장애 사례]] |
| 2주차  | HTTP와 요청/응답                   | 작성 예정 | 작성 예정   |
| 3주차  | DNS, HTTPS, Proxy, Load Balancer   | 작성 예정 | 작성 예정   |
| 4주차  | Network 종합                       | 작성 예정 | 작성 예정   |
| 5주차  | Process, Thread, CPU               | 작성 예정 | 작성 예정   |
| 6주차  | Virtual Memory와 Paging            | 작성 예정 | 작성 예정   |
| 7주차  | 동시성과 I/O                       | 작성 예정 | 작성 예정   |
| 8주차  | OS 종합과 Linux 진단               | 작성 예정 | 작성 예정   |
| 9주차  | Transaction, Isolation Level, MVCC | 작성 예정 | 작성 예정   |
| 10주차 | Index와 Execution Plan             | 작성 예정 | 작성 예정   |
| 11주차 | Lock, Connection Pool, N+1         | 작성 예정 | 작성 예정   |
| 12주차 | Database 종합                      | 작성 예정 | 작성 예정   |

---

# 1~4주차 Network

## 1주차 - TCP/IP와 연결

### 핵심 학습

- OSI / TCP-IP 계층 개념
- TCP와 UDP
- TCP 신뢰성 보장
- IP, Port, Socket
- 3-way Handshake
- 4-way Handshake
- TCP Socket State
- TIME_WAIT
- 흐름 제어
- 혼잡 제어

### 추가 학습

- NAT / Subnet / Gateway
- ARP / Routing 기초
- Connection Timeout
- Local Port 고갈
- TIME_WAIT 증가

### 학습 목표

- OSI 모델과 TCP/IP 모델의 계층별 역할을 설명할 수 있다.
- TCP와 UDP의 차이와 사용 사례를 설명할 수 있다.
- TCP가 순서 보장, 오류 감지, 재전송으로 신뢰성을 보장하는 방식을 설명할 수 있다.
- TCP 연결 생성과 종료 과정을 설명할 수 있다.
- TIME_WAIT이 필요한 이유를 설명할 수 있다.
- 흐름 제어와 혼잡 제어의 차이를 설명할 수 있다.
- Subnet, Gateway, ARP, Routing, NAT가 IP 패킷 전달에 관여하는 과정을 설명할 수 있다.
- 하나의 TCP 연결이 어떻게 생성되고 종료되는지 전체 흐름을 설명할 수 있다.

### 트러블슈팅

실제 사례 중 다음과 관련된 사례를 선정한다.

- TCP 연결 실패
- Connection Storm
- Local Port 고갈
- TIME_WAIT 증가

사례의 증상만 먼저 확인한 뒤 다음 순서로 역추론한다.

1. 문제 상황 파악
2. TCP 연결 관점에서 원인 가설 설정
3. 확인할 로그, 메트릭, 명령어 정의
4. 실제 원인 확인
5. 가설과 실제 원인 비교

---

## 2주차 - HTTP와 요청/응답

### 핵심 학습

- HTTP Request / Response 구조
- HTTP Method
- HTTP Status Code
- HTTP 멱등성
- HTTP/1.1
- HTTP/2
- HTTP/3
- Keep-Alive
- Stateless
- Cookie
- Session

### 연관 학습

- Timeout
- Retry
- Rate Limiting

### 학습 목표

- HTTP 요청과 응답 구조를 설명할 수 있다.
- HTTP Method의 멱등성과 재시도의 관계를 설명할 수 있다.
- HTTP/1.1, HTTP/2, HTTP/3의 주요 차이를 설명할 수 있다.
- Keep-Alive가 연결과 성능에 어떤 영향을 주는지 설명할 수 있다.
- Stateless한 HTTP에서 로그인 상태를 유지할 수 있는 이유를 설명할 수 있다.
- 실패한 HTTP 요청을 재시도할 때 고려해야 할 점을 설명할 수 있다.

### 트러블슈팅

외부 OpenAPI 호출 시 발생했던 HTTP 429 경험을 활용한다.

```text
피크 시간대 API 요청 실패 증가
→ HTTP Status 확인
→ Rate Limit 가능성 확인
→ 응답 Header 확인
→ Retry 전략 검토
→ Header 기반 대기 적용
→ 성공률 변화 확인
```

추가로 다음 내용을 복습한다.

- Retry가 장애를 악화시킬 수 있는 이유
- Exponential Backoff
- Jitter
- Retry 횟수 제한

---

## 3주차 - DNS, HTTPS, Proxy, Load Balancer

### 핵심 학습

- DNS 조회 과정
- HTTP와 HTTPS
- TLS Handshake
- 대칭키와 비대칭키
- 인증서
- 인증서 체인
- Proxy
- Reverse Proxy
- L4 Load Balancer
- L7 Load Balancer

### 학습 목표

- DNS 조회 과정을 설명할 수 있다.
- HTTPS 연결에서 TLS와 인증서가 어떤 역할을 하는지 설명할 수 있다.
- Proxy와 Reverse Proxy의 차이를 설명할 수 있다.
- L4와 L7 Load Balancer의 차이를 설명할 수 있다.
- URL 요청이 실제 서버에 도달하기 전까지 거치는 주요 단계를 설명할 수 있다.

### 트러블슈팅

다음과 같은 실제 공개 장애 사례를 선정한다.

- Load Balancer와 Backend 간 연결 장애
- DNS 장애
- TLS 인증서 장애
- Reverse Proxy 설정 문제

증상까지만 확인한 뒤 다음 관점에서 가설을 세운다.

```text
DNS
→ Network Connection
→ TLS
→ Load Balancer
→ Reverse Proxy
→ Backend
```

개인 Kubernetes 경험은 해당 흐름을 이해하는 데 도움이 되는 경우에만 보조적으로 연결한다.

---

## 4주차 - Network 종합

### 핵심 학습

- Authentication과 Authorization
- Same-Origin Policy
- CORS
- CORS Preflight
- XSS / CSRF 기초
- REST
- WebSocket 개념
- CDN 개념

### 종합 복습

새로운 개념 학습보다 1~3주차 내용을 연결하는 데 집중한다. 다음 질문을 자료 없이 설명한다.

> 브라우저에서 URL을 입력한 뒤 서버의 응답을 받기까지 어떤 과정이 일어나는가?

```text
DNS 조회
→ TCP 또는 QUIC 연결
→ TLS
→ HTTP 요청
→ Proxy 또는 Load Balancer
→ 서버 처리
→ HTTP 응답
```

### 학습 목표

- Authentication과 Authorization의 차이를 설명할 수 있다.
- Same-Origin Policy와 CORS의 관계를 설명할 수 있다.
- 브라우저가 CORS Preflight 요청을 보내는 조건과 목적을 설명할 수 있다.
- XSS와 CSRF의 차이와 기본 방어 방법을 설명할 수 있다.
- REST, WebSocket, CDN의 역할을 요청 흐름과 연결해 설명할 수 있다.

---

# 5~8주차 OS

## 5주차 - Process, Thread, CPU

### 핵심 학습

- Program
- Process
- PCB / Process State
- Thread
- 동시성과 병렬성
- Process Memory 영역
- Context Switching
- CPU Scheduling
- 기본 Scheduling Algorithm
- CPU Bound
- I/O Bound

### 연관 학습

Java 서버와 연결해서 다음 정도를 확인한다.

- JVM은 OS 관점에서 무엇인가?
- Java Thread와 OS Thread의 관계
- Spring 서버의 요청 처리 Thread

JVM 자체를 깊게 공부하는 것이 목적은 아니다.

### 학습 목표

- Process와 Thread의 차이를 설명할 수 있다.
- PCB가 관리하는 정보와 Process State의 전이 과정을 설명할 수 있다.
- 동시성과 병렬성을 구분할 수 있다.
- Process의 주요 Memory 영역을 설명할 수 있다.
- Context Switching이 발생하는 이유와 비용을 설명할 수 있다.
- FCFS, SJF, Round Robin 등 기본 Scheduling Algorithm의 차이를 설명할 수 있다.
- CPU Bound와 I/O Bound 작업을 구분할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

- CPU 사용률 급증
- 특정 Process CPU 과점유
- 특정 Thread CPU 과점유
- Resource Exhaustion

```text
CPU 사용률
→ Load Average
→ Process
→ Thread
→ CPU Bound 여부
→ I/O Wait 여부
```

---

## 6주차 - Virtual Memory와 Paging

### 핵심 학습

- Virtual Memory
- Segmentation / Fragmentation
- Paging
- Page / Frame
- Page Table
- MMU / TLB
- Page Fault
- Thrashing / Page Replacement 기초
- Swap
- RSS
- OOM

### 연관 학습

- Heap과 Process Memory의 차이
- JVM Heap과 실제 Process Memory의 차이

### 학습 목표

- Virtual Memory가 필요한 이유를 설명할 수 있다.
- Segmentation과 Paging을 구분하고 Fragmentation이 발생하는 이유를 설명할 수 있다.
- Page와 Frame의 관계를 설명할 수 있다.
- MMU와 TLB가 가상 주소를 물리 주소로 변환할 때 하는 역할을 설명할 수 있다.
- Paging이 어떻게 동작하는지 설명할 수 있다.
- Page Fault가 발생했을 때 어떤 일이 일어나는지 설명할 수 있다.
- Page Replacement가 필요한 이유와 Thrashing이 발생하는 과정을 설명할 수 있다.
- Swap 증가가 서버 성능에 어떤 영향을 줄 수 있는지 설명할 수 있다.
- OOM이 발생하는 기본적인 과정을 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

- Memory Leak
- OOM
- Swap 증가
- OOM Killer

```text
Memory 사용량 증가
→ Heap
→ Native Memory
→ Page Cache
→ Swap
→ Memory Leak
→ OOM Killer
```

---

## 7주차 - 동시성과 I/O

### 핵심 학습

- Race Condition
- Critical Section
- Mutex
- Semaphore
- Deadlock
- Thread Safe / Thread Pool
- IPC 기초
- Blocking / Non-Blocking
- Synchronous / Asynchronous
- I/O Multiplexing
- select
- poll
- epoll

### 학습 목표

- Race Condition과 Critical Section을 설명할 수 있다.
- Mutex와 Semaphore의 차이를 설명할 수 있다.
- Deadlock의 네 가지 발생 조건을 설명할 수 있다.
- Thread Safe의 의미와 Thread Pool을 사용하는 이유를 설명할 수 있다.
- Process 간 데이터를 교환하는 기본 IPC 방식을 설명할 수 있다.
- Blocking / Non-Blocking과 Synchronous / Asynchronous를 구분할 수 있다.
- I/O Multiplexing이 필요한 이유를 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음 중 하나를 선정한다.

- Blocking I/O로 인한 요청 적체
- Thread Pool Exhaustion
- Deadlock

```text
CPU가 높은가?
→ 아니면 Thread가 대기 중인가?
→ I/O 대기인가?
→ Lock 대기인가?
→ Thread Pool이 고갈됐는가?
```

---

## 8주차 - OS 종합과 Linux 진단

### 핵심 학습

- Kernel Mode
- User Mode
- System Call
- Interrupt
- File Descriptor
- File System / inode 기초

### 주요 진단 도구

- top
- ps
- free
- vmstat
- iostat
- strace
- lsof
- ss

명령어 옵션 암기보다 어떤 상황에서 어떤 도구를 사용하는지 이해하는 데 집중한다.

### 학습 목표

- System Call과 User Mode / Kernel Mode의 관계를 설명할 수 있다.
- File Descriptor가 무엇인지 설명할 수 있다.
- File System에서 inode가 파일의 메타데이터와 데이터 블록을 연결하는 방식을 설명할 수 있다.
- File Descriptor 고갈 시 발생할 수 있는 문제를 설명할 수 있다.
- CPU, Memory, Disk I/O 문제를 각각 어떤 도구로 확인할지 설명할 수 있다.

### 종합 질문

> 서버의 CPU 또는 Memory 사용량이 급증했을 때 어떤 순서로 원인을 확인할 것인가?

```text
증상 확인
→ Process와 Thread
→ Memory와 Swap
→ Disk와 Network I/O
→ 필요 시 System Call 추적
```

### 트러블슈팅

겉으로는 Application 또는 Database 장애처럼 보였지만 실제로는 다음과 같은 OS 계층 문제였던 실제 사례를 선정한다.

- Disk I/O 지연
- VM 또는 Host 문제
- File Descriptor 고갈
- Memory 문제

OS 계층과 상위 Application 계층의 장애가 어떻게 연결되는지 분석한다.

---

# 9~12주차 Database

## 9주차 - Transaction, Isolation Level, MVCC

### 핵심 학습

- Transaction
- ACID
- Commit
- Rollback
- Transaction 범위
- Isolation Level
- Dirty Read
- Non-Repeatable Read
- Phantom Read
- MVCC
- Undo / Redo / WAL

### 연관 학습

Spring 환경에서 다음 정도를 연결한다.

- `@Transactional`
- Transaction Boundary
- Long Transaction

### 학습 목표

- Transaction과 ACID를 설명할 수 있다.
- Transaction 범위를 잘못 잡았을 때 발생할 수 있는 문제를 설명할 수 있다.
- Isolation Level별 차이를 설명할 수 있다.
- MVCC가 무엇이며 왜 사용하는지 설명할 수 있다.
- Undo, Redo, WAL이 Transaction의 Rollback과 장애 복구에 어떻게 사용되는지 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

- Long Transaction
- Transaction Contention
- 잘못된 Transaction 범위

```text
Transaction 시작 시점
→ Transaction 종료 시점
→ Transaction 유지 시간
→ Lock 유지 여부
→ 다른 요청에 미치는 영향
```

---

## 10주차 - Index와 Execution Plan

### 핵심 학습

- B+Tree
- Index
- Clustered Index
- Composite Index
- Covering Index
- Selectivity
- Cardinality
- Index가 사용되지 않는 경우
- Execution Plan
- EXPLAIN
- EXPLAIN ANALYZE
- Optimizer / CBO
- Full Table Scan
- Index Scan
- Nested Loop / Hash Join

### 실습

직접 테스트 테이블과 데이터를 만들어 실행계획을 비교한다.

```text
Index 없음
→ Single Column Index
→ Composite Index
→ Composite Index 컬럼 순서 변경
```

각 경우의 Execution Plan을 확인한다.

### 학습 목표

- B+Tree가 Database Index에 적합한 이유를 설명할 수 있다.
- Clustered Index와 Non-Clustered Index의 차이를 설명할 수 있다.
- Composite Index의 컬럼 순서가 중요한 이유를 설명할 수 있다.
- Covering Index를 설명할 수 있다.
- Selectivity와 Cardinality가 Index 선택에 미치는 영향을 설명할 수 있다.
- Execution Plan에서 확인해야 할 주요 항목을 설명할 수 있다.
- Optimizer와 CBO가 실행계획을 선택하는 방식을 설명할 수 있다.
- EXPLAIN과 EXPLAIN ANALYZE의 차이를 설명할 수 있다.
- Nested Loop Join과 Hash Join의 동작 방식과 선택 조건을 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

- Slow Query
- 잘못된 Query 배포
- Index 미사용
- 잘못된 Composite Index

```text
Query 자체가 느린가?
→ Full Scan인가?
→ Index가 있는가?
→ Index를 사용하는가?
→ Execution Plan은?
→ 데이터 분포는?
```

---

## 11주차 - Lock, Connection Pool, N+1

### 핵심 학습

- Shared Lock
- Exclusive Lock
- Lock Wait
- Deadlock
- Long Transaction
- Connection Pool
- Connection Timeout
- N+1
- Optimistic Lock
- Pessimistic Lock

### 학습 목표

- Shared Lock과 Exclusive Lock의 차이를 설명할 수 있다.
- Lock Wait와 Deadlock의 차이를 설명할 수 있다.
- Connection Pool이 고갈되었을 때 나타나는 증상을 설명할 수 있다.
- N+1 문제가 무엇이며 어떻게 확인하는지 설명할 수 있다.
- Optimistic Lock과 Pessimistic Lock을 어떤 상황에서 선택하는지 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

- Lock Contention
- Deadlock
- Connection Pool Exhaustion
- Long Transaction으로 인한 요청 지연

```text
Application Thread
→ Connection Pool
→ DB Connection
→ Transaction
→ Query
→ Lock
```

어느 구간에서 대기하는지 구분하는 데 집중한다.

---

## 12주차 - Database 종합

### 추가 복습

- RDB vs NoSQL
- Replication
- Replication Lag
- Sharding
- Partitioning
- Backup
- Recovery
- Normalization
- Denormalization

### 학습 목표

- RDB와 NoSQL의 데이터 모델과 선택 기준을 설명할 수 있다.
- Replication, Sharding, Partitioning의 목적과 차이를 설명할 수 있다.
- Replication Lag이 읽기 일관성과 장애 전환에 미치는 영향을 설명할 수 있다.

### 종합 질문

> 평소 정상적으로 동작하던 API가 느려졌을 때 Database 관점에서 무엇을 어떤 순서로 확인할 것인가?

```text
Connection Pool
→ Slow Query
→ Execution Plan과 Index
→ Lock과 Transaction
→ Replication 상태
```

### 트러블슈팅

Database의 여러 요소가 동시에 영향을 준 실제 장애 사례를 선정한다.

- Connection Capacity 증가
- Query Contention
- Lock
- Traffic 증가
- Schema Migration
- Timeout
- Replication 영향

하나의 원인만 찾는 것이 아니라 장애가 어떤 연쇄 과정을 거쳐 확대되었는지 분석한다.

---

# 매주 학습 방식

## 1. 개념 학습

해당 주차의 핵심 개념을 학습한다. 모든 개념을 동일한 깊이로 공부하기보다 이미 설명 가능한 내용은 빠르게 복습하고, 설명이 어려운 부분에 시간을 더 사용한다.

## 2. 백지복습

학습이 끝난 뒤 자료를 보지 않고 해당 주차에 공부한 내용을 자유롭게 정리한다. 목적은 정답을 작성하는 것이 아니라 다음을 확인하는 것이다.

- 무엇을 기억하고 있는가?
- 무엇을 설명할 수 있는가?
- 어느 부분에서 막히는가?
- 개념 사이의 연결을 이해하고 있는가?

백지복습 후 자료를 다시 확인하고 부족한 부분만 보완한다.

## 3. 트러블슈팅 역추론

매주 실제 사례 1개를 사용한다.

```text
해당 개념을 잘 보여주는 실제 공개 사례
→ 자연스럽게 연결되는 개인 실무 경험
```

개인 경험을 활용하기 위해 억지로 사례를 끼워 넣지 않는다.

```text
1. 공개된 증상까지만 확인
2. 원인 가설 설정
3. 확인해야 할 로그, 메트릭, 명령어 설계
4. 실제 원인 확인
5. 내 가설과 실제 원인의 차이 분석
6. 이번 주 학습한 CS 개념으로 다시 설명
```

## 4. PR

PR은 한 주 동안의 학습 기록을 제출하는 단위다.

```markdown
## 이번 주 학습 내용

## 백지복습

## 트러블슈팅 역추론

## 이전 PR에서 배운 내용
```

필요한 경우 실습 결과나 추가 정리를 포함한다.

---

# 12주 완료 목표

## Network

단순히 특정 요청이 실패했다는 사실만 보는 것이 아니라 다음 계층을 구분해서 생각할 수 있다.

```text
DNS
→ TCP / QUIC
→ TLS
→ HTTP
→ Proxy / Load Balancer
→ Application
```

## OS

서버의 CPU 또는 Memory 사용량이 높다는 현상에서 끝나지 않고 다음 관점으로 원인을 좁힐 수 있다.

```text
Process
→ Thread
→ CPU
→ Memory
→ Disk / Network I/O
→ System Call
```

## Database

API가 느리다는 현상에서 바로 Index를 추가하는 것이 아니라 다음 순서로 병목을 확인할 수 있다.

```text
Connection Pool
→ Query
→ Execution Plan
→ Index
→ Transaction
→ Lock
→ Replication
```

12주 동안 개별 개념을 암기하는 것이 아니라 Network, OS, Database 각각에서 실제 장애 상황을 만났을 때 어떤 계층을 어떤 순서로 확인해야 하는지 판단할 수 있는 수준을 목표로 한다.
