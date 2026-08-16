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

## Authentication과 Authorization

### Authentication

<!-- 신원을 확인하는 과정과 HTTP에서 자격 증명이 전달되는 방식을 기록한다. -->

유저의 신원을 확인하는 과정이다.

<!-- The authentication process relies on credentials, such as passwords or fingerprint scans, that users present to prove they are who they claim to be. The authorization process uses user permissions to define what each user can do within a particular resource or network. For example, permissions in a file system might dictate whether a user can create, read, update or delete files. -->

authentication 프로세스는 패스워드 혹은 핑거프린트 등과 같은 신원 확인이 가능한 credential에 의존한다. 

### Authorization

<!-- 확인된 신원에 대해 권한을 판단하는 과정을 기록한다. 401과 403의 차이도 함께 정리한다. -->

유저 또는 entity가 특정 resource에 대해 어떤 행위를 수행할 수 있는지를 결정하는 과정이다.

Authentication에서 확인된 identity에 기반해 접근 권한을 판단한다.

RBAC(Role-based Access Control), MAC(Mandatory Access Control), DAC(Direct Access Control) 등이 있다.

## Same-Origin Policy

### Origin의 정의

<!-- scheme, host, port로 구성된 origin의 정의와 같은 origin으로 판단되는 조건을 기록한다. -->

두 url의 host, scheme, port가 동일한 경우 same origin이라 할 수 있다. 이를 튜플이라 칭할 수 있다. 아래는 `http://store.company.com/dir/page.html` URL과의 origin 비교 예시이다.


