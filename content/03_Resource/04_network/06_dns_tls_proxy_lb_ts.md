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

# Endpoint가 정상인데 Ingress에서 503이 발생한 이유

## 문제 상황

- Kubernetes에 Keycloak 배포
- public-nginx Ingress를 통해 외부 공개
- Pod와 Service는 정상처럼 보였지만 외부 요청은 503 반환

## 시스템 구성

Client
→ DNS
→ public-nginx
→ Ingress
→ keycloak-svc
→ Keycloak Pod

## 관측한 증상

- 외부 요청: HTTP 503
- Service selector: 정상
- Endpoint: Pod IP:8080 존재
- Controller log: devtools-keycloak-svc-80

## 당시 가설

1. DNS가 잘못된 IP를 가리킨다.
2. IngressClass가 잘못됐다.
3. Service selector가 Pod를 찾지 못한다.
4. Pod가 8080에서 listen하지 않는다.
5. Ingress와 Service의 port가 일치하지 않는다.

## 진단 과정

- DNS 조회
- Ingress ADDRESS 및 IngressClass 확인
- Ingress Controller log 확인
- Service port와 selector 확인
- Endpoint 확인
- Pod 내부 listen port 확인
- Ingress backend service port 비교

## 실제 원인

Ingress backend는 keycloak-svc:80을 참조했지만,
keycloak-svc에는 port 8080만 정의되어 있었다.

## 해결

Ingress backend port를 8080으로 변경

## 당시 몰랐던 개념

- Service port와 targetPort
- Ingress backend가 참조하는 port
- Service와 EndpointSlice의 관계
- Endpoint가 존재해도 전체 요청 경로가 정상이라는 의미는 아님

## 추가로 공부한 개념

- Ingress의 L7 host/path routing
- Ingress Controller의 역할
- HTTP 503이 발생하는 위치 구분
- readiness와 Endpoint eligibility
- Controller log를 이용한 backend 식별

## 지금 다시 대응한다면

DNS
→ Ingress rule
→ Service port
→ EndpointSlice
→ Pod listen port

순서로 각 hop의 입력과 출력을 비교한다.

## 재발 방지 체크리스트



## 함께 읽기

- [[03_Resource/04_network/05_dns_https_proxy_lb|3주차 - DNS, HTTPS, Proxy, Load Balancer]]
