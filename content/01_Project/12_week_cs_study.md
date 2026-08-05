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

트러블슈팅 사례는 **실제 공개 사례를 우선 사용**한다. 겪은 경험 중 해당 개념과 유관한 경험이 존재하는 경우에만 관련 내용을 작성한다.

## 학습 기록

| 주차 | 주제 | 학습 내용 | 트러블슈팅 |
| --- | --- | --- | --- |
| 1주차  | TCP/IP와 연결                      | [TCP IP와 연결](03_Resource/04_network/01_tcp) | [[03_Resource/04_network/02_tcpip_ts|TCP 연결 장애 사례]] |
| 2주차  | HTTP와 요청/응답                   | [[03_Resource/04_network/03_http|HTTP와 요청/응답]] | [[03_Resource/04_network/04_http_429_ts|HTTP 429 트러블슈팅 사례]] |
| 3주차  | DNS, HTTPS, Proxy, Load Balancer   | [[03_Resource/04_network/05_dns_https_proxy_lb|DNS, HTTPS, Proxy, Load Balancer]] | [[03_Resource/04_network/06_dns_tls_proxy_lb_ts|DNS, TLS, Proxy, Load Balancer 트러블슈팅 사례]] |
| 4주차  | Network 종합                       | [[03_Resource/04_network/07_network_summary\|Network 종합]] | [[03_Resource/04_network/08_network_summary_ts\|Network 종합 트러블슈팅 사례]] |
| 5주차  | Process, Thread, CPU               | [[03_Resource/05_os/01_process_thread_cpu\|Process, Thread와 CPU Scheduling]] | [[03_Resource/05_os/02_process_thread_cpu_ts\|CPU와 Thread 트러블슈팅 사례]] |
| 6주차  | Virtual Memory와 Paging            | [[03_Resource/05_os/03_virtual_memory\|Virtual Memory와 Memory 문제]] | [[03_Resource/05_os/04_virtual_memory_ts\|Memory 트러블슈팅 사례]] |
| 7주차  | 동시성과 I/O                       | [[03_Resource/05_os/05_concurrency_io\|동시성과 I/O]] | [[03_Resource/05_os/06_concurrency_io_ts\|동시성과 I/O 트러블슈팅 사례]] |
| 8주차  | OS 종합과 Linux 진단               | [[03_Resource/05_os/07_os_linux_summary\|OS와 Linux 진단 종합]] | [[03_Resource/05_os/08_os_linux_summary_ts\|File Descriptor 고갈 트러블슈팅 사례]] |
| 9주차  | Transaction, Isolation Level, MVCC | [[03_Resource/06_database/01_transaction_isolation_mvcc\|Transaction, Isolation Level, MVCC]] | [[03_Resource/06_database/02_transaction_isolation_mvcc_ts\|Transaction 트러블슈팅 사례]] |
| 10주차 | Index와 Execution Plan             | [[03_Resource/06_database/03_index_execution_plan\|Index와 Execution Plan]] | [[03_Resource/06_database/04_index_execution_plan_ts\|Slow Query 트러블슈팅 사례]] |
| 11주차 | Lock, Connection Pool, N+1         | [[03_Resource/06_database/05_lock_pool_nplus1\|Lock, Connection Pool, N+1]] | [[03_Resource/06_database/06_lock_pool_nplus1_ts\|Lock과 Connection Pool 트러블슈팅 사례]] |
| 12주차 | Database 종합                      | [[03_Resource/06_database/07_database_summary\|Database 종합]] | [[03_Resource/06_database/08_database_summary_ts\|Database 종합 장애 사례]] |

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

Kubernetes 장애 대응 경험은 해당 흐름을 이해하는 데 도움이 되는 경우에만 보조적으로 연결한다.

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

## 5주차 - Process, Thread와 CPU Scheduling

### 핵심 학습

#### Process와 Thread

* Program
* Process
* Thread
* Process State
* PCB의 역할

#### Process Memory

* Code
* Data
* BSS
* Heap
* Stack
* Thread별 Stack

