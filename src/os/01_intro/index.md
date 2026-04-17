---
layout: default
title: "1주차: 운영체제란 무엇인가 (현대 OS의 역할과 구조)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="40" width="100" height="120" fill="#005A9E" rx="5"/><text x="100" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Apps</text><path d="M 160 100 L 240 100" stroke="#00FF00" stroke-width="4"/><rect x="250" y="40" width="100" height="120" fill="#E81123" rx="5"/><text x="300" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">OS Kernel</text><path d="M 360 100 L 440 100" stroke="#00FF00" stroke-width="4"/><rect x="450" y="40" width="100" height="120" fill="#333" rx="5"/><text x="500" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Hardware</text></svg>
</div>

# 1주차: 운영체제란 무엇인가 (현대 OS의 역할과 구조)

운영체제(Operating System, OS)는 사용자와 컴퓨터 하드웨어 사이의 중재자 역할을 수행하는 가장 핵심적인 시스템 소프트웨어입니다. 본 강의에서는 운영체제의 학술적 기본 개념부터 현대적 리눅스 커널 분석 및 실무 아키텍처까지 포괄적인 딥-테크 이론을 학습합니다.

---

## 🎯 핵심 학습 목표

* **운영체제의 개념과 목적**을 명확히 설명할 수 있다.
* 운영체제가 제공하는 **핵심 기능과 주요 4대 서비스**를 이해한다.
* 시대별 **시분할 체계 등 운영체제 특성 및 발전 과정**을 구분할 수 있다.
* **운영체제 아키텍처(Monolithic vs Microkernel)**의 특징을 실무 관점에서 비교한다.
* 현대 **링 모델(Ring Model)** 과 권한 증명 메커니즘을 파악한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

아래 링크를 통해 1주차의 상세 학습 내용과 커널 구조의 핵심 파트들을 순차적으로 학습하실 수 있습니다.

1. [시스템 구성과 역할](./01_components/index.md)
   > 하드웨어와 응용 프로그램 사이의 강력한 중재자 브리지로서의 운영체제 역할을 분석합니다.
2. [운영체제 4대 서비스 및 시스템 콜](./02_services/index.md)
   > 운영체제가 내부 자원을 어떻게 관리하며, 부팅부터 시스템 콜(System Call)을 통한 권한 노출까지 어떻게 서비스하는지 파악합니다.
3. [커널 아키텍처와 링 모델](./03_architecture/index.md)
   > Ring 3 (유저 모드)와 Ring 0 (커널 모드)의 구조적 단절과, 모놀리식/마이크로 커널 아키텍처의 트레이드오프를 확인합니다.
4. [OS 발전사와 리눅스 계보](./04_history/index.md)
   > 시분할(Time-sharing) 시스템부터 시작된 유닉스 다중 사용자 철학과 리눅스 커널/윈도우의 발전 역사를 추적합니다.
5. [실습 환경 준비](./05_setup/index.md)
   > 터미널 기반의 쉘 조작과 디버깅 분석을 위한 권장 리눅스(Ubuntu/WSL) 셋업 가이드입니다.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, 조유근 외 번역, 초판, 교보문고, 2014.
> * 구현회, 『운영체제 - 그림으로 배우는 구조와 원리』, 한빛아카데미, 2016.
