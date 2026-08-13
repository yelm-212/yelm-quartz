---
title: CS 학습 계획
draft: false
tags:
  - project
  - cs
  - network
  - os
  - database
---

# CS 학습 계획

## 전체 구성

- 1~4주차: Network
- 5~10주차: OS
- 11~14주차: Database

## 매주 진행할 일

- 해당 주차 핵심 개념 학습 및 백지복습
- 주제별 추가 기록 작성
- 일요일까지 PR 제출
- 팀원 PR 1개 이상 리뷰

Network와 Database는 트러블슈팅 역추론 또는 딥다이브 중 하나를 진행한다. 그 주 개념을 어느 쪽으로 더 확실하게 확인할 수 있는지를 기준으로 고른다. OS는 트러블슈팅 글 대신 학습 중 새롭게 이해하거나 연결한 내용을 인사이트로 정리한다.

| 선택 | 하는 일 | 고르는 기준 |
| --- | --- | --- |
| 트러블슈팅 역추론 | 실제 장애 사례의 증상까지만 보고 원인을 추론한 뒤 실제 원인과 비교한다 | 해당 개념이 실제 장애로 잘 드러나는 사례를 찾을 수 있을 때 |
| 딥다이브 | 직접 실행하고 관측한다 | 사례를 찾기 어렵거나, 직접 재현해봐야 이해되는 개념일 때 |

트러블슈팅 사례는 **실제 공개 사례를 우선 사용**한다. 겪은 경험 중 해당 개념과 유관한 경험이 존재하는 경우에만 관련 내용을 작성한다.

딥다이브는 **학습한 내용을 다시 정리하는 문서가 아니다.** 개념 정리는 학습 내용 문서에서 이미 하므로, 딥다이브에서는 확인하고 싶은 질문을 정하고 예상 결과를 먼저 적은 뒤 직접 돌려서 관측한 결과와 비교한다.

## 학습 기록

| 주차 | 주제 | 학습 내용 | 추가 기록 |
| --- | --- | --- | --- |
| 1주차  | TCP/IP와 연결                      | [TCP IP와 연결](03_Resource/04_network/01_tcp) | [TCP 연결 장애 사례](03_Resource/04_network/02_tcpip_ts) |
| 2주차  | HTTP와 요청 및 응답                | [HTTP와 요청 및 응답](03_Resource/04_network/03_http) | [HTTP 429 트러블슈팅 사례](03_Resource/04_network/04_http_429_ts) |
| 3주차  | DNS, HTTPS, Proxy, Load Balancer   | [DNS, HTTPS, Proxy, Load Balancer](03_Resource/04_network/05_dns_https_proxy_lb) | [DNS, TLS, Proxy, Load Balancer 트러블슈팅 사례](03_Resource/04_network/06_dns_tls_proxy_lb_ts) |
| 4주차  | Network 종합                       | [Network 종합](03_Resource/04_network/07_network_summary) | [Network 종합 트러블슈팅 사례](03_Resource/04_network/08_network_summary_ts) |
| 5주차  | 가상화: 프로세스와 CPU             | [프로세스 가상화](03_Resource/05_os/01_virtualization_process) | [프로세스 가상화 인사이트](03_Resource/05_os/02_virtualization_process_insight) |
| 6주차  | 가상화: 주소 공간과 메모리         | [메모리 가상화](03_Resource/05_os/03_virtualization_memory) | [메모리 가상화 인사이트](03_Resource/05_os/04_virtualization_memory_insight) |
| 7주차  | 병행성: 스레드와 락                | [병행성 기초](03_Resource/05_os/05_concurrency_basics) | [병행성 기초 인사이트](03_Resource/05_os/06_concurrency_basics_insight) |
| 8주차  | 병행성: 동기화와 교착 상태         | [병행성 제어](03_Resource/05_os/07_concurrency_coordination) | [병행성 제어 인사이트](03_Resource/05_os/08_concurrency_coordination_insight) |
| 9주차  | 영속성: I/O와 저장 장치            | [I/O와 저장 장치](03_Resource/05_os/09_persistence_io_storage) | [I/O와 저장 장치 인사이트](03_Resource/05_os/10_persistence_io_storage_insight) |
| 10주차 | 영속성: 파일과 파일 시스템         | [파일 시스템과 데이터 무결성](03_Resource/05_os/11_persistence_filesystems) | [파일 시스템 인사이트](03_Resource/05_os/12_persistence_filesystems_insight) |
| 11주차 | Transaction, Isolation Level, MVCC | [Transaction, Isolation Level, MVCC](03_Resource/06_database/01_transaction_isolation_mvcc) | [Transaction 트러블슈팅 사례](03_Resource/06_database/02_transaction_isolation_mvcc_ts) |
| 12주차 | Index와 Execution Plan             | [Index와 Execution Plan](03_Resource/06_database/03_index_execution_plan) | [Slow Query 트러블슈팅 사례](03_Resource/06_database/04_index_execution_plan_ts) |
| 13주차 | Lock, Connection Pool, N+1         | [Lock, Connection Pool, N+1](03_Resource/06_database/05_lock_pool_nplus1) | [Lock과 Connection Pool 트러블슈팅 사례](03_Resource/06_database/06_lock_pool_nplus1_ts) |
| 14주차 | Database 종합                      | [Database 종합](03_Resource/06_database/07_database_summary) | [Database 종합 장애 사례](03_Resource/06_database/08_database_summary_ts) |