#### CPU와 Scheduling

* CPU Bound
* I/O Bound
* CPU Scheduling의 목적
* FCFS
* Round Robin
* Time Slice

#### Context Switching

* Context Switching
* Process와 Thread의 Context Switching 차이
* Context Switching 비용

#### 실행 모델

* 동시성
* 병렬성

### 연관 학습

Java 서버와 연결해서 다음 정도를 확인한다.

* JVM은 OS 관점에서 하나의 Process인가?
* Java Thread와 OS Thread는 어떤 관계인가?
* Spring 서버는 요청을 어떤 Thread에서 처리하는가?

JVM이나 Thread 구현을 깊게 파는 것이 목적은 아니다.

### 학습 목표

* Program, Process, Thread의 차이를 설명할 수 있다.
* Process의 주요 상태와 상태 전이를 설명할 수 있다.
* PCB가 어떤 정보를 관리하는지 개략적으로 설명할 수 있다.
* Process의 주요 Memory 영역을 설명할 수 있다.
* Context Switching이 발생하는 이유와 비용을 설명할 수 있다.
* CPU Bound와 I/O Bound 작업을 구분할 수 있다.
* CPU Scheduling이 필요한 이유를 설명할 수 있다.
* FCFS와 Round Robin의 기본 동작과 차이를 설명할 수 있다.
* 동시성과 병렬성을 구분할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

* CPU 사용률 급증
* 특정 Process 또는 Thread의 CPU 과점유
* Context Switching 증가
* CPU는 낮지만 Load Average가 높은 문제

역추론 시 다음을 확인한다.

```text
CPU 사용률
→ Load Average
→ Process
→ Thread
→ Process State
→ CPU Bound / I/O Bound
→ Context Switching
```

---

## 6주차 - Virtual Memory와 Memory 문제

### 핵심 학습

#### Virtual Memory

* Virtual Memory가 필요한 이유
* Virtual Address
* Physical Address
* Page
* Frame
* Paging
* Page Table
* Page Fault

#### 주소 변환

* MMU의 역할
* TLB의 역할
* Virtual Address에서 Physical Address로 변환되는 기본 흐름

#### Memory 문제

* Swap
* Thrashing
* OOM
* OOM Killer

### 연관 학습

* Heap과 Process Memory의 차이
* JVM Heap과 실제 Process Memory의 차이
* RSS
* Paging과 Segmentation의 차이
* 내부 단편화와 외부 단편화

Segmentation과 단편화는 Paging과 비교하기 위한 개념 수준으로만 학습한다.

Page Replacement Algorithm과 LRU 구현은 필수 범위에서 제외한다.

### 학습 목표

* Virtual Memory가 필요한 이유를 설명할 수 있다.
* Page와 Frame의 차이를 설명할 수 있다.
* Paging과 Page Table의 역할을 설명할 수 있다.
* MMU와 TLB가 필요한 이유를 설명할 수 있다.
* Page Fault가 발생했을 때 어떤 일이 일어나는지 설명할 수 있다.
* Swap이 증가하면 성능이 저하될 수 있는 이유를 설명할 수 있다.
* Thrashing이 무엇인지 설명할 수 있다.
* Process Memory와 JVM Heap의 차이를 설명할 수 있다.
* OOM과 OOM Killer의 기본적인 동작을 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음과 관련된 사례를 선정한다.

* Memory Leak
* Swap 증가
* Thrashing
* OOM
* OOM Killer에 의한 Process 종료

분석 관점:

```text
Memory 사용량 증가
→ Process Memory
→ Heap / Native Memory
→ RSS
→ Page Cache
→ Swap
→ Page Fault
→ Thrashing
→ OOM Killer
```

모든 항목을 실제 사례에 억지로 적용하지 않고, 공개된 증상과 관련된 범위만 확인한다.

---

## 7주차 - 동시성과 I/O

### 핵심 학습

#### 동시성 제어

* Race Condition
* Critical Section
* Mutex
* Semaphore
* Deadlock
* Deadlock의 네 가지 발생 조건
* Thread Safe

