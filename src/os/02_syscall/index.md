---
layout: default
title: "2주차: 컴퓨터 시스템 구조와 시스템 콜 (하드웨어 인터페이스와 OS 트랩)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">System Request (INT 0x80 / SYSCALL)</text><rect x="250" y="90" width="100" height="50" fill="#E81123" rx="5"/><text x="300" y="120" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Trap!</text></svg>
</div>

# 2주차: 컴퓨터 시스템 구조와 시스템 콜 (하드웨어 인터페이스와 OS 트랩)

소프트웨어 엔지니어가 운영체제를 깊이 있게 이해하고 고성능의 시스템 소프트웨어를 작성하기 위해서는, 그 토대가 되는 **하드웨어 아키텍처(Computer Architecture)**와 유저 스페이스에서 OS 권한 영역으로 진입하는 메커니즘인 **시스템 콜(System Call)** 환경에 대한 명확한 통찰이 선행되어야 합니다. 본 챕터에서는 폰 노이먼 하드웨어 구조부터 시스템 콜 트랩 비용, 그리고 실제 C 프로그램 컴파일 툴체인까지 딥-테크(Deep-tech) 관점에서 심화 학습합니다.

---

## 🎯 핵심 학습 목표

* 현대 컴퓨터의 근간인 **폰 노이먼(Von Neumann) 아키텍처** 관점에서 CPU, 메모리, 입출력 장치 메커니즘을 파악한다.
* CPU 레지스터의 역할과 **명령어 파이프라이닝(Instruction Pipelining)** 구조를 이해한다.
* **시스템 콜(System Call)** 작동 원리와 트랩(Trap)에 의한 컨텍스트 스위칭 권한 변경 비용을 증명한다.
* **하드웨어 인터럽트 제어 메커니즘과 `strace` 디버깅 방법론**을 실무에 적용한다.
* **GCC 컴파일 파이프라인**(전처리, 컴파일, 어셈블, 링크) 아키텍처를 추적한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

방대한 하드웨어 인터페이스 내용을 논리적으로 다루기 위해 4개의 서브 모듈로 구성되어 있습니다. 아래 링크를 통해 상세 내용을 학습하십시오.

1. **[하드웨어 아키텍처와 CPU](./01_architecture/index.md)**
   > 폰 노이먼 구조 모델과 CPU 필수 레지스터, 더 나아가 명령어 인출/실행 파이프라인(Pipelining) 사이클의 원리를 추적합니다.
2. **[시스템 버스와 I/O 제어](./02_bus_io/index.md)**
   > 고속 시스템 버스에서 발생하는 I/O 병목을 해결하기 위한 하드웨어 인터럽트와 DMA의 태동을 설명합니다.
3. **[시스템 콜 전환과 디버깅 (strace)](./03_syscall/index.md)**
   > 유저 모드와 커널 모드를 관통하는 Trap 오버헤드의 실체를 파악하고, 강력한 커널 인터페이스 모니터링 툴인 `strace`의 사용법을 학습합니다.
4. **[(별첨) GCC 시스템 툴체인](./04_compiler/index.md)**
   > GCC가 바이너리 파일을 구워내는 전처리 ➔ 컴파일 ➔ 어셈블 ➔ 링킹 4단계 파이프라인 연산 과정을 해부합니다.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * David A. Patterson, John L. Hennessy, 『Computer Organization and Design』
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, 번역판, 2014.
