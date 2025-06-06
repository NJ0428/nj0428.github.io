---
layout: single
title: "다중 프로그래밍(Multi-programming) 시스템이란?"
categories: OperatingSystem
author_profile: false
toc: true
---

다중 프로그래밍 시스템은 **단일 CPU**에서 여러 프로그램을 *동시에* 실행해 **CPU 유휴 시간**을 최소화하고 **시스템 자원 활용률**을 극대화하는 운영 방식입니다. -1950~60년대 메인프레임 시대에 등장했지만, 오늘날 클라우드·서버 환경에서도 *스케줄링의 기본 원리*로 널리 쓰이고 있습니다.

------

## 다중 프로그래밍 시스템이 필수로 고려해야 할 5가지

### 1. CPU 스케줄링

- *준비(Ready) 큐*에 있는 여러 작업 중 **어떤 프로세스에 CPU를 먼저 줄지** 결정합니다.
- **FCFS, SJF, RR** 같은 알고리즘으로 응답 시간·처리량 균형을 맞춥니다.

### 2. 기억장치(메모리) 관리

- 여러 프로그램이 동시에 메모리에 상주하므로 **분할·가상 메모리** 기법으로 충돌 없이 공간을 배분합니다.
- **스와핑(swapping)**으로 메모리 부족 시 일부 프로세스를 디스크로 옮겨 RAM을 확보합니다.

### 3. 장치 스케줄링

- 디스크·프린터 등 **I/O 장치 경쟁**을 제어해 병목을 줄입니다.
- **SSTF, SCAN, C-LOOK** 등 디스크 스케줄링 알고리즘이 대표적입니다.

### 4. 교착 상태(Deadlock) 방지

- *은행원 알고리즘*, 자원 할당 그래프 등으로 **서로 자원을 기다리다 멈추는 상황**을 예방·회복합니다.

### 5. 병행 제어 및 보호

- **세마포어, 모니터**로 임계 구역(Critical Section)을 보호하여 *데이터 일관성*을 유지합니다.
- 각 프로세스의 **주소 공간 격리**로 보안도 강화합니다.

------

## 다중 프로그래밍 시스템의 장단점

| 구분            | 장점                                 | 단점                                        |
| --------------- | ------------------------------------ | ------------------------------------------- |
| **시스템 효율** | CPU 사용률 대폭 향상                 | I/O 대기 동안 CPU가 여전히 유휴일 수 있음   |
| **사용자 경험** | 동시에 여러 작업 가능                | 관리 기법이 복잡—스케줄링, 메모리 보호 필요 |
| **확장성**      | 멀티프로세서와 결합 시 *병렬성* 증가 | **공유 메모리** 충돌 위험                   |

> Tip: 현대 OS는 다중 프로그래밍 + 시분할 + 멀티스레딩을 결합해 단점을 크게 완화했습니다.

------

## 멀티프로세서에서의 다중 프로그래밍

- **공유 메모리** 모델: 여러 CPU가 *하나의 메모리*를 함께 사용
- **작업 속도** 향상: 병렬로 Job을 분산 처리 → Throughput 극대화
- **신뢰성** 증가: 한 CPU가 장애여도 나머지가 서비스 지속

------

## 질문 정리– 다중 프로그래밍 시스템 자주 묻는 질문

1. **다중 프로그래밍과 시분할의 차이는?**

   *다중 프로그래밍*은 CPU 활용률 향상 목적, *시분할*은 **사용자 응답 시간** 개선 목적이 큽니다.

2. **교착 상태를 완전히 없앨 수 있나요?**

   실무에선 *탐지-회복* 또는 *예방* 전략을 적절히 섞어 **리스크를 최소화**합니다.

3. **CPU 유휴 시간을 줄이는 최신 방법은?**

   **비동기 I/O**와 *멀티스레딩*으로 I/O 대기 중에도 다른 작업을 실행합니다.

4. **메모리 충돌을 막으려면?**

   **가상 메모리 + 페이지 보호 비트**로 프로세스 간 접근을 차단합니다.

5. **멀티프로세서와 다중 프로그래밍을 함께 쓰면 문제 없나요?**

   캐시 일관성·락 경합 같은 과제가 있지만, **NUMA 인식 스케줄러**로 대부분 해결합니다.
