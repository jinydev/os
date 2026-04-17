---
layout: default
title: "3주차: 프로세스와 스레드 구조 및 IPC 대통합"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="150" height="100" fill="#0078D7" rx="5"/><text x="125" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Process</text><path d="M 210 100 Q 300 20 390 60" fill="none" stroke="#00FF00" stroke-width="4" marker-end="url(#a)"/><path d="M 210 100 Q 300 180 390 140" fill="none" stroke="#00FF00" stroke-width="4" marker-end="url(#a)"/><rect x="400" y="30" width="100" height="60" fill="#333" rx="5"/><text x="450" y="65" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Thread 1</text><rect x="400" y="110" width="100" height="60" fill="#333" rx="5"/><text x="450" y="145" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Thread 2</text><defs><marker id="a" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs></svg>
</div>

# 3주차: 프로세스와 스레드 구조 및 IPC 통신 대통합

운영체제의 핵심 임무 중 하나는 한정된 CPU 자원을 여러 개의 논리 프로그램이 동시에 병렬/병행으로 효율적으로 나누어 쓸 수 있도록 철저히 조율하는 것입니다. 본 과정에서는 **프로세스(Process)**와 **스레드(Thread)**의 근본적 메모리 격리 아키텍처부터 컨텍스트 스위칭의 속도 지연 인프라, 그리고 보호된 프로세스 간 메모리를 뚫고 교환하는 궁극의 기법인 **IPC(Inter-Process Communication)** 레이어까지 현대 멀티코어 환경의 "동시성과 격리성"을 심층 렉처로 분석합니다.

---

## 🎯 핵심 학습 목표

1. **프로세스와 메모리**: 프로그램과 프로세스의 차이를 규명하고, 컴파일된 바이너리가 구성하는 메모리 할당 구역(Code, Data, Heap, Stack)을 이해한다.
2. **생명 주기와 스위칭 오버헤드**: 프로세스 상태 전이 모델과 빈번한 단박 문맥 교환(Context Switching)이 유발하는 성능 패널티 이슈를 설명한다.
3. **스레드 매핑 아키텍처**: 전역 자원(Heap)을 공유하며 스택(Stack)만 세분화하는 스레딩 패턴 구조와 파이프라인 블로킹 이슈를 파악한다.
4. **리눅스 분기 모델**: `fork()`와 `exec()`, `wait()` 시스템 호출 연결 패턴의 철학과 CoW 성능 개선 분기를 통달한다.
5. **프로세스 간 통신(IPC)**: 메모리 보안 구역 장벽을 넘나드는 시그널, 파이프, 그리고 제로 카피 지향의 초고비용 공유 메모리(Shared Memory) 메커니즘을 분석한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

메모리 레이아웃 구조와 비동기 자원 통신 모델을 체계적으로 서술하기 위하여 5개의 서브 모듈로 포털화되었습니다.

1. [프로세스와 코어 메모리 구조](./01_memory/index.md)
   > 단순 정적 바이너리가 운영체제의 권한을 받아 활성 메모리 세그먼트(Code, Data, Heap, Stack) 4대 요소로 태어나는 물리적 환경을 묘사합니다.
2. [PCB와 생명 주기 시스템](./02_pcb_lifecycle/index.md)
   > 문맥 교환(Context Switching) 전환 시간 동안 레지스터 덤프를 저장하는 Process Control Block의 비용 오버헤드를 추적합니다.
3. [공간 독립성과 fork()의 철학](./03_fork_exec/index.md)
   > 빈 땅에서 창조를 허용하지 않고, 무조건 부모 자신을 복제하는 유닉스의 괴상하고도 안전한 `fork()` 와 변태 명령 `exec()`를 분석합니다.
4. [멀티 스레드와 GIL 코루틴](./04_thread/index.md)
   > 프로세스의 한계를 박살 내며 자원을 파격적으로 뚫어 공유하는 NPTL 멀티 스레드 구조와, Python 프레임워크의 코어 GIL 한계를 우회하는 비동기 이벤트를 파고듭니다.
5. [프로세스 간 통신(IPC) 기법](./05_ipc/index.md)
   > 파이프와 시그널을 넘어 `shmget` 커널 물리 메모리 포인터 부착까지, 극단적인 제로-카피 IPC 공유 메모리 아키텍처를 학습합니다.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, J. Wiley & Sons. 
> * 리눅스 API 커널 소스 및 `man 2 shmget` 시스템 콜 맵핑 규약.
