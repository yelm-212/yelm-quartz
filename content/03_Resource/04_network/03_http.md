---
title: HTTP와 요청&응답
draft: false
tags:
  - network
  - http
---

# HTTP와 요청&응답

## 학습 목표

- HTTP 요청과 응답 구조를 설명할 수 있다.
- HTTP Method의 멱등성과 재시도의 관계를 설명할 수 있다.
- HTTP/1.1, HTTP/2, HTTP/3의 주요 차이를 설명할 수 있다.
- Keep-Alive가 연결과 성능에 어떤 영향을 주는지 설명할 수 있다.
- Stateless한 HTTP에서 로그인 상태를 유지할 수 있는 이유를 설명할 수 있다.
- 실패한 HTTP 요청을 재시도할 때 고려해야 할 점을 설명할 수 있다.

## HTTP: Hypertext Transfer Protocol

- HTTP는 네트워크상의 리소스 표현을 요청하고 응답받기 위한 application-level request/response 프로토콜이다.
- stateless
  - 각 요청은 원칙적으로 다른 요청이나 연결의 상태에 의존하지 않고 독립적으로 해석할 수 있으나, 이것이 서버가 애플리케이션 상태를 저장할 수 없다는 의미는 아니다.
  - Cookie, Session, Token 등을 사용해 여러 요청에 걸친 사용자 상태를 유지할 수 있다.

## HTTP Request / Response 구조

<!-- HTTP/1.1 기준 status line의 HTTP version, status code, reason phrase를 설명하고,
HTTP/2 이상에서는 표현 방식이 달라짐을 설명한다. -->

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/http-message-anatomy.svg)

1. start-line은 http 버전과 요청 메서드 혹은 응답 코드를 명시
2. HTTP header field에는 메시지 처리 조건, 대상 리소스, 표현 형식 등의 메타데이터가 포함된다.
   메시지 구조상 header field가 없을 수도 있지만, HTTP 버전과 메시지 종류에 따라
   `Host`처럼 반드시 포함해야 하는 field가 존재한다.
3. 헤더 이후 빈 line은 헤더 종료를 의미
4. message body(필수 X)는 메시지의 데이터를 포함한다. 
    이는 서버에 post하려는 데이터일수도 있고, client에게 전달될 리소스일수도 있다. 
    body를 포함할지 아닌지는 start line과 http header에서 결정된다.

위 구조는 HTTP/1.1 메시지의 textual wire format을 기준으로 한다.
HTTP/2와 HTTP/3는 같은 HTTP semantics를 binary frame과 pseudo-header로 표현한다.

### Request

<!-- request line의 method, request target, HTTP version과 주요 request header를 실제 예시로 설명한다. -->

```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 49

name=FirstName+LastName&email=bsmth%40example.com
```

#### start line

- start line은 위와 같이 `<method> <request-target> <HTTP-version>`의 세 파트 형태로 구성된다.
  - `<method>`: request의 의미와 요청으로 원하는 결과를 명시함
  - `request-target`은 상황에 따라 다음 형태를 사용한다.
    - origin-form: `/users/123`
    - absolute-form: `https://example.com/users/123`
    - authority-form: `example.com:443`
      - `CONNECT`에서 사용한다.
    - asterisk-form: `*`
      - `OPTIONS *`처럼 특정 리소스가 아닌 서버 전체의 통신 옵션을 조회할 때 사용한다.
  - HTTP/2와 HTTP/3에는 HTTP/1.1의 textual request line이 없다.
  - method, scheme, authority, path는 `:method`, `:scheme`, `:authority`, `:path`
    pseudo-header로 표현한다.
  - 사용하는 HTTP 버전은 연결을 수립하거나 프로토콜을 협상하는 과정에서 결정된다.

#### request header

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/request-headers.svg)

- 요청 헤더는 요청에 필요한 추가 정보 혹은 이 요청이 서버에서 다뤄져야하는 방식을 명시한다.
- Representation headers는 body가 있는 경우 메시지 데이터의 형식과 인코딩을 명시한다.

#### request content

- 서버가 처리할 데이터를 전달한다.
- POST, PUT, PATCH는 일반적으로 request content를 사용한다.
- GET, HEAD, DELETE의 request content에는 일반적으로 정의된 의미가 없으므로
  특별한 사전 합의가 없다면 전송하지 않는 것이 권장된다.
