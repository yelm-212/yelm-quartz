---
title: DNS, TLS, Proxy, Load Balancer 트러블슈팅 사례
draft: false
tags:
  - network
  - dns
  - tls
  - proxy
  - load-balancer
  - troubleshooting
---

# Endpoint가 정상인데 Ingress에서 503이 발생한 이유

## 문제 상황

Kubernetes Cluster에 Keycloak을 배포하고 public-nginx Ingress Controller를 통해 외부에 공개하는 과정에서 외부 요청이 `503 Service Unavailable`로 실패했다.

당시 Keycloak Pod는 실행 중이었고 keycloak-svc의 selector도 Pod를 정상적으로 선택하고 있었다.
Endpoint에도 Keycloak Pod의 IP와 8080 port가 존재했기 때문에 처음에는 Service와 Pod 사이의 연결은 정상이라고 판단했다.

하지만 Ingress Controller가 참조하던 Backend Service port와 실제 Service에 정의된 port가 서로 달랐다.

## 시스템 구성

Client
→ DNS
→ public-nginx
→ Ingress
→ keycloak-svc
→ Keycloak Pod

문제가 발생했던 설정을 단순화하면 다음과 같았다.

```yaml
# Ingress
backend:
  service:
    name: keycloak-svc
    port:
      number: 80
```

```yaml
# Service
spec:
  selector:
    app: keycloak
  ports:
    - port: 8080
      targetPort: 8080
```

즉 Ingress는 `keycloak-svc:80`을 Backend로 참조했지만 `keycloak-svc`가 노출하고 있던 Service port는 `8080`이었다.

Kubernetes Ingress의 Backend는 `service.name`과 `service.port.name` 또는 `service.port.number`로 Service를 참조한다. 따라서 Ingress에 작성하는 port는 Pod의 container port를 직접 가리키는 값이 아니라 **Service에 정의된 port**와 대응해야 한다.

## 관측한 증상

- 외부 요청: HTTP `503 Service Unavailable`
- Keycloak Pod: Running
- Service selector: 정상
- Endpoint: Keycloak Pod IP와 `8080` 존재
- Ingress Controller log: `devtools-keycloak-svc-80` 형태의 Backend 확인
- Ingress backend: `keycloak-svc:80`
- 실제 Service port: `8080`

처음에는 Endpoint가 존재했기 때문에 Service 구성이 전체적으로 정상이라고 생각했다.

하지만 Endpoint가 존재한다는 것은 **Service가 Backend Pod를 찾았다는 것**을 확인하는 데 유용할 뿐, Ingress → Service 연결 설정까지 정상이라는 의미는 아니었다.

### 1. Ingress와 IngressClass 확인

```bash
kubectl get ingress -n <namespace>
kubectl describe ingress <ingress-name> -n <namespace>
```

확인 항목:

- `ingressClassName`
- Address
- Host / Path Rule
- Backend Service 이름
- Backend Service port
- Event

Ingress Resource는 routing rule을 선언하고, 실제 요청을 받아 이 rule을 구현하는 것은 Ingress Controller다.

```text
Ingress Resource
    = Host / Path / Backend 설정

Ingress Controller
    = 실제 HTTP/HTTPS 요청 처리 및 Proxy
```

### 2. Service의 port와 selector 확인

```bash
kubectl get svc keycloak-svc -n <namespace>
kubectl describe svc keycloak-svc -n <namespace>
```

당시 핵심 값:

```text
Service: keycloak-svc
port:       8080
targetPort: 8080
selector:   app=keycloak
```

Service의 port 관계는 다음과 같다.

```text
Ingress
   │
   │ service.port
   ▼
Service :8080
   │
   │ targetPort
   ▼
Pod :8080
```

- `port`: Service가 제공하는 port
- `targetPort`: Service가 선택한 Backend Pod로 전달할 destination port

예를 들어 다음처럼 서로 다른 값을 사용할 수도 있다.

```yaml
ports:
  - port: 80
    targetPort: 8080
```

이 경우 Ingress는 Service의 `80`을 참조하고 실제 Pod에는 `8080`으로 전달할 수 있다.

하지만 당시에는 Service가 `8080`만 제공하고 있는데 Ingress가 `80`을 참조하고 있었다.

### 3. Endpoint / EndpointSlice 확인

당시에는 다음과 같이 Endpoint를 확인했다.

```bash
kubectl get endpoints keycloak-svc -n <namespace>
```

Endpoint에는 Keycloak Pod의 IP와 `8080` port가 존재했다.

현재 Kubernetes에서는 `EndpointSlice`를 기준으로 다음처럼 확인할 수 있다.

```bash
kubectl get endpointslices \
  -n <namespace> \
  -l kubernetes.io/service-name=keycloak-svc
```

Service selector와 EndpointSlice의 관계는 다음과 같다.

```text
Service selector
      ↓
일치하는 Pod 선택
      ↓
EndpointSlice에 Backend 정보 반영
```

따라서 Endpoint가 정상이라는 사실로 Service가 Pod를 찾고 있다는 것은 확인할 수 있었다.

하지만 다음 구간은 별개였다.

```text
Ingress backend port
      ↓
Service port
```

### 4. Pod의 Application port 확인

```bash
kubectl get pod -n <namespace> -l app=keycloak
kubectl describe pod <keycloak-pod> -n <namespace>
```

