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

- 기본적으로 stateless한 프로토콜이어서 세션 유지하지 않음
  - cookie 등으로 클라이언트-서버 동작에 state
- HTML 문서 등 웹에서 사용하는 리소스들을 가져올때 사용하는 프로토콜

## HTTP Request / Response 구조

<!-- HTTP/1.1 기준 status line의 HTTP version, status code, reason phrase를 설명하고,
HTTP/2 이상에서는 표현 방식이 달라짐을 설명한다. -->

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/http-message-anatomy.svg)

<!-- 1. A start-line is a single line that describes the HTTP version along with the request method or the outcome of the request.
2. An optional set of HTTP headers containing metadata that describes the message. For example, a request for a resource might include the allowed formats of that resource, while the response might include headers to indicate the actual format returned.
3. An empty line indicating the metadata of the message is complete.
4. An optional body containing data associated with the message. This might be POST data to send to the server in a request, or some resource returned to the client in a response. Whether a message contains a body or not is determined by the start-line and HTTP headers. -->

1. start-line은 http 버전과 요청 메서드 혹은 응답 코드를 명시
2. HTTP header들에는 http 메시지의 메타데이타가 포함됨, 헤더가 필수는 아님
3. 헤더 이후 빈 line은 헤더 종료를 의미
4. message body(필수 X)는 메시지의 데이터를 포함한다. 
    이는 서버에 post하려는 데이터일수도 있고, client에게 전달될 리소스일수도 있다. 
    body를 포함할지 아닌지는 start line과 http header에서 결정된다.


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

- start line은 위와 같이 `<method> <request-target> <protocol>`의 세 파트 형태로 구성된다.
  - `<method>`: request의 의미와 요청으로 원하는 결과를 명시함
  - `<request-target>`: 절대/상대 URL 명시. 포맷은 사용하는 HTTP 메서드와 request context에 따라 다를 수 있음.
    - `*`로 명시되는 경우는 options preflight 요청인 경우에만 사용
    - HTTP method가 `CONNECT`인 경우 `<authority>:<port>` 형태로 명시한다.
  - `<protocol>`: HTTP 버전을 명시한다. HTTP/2 이상에서는 연결하면서 버전을 알수 있어서 헤더에서 명시하지 않는다.

#### request header

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/request-headers.svg)

- 요청 헤더는 요청에 필요한 추가 정보 혹은 이 요청이 서버에서 다뤄져야하는 방식을 명시한다.
- Representation headers는 body가 있는 경우 메시지 데이터의 형식과 인코딩을 명시한다.

#### request body

- 서버에 정보를 전달하기 위해 사용한다.
- `PATCH`, `POST`, `PUT`에만 존재

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

- start line은 위와 같이 `<protocol> <status-code> <reason-phrase>`의 세 파트 형태로 구성된다.
  - `<protocol>`: HTTP 버전을 명시한다.
  - `<status-code>`: 클라이언트 요청의 성공/실패 여부를 표시한다.
  - `<reason-phrase>`: Optional. 상태 코드가 간단히 상태만을 명시한다면 이 부분은 요청에 의한 결과를 상세히 알려주는 역할이다.

#### response header