- OPTIONS는 content를 포함할 수 있지만 표준에서 그 용도를 정의하지 않는다.
- TRACE와 CONNECT request에는 content를 포함할 수 없다.

### Response

<!-- status line의 HTTP version, status code, reason phrase와 주요 response header를 실제 예시로 설명한다. -->

서버로부터 응답받은 메시지를 의미한다.

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: http://example.com/users/123

{
  "message": "New user created",
  "user": {
    "id": 123,
    "firstName": "Example",
    "lastName": "Person",
    "email": "bsmth@example.com"
  }
}
```

#### start line

- start line은 위와 같이 `<HTTP-version> <status-code> <reason-phrase>`의 세 파트 형태로 구성된다.
  - `<HTTP-version>`: HTTP 버전을 명시한다.
  - `<status-code>`: 클라이언트 요청의 성공/실패 여부를 표시한다.
  - `<reason-phrase>`: 상태 코드에 대한 선택적 텍스트 설명이다.

#### response header

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/response-headers.svg)

- Response header : 클라이언트가 추가 요청을 위해 필요한 정보들을 제공한다.
- Representation header : message부분의 데이터 형태 및 인코딩 형태 등 형태 정보를 제공한다.

#### response body

응답 content의 의미는 request method와 status code에 따라 달라진다.
성공 응답은 resource representation이나 처리 결과를 포함할 수 있고,
오류 응답은 오류를 설명하는 representation을 포함할 수 있다.

- `201 Created`는 응답 content를 포함할 수도 있고 포함하지 않을 수도 있다.
- `204 No Content` 응답은 content를 포함할 수 없다.

## HTTP Method

<!-- 각 Method의 의미와 안전성(safe), 멱등성(idempotent), 캐시 가능 여부를 비교한다. -->

| Method  | 주요 의미                                        | 안전성 | 멱등성 | 요청 Content | 응답 캐시 |
| ------- | -------------------------------------------- | --: | --: | ---------: | ----: |
| GET     | target resource의 representation 조회           |   O |   O |          △ |     O |
| HEAD    | GET과 동일한 header 조회, response content 제외      |   O |   O |          △ |     O |
| OPTIONS | resource 또는 server의 통신 옵션 조회                 |   O |   O |          △ |     X |
| TRACE   | request message의 application-level loop-back |   O |   O |          X |     X |
| PUT     | target resource를 request content로 생성 또는 대체   |   X |   O |          O |     X |
| DELETE  | target URI와 현재 기능 간 연결 제거 요청                 |   X |   O |          △ |     X |
| POST    | target resource 고유 semantics에 따라 content 처리  |   X |   X |          O |   조건부 |
| PATCH   | patch document를 적용해 resource 일부 수정           |   X |   X |          O |   조건부 |
| CONNECT | 대상 서버로 tunnel 생성                             |   X |   X |          X |     X |

- △: 프로토콜상 message framing은 가능하지만 일반적으로 정의된 의미가 없거나,
  특별한 지원이 없으면 전송하지 않는 것이 권장
- POST와 PATCH 응답은 명시적인 freshness 정보와 target URI를 가리키는
  `Content-Location`이 있는 경우에 한해 캐시할 수 있다.
- 캐시된 POST/PATCH 응답은 이후 동일한 POST/PATCH를 대신하기 위한 것이 아니라,
  조건을 만족하는 GET 또는 HEAD 요청에 재사용된다.

## HTTP Status Code

<!-- 상태 코드 클래스별 의미를 설명하고 자주 접하는 상태 코드를 요청 성공, 클라이언트 오류, 서버 오류 관점에서 정리한다. -->

| 범위 | 의미 | 대표 상태 코드 | 처리 시 고려할 점 |
| ---- | ---- | -------------- | ----------------- |
| 1xx  | Informational responses | `100 Continue`, `101 Switching Protocols` | * 요청 처리 진행 상황 등을 전달하는 중간 응답 <br> * 일반적으로 이후 final response가 이어지며, `101`은 응답 이후 합의된 protocol로 전환 |
| 2xx  | Successful responses | `200 OK`, `201 Created` | 성공 의미와 response content 유무는 개별 status code와 method에 따라 다르다.                      |
| 3xx  | Redirection messages | `301 Moved Permanently` | `Location`, 캐시 정책, method 변경 여부를 확인한다.       |
| 4xx  | Client error responses | `400 Bad Request`, `401 Unauthorized`, `403 Forbidden` ... | 일반적으로 request를 수정하지 않은 단순 재시도는 의미가 없다. 단, 408·409·429처럼 상황에 따라 재시도할 수 있는 코드도 있다. |
| 5xx  | Server error responses | `500 Internal Server Error`              | 일시적 장애인지 판단하고, 멱등성·재시도 횟수·backoff를 고려한다. 모든 5xx를 무조건 재시도하면 안 된다.                 |


## HTTP 멱등성

<!-- 같은 요청을 여러 번 수행해도 서버의 의도된 상태가 한 번 수행했을 때와 같은 성질을 설명한다. -->

동일한 요청을 한 번 수행했을 때와 여러 번 수행했을 때,
서버에 대한 의도된 효과가 같다면 해당 요청은 멱등하다.

멱등성은 다음을 보장하지 않는다.

- 매번 동일한 status code를 반환하는 것
- 매번 동일한 response content를 반환하는 것
- 로그 기록 등 부수적인 내부 동작이 한 번만 발생하는 것


```http
POST /add_row HTTP/1.1
POST /add_row HTTP/1.1   -> Adds a 2nd row
POST /add_row HTTP/1.1   -> Adds a 3rd row