---

# 1~4주차 Network

## 1주차 - TCP/IP와 연결

### 핵심 학습

- OSI와 TCP-IP 계층 개념
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

- NAT, Subnet, Gateway
- ARP와 Routing 기초
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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- Wireshark로 연결 수립과 종료를 캡처한다. flag, seq, ack가 예상과 일치하는지 확인한다.
- `tc netem`으로 지연과 패킷 손실을 주입하고 재전송과 전송량 변화를 관측한다.
- 짧은 연결을 반복 생성해 TIME_WAIT 수와 ephemeral port 사용량이 어떻게 변하는지 측정한다.

---

## 2주차 - HTTP와 요청 및 응답

### 핵심 학습

- HTTP 요청과 응답 구조
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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- 같은 요청을 `--http1.1`, `--http2`, `--http3`로 보내 연결 수와 전송 완료 시간을 비교한다.
- Keep-Alive를 켜고 끄면서 연결 재사용 여부와 요청당 지연 차이를 측정한다.
- 로컬 서버에 rate limit을 걸어 429와 `Retry-After`를 재현하고, 즉시 재시도와 backoff+jitter의 성공률을 비교한다.

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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- `dig +trace`로 위임 경로를 따라가고, TTL이 남은 동안 응답이 어디서 오는지 확인한다.
- 자체 CA로 인증서를 발급해 hostname mismatch, 만료, intermediate 누락 상황을 각각 재현하고 오류 메시지를 비교한다.
- nginx로 reverse proxy를 구성해 `X-Forwarded-*` 전달 여부와 upstream timeout 동작을 확인한다.

---

## 4주차 - Network 종합

### 핵심 학습

- Authentication과 Authorization
- Same-Origin Policy
- CORS
- CORS Preflight
- XSS와 CSRF 기초
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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- 요청 하나를 DNS, connect, TLS, TTFB로 분해해 각 구간이 전체 시간에서 차지하는 비중을 측정한다.
- Preflight가 발생하는 요청과 발생하지 않는 요청을 각각 만들어 OPTIONS 흐름과 응답 Header를 비교한다.
- 로컬에 XSS 또는 CSRF에 취약한 페이지를 만들고 방어 적용 전후의 동작 차이를 확인한다.

---

# 5~10주차 OS

## 학습 방향

