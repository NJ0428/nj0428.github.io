---
layout: single
title: "분산처리 시스템 정리"
categories: OperatingSystem
author_profile: false
toc: true
---

## 분산처리 시스템이란?

**분산처리 시스템(Distributed Processing System)** 은 지리적으로 분산된 여러 대의 컴퓨터(노드)가 **네트워크**로 연결되어 *한 팀처럼* 협업하며 동일 업무를 수행하도록 설계한 구조입니다. CPU·메모리·스토리지 등 자원을 **공동 활용**해 **고가용성**과 **확장성**을 동시에 달성하죠.

------

## 분산처리 시스템의 핵심 특징

### 1. 자원 공유(Resource Sharing)

- **노드 간 자원 풀 구성** → 파일, 데이터베이스, 프린터까지 공동 사용
- 병목 없이 필요한 노드가 즉시 자원에 접근

### 2. 신뢰성·내구성(Reliability)

- 한 노드가 고장 나면 **다른 노드가 즉시 작업을 인계**
- *장애 허용(fault-tolerance)* 구조로 서비스 중단 최소화

### 3. 계산 속도 향상(Parallelism)

- 대규모 연산을 **병렬 처리**해 처리량 폭발적 증가
- 빅데이터 분석·AI 학습처럼 연산 집약적 작업에 최적

### 4. 네트워크 기반 통신

- TCP/IP, gRPC, 메시지 큐를 통해 **노드 간 데이터 교환**
- 실시간 협업·데이터 동기화 지원

------

## 분산처리 시스템 아키텍처 살펴보기

| 요소                | 설명                                  | 예시                         |
| ------------------- | ------------------------------------- | ---------------------------- |
| **노드(Node)**      | 독립 실행 가능한 컴퓨터               | EC2 인스턴스, Kubernetes Pod |
| **네트워크**        | 노드 연결 및 데이터 전송 경로         | 이더넷, 광-LAN, SD-WAN       |
| **미들웨어**        | 노드 간 통신·데이터 직렬화·로드밸런싱 | Kafka, RabbitMQ              |
| **분산 파일시스템** | 데이터 무중단 공유·복제               | HDFS, Ceph                   |
| **분산 스케줄러**   | 작업 분배·리소스 최적화               | YARN, Mesos                  |

------

## 실무 예시: Python + Ray로 분산 워드카운트

```python
import ray, re, collections
ray.init()  # 클러스터에 연결

@ray.remote
def word_count(chunk):
    words = re.findall(r"\\w+", chunk.lower())
    return collections.Counter(words)

# 텍스트 파일을 여러 조각으로 분할 후 병렬 처리
chunks = open("large_text.txt").read().split("===SPLIT===")
futures = [word_count.remote(c) for c in chunks]
result = sum(ray.get(futures), collections.Counter())

print("단어 ‘data’ 빈도:", result["data"])
```

> 위 코드는 분산 워드카운트의 간단 데모입니다. 각 노드가 텍스트 청크를 병렬로 세어 큰 파일도 빠르게 집계할 수 있습니다.

------

## 분산처리 시스템의 대표 응용 분야

- **클라우드 컴퓨팅**: AWS, Azure, GCP의 마이크로서비스
- **대규모 데이터 처리**: Hadoop, Spark, Flink
- **과학 시뮬레이션**: 기후 모델링, 유전자 분석
- **온라인 서비스**: 글로벌 웹·이메일·동영상 스트리밍

------

## 질문 정리 – 분산처리 시스템

**Q1. 분산처리 시스템과 병렬처리 시스템 차이는?**

병렬처리는 *단일* 머신의 멀티코어를, **분산처리 시스템**은 *여러* 노드를 네트워크로 묶어 작업합니다.

**Q2. 데이터 일관성은 어떻게 보장하나요?**

CAP 이론을 고려해 **분산 트랜잭션, 레플리카 동기화** 전략(예: Raft, Paxos)을 사용합니다.

**Q3. 노드 간 지연(latency)을 줄이는 방법은?**

지역 근접 배치, **CDN**, 프로토콜 최적화(gRPC, HTTP/2)로 RTT를 최소화합니다.

**Q4. 장애 허용을 구현하려면?**

헬스 체크 + **자동 페일오버**, 데이터 다중 복제, 무중단 배포(Blue-Green) 패턴을 적용합니다.

**Q5. 분산처리 시스템 초보자는 무엇부터 배워야 하나요?**

TCP/IP·리눅스 네트워크, **컨테이너(Kubernetes)**, 그리고 Spark 같은 분산 프레임워크를 순차적으로 학습하세요.
