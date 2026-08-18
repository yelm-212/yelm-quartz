---
title: 파일 시스템 복구와 데이터 무결성
draft: true
tags:
  - os
  - persistence
  - filesystem
  - journaling
  - integrity
---

# 파일 시스템 복구와 데이터 무결성

## 이번 주 범위

OSTEP Ch 41~51을 학습한다. Fast File System, 파일 시스템 검사, 저널링, 로그 구조 파일 시스템, Flash 기반 SSD, 데이터 무결성, 분산 시스템과 분산 파일 시스템을 포함한다.

## 학습 목표

- Fast File System이 지역성을 높이는 배치 정책을 설명할 수 있다.
- 비정상 종료가 파일 시스템 일관성을 깨뜨리는 이유를 설명할 수 있다.
- 파일 시스템 검사와 저널링의 복구 방식을 비교할 수 있다.
- 로그 구조 설계와 체크섬이 해결하려는 문제를 설명할 수 있다.
- Flash 기반 SSD의 특성이 저장 계층 설계에 미치는 영향을 설명할 수 있다.
- Network File System과 Andrew File System의 캐시 및 일관성 정책을 비교할 수 있다.

## Fast File System

<!-- 실린더 그룹, 관련 데이터 배치, 큰 파일 처리 정책이 지역성과 성능에 미치는 영향을 정리한다. -->

## 충돌 일관성

### 일관성이 깨지는 이유

<!-- 하나의 논리적 연산이 여러 디스크 쓰기로 나뉠 때 일부만 반영될 수 있는 상태를 예로 든다. -->

### 파일 시스템 검사와 저널링

| 방식             | 복구에 사용하는 정보 | 장점 | 비용 |
| ---------------- | -------------------- | ---- | ---- |
| 파일 시스템 검사 |                      |      |      |
| 저널링           |                      |      |      |

## 로그 구조 파일 시스템

<!-- 쓰기를 로그 형태로 모으는 목적과 세그먼트 정리 비용을 함께 정리한다. -->

## Flash 기반 SSD

<!-- 페이지 단위 읽기와 쓰기, 블록 단위 삭제, Flash Translation Layer, 가비지 컬렉션, 마모 평준화를 정리한다. -->

## 데이터 무결성

<!-- 잠복 섹터 오류, 잘못 전달된 쓰기, 체크섬이 탐지할 수 있는 오류를 정리한다. -->

## 분산 시스템

<!-- 통신 실패, 부분 실패, 재시도, 멱등성이 분산 시스템 설계에 미치는 영향을 정리한다. -->

### Network File System

<!-- 상태를 적게 유지하는 서버 설계, 클라이언트 캐시, 일관성 정책을 정리한다. -->

### Andrew File System

<!-- 전체 파일 캐시, Callback 기반 캐시 검증, 확장성 확보 방식을 정리한다. -->

## 백지복습 질문

- 쓰기 완료 응답과 데이터의 영속성 보장은 왜 같은 의미가 아닐 수 있는가?
- 저널링과 로그 구조 파일 시스템은 로그를 사용하지만 목적이 어떻게 다른가?
- 체크섬만으로 데이터를 복구할 수 없는 이유는 무엇인가?
- Network File System과 Andrew File System은 캐시 일관성을 어떻게 유지하는가?

## 참고 자료

- [OSTEP - Persistence](https://pages.cs.wisc.edu/~remzi/OSTEP/#book-chapters)
- [Linux Kernel Documentation - Filesystems](https://docs.kernel.org/filesystems/index.html)

## 함께 읽기

- [I/O와 파일 시스템 기초](03_Resource/05_os/09_persistence_io_storage)
- [파일 시스템 인사이트](03_Resource/05_os/12_persistence_filesystems_insight)
- [OSTEP Security](03_Resource/05_os/13_security)