OS는 OSTEP의 큰 목차를 기준으로 가상화, 병행성, 영속성을 각각 2주씩 학습한다. OSTEP을 기본 안내서로 활용하되 반드시 한 권을 순서대로 읽을 필요는 없다. 강의, 공식 문서, 다른 책 등 어떤 자료를 사용해도 되며, 각 주차의 범위와 학습 목표를 충족하면 된다.

세부 챕터는 이해도와 진도에 따라 조정한다. 처음 정한 챕터 수를 채우는 것보다 각 영역의 핵심 질문에 답하고 개념 사이의 연결을 설명하는 것을 우선한다.

OS 기간에도 다음 진행 방식은 유지한다.

- 일요일까지 학습 내용과 인사이트를 PR로 제출한다.
- 팀원 PR을 1개 이상 리뷰한다.
- 같은 영역을 공부하므로 리뷰할 때 배경지식 부담이 낮아지고, 서로 다른 해석과 자료를 비교할 수 있다.
- 트러블슈팅 글 대신 학습 전후에 관점이 달라진 지점이나 개념 사이의 연결을 인사이트로 정리한다.

## 5주차 - 가상화 1: 프로세스와 CPU

### 핵심 학습

- 프로세스와 프로세스 상태
- 프로세스 생성과 제어를 위한 API
- 제한적 직접 실행
- CPU 스케줄링의 목적과 기본 정책
- 멀티 레벨 피드백 큐
- 문맥 교환과 CPU 가상화 비용

### 학습 목표

- 운영체제가 하나의 CPU를 여러 프로세스가 사용하는 것처럼 보이게 만드는 방식을 설명할 수 있다.
- 프로세스 생성, 실행, 대기, 종료 흐름을 설명할 수 있다.
- 스케줄링 정책이 응답 시간, 반환 시간, 공정성에 미치는 영향을 비교할 수 있다.
- 문맥 교환이 필요한 이유와 비용을 설명할 수 있다.

### 인사이트 기록

프로세스 추상화 또는 스케줄링 정책을 학습하며 기존 생각이 바뀐 지점, 실제 애플리케이션 실행과 연결한 내용을 하나 이상 정리한다.

---

## 6주차 - 가상화 2: 주소 공간과 메모리

### 핵심 학습

- 주소 공간
- 주소 변환
- 세그멘테이션과 페이징
- 페이지 테이블과 TLB
- 페이지 폴트와 스와핑
- 메모리 가상화의 비용과 한계

### 학습 목표

- 운영체제가 프로세스마다 독립된 주소 공간을 제공하는 이유를 설명할 수 있다.
- 가상 주소가 물리 주소로 변환되는 흐름을 설명할 수 있다.
- 페이징과 TLB가 성능과 메모리 사용량에 미치는 영향을 설명할 수 있다.
- 페이지 폴트와 스와핑이 지연으로 이어지는 과정을 설명할 수 있다.

### 인사이트 기록

주소 공간이라는 추상화가 격리와 편의성을 제공하는 방식, 그 대가로 생기는 변환 비용을 연결해 정리한다.

---

## 7주차 - 병행성 1: 스레드와 락

### 핵심 학습

- 병행성이 필요한 이유
- 스레드와 스레드 API
- 공유 상태와 경쟁 조건
- 임계 영역
- 락의 기본 동작
- 효율적인 락을 위한 자료구조와 하드웨어 지원

### 학습 목표

- 병행 실행에서 비결정적인 결과가 발생하는 이유를 설명할 수 있다.
- 경쟁 조건과 임계 영역을 구분할 수 있다.
- 락이 상호 배제를 제공하는 방식을 설명할 수 있다.
- 정확성뿐 아니라 대기와 공정성 관점에서도 락을 비교할 수 있다.

### 인사이트 기록

순차 실행을 전제로 한 직관이 병행 실행에서 깨지는 사례와 락이 해결하는 문제 및 새로 만드는 비용을 함께 정리한다.