// POST는 멱등하지 않기 때문에 여러번 호출하면 여러개의 row를 추가한다.
```

```http
DELETE /idX/delete HTTP/1.1   -> Returns 200 if idX exists
DELETE /idX/delete HTTP/1.1   -> Returns 404 as it just got deleted
DELETE /idX/delete HTTP/1.1   -> Returns 404

// 첫 번째 요청과 이후 요청의 status code는 다를 수 있지만
// 여러 번 수행한 뒤에도 `/users/idX`가 존재하지 않는다는 의도된 서버 상태는 동일하다.
```

### 멱등성과 재시도

<!-- TODO: timeout으로 응답을 받지 못했지만 서버에서는 요청을 처리했을 가능성을 포함하여, Method별 재시도 위험을 설명한다. -->

### Idempotency Key

<!-- 결제나 주문처럼 중복 처리가 위험한 요청에서 idempotency key를 사용하는 목적과 서버의 처리 방식을 설명한다. -->

POST와 PATCH는 Method 자체의 semantics만으로 멱등성이 보장되지 않는다. 결제/주문처럼 중복 처리가 위험한 요청인 경우 `Idempotency-Key` 헤더를 사용해서 중복 처리를 방지할 수 있다. 표준은 아니다.

- Client 에서는 요청시 헤더에 이 키값을 붙여서 보낸다.
  - 새로운 논리적 작업마다 고유한 key를 생성한다.
  - 같은 작업을 재시도할 때는 최초 요청과 동일한 key를 사용한다.
- server는 key와 함께 요청의 fingerprint, 처리 상태, 처리 결과를 저장한다.
  - 같은 key와 같은 요청이 다시 오면 기존 처리 결과를 반환한다.
  - 같은 key를 다른 요청 content에 재사용하면 오류로 처리해야 한다.
  - 동시에 같은 key의 요청이 들어오는 경우 중복 실행되지 않도록 원자적으로 처리해야 한다.
  - 저장 기간과 만료 정책은 API가 정의해야 한다.

`Idempotency-Key`를 사용한다고 해서 POST나 PATCH Method 자체가 멱등해지는 것은 아니며,
해당 API가 정의한 범위에서 같은 논리적 작업의 중복 실행을 방지하는 것이다.

## HTTP 버전별 특징

### HTTP/1.1

<!-- 지속 연결, 요청 순서, 파이프라이닝과 head-of-line blocking을 설명한다. -->

- HTTP/1.1은 persistent connection을 기본으로 사용하며 하나의 TCP connection을 여러 request와 response에 재사용할 수 있다.
- HTTP/1.1은 request pipelining을 허용한다.
  - client는 앞선 response를 받기 전에 다음 request를 전송할 수 있다.
  - server는 request를 받은 순서대로 response를 전송해야 한다.
  - 앞선 response가 지연되면 뒤의 response도 전송되지 못하는
    application-level head-of-line blocking이 발생한다.
- `chunked` transfer coding을 사용해 content 길이를 미리 알지 못해도 분할 전송할 수 있다.
- 동일 IP 주소 내에서 다른 호스트 도메인을 사용할 수 있다. (`Host` 헤더)

### HTTP/2

<!-- binary framing, stream multiplexing, header compression과 TCP 수준 head-of-line blocking을 설명한다. -->

- HTTP semantics를 binary frame으로 표현한다.
- 각 request/response exchange를 독립된 stream에 할당한다.
- 하나의 TCP connection에서 여러 stream의 frame을 교차 전송하는 multiplexing을 지원한다.
- HPACK을 사용해 반복되는 HTTP field를 압축한다.
- HTTP 수준의 response ordering 문제는 완화하지만,
  TCP packet loss가 발생하면 해당 TCP connection의 모든 stream이 영향을 받는
  transport-level head-of-line blocking은 남아 있다.

### HTTP/3

<!-- QUIC과 UDP의 관계, stream 단위 전송, 연결 수립 지연 관점에서 HTTP/2와 비교한다. -->

- Transport 레이어에서 tcp대신 quic 사용.
- http/2가 multiplex 지원하긴하는데 tcp라 스트림 블로킹할수 있어서 QUIC씀
- QUIC은 UDP datagram 위에서 동작하며 신뢰성, stream, flow control,
  congestion control, loss recovery, TLS 기반 보안을 제공한다.
- 하나의 QUIC connection에서 여러 독립적인 stream을 사용한다.
- 특정 stream의 data가 유실되더라도 다른 stream의 전송은 계속 진행할 수 있다.


| 구분           | HTTP/1.1                              | HTTP/2                               | HTTP/3                                    |
| ------------ | ------------------------------------- | ------------------------------------ | ----------------------------------------- |
| 기반 전송        | TCP                                   | TCP                                  | QUIC over UDP                             |
| 메시지 표현       | Textual message                       | Binary frame                         | Binary frame                              |
| 동시 요청 처리     | 여러 connection 또는 pipelining           | 하나의 connection에서 stream multiplexing | 하나의 connection에서 QUIC stream multiplexing |
| Field 압축     | 기본 제공 없음                              | HPACK                                | QPACK                                     |
| HOL blocking | response 순서에 따른 application-level HOL | HTTP stream 수준은 완화되지만 TCP HOL 존재     | 다른 stream 사이의 transport HOL 완화            |
| 연결 수립        | TCP, HTTPS는 별도 TLS handshake          | TCP, HTTPS는 TLS/ALPN 사용              | QUIC transport와 TLS handshake 결합          |
| 연결 재개        | TCP/TLS 정책에 따름                        | TCP/TLS 정책에 따름                       | 조건에 따라 0-RTT 가능                           |

## Keep-Alive

<!-- TODO: 요청마다 새 TCP 연결을 생성하는 방식과 연결을 재사용하는 방식을 비교하고, latency와 서버 자원에 미치는 영향을 설명한다. -->

### Timeout과 연결 관리

<!-- TODO: keep-alive timeout이 너무 짧거나 길 때의 장단점과 서버, proxy, client 간 timeout 불일치가 만드는 문제를 정리한다. -->

## Stateless

<!-- TODO: HTTP가 stateless하다는 의미와 개별 요청이 독립적으로 처리되는 이유를 설명한다. -->

## Cookie와 Session

<!-- TODO: Cookie가 클라이언트에 저장되고 요청에 포함되는 과정과 Session이 서버 측 상태를 유지하는 과정을 설명한다. -->

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    C->>S: 로그인 요청
    S-->>C: 세션 생성 및 Cookie 전달
    C->>S: Cookie를 포함한 후속 요청
    S-->>C: 세션 확인 후 응답
```

<!-- TODO: 위 흐름에 Cookie의 보안 속성, 세션 만료, 분산 환경에서의 세션 저장 방식을 보충한다. -->

## Timeout

<!-- TODO: connection timeout, read timeout 등 timeout의 종류를 나누고 무한 대기를 방지하는 목적을 설명한다. -->

## Retry

<!-- TODO: 재시도 가능한 실패와 재시도하면 안 되는 실패를 구분하고 최대 횟수, exponential backoff, jitter를 설명한다. -->

## Rate Limiting

<!-- TODO: rate limiting의 목적과 HTTP 429 응답, 응답 Header를 활용한 대기 전략을 설명한다. -->

## 참고 자료

<!-- RFC와 브라우저 또는 서버의 공식 문서를 우선 기록한다. -->

-[MDN HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)

## 함께 읽기

- [[03_Resource/04_network/01_tcp|1주차 - TCP IP와 연결]]
- [[03_Resource/04_network/04_http_429_ts|HTTP 429 트러블슈팅 사례]]
