---
title: Network 종합
draft: true
tags:
  - network
  - cors
  - rest
  - websocket
  - cdn
---
# Network 종합

## 학습 목표

- Authentication과 Authorization의 차이를 설명할 수 있다.
- Same-Origin Policy와 CORS의 관계를 설명할 수 있다.
- 브라우저가 CORS Preflight 요청을 보내는 조건과 목적을 설명할 수 있다.
- XSS와 CSRF의 차이와 기본 방어 방법을 설명할 수 있다.
- REST, WebSocket, CDN의 역할을 요청 흐름과 연결해 설명할 수 있다.

## 전체 요청 흐름

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

<!-- 새로운 개념을 추가하기보다 1~3주차 내용을 하나의 흐름으로 연결한다. 각 단계에서 무엇이 결정되고 무엇이 실패할 수 있는지 정리한다. -->

### 단계별 정리


| 단계                   | 하는 일 | 관여하는 구성 요소 | 실패했을 때의 증상 |
| -------------------- | ---- | ---------- | ---------- |
| DNS 조회               |      |            |            |
| TCP 또는 QUIC 연결       |      |            |            |
| TLS                  |      |            |            |
| HTTP 요청              |      |            |            |
| Proxy와 Load Balancer |      |            |            |
| 서버 처리                |      |            |            |
| HTTP 응답              |      |            |            |


## Authentication과 Authorization

### Authentication

<!-- 신원을 확인하는 과정과 HTTP에서 자격 증명이 전달되는 방식을 기록한다. -->

### Authorization

<!-- 확인된 신원에 대해 권한을 판단하는 과정을 기록한다. 401과 403의 차이도 함께 정리한다. -->

## Same-Origin Policy

### Origin의 정의

<!-- scheme, host, port로 구성된 origin의 정의와 같은 origin으로 판단되는 조건을 기록한다. -->

두 url이 host, protocol, port가 동일한 경우 same origin이라 할 수 있다. 이를 튜플이라 칭할 수 있다. 아래는 `http://store.company.com/dir/page.html` URL과의 origin 비교 예시이다.

| URL |	Outcome |	Reason |
|-----|---------|--------|
| http://store.company.com/dir2/other.html	| Same origin	| path 만 다름 |
| http://store.company.com/dir/inner/another.html	| Same origin	| path 만 다름 |
| https://store.company.com/page.html	| Failure	| protocol 차이 |
| http://store.company.com:81/dir/page.html	| Failure	| port (http는 80을 디폴트로 씀) |
| http://news.company.com/dir/page.html	| Failure	| host 차이 |

### Same-Origin Policy가 필요한 이유

<!-- 브라우저가 다른 origin의 리소스 접근을 제한하는 이유를 공격 시나리오와 함께 정리한다. -->

## CORS

### CORS의 역할

<!-- Same-Origin Policy를 완화하기 위해 server가 어떤 header로 접근을 허용하는지 기록한다. -->

### 주요 Header


| Header                             | 방향       | 역할  |
| ---------------------------------- | -------- | --- |
| `Origin`                           | Request  |     |
| `Access-Control-Allow-Origin`      | Response |     |
| `Access-Control-Allow-Methods`     | Response |     |
| `Access-Control-Allow-Headers`     | Response |     |
| `Access-Control-Allow-Credentials` | Response |     |
| `Access-Control-Max-Age`           | Response |     |


### CORS Preflight

<!-- Simple Request와 Preflight가 필요한 요청의 조건을 구분하고, OPTIONS 요청이 오가는 순서를 정리한다. -->

```text
브라우저가 요청 조건 확인
→ Preflight 필요 여부 판단
→ OPTIONS 요청 전송
→ 서버의 허용 응답 확인
→ 실제 요청 전송
```

### CORS 오류를 진단하는 순서

<!-- 브라우저 콘솔 메시지, 실제 요청 도달 여부, 응답 header를 어떤 순서로 확인할지 기록한다. 서버 오류와 CORS 차단을 구분하는 기준도 함께 정리한다. -->

## XSS와 CSRF

### XSS

<!-- 공격이 성립하는 조건과 기본 방어 방법을 기록한다. -->

### CSRF

<!-- 공격이 성립하는 조건, SameSite Cookie와 CSRF Token의 역할을 기록한다. -->

### 두 공격의 차이


| 구분         | XSS | CSRF |
| ---------- | --- | ---- |
| 공격 대상      |     |      |
| 악용하는 신뢰 관계 |     |      |
| 기본 방어      |     |      |


## REST

<!-- Resource, Method, 표현, Stateless 등 REST가 전제하는 제약을 HTTP와 연결해 정리한다. -->

## WebSocket

<!-- HTTP Upgrade로 연결이 전환되는 과정과 요청 및 응답 모델과의 차이를 기록한다. -->

## CDN

<!-- Edge 캐싱이 요청 흐름의 어느 지점에 위치하는지, Cache Hit과 Miss가 응답 경로에 어떤 차이를 만드는지 기록한다. -->

## 백지복습 질문

<!-- 자료를 보지 않고 답해 본 뒤 막힌 부분만 보완한다. -->

- 브라우저에서 URL을 입력한 뒤 응답을 받기까지의 과정을 설명할 수 있는가?
- 요청이 실패했을 때 DNS, 연결, TLS, HTTP, Proxy 중 어느 계층의 문제인지 구분할 수 있는가?
- CORS 오류와 서버 오류를 어떻게 구분하는가?

## 참고 자료

<!-- RFC와 공식 문서를 우선 기록한다. -->

- [RFC 9110 - HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html)
- [RFC 6455 - The WebSocket Protocol](https://www.rfc-editor.org/rfc/rfc6455.html)
- [Fetch Standard - CORS protocol](https://fetch.spec.whatwg.org/#http-cors-protocol)
- [MDN - Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [MDN - Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [OWASP - Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [OWASP - Cross-Site Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)

## 함께 읽기

- [1주차 - TCP/IP와 연결](03_Resource/04_network/01_tcp)
- [2주차 - HTTP와 요청 및 응답](03_Resource/04_network/03_http)
- [3주차 - DNS, HTTPS, Proxy, Load Balancer](03_Resource/04_network/05_dns_https_proxy_lb)
- [Network 종합 트러블슈팅 사례](03_Resource/04_network/08_network_summary_ts)