---

## 8주차 - 병행성 2: 동기화와 교착 상태

### 핵심 학습

- 조건 변수
- 세마포어
- 생산자와 소비자 문제
- 교착 상태의 발생 조건과 대응
- 이벤트 기반 병행성
- 스레드 기반 모델과 이벤트 기반 모델의 차이

### 학습 목표

- 락과 조건 변수의 역할을 구분할 수 있다.
- 세마포어로 실행 순서와 자원 개수를 제어하는 방식을 설명할 수 있다.
- 교착 상태의 발생 조건과 예방, 회피, 탐지 전략을 설명할 수 있다.
- 스레드 기반 처리와 이벤트 기반 처리의 장단점을 비교할 수 있다.

### 인사이트 기록

상호 배제만으로 해결되지 않는 실행 순서 문제나 교착 상태의 구조를 정리하고, 익숙한 서버 모델과 연결한다.

---

## 9주차 - 영속성 1: I/O와 저장 장치

### 핵심 학습

- 장치와 운영체제의 상호작용
- 인터럽트와 DMA
- 하드 디스크의 구조와 접근 비용
- 디스크 스케줄링
- RAID의 성능과 내결함성
- 저장 장치 추상화의 한계

### 학습 목표

- CPU와 장치가 I/O 요청을 주고받는 흐름을 설명할 수 있다.
- 저장 장치의 물리적 특성이 접근 지연에 미치는 영향을 설명할 수 있다.
- RAID 구성이 성능, 용량, 내결함성 사이에서 만드는 절충을 설명할 수 있다.
- 메모리 접근과 저장 장치 접근의 비용 차이를 애플리케이션 관점에서 설명할 수 있다.

### 인사이트 기록

I/O가 단순히 느린 연산이 아니라 장치 특성과 운영체제 정책의 영향을 받는 과정임을 보여주는 내용을 정리한다.

---

## 10주차 - 영속성 2: 파일 시스템과 데이터 무결성

### 핵심 학습

- 파일과 디렉터리 추상화
- 파일 시스템의 자료구조와 접근 경로
- 빈 공간 관리와 지역성
- 충돌 일관성과 저널링
- 로그 구조 파일 시스템
- 체크섬과 데이터 무결성

### 학습 목표

- 파일과 디렉터리가 저장 장치의 블록에 매핑되는 방식을 설명할 수 있다.
- 파일을 읽고 쓸 때 파일 시스템 내부에서 일어나는 주요 단계를 설명할 수 있다.
- 비정상 종료가 파일 시스템 일관성을 깨뜨리는 이유와 복구 방식을 설명할 수 있다.
- 저널링, 로그 구조 설계, 체크섬이 각각 해결하려는 문제를 구분할 수 있다.

### 인사이트 기록

영속성 보장이 단순한 쓰기 완료가 아니라 순서, 복구, 무결성의 문제라는 점을 중심으로 새롭게 이해한 내용을 정리한다.

---

# OS 6주 완료 목표

6주 동안 개별 용어를 암기하기보다 운영체제가 제공하는 세 가지 핵심 추상화와 그 비용을 연결해서 설명하는 것을 목표로 한다.

```text
가상화
→ CPU와 메모리를 여러 실행 주체가 안전하게 공유

병행성
→ 여러 실행 흐름이 공유 상태를 올바르게 다루도록 조정

영속성
→ 장치 위에 파일과 파일 시스템을 구성하고 장애 이후에도 데이터를 보존
```

6주 완료 후에는 다음 질문에 자료 없이 답할 수 있어야 한다.

