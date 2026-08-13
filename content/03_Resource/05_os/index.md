---
title: OS
draft: true
tags:
  - os
---

# OS

OSTEP의 큰 목차를 기준으로 가상화, 병행성, 영속성을 각각 2주씩 학습한 기록입니다.

> 전체 일정과 진행 방식은 [CS 학습 계획](01_Project/12_week_cs_study)에서 관리합니다.

## 학습 원칙

- OSTEP을 기본 안내서로 사용하되 반드시 한 권만 사용하거나 정해진 챕터를 그대로 따를 필요는 없다.
- 강의, 공식 문서, 다른 책을 포함해 각 주차의 학습 목표에 맞는 자료를 선택할 수 있다.
- 세부 범위는 진도와 이해도에 따라 조정한다.
- 매주 학습 내용과 인사이트를 PR로 제출한다.
- 팀원 PR을 1개 이상 리뷰하고, 서로 다른 설명과 자료에서 배운 점을 기록한다.
- 트러블슈팅 글 대신 학습 전후에 관점이 달라진 지점이나 개념 사이의 연결을 인사이트로 정리한다.

## 학습 목차

### 5주차 - 가상화 1

- 학습 내용: [프로세스 가상화](03_Resource/05_os/01_virtualization_process)
- 인사이트: [프로세스 가상화 인사이트](03_Resource/05_os/02_virtualization_process_insight)

### 6주차 - 가상화 2

- 학습 내용: [메모리 가상화](03_Resource/05_os/03_virtualization_memory)
- 인사이트: [메모리 가상화 인사이트](03_Resource/05_os/04_virtualization_memory_insight)

### 7주차 - 병행성 1

- 학습 내용: [병행성 기초](03_Resource/05_os/05_concurrency_basics)
- 인사이트: [병행성 기초 인사이트](03_Resource/05_os/06_concurrency_basics_insight)

### 8주차 - 병행성 2

- 학습 내용: [병행성 제어](03_Resource/05_os/07_concurrency_coordination)
- 인사이트: [병행성 제어 인사이트](03_Resource/05_os/08_concurrency_coordination_insight)

### 9주차 - 영속성 1

- 학습 내용: [I/O와 저장 장치](03_Resource/05_os/09_persistence_io_storage)
- 인사이트: [I/O와 저장 장치 인사이트](03_Resource/05_os/10_persistence_io_storage_insight)

### 10주차 - 영속성 2

- 학습 내용: [파일 시스템과 데이터 무결성](03_Resource/05_os/11_persistence_filesystems)
- 인사이트: [파일 시스템 인사이트](03_Resource/05_os/12_persistence_filesystems_insight)

## 6주 완료 목표

```text
가상화
→ CPU와 메모리를 여러 실행 주체가 안전하게 공유

병행성
→ 여러 실행 흐름이 공유 상태를 올바르게 다루도록 조정

영속성
→ 장치 위에 파일과 파일 시스템을 구성하고 장애 이후에도 데이터를 보존
```

각 영역의 세부 개념을 외우는 데 그치지 않고 운영체제가 제공하는 추상화, 이를 구현하는 방법, 추상화가 만드는 비용을 연결해서 설명할 수 있는 상태를 목표로 한다.