![](https://mdn.github.io/shared-assets/images/diagrams/http/messages/response-headers.svg)

- Response header : 클라이언트가 추가 요청을 위해 필요한 정보들을 제공한다.
- Representation header : message부분의 데이터 형태 및 인코딩 형태 등 형태 정보를 제공한다.

#### request body

성공시 클라이언트가 요청한 데이터, 실패 혹은 이상이 있는 경우 요청에 왜 문제가 생겼는지 / 이 현상이 일시적인지 혹은 영구적인지 등을 표시한다. 필수는 아니며 `201 Created`, `204 No Content`인 경우 body가 없을 수 있다.

## HTTP Method

<!-- 각 Method의 의미와 안전성(safe), 멱등성(idempotent), 캐시 가능 여부를 비교한다. -->

| Method | 주요 용도 | 안전성 | 멱등성 | 요청 Body | 캐시 가능 여부 |
| ------ | --------- | ------ | ------ | --------- | ---- |
| GET     | 리소스 요청  | O      | O      | X         | O     |
| HEAD    |           | O      | O      |           | O     |
| OPTIONS |           | O      | O      |           | O     |
| TRACE   |           | O      | O      |           | O     |
| PUT     |           | X      | O      |           | X     |
| DELETE  |           | X      | O      |           | X     |
| POST    |           | X      | X      |           | 조건부*  |
| PATCH   |           | X      | X      |           | 조건부*  |
| CONNECT |           | X      | X      |           | O     |


- POST, PATCH 는 응답에 명시적으로 캐시 갱신 정보랑 `Content-Location` 헤더가 있을때 캐싱가능

## HTTP Status Code

<!-- 상태 코드 클래스별 의미를 설명하고 자주 접하는 상태 코드를 요청 성공, 클라이언트 오류, 서버 오류 관점에서 정리한다. -->

| 범위 | 의미 | 대표 상태 코드 | 처리 시 고려할 점 |
| ---- | ---- | -------------- | ----------------- |
| 1xx  |      |                |                   |
| 2xx  |      |                |                   |
| 3xx  |      |                |                   |
| 4xx  |      |                |                   |
| 5xx  |      |                |                   |

## HTTP 멱등성

<!-- 같은 요청을 여러 번 수행해도 서버의 의도된 상태가 한 번 수행했을 때와 같은 성질을 설명한다. -->

### 멱등성과 재시도

<!-- timeout으로 응답을 받지 못했지만 서버에서는 요청을 처리했을 가능성을 포함하여, Method별 재시도 위험을 설명한다. -->

### Idempotency Key

<!-- 결제나 주문처럼 중복 처리가 위험한 요청에서 idempotency key를 사용하는 목적과 서버의 처리 방식을 설명한다. -->

## HTTP 버전별 특징

### HTTP/1.1

<!-- 지속 연결, 요청 순서, 파이프라이닝과 head-of-line blocking을 설명한다. -->

- 연결이 재사용 될 수 있다.
- 파이프라이닝이 추가되어, 첫번째 요청이 완료되지 않아도 두번째 요청을 보낼 수 있게 해 레이턴시를 줄였다.
- Chunked response 지원
- 캐시 컨트롤 지원
- client와 server가 어떤 content를 주고받을지 명시해야 한다.
- 동일 IP 주소 내에서 다른 호스트 도메인을 사용할 수 있다. (`Host` 헤더)

### HTTP/2

<!-- binary framing, stream multiplexing, header compression과 TCP 수준 head-of-line blocking을 설명한다. -->

- binary 프로토콜. 임의로 생성 및 읽기 안됨. 향상된 최적화 테크닉 구현을 가능하게 함.
- multiplexed protocol이라 동일 connection 내에서 parallel request 가능
- 헤더 압축. 데이터 전송 중복과 overhead를 줄임.

### HTTP/3

<!-- QUIC과 UDP의 관계, stream 단위 전송, 연결 수립 지연 관점에서 HTTP/2와 비교한다. -->

- Transport 레이어에서 tcp대신 quic 사용.
- http/2가 multiplex 지원하긴하는데 tcp라 스트림 블로킹할수 있어서 QUIC씀
- quic: multiple stream 지원, 패킷 로스 감지, 각 stream단위 재전송. 오류가 있으면 해당 패킷 스트림만 블럭됨

| 구분                  | HTTP/1.1 | HTTP/2 | HTTP/3 |
| --------------------- | -------- | ------ | ------ |
| 기반 전송             | O         | O       | O       |
| 메시지 표현           | O         | O       | O       |
| 동시 요청 처리        | O         | O       | O       |
| Head-of-line blocking | O         | X       | X       |
| 연결 수립             | O         | O       | X       |


## Keep-Alive

<!-- 요청마다 새 TCP 연결을 생성하는 방식과 연결을 재사용하는 방식을 비교하고, latency와 서버 자원에 미치는 영향을 설명한다. -->

### Timeout과 연결 관리

<!-- keep-alive timeout이 너무 짧거나 길 때의 장단점과 서버, proxy, client 간 timeout 불일치가 만드는 문제를 정리한다. -->

## Stateless

<!-- HTTP가 stateless하다는 의미와 개별 요청이 독립적으로 처리되는 이유를 설명한다. -->

## Cookie와 Session

<!-- Cookie가 클라이언트에 저장되고 요청에 포함되는 과정과 Session이 서버 측 상태를 유지하는 과정을 설명한다. -->

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    C->>S: 로그인 요청
    S-->>C: 세션 생성 및 Cookie 전달
    C->>S: Cookie를 포함한 후속 요청
    S-->>C: 세션 확인 후 응답
```

<!-- 위 흐름에 Cookie의 보안 속성, 세션 만료, 분산 환경에서의 세션 저장 방식을 보충한다. -->

## Timeout

<!-- connection timeout, read timeout 등 timeout의 종류를 나누고 무한 대기를 방지하는 목적을 설명한다. -->

## Retry

<!-- 재시도 가능한 실패와 재시도하면 안 되는 실패를 구분하고 최대 횟수, exponential backoff, jitter를 설명한다. -->

## Rate Limiting

<!-- rate limiting의 목적과 HTTP 429 응답, 응답 Header를 활용한 대기 전략을 설명한다. -->

## 참고 자료

<!-- RFC와 브라우저 또는 서버의 공식 문서를 우선 기록한다. -->

## 함께 읽기

- [[03_Resource/04_network/01_tcp|1주차 - TCP IP와 연결]]
- [[03_Resource/04_network/04_http_429_ts|HTTP 429 트러블슈팅 사례]]
