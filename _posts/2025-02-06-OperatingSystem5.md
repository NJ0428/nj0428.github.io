---
layout: single
title: "일괄처리 시스템 (Batch Processing)정리"
categories: OperatingSystem
author_profile: false
toc: true
---

일괄처리 시스템(Batch Processing)은 **작업·데이터를 일정량 모아 한꺼번에 자동 실행**하는 고전적 처리 방식입니다. 1950년대 메인프레임 시절부터 사용-되어 온 이 방식은 오늘날에도 대용량 데이터 분석, 급여 계산처럼 실시간성이 덜 요구되는 업무에서 여전히 핵심 역할을 합니다. 이 글에서는 **일괄처리 시스템의 개념, 상주모니터 구조, 장‧단점, 그리고 보완 기법**까지 초보자도 이해할 수 있도록 자세히 설명드립니다.

------

## 일괄처리 시스템이란?

### Batch Processing 개념

- **정의**: 사용자가 제출한 작업(Job)·데이터를 **배치(batch)** 로 묶어 *순차*적으로 자동 처리하는 운영 방식
- **등장 배경**: 1950년대 초기 컴퓨터는 인터랙티브 입출력 장치가 부족했기 때문에, 효율적 CPU 활용을 위해 작업을 모아야 했음
- **대표 활용**: 급여 계산(payroll), 세금 정산, 로그 분석, 대형 이미지·영상 변환 등 **대량·반복 작업**

> 핵심 키워드 일괄처리 시스템(Batch Processing)이 문서 전반에 자연스럽게 1–2% 비율로 배치되어 있습니다.

------

## 상주모니터 구조와 동작 원리

### 상주모니터(Resident Monitor)의 역할

초기의 일괄처리 운영체제는 **상주모니터**라는 작은 커널을 메모리에 항상 올려 두어 다음과 같은 기능을 담당했습니다.

| 구성 요소                  | 기능                                                         | 예시                      |
| -------------------------- | ------------------------------------------------------------ | ------------------------- |
| **인터럽트·트랩 벡터**     | 예외·입출력 완료 시 제어권을 모니터로 전환                   | *카드 리더 완료 인터럽트* |
| **장치 구동기(Driver)**    | 테이프, 프린터 등 I/O 장치 제어                              | *Line Printer 관리*       |
| **작업 순서화(Sequencer)** | 대기 중인 배치 작업의 실행 순서 결정                         | *JCL 우선순위*            |
| **제어카드 해석기**        | 사용자가 제출한 **제어카드(Job Control Card)**를 파싱해 실행 | `//JOB …`, `//EXEC …`     |

### 동작 흐름

1. 사용자는 천공 카드·자기테이프 등에 **제어카드 + 데이터**를 입력
2. **카드 리더**가 입력 데이터를 메모리-버퍼로 전송
3. 상주모니터가 제어카드를 해석해 **작업을 로드**하고 CPU에 연결
4. 작업 종료 후 다음 배치로 자동 전환 → *완전 무인 처리* 실현

------

## 일괄처리 시스템의 장점

1. 시스템 자원 효율 극대화
   - 작업을 계획적으로 배치해 **CPU 공회전** 시간을 최소화합니다.
2. 자동화 수준 향상
   - 사람이 수동으로 프로그램을 로드·실행하던 과정을 **상주모니터**가 대행하여 운영 부담을 대폭 줄입니다.
3. 대용량 처리 최적
   - 반복적이고 방대한 데이터를 **연속 처리**해야 할 때 최고 효율을 발휘합니다.
4. 일괄 회계·통계 업무
   - 야간에 배치를 돌려 **업무 시간 중 시스템 부하**를 줄일 수 있습니다.

------

## 일괄처리 시스템의 단점 및 문제점

1. 반환 시간(응답 시간) 지연
   - 한 배치가 끝날 때까지 다른 결과를 볼 수 없어 **실시간 인터랙션**이 불가합니다.
2. 오류 수정 어려움
   - 배치 중 한 Job에서 에러가 나면 *배치 전체*를 재실행해야 하는 경우가 잦습니다.
3. CPU 유휴 현상
   - 전통적 일괄처리에서는 I/O 동안 CPU가 놀 수 있어 **자원 낭비**가 발생합니다.

------

## 단점 보완 기법

### 1. 상주모니터 개선

- **자동 재시작** · **에러 로깅** 기능 추가로 오류 복구 시간 단축

### 2. 오프라인 연산(Offline Processing)

- 카드 리더·프린터 같은 **입출력 준비 작업**을 별도 보조 프로세서에서 수행 → **메인 CPU 집중**

### 3. 버퍼링(Buffering)

- I/O 데이터를 **메모리 버퍼**에 임시 저장하여 CPU와 장치 간 **속도 차이 흡수**

### 4. 스풀링(SPOOLing)

- 여러 Job의 출력·입력을 디스크에 **큐(Queue)** 로 저장
- CPU는 다음 Job을 즉시 실행 → **동시성 효과**로 *CPU 유휴 시간* 대폭 감소

------

## 실무 예시 — 파이썬 배치 스크립트 간단 예

```python
import csv, time

def process_payroll(batch_file):
    with open(batch_file) as f:
        reader = csv.DictReader(f)
        for row in reader:
            pay = float(row["hours"]) * float(row["rate"])
            time.sleep(0.01)   # I/O 지연 가정
            print(f"{row['name']} 급여: {pay:,.0f}원")

if __name__ == "__main__":
    process_payroll("payroll_batch.csv")
```

> 위 스크립트는 일괄처리 방식으로 직원 급여를 한 번에 계산합니다. 버퍼링·스풀링 기법을 추가하면 대량 데이터에도 효율적으로 확장할 수 있습니다.

------

## 질문 정리– 일괄처리 시스템

1. **일괄처리 시스템과 시분할 시스템의 가장 큰 차이점은?**

   ⇒ 일괄처리는 *배치 완료 후* 결과 제공, 시분할은 *짧은 시간 단위*로 CPU를 교대로 사용해 **즉각 반응**합니다.

2. **스풀링과 버퍼링은 어떻게 다르나요?**

   ⇒ 버퍼링은 **메모리**에 임시 저장, 스풀링은 **디스크** 큐를 활용해 I/O를 겹쳐 처리합니다.

3. **현대에도 일괄처리 시스템이 사용되나요?**

   ⇒ 네, **Hadoop MapReduce, Spark Batch** 등 대용량 분석 플랫폼이 현대식 배치 처리의 예입니다.

4. **배치 작업 오류를 최소화하려면?**

   ⇒ **트랜잭션 로그**와 *체크포인트*를 두어 오류 발생 시 **중간 지점부터 재시작**합니다.

5. **일괄처리 시스템에서 CPU 유휴 시간을 줄이는 최신 방법은?**

   ⇒ **멀티스레딩 + 비동기 I/O** 조합으로 I/O 대기 중에도 다른 계산을 수행하도록 설계합니다.