#### Thread 관리

* Thread Pool
* Thread Pool을 사용하는 이유
* Thread 수 결정 시 고려 사항
* Thread Pool Exhaustion

#### I/O Model

* Blocking
* Non-Blocking
* Synchronous
* Asynchronous
* I/O Multiplexing
* select / poll / epoll의 관계
* epoll이 필요한 이유

### 연관 학습

* CPU Bound 작업과 Thread Pool
* I/O Bound 작업과 Thread Pool
* Lock 대기와 I/O 대기의 차이

`select`, `poll`, `epoll`의 내부 구현을 자세히 비교하기보다, 기존 방식의 한계와 epoll이 필요한 이유를 중심으로 학습한다.

IPC, Spin Lock, Lock-Free, Wait-Free는 필수 범위에서 제외한다.

### 학습 목표

* Race Condition과 Critical Section을 설명할 수 있다.
* Mutex와 Semaphore의 차이를 설명할 수 있다.
* Deadlock의 네 가지 발생 조건을 설명할 수 있다.
* Thread Safe의 의미를 설명할 수 있다.
* Thread Pool을 사용하는 이유를 설명할 수 있다.
* CPU Bound와 I/O Bound 작업에 따라 Thread Pool 크기 기준이 달라지는 이유를 설명할 수 있다.
* Thread Pool이 고갈되었을 때 나타나는 증상을 설명할 수 있다.
* Blocking / Non-Blocking과 Synchronous / Asynchronous를 구분할 수 있다.
* I/O Multiplexing이 필요한 이유를 설명할 수 있다.
* epoll이 다수의 연결을 처리하는 데 유리한 이유를 개략적으로 설명할 수 있다.

### 트러블슈팅

실제 공개 사례 중 다음 중 하나를 선정한다.

* Blocking I/O로 인한 요청 적체
* Thread Pool Exhaustion
* Lock 대기 또는 Deadlock
* Event Loop에서 Blocking 작업을 실행해 발생한 지연

역추론 시 다음을 구분한다.

```text
요청이 적체됨
→ CPU 사용률 확인
→ 실행 중인 Thread 수 확인
→ Thread State 확인
→ I/O 대기인가?
→ Lock 대기인가?
→ Thread Pool이 고갈됐는가?
```

---

## 8주차 - OS와 Linux 진단 종합

### 핵심 학습

#### Kernel Interface

* User Mode
* Kernel Mode
* System Call
* Application과 Kernel의 관계

#### File Descriptor

* File Descriptor
* Process별 File Descriptor Table
* File, Socket, Pipe와 File Descriptor의 관계
* Soft Limit
* Hard Limit
* Process별 `nofile`
* 시스템 전체 File Handle Limit
* File Descriptor 고갈

#### 주요 진단 도구

* `top`
* `ps`
* `free`
* `vmstat`
* `iostat`
* `lsof`
* `ss`
* `strace`
* `prlimit`
* `/proc`

명령어의 모든 옵션을 외우기보다 다음을 구분하는 데 집중한다.

* CPU 문제를 확인할 때 사용할 도구
* Memory와 Swap 문제를 확인할 때 사용할 도구
* Disk I/O 문제를 확인할 때 사용할 도구
* Network Socket 문제를 확인할 때 사용할 도구
* File Descriptor 문제를 확인할 때 사용할 도구
* Process가 어떤 System Call에서 대기하는지 확인할 때 사용할 도구

### 학습 목표

* User Mode와 Kernel Mode를 구분하는 이유를 설명할 수 있다.
* System Call이 Application과 Kernel을 연결하는 방식을 설명할 수 있다.
* File Descriptor가 무엇인지 설명할 수 있다.
* 일반 파일뿐 아니라 Socket과 Pipe도 FD로 관리되는 이유를 설명할 수 있다.
* Process별 FD Limit과 시스템 전체 File Handle Limit을 구분할 수 있다.
* File Descriptor가 고갈되었을 때 나타나는 증상을 설명할 수 있다.
* CPU, Memory, Disk I/O, Network, FD 문제를 어떤 도구로 확인할지 설명할 수 있다.