| URL                                                                                                | Outcome     | Reason                  |
| -------------------------------------------------------------------------------------------------- | ----------- | ----------------------- |
| [http://store.company.com/dir2/other.html](http://store.company.com/dir2/other.html)               | Same origin | path 만 다름               |
| [http://store.company.com/dir/inner/another.html](http://store.company.com/dir/inner/another.html) | Same origin | path 만 다름               |
| [https://store.company.com/page.html](https://store.company.com/page.html)                         | Failure     | protocol 차이             |
| [http://store.company.com:81/dir/page.html](http://store.company.com:81/dir/page.html)             | Failure     | port (http는 80을 디폴트로 씀) |
| [http://news.company.com/dir/page.html](http://news.company.com/dir/page.html)                     | Failure     | host 차이                 |


### Same-Origin Policy가 필요한 이유

<!-- 브라우저가 다른 origin의 리소스 접근을 제한하는 이유를 공격 시나리오와 함께 정리한다. -->

<!-- It helps isolate potentially malicious documents, reducing possible attack vectors. For example, it prevents a malicious website on the Internet from running JS in a browser to read data from a third-party webmail service (which the user is signed into) or a company intranet (which is protected from direct access by the attacker by not having a public IP address) and relaying that data to the attacker. -->

Same-Origin Policy는 한 origin에서 실행된 script가 다른 origin의 resource를 임의로 읽는 것을 제한하는 브라우저의 보안 메커니즘이다.

가령, 클라이언트 브라우저에서 악의적인 JS 스크립트를 실행해 서드파티 웹메일 혹은 회사 인트라넷에서 데이터를 읽어 공격자에게 전송하는 행위를 방지할 수 있다.

## CORS

### CORS의 역할

<!-- Same-Origin Policy를 완화하기 위해 server가 어떤 header로 접근을 허용하는지 기록한다. -->

http 기반 헤더를 사용한 메커니즘으로, 어떤 origin의 브라우저 script에게 response를 공유할지를 HTTP header로 나타내는 메커니즘이다. 

Preflight 요청을 보내 cross-origin source에서 실제로 요청이 가능한지 확인하는 과정을 거치며, 이때 실제 요청의 메서드와 헤더 값을 지시하는 요청을 먼저 보낸다.

### 주요 Header


| Header                             | 방향       | 역할                             |
| ---------------------------------- | -------- | ------------------------------ |
| `Origin`                           | Request  | CORS의 요청 origin값을 명시, null 값이 올 수 있음 |
| `Access-Control-Allow-Origin`      | Response | resource에 접근 가능한 origin을 명시    |
| `Access-Control-Allow-Methods`     | Response | resource에 접근 가능한 메서드 명시        |
| `Access-Control-Allow-Headers`     | Response | 실제 요청 시 사용 가능한 http header     |
| `Access-Control-Allow-Credentials` | Response | credentials가 포함된 요청의 response 공유 허용 여부 |
| `Access-Control-Max-Age`           | Response | Preflight 요청의 캐시 가능 시간         |


### CORS Preflight

<!-- Simple Request와 Preflight가 필요한 요청의 조건을 구분하고, OPTIONS 요청이 오가는 순서를 정리한다. -->

```text
브라우저가 요청 조건 확인
→ Preflight 필요 여부 판단
→ OPTIONS 요청 전송
→ 서버의 허용 응답 확인
→ 실제 요청 전송
```

cross-origin 요청 중 CORS-safelisted request 조건을 만족하지 않는 경우, 브라우저는 실제 요청 전에 Preflight 요청을 수행한다.

대표적으로 다음과 같은 요청은 Preflight가 발생한다.

- PUT, PATCH, DELETE 등의 method 사용
- Authorization 등의 safelisted되지 않은 header 사용
- POST 요청에서 Content-Type으로 application/json 사용

브라우저는 OPTIONS 요청에 `Access-Control-Request-Method`, `Access-Control-Request-Headers`를 포함해 실제 요청 조건을 전달한다.

- Simple Request: Preflight를 필요로 하지 않는 요청
- Preflight request: CORS 요청이 가능한지 확인하는 요청

Preflight request는 OPTIONS 메서드로 요청되며 CORS 요청 헤더들을 포함한다. 브라우저에서 자동적으로 수행하므로 어플리케이션 코드 상에서 직접 구현할 필요는 없다.

### CORS 오류 진단 순서

<!-- 브라우저 콘솔 메시지, 실제 요청 도달 여부, 응답 header를 어떤 순서로 확인할지 기록한다. 서버 오류와 CORS 차단을 구분하는 기준도 함께 정리한다. -->

1. Browser DevTools Network에서 Preflight(OPTIONS)가 발생했는지 확인
2. OPTIONS 요청이 실패했다면 response의 
  `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods` `Access-Control-Allow-Headers` 확인
3. Credential을 사용하는 경우
   `Access-Control-Allow-Credentials` 및 `Access-Control-Allow-Origin` 설정 확인
4. Preflight 성공 후 실제 요청이 전송되었는지 확인
5. 실제 요청이 4xx/5xx라면 CORS가 아닌 서버 오류 가능성도 확인
6. 서버 로그와 브라우저 Network 응답을 함께 확인

## XSS와 CSRF

### XSS

<!-- 공격이 성립하는 조건과 기본 방어 방법을 기록한다. -->

cross-site scripting은 공격자가 주입한 악성 script가 신뢰되는 웹사이트의 context에서 다른 사용자의 브라우저에 의해 실행되는 공격이다.

![](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS/xss.svg)

사용자 입력 등의 신뢰할 수 없는 데이터가 적절한 output encoding이나 sanitization 없이 실행 가능한 HTML/JavaScript context에 삽입되는 경우 발생할 수 있다.

아래와 같은 방식으로 방어할 수 있다. 단, CSP는 추가적인 방어 계층으로 사용해야 한다.

- context에 맞는 output encoding
- 필요한 경우 HTML sanitization
- 안전한 DOM API 사용

### CSRF

<!-- 공격이 성립하는 조건, SameSite Cookie와 CSRF Token의 역할을 기록한다. -->

![](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF/form-post.svg)

cross-site request forgery (CSRF) attack은 악성 사이트가 피해자의 브라우저를 이용해 target site로 원하지 않는 요청을 보내게 한다.

위 예시에서, 유저의 로그인 세션 쿠키를 클라이언트(브라우저)가 가지고 있다. 페이지는 `<form>` element를 가지며 유저가 다른 사람에게 전송이 가능하도록 한다. 유저가 submit 버튼을 누르면 브라우저가 서버에 쿠키를 포함하는 POST 요청을 보내게 된다.  

![](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF/csrf-form-post.svg)

위 그림과 같이 CSRF 공격이 일어나는 경우, 공격자가 form을 포함한 웹사이트를 만들고 form 내 `action` attribute가 bank website로 설정되며 form은 bank의 input field를 흉내내게 한다. 


## REST

<!-- Resource, Method, 표현, Stateless 등 REST가 전제하는 제약을 HTTP와 연결해 정리한다. -->

RES (Representational State Transfer)는 분산 hypermedia system을 위한 architectural style로, 시스템의 component 간 상호작용에 여러 제약 조건을 적용한다.

주요 constraint는 다음과 같다.

- Client-Server
- Stateless
- Cache
- Uniform Interface
- Layered System
- Code-On-Demand (optional)

## WebSocket

<!-- HTTP Upgrade로 연결이 전환되는 과정과 요청 및 응답 모델과의 차이를 기록한다. -->

WebSocket은 클라이언트와 서버가 양방향으로 전송이 가능한 연결을 생성하는 프로토콜이다. 이를 통해 서버와 클라이언트가 독립적으로 메시지를 보내고, 이에 대한 응답을 polling할 필요 없이 받아볼 수 있다.

채팅, 실시간 알림, 게임 등 실시간 양방향 통신이 필요한 경우 사용할 수 있다.

- `WebSocket` interface : 브라우저에서 널리 사용되는 WebSocket API, application-level backpressure를 지원하지 않음
- `WebSocketStream` interface : `WebSocket`을 대체하기 위한 `Promise` 기반 대체재. Streams API를 사용해 backpressure를 지원한다. 현재 표준 X

## CDN

<!-- Edge 캐싱이 요청 흐름의 어느 지점에 위치하는지, Cache Hit과 Miss가 응답 경로에 어떤 차이를 만드는지 기록한다. -->

CDN (Content Delivery Network) 여러 지역에 분산된 edge server를 이용해 사용자에게 콘텐츠를 전달하는 시스템이다.

사용자의 요청은 일반적으로 낮은 latency로 콘텐츠를 제공할 수 있는 edge server로 전달된다.

요청한 콘텐츠가 edge server에 cache되어 있는 경우 바로 응답하고, cache되어 있지 않거나 만료된 경우 origin server로부터 콘텐츠를 가져온 뒤 사용자에게 전달하며 필요에 따라 이를 cache한다.

이를 통해 사용자와 콘텐츠를 제공하는 서버 사이의 네트워크 거리를 줄여 latency를 줄일 수 있고, origin server로 직접 전달되는 요청도 감소시킬 수 있다.


## 참고 자료

<!-- RFC와 공식 문서를 우선 기록한다. -->

- [RFC 9110 - HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html)
- [RFC 6455 - The WebSocket Protocol](https://www.rfc-editor.org/rfc/rfc6455.html)
- [Fetch Standard - CORS protocol](https://fetch.spec.whatwg.org/#http-cors-protocol)
- [MDN - Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [MDN - Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [OWASP - Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [OWASP - Cross-Site Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)
- [CDN](https://developer.mozilla.org/en-US/docs/Glossary/CDN)

## 함께 읽기

- [1주차 - TCP/IP와 연결](03_Resource/04_network/01_tcp)
- [2주차 - HTTP와 요청 및 응답](03_Resource/04_network/03_http)
- [3주차 - DNS, HTTPS, Proxy, Load Balancer](03_Resource/04_network/05_dns_https_proxy_lb)
- [Network 종합 트러블슈팅 사례](03_Resource/04_network/08_network_summary_ts)