- 운영체제는 CPU와 메모리를 어떻게 가상화하는가?
- 프로세스 스케줄링 정책은 어떤 기준으로 비교할 수 있는가?
- 가상 주소는 어떻게 물리 주소로 변환되는가?
- 병행 실행에서 경쟁 조건은 왜 발생하며 락은 무엇을 보장하는가?
- 조건 변수와 세마포어는 어떤 문제를 해결하는가?
- 교착 상태는 어떤 조건에서 발생하며 어떻게 대응할 수 있는가?
- 운영체제는 저장 장치와 어떻게 통신하는가?
- 파일 시스템은 파일과 디렉터리를 디스크에 어떻게 배치하는가?
- 비정상 종료 이후 파일 시스템의 일관성과 데이터 무결성을 어떻게 지키는가?

# 11~14주차 Database

## 11주차 - Transaction, Isolation Level, MVCC

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
- Undo, Redo, WAL

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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- 세션 두 개를 열고 Isolation Level을 바꿔가며 Dirty Read, Non-Repeatable Read, Phantom Read가 각각 어느 Level에서 재현되는지 확인한다.
- 표준 정의와 실제 DBMS 동작이 다른 지점을 직접 확인한다. REPEATABLE READ에서 Phantom Read가 어떻게 되는지 등.
- 긴 Transaction을 열어둔 채 다른 세션에서 갱신과 조회를 반복하고, 오래된 버전이 정리되지 않는 영향을 관측한다.

---

## 12주차 - Index와 Execution Plan

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
- Optimizer와 CBO
- Full Table Scan
- Index Scan
- Nested Loop과 Hash Join

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

### 딥다이브

직접 테스트 테이블과 데이터를 만들어 실행계획을 비교한다.

```text
Index 없음
→ Single Column Index
→ Composite Index
→ Composite Index 컬럼 순서 변경
```

각 경우의 Execution Plan과 실제 실행 시간을 함께 기록한다. 추가로 다음 중 하나를 확인한다.

- 통계 정보를 갱신하기 전후로 같은 Query의 실행계획이 달라지는지 확인한다.
- Covering Index 적용 전후의 접근 방식과 읽은 행 수를 비교한다.
- 컬럼을 가공하거나 타입이 맞지 않는 조건을 넣어 Index가 사용되지 않는 상황을 재현한다.

---

## 13주차 - Lock, Connection Pool, N+1

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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- 세션 두 개로 Lock Wait를 만들고, 이어서 Deadlock을 의도적으로 재현해 DB가 어느 쪽을 종료시키는지 확인한다.
- Connection Pool 크기를 작게 잡고 부하를 줘 고갈 상황을 재현하고, 대기 시간과 획득 실패가 어떻게 나타나는지 측정한다.
- N+1이 발생하는 코드와 Fetch Join을 적용한 코드의 실행 Query 수와 응답 시간을 비교한다.

---

## 14주차 - Database 종합

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

### 딥다이브

다음 중 하나를 골라 직접 실행하고 관측한다.

- Replication을 구성하고 Primary에 부하를 줘 Lag을 만든 뒤, Replica에서 읽을 때 어떤 불일치가 보이는지 확인한다.
- 데이터가 쌓인 테이블에 스키마 변경을 걸고 그동안 읽기와 쓰기가 어떤 영향을 받는지 측정한다.
- 부하를 올려가며 Connection 수, Slow Query 수, Lock 대기 중 어떤 지표가 먼저 움직이는지 순서를 기록한다.

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

## 3. 추가 기록

Network와 Database는 트러블슈팅 역추론 또는 딥다이브 중 하나를 택해 1개만 진행한다. OS는 트러블슈팅 글 대신 인사이트를 작성한다.

### 트러블슈팅 역추론

실제 사례 1개를 사용한다.

```text
해당 개념을 잘 보여주는 실제 공개 사례
→ 자연스럽게 연결되는 개인 실무 경험
```

개인 경험을 활용하기 위해 억지로 사례를 끼워 넣지 않는다.