### 종합 질문

> 서버의 CPU 또는 Memory 사용량이 급증하거나 요청 처리가 지연될 때 어떤 순서로 원인을 확인할 것인가?

기본 흐름:

```text
증상과 영향 범위 확인
→ Process 확인
→ CPU와 Thread 상태 확인
→ Memory와 Swap 확인
→ Disk / Network I/O 확인
→ File Descriptor 확인
→ 필요 시 System Call 추적
```

### 트러블슈팅

1. 직접 경험한 Jenkins `Too many open files` 사례를 사용
2. 실제 공개 사례 중 다음과 관련된 사례를 선정한다.


---

# OS 4주 완료 목표

OS 면접 질문 전체를 다루는 것이 아니라, 백엔드 서버에서 발생할 수 있는 주요 문제를 OS 개념과 연결하는 것을 목표로 한다.

```text
요청 지연 또는 서버 이상
→ Process / Thread
→ CPU / Scheduling
→ Virtual Memory / Memory
→ Lock / I/O
→ File Descriptor
→ System Call
```

4주 완료 후에는 다음 질문에 자료 없이 답할 수 있어야 한다.

* Process와 Thread는 무엇이 다른가?
* CPU가 높은 상황과 Thread가 대기 중인 상황을 어떻게 구분할 것인가?
* Virtual Memory와 Paging은 왜 필요한가?
* Page Fault와 Swap은 성능에 어떤 영향을 주는가?
* Race Condition과 Deadlock은 무엇인가?
* Blocking / Non-Blocking과 Sync / Async는 어떻게 다른가?
* Thread Pool이 고갈되면 어떤 현상이 나타나는가?
* File Descriptor가 고갈되면 왜 파일과 Network 연결을 새로 열 수 없는가?
* CPU, Memory, I/O, FD 문제를 어떤 순서와 도구로 확인할 것인가?

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

---

# 참고 자료

## 공통

- [RFC Editor](https://www.rfc-editor.org/)
- [MDN Web Docs](https://developer.mozilla.org/en-US/)
- [Cloudflare Blog](https://blog.cloudflare.com/)

## Network

- [RFC 9293 - Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293)
- [RFC 9110 - HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
- [RFC 9113 - HTTP/2](https://www.rfc-editor.org/rfc/rfc9113)
- [RFC 9114 - HTTP/3](https://www.rfc-editor.org/rfc/rfc9114)
- [RFC 9000 - QUIC](https://www.rfc-editor.org/rfc/rfc9000)
- [Computer Networking: A Top-Down Approach Resources - UMass Amherst](https://gaia.cs.umass.edu/kurose_ross/)
- [Computer Networking Interactive Problems - UMass Amherst](https://gaia.cs.umass.edu/kurose_ross/interactive/)
- [Wireshark Labs - UMass Amherst](https://gaia.cs.umass.edu/kurose_ross/wireshark.php)
- [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/)

## OS

- [Operating Systems: Three Easy Pieces - University of Wisconsin–Madison](https://pages.cs.wisc.edu/~remzi/OSTEP/)
- [Operating Systems Course Notes - University of Illinois Chicago](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/)
- [Linux Kernel Documentation](https://docs.kernel.org/)
- [Linux man-pages](https://man7.org/linux/man-pages/)

## Database

- [MySQL 8.4 Reference Manual](https://dev.mysql.com/doc/refman/8.4/en/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/current/)
- [Spring Framework - Transaction Management](https://docs.spring.io/spring-framework/reference/data-access/transaction.html)
- [Hibernate ORM Documentation](https://docs.jboss.org/hibernate/orm/current/userguide/html_single/Hibernate_User_Guide.html)

## 사례 reference

- [Google Cloud Architecture Framework - Reliability](https://cloud.google.com/architecture/framework/reliability)
- [Netflix TechBlog](https://netflixtechblog.com/)
- [Uber Engineering](https://www.uber.com/blog/engineering/)
