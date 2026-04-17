---
layout: default
title: "5주차: 프로세스 동기화와 교착 상태 (멀티코어 병렬 구조와 락 메커니즘)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="200" y="80" width="200" height="40" fill="#E81123" rx="5"/><text x="300" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Critical Section Lock</text><rect x="150" y="60" width="100" height="20" fill="#00FF00" rx="5"/><rect x="350" y="120" width="100" height="20" fill="#0078D7" rx="5"/><circle cx="200" cy="180" r="10" fill="none" stroke="#E81123" stroke-width="4"/><circle cx="400" cy="180" r="10" fill="none" stroke="#0078D7" stroke-width="4"/><path d="M 230 180 L 370 180" stroke="#00FF00" stroke-width="2" marker-end="url(#a)"/><text x="300" y="195" fill="gray" font-size="12" font-family="monospace" text-anchor="middle">Deadlock Avoidance</text><defs><marker id="a" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs></svg>
</div>

# 5주차: 동기화와 교착 상태 (멀티코어 병렬 구조와 락 메커니즘)

다중 스레드 환경에서 메모리와 힙(Heap)을 공유하는 것은 통신 속도 측정에 엄청난 축복이지만, 순서와 접근 권한 제어에 실패할 경우 모든 시스템을 다운시키는 파멸의 씨앗이 됩니다. 이번 강좌에서는 병렬 프로세싱에서 발생하는 **경쟁 상태(Race Condition)**의 어셈블리 측면 원리와 이를 방어하는 **상호배제(Mutex, Semaphore)**, 그리고 락의 남용이 가져오는 최악의 항구적 마비인 **교착 상태(Deadlock)**의 방어 아키텍처를 하나로 연결하여 딥-테크 레벨로 분석합니다.

---

## 🎯 통합 핵심 학습 목표

1. **병행성 오류 규명**: 경쟁 상태에서 발생하는 데이터 유실 메커니즘을 어셈블리어 레벨에서 설명할 수 있다.
2. **임계 영역(Critical Section) 아키텍처**: 안전한 동기화를 위한 진입/퇴출 구역 설계 및 상호배제, 진행, 한정 대기의 3조건을 검증한다.
3. **하드웨어 제어와 퓨텍스(Futex)**: 원자적 연산(`TestAndSet`, CAS) 명령어의 스핀락 한계와 유저 모드 락 트위킹을 파악한다.
4. **고급 OS 동기화 객체**: 세마포어(Semaphore) 카운팅과 모니터(Monitor) 객체의 내부 블로킹 파이프라인을 활용할 수 있다.
5. **데드락과 자원 회피**: 교착 상태 4대 발생 조건을 이해하고, 은행원 알고리즘(Banker's)과 락 오더링(Lock Ordering) 등 현대적 극복 방안을 체득한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

다중 코어 레이스의 경쟁 붕괴를 막고, 안전하게 순서를 보장하기 위한 락(Lock) 알고리즘 진화 역사를 5개 모듈로 세분화했습니다. 아래 링크를 참조하세요.

1. [동시성과 임계 영역 (Critical Section)](./01_race_condition/index.md)
   > 1+1 이 2가 아닌 1이 되는 어셈블리 라인 분쇄 과정과 이 오류를 회피하는 임계 영역 캡슐화 조건 3단계를 점검합니다.
2. [하드웨어 원자적 락 (Spinlock/Futex)](./02_sync_hardware/index.md)
   > 쪼개지지 않는 `CAS` 원자적 명령어를 통한 스핀락의 CPU 점유 낭비와 이를 회피하기 위한 퓨텍스 체계를 진단합니다.
3. [OS 동기화 객체 (세마포어/모니터)](./03_sync_os/index.md)
   > 큐 기반의 `wait()`/`signal()` 신호등 제어기 세마포어와 실수를 방지하는 고급 객체 지향 락인 모니터(Monitor)를 추적합니다.
4. [교착 상태(Deadlock) 회피와 아키텍처](./04_deadlock/index.md)
   > 동기화 락의 과용으로 인해 서로 무한 대기하는 교착 상태 4대 발생 조건 및 타조 알고리즘 등 회피 매버릭을 분석합니다.
5. [우선순위 역전과 커널 상속](./05_priority_inversion/index.md)
   > (특수 심화) RTOS 등에서 낮은 권한의 스레드가 높은 권한 스레드의 길을 막는 우선순위 역전(Inversion) 버그와 OS 개입 해결책을 조망합니다.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * Abraham Silberschatz, 『Operating System Concepts』, J. Wiley & Sons.
> * 『Linux Kernel Source Tree』 (futex.c implementation)
> * 에츠허르 다익스트라 논문 리뷰 시리즈 (임계 구역과 은행원 정리)
