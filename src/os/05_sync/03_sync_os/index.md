---
layout: default
title: "3. OS 동기화 객체 (세마포어/모니터)"
---

# 3. OS 레벨 동기화 객체 캡슐화: 세마포어와 모니터

앞선 스핀락의 CPU 극단적 낭비를 막고, 대기 큐(Queue)에 정식으로 잠들어 있다가 락이 풀렸을 때 Block ➔ Wakeup 처리되기 위해 운영체제는 추상적 도구를 제공합니다.

![Semaphore Wait and Signal](./img/os05_40.svg)

### 세마포어 (Semaphore)
컴퓨터 과학자 에츠허르 다익스트라(Dijkstra)가 고안한 도구로 `wait`(P) 와 `signal`(V) 연산으로 구동됩니다.
* 0과 1사이에서만 동작하는 **Mutex(Binary Semaphore)**는 완전한 통제용 수문장 구실을 하며,
* 풀(Pool)값을 5로 두는 **Counting Semaphore**는 화장실 칸이나 DB 커넥션 등 가용한 다중 자원 인스턴스 개수를 통제합니다. 

### 개발자를 위한 최종 진화: 모니터 (Monitor)
세마포어를 잘못 써서 발생할 수 있는 휴먼 에러(wait 호출 누락 등)마저 틀어막기 위해, Java의 `synchronized` 같은 프로그래밍 언어 자체가 클래스 내부 진입에 기본 상호배제를 강제하는 더 고도화된 객체지향 락 아키텍처가 모니터(Monitor)입니다. 모니터 내부에는 오직 단 하나의 스레드만 활동할 수 있습니다.