Service가 올바른 Pod를 선택해도 Application이 `targetPort`에서 listen하지 않는다면 요청은 실패할 수 있다.

필요하면 다음과 같이 Ingress나 Service를 우회하며 문제 구간을 좁힐 수 있다.

```text
외부 요청
Client → Ingress → Service → Pod

Service 직접 테스트
Debug Pod → Service → Pod

Pod 직접 테스트
Debug Pod → Pod IP
```

### 5. Ingress backend와 Service port 비교

최종적으로 두 Resource의 port를 직접 비교했다.

```text
Ingress
keycloak-svc:80
       │
       X  Service에 port 80 없음
       │
Service
keycloak-svc:8080
       │
       ▼
Endpoint / Pod:8080
```

Ingress Controller log에서도 `devtools-keycloak-svc-80` 형태의 Backend를 확인했고, 실제 Service의 port와 비교하면서 port mismatch를 원인으로 특정했다.

## 실제 원인

문제는 Pod의 port나 Service selector가 아니라 **Ingress가 Service에 존재하지 않는 port를 Backend로 참조하고 있었던 것**이었다.

```yaml
# 문제 설정
backend:
  service:
    name: keycloak-svc
    port:
      number: 80
```

실제 Service:

```yaml
ports:
  - port: 8080
    targetPort: 8080
```

Endpoint 자체는 존재했지만 Ingress Controller가 참조하던 `keycloak-svc:80`과 Service 설정이 연결되지 않았다.

## 해결

Ingress backend port를 실제 Service port와 동일한 `8080`으로 수정했다.

```yaml
backend:
  service:
    name: keycloak-svc
    port:
      number: 8080
```

수정 후 요청 흐름:

```text
Client
  ↓
public-nginx
  ↓
Ingress
  ↓
keycloak-svc:8080
  ↓
targetPort:8080
  ↓
Keycloak Pod:8080
```

변경 후 외부에서 Keycloak에 정상적으로 접근할 수 있었다.

## 당시 몰랐던 개념

### Service `port`와 `targetPort`

Ingress에서 지정하는 `service.port`는 **Service가 제공하는 port**를 참조한다.

그 이후 Service의 `targetPort`가 실제 Pod의 destination port를 결정한다.

```text
Ingress
  │
  │ Service port
  ▼
Service
  │
  │ targetPort
  ▼
Pod
```

따라서 아래 구성도 정상이다.

```yaml
# Service
ports:
  - port: 80
    targetPort: 8080
```

```yaml
# Ingress
backend:
  service:
    name: keycloak-svc
    port:
      number: 80
```

### Service와 EndpointSlice

Service에 selector가 있으면 Kubernetes는 selector와 일치하는 Backend Pod를 EndpointSlice에 반영한다.

EndpointSlice를 확인하면 다음을 진단하는 데 도움이 된다.

- Service selector가 Pod label과 일치하는지
- 실제 Backend Pod가 존재하는지
- Backend Endpoint의 IP와 port가 무엇인지

하지만 이것만으로 Ingress의 Backend Service 이름과 port가 올바른지는 확인할 수 없다.

### Endpoint가 정상이라는 것의 범위

Endpoint가 정상이라고 해서 정상 전체 요청 경로가 정상이지 않을 수 있고, 각 hop을 별도로 확인해야 한다.

```text
DNS
↓
Ingress Controller
↓
Ingress Rule
↓
Service port
↓
EndpointSlice
↓
Pod listen port
```

## 추가로 공부한 개념

### Ingress의 L7 Routing

Ingress는 HTTP/HTTPS 요청의 Host와 Path를 기준으로 Backend Service를 선택할 수 있다.

```yaml
rules:
  - host: keycloak.example.com
    http:
      paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: keycloak-svc
              port:
                number: 8080
```

이번 문제는 Pod networking 자체보다 **Ingress Controller가 L7 rule을 처리한 뒤 Backend Service를 선택하는 구간의 설정 오류**였다.

### Readiness와 Endpoint eligibility

Pod가 `Running`이라는 사실만으로 traffic을 받을 준비가 되었다는 의미는 아니다.

Readiness Probe가 실패한 Pod는 Ready 상태에서 제외되며 Service traffic 대상에서도 빠질 수 있다.

따라서 Backend가 보이지 않을 때는 다음 순서도 확인해야 한다.

```text
Pod Running?
    ↓
Pod Ready?
    ↓
Service selector match?
    ↓
EndpointSlice에 Backend 존재?
```

이번 장애의 직접 원인은 readiness가 아니라 Ingress/Service port mismatch였다.

### HTTP 503으로 알 수 있는 범위

`503 Service Unavailable`만으로 정확한 원인을 특정할 수는 없다.

Ingress Controller에서는 Backend Service가 없거나 사용할 Backend를 구성하지 못한 경우 등 여러 상황에서 `503`이 나타날 수 있다.

따라서 다음처럼 범위를 줄이는 것이 낫다.

```text
503
↓
응답을 만든 컴포넌트 확인
↓
Ingress Controller log
↓
Ingress Backend Service / port
↓
EndpointSlice
↓
Pod
```

이번 경우에는 `503`과 Ingress Controller log, 실제 Ingress/Service 설정을 함께 비교해서 원인을 찾았다.


## 함께 읽기

- [3주차 - DNS, HTTPS, Proxy, Load Balancer](03_Resource/04_network/05_dns_https_proxy_lb)