```text
1. 문제 상황과 시스템 구성 정리
2. 관측한 증상까지만 확인
3. 증상만 보고 가설 설정
4. 진단 과정 재구성
5. 실제 원인과 해결 확인
6. 당시 몰랐던 개념과 추가로 공부한 개념 정리
7. 지금 다시 대응한다면 어떤 순서로 볼지 정리
```

문서 구조는 [3주차 트러블슈팅 사례](03_Resource/04_network/06_dns_tls_proxy_lb_ts)를 기준으로 한다. 가설은 틀린 것으로 밝혀져도 지우지 않고 그대로 남긴다. 무엇을 몰라서 그 가설을 세웠는지가 `당시 몰랐던 개념`으로 이어진다.

### 딥다이브

개념을 직접 돌려보고 관측한다. 학습 내용을 다시 요약하는 문서가 되지 않도록, 반드시 **실행한 결과와 관측값**이 들어가야 한다.

```text
1. 확인하고 싶은 질문 1개 정의
2. 예상 결과를 먼저 기록
3. 실습 환경과 절차 정의
4. 실행하고 관측값 수집
5. 예상과 실제 결과의 차이 분석
6. 이번 주 학습한 CS 개념으로 다시 설명
```

다음을 지킨다.

- 질문은 예 또는 아니오나 수치로 답할 수 있을 만큼 좁게 잡는다.
- 예상 결과는 반드시 실행 **전에** 적는다. 이게 없으면 관측만 하고 끝난다.
- 환경, 버전, 명령어, 파라미터를 함께 적어 다시 돌릴 수 있게 한다.
- 예상과 결과가 같아도 왜 그런지 설명할 수 없으면 아직 확인된 것이 아니다.
- 여러 조건을 비교할 때는 한 번에 한 가지만 바꾼다.

### OS 인사이트

학습 내용을 다시 요약하기보다 공부 전후에 생각이 달라진 지점을 기록한다. 다음 항목을 모두 채울 필요는 없지만, 주장과 근거가 드러나도록 작성한다.

```text
1. 학습 전에 갖고 있던 생각 또는 질문
2. 새롭게 이해한 핵심 내용
3. 기존 생각이 달라진 이유
4. 다른 OS 개념이나 실제 시스템과의 연결
5. 아직 남은 질문
```

인사이트의 크기는 작아도 된다. 개념 하나를 정확히 구분하게 된 계기, 서로 떨어져 보이던 개념의 연결, 설계상 절충을 발견한 지점처럼 학습 과정에서 실제로 생긴 변화에 집중한다.

## 4. PR

PR은 한 주 동안의 학습 기록을 제출하는 단위다.

```markdown
## 이번 주 학습 내용

## 백지복습

## 추가 기록

## 이전 PR에서 배운 내용
```

필요한 경우 실습 결과나 추가 정리를 포함한다.

OS 기간에도 팀원 PR을 1개 이상 리뷰한다. 같은 영역과 비슷한 범위를 공부한 상태에서 서로 다른 설명, 자료, 인사이트를 비교하고 이해가 어긋난 부분을 확인한다.

---

# 14주 완료 목표

## Network

단순히 특정 요청이 실패했다는 사실만 보는 것이 아니라 다음 계층을 구분해서 생각할 수 있다.

```text
DNS
→ TCP 또는 QUIC
→ TLS
→ HTTP
→ Proxy와 Load Balancer
→ Application
```

## OS

운영체제가 제공하는 핵심 추상화와 이를 구현하기 위한 비용을 세 영역으로 나누어 설명할 수 있다.

```text
가상화
→ CPU와 메모리 공유

병행성
→ 공유 상태와 실행 순서 조정

영속성
→ 파일 시스템과 데이터 무결성
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

14주 동안 개별 개념을 암기하는 것이 아니라 Network, OS, Database의 핵심 원리를 연결해 설명하고, 실제 시스템의 동작과 문제를 구조적으로 바라볼 수 있는 수준을 목표로 한다.

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
