---
title: DNS, TLS, Proxy, Load Balancer 트러블슈팅 사례
draft: true
tags:
  - network
  - dns
  - tls
  - proxy
  - load-balancer
  - troubleshooting
---

# DNS, TLS, Proxy, Load Balancer 트러블슈팅 사례

## 사례 선정 기준

- DNS 장애, TLS 인증서 장애, Load Balancer와 Backend 간 연결 장애, Reverse Proxy 설정 문제 중 하나와 관련된 공개 사례를 선택한다.
- 장애를 겪은 조직이 직접 공개한 기술 블로그, 발표 자료, 사후 분석 문서를 우선 사용한다.
- 처음 관찰된 증상과 실제 원인을 구분할 수 있고, 조사 과정이나 근거가 공개된 사례를 선택한다.

## 사례 출처와 배경

<!-- 조직, 시스템의 역할, 장애 발생 시점, 원문 링크를 기록한다. 이 단계에서는 실제 원인을 밝히지 않는다. -->

## 처음 관찰된 증상

<!-- 사용자 영향, 오류 메시지, 최초 로그와 메트릭만 기록한다. 실제 원인과 해결 방법은 아직 적지 않는다. -->

> 여기까지만 읽고 가능한 원인과 확인 방법을 먼저 추론해 본다.

## 1. 문제 상황 파악

<!-- 영향 범위, 발생 조건, 시작 시점, 지속 시간, 최근 배포·인프라·인증서·DNS 변경 사항을 정리한다. -->

| 확인 항목             | 관찰 결과 |
| --------------------- | --------- |
| 사용자 영향           |           |
| 영향 범위             |           |
| 시작 시점과 지속 시간 |           |
| 재현 조건             |           |
| 최근 변경 사항        |           |

## 2. 계층별 원인 가설 설정

```text
DNS
→ Network Connection
→ TLS
→ Load Balancer
→ Reverse Proxy
→ Backend
```

| 우선순위 | 계층 | 가설 | 가설의 근거 | 예상되는 관찰 결과 |
| -------- | ---- | ---- | ----------- | ------------------ |
| 1        |      |      |             |                    |
| 2        |      |      |             |                    |
| 3        |      |      |             |                    |

<!-- 사용자에게 보이는 증상과 최근 변경 사항을 기준으로 가설의 우선순위를 정한다. -->

## 3. 확인할 로그, 메트릭, 명령어 정의

### DNS

<!-- 조회 결과, 응답 코드, authoritative server, TTL, resolver별 차이를 확인한다. -->

```bash
dig example.com
dig +trace example.com
```

### Network Connection

<!-- 이름 조회 후 얻은 IP와 목적지 Port에 TCP 연결이 가능한지, timeout과 connection refused를 구분한다. -->

```bash
nc -vz example.com 443
```

### TLS

<!-- 인증서의 hostname·유효 기간·chain, SNI, protocol 협상 결과를 확인한다. -->

```bash
openssl s_client -connect example.com:443 -servername example.com
curl -v https://example.com
```

### Load Balancer

<!-- Frontend 연결 오류, Backend health, healthy host 수, target response time, reset·timeout 지표를 확인한다. -->

### Reverse Proxy

<!-- access/error log, routing 규칙, upstream 주소, timeout, 전달 Header와 TLS 설정을 확인한다. -->

### Backend

<!-- 애플리케이션 로그, 응답 시간, 오류율, resource 사용량, connection pool 상태를 확인한다. -->

| 계층               | 로그·메트릭·명령어 | 판단 기준 | 관찰 결과 |
| ------------------ | ------------------ | --------- | --------- |
| DNS                |                    |           |           |
| Network Connection |                    |           |           |
| TLS                |                    |           |           |
| Load Balancer      |                    |           |           |
| Reverse Proxy      |                    |           |           |
| Backend            |                    |           |           |

<!-- 운영 환경에서 명령을 실행할 때 필요한 권한과 부하, 민감 정보 노출 가능성을 확인한다. -->

## 4. 조사 과정

<!-- 실제 사례의 조사 순서를 시간순으로 재구성한다. 각 단계에서 무엇을 관찰했고 어떤 가설을 배제하거나 강화했는지 기록한다. -->

| 순서 | 확인한 내용 | 관찰 결과 | 가설에 미친 영향 | 다음 행동 |
| ---- | ----------- | --------- | ---------------- | --------- |
| 1    |             |           |                  |           |
| 2    |             |           |                  |           |
| 3    |             |           |                  |           |

## 5. 실제 원인 확인

<!-- 공개 사례가 밝힌 직접 원인과 근본 원인을 구분하고, 이를 뒷받침한 증거를 기록한다. -->

### 직접 원인

### 근본 원인

### 원인을 뒷받침한 증거

## 6. 가설과 실제 원인 비교

| 가설 | 판정 | 실제 조사 결과와의 차이 | 놓친 단서 |
| ---- | ---- | ----------------------- | --------- |
|      |      |                         |           |

## 해결 방법과 재발 방지

### 즉시 조치

<!-- 서비스 복구를 위해 수행한 조치와 선택 이유를 기록한다. -->

### 장기 개선

<!-- 구성 검증, 자동 갱신, health check, monitoring, alert, runbook 등 재발 방지책을 기록한다. -->

| 개선 항목 | 방지하거나 줄이는 위험 | 검증 방법 |
| --------- | ---------------------- | --------- |
|           |                        |           |

## 개인 경험과의 연결

<!-- Kubernetes 장애 대응 경험 등이 사례의 요청 흐름을 이해하는 데 실제로 도움이 될 때만 작성하고, 없다면 이 절을 삭제한다. -->

## 배운 점

<!-- 같은 증상이 발생했을 때 재사용할 수 있는 계층별 판단 기준과 조사 순서를 정리한다. -->

## 참고 자료

<!-- 공개 사례 원문과 관련 RFC 또는 공식 문서를 기록한다. -->

## 함께 읽기

- [[03_Resource/04_network/05_dns_https_proxy_lb|3주차 - DNS, HTTPS, Proxy, Load Balancer]]
