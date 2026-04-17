---
layout: default
title: "4주차: CPU 스케줄링 이론과 현대 리눅스/이종코어 스케줄러"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="150" cy="100" r="40" fill="#0078D7"/><text x="150" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">CFS</text><path d="M 210 100 L 390 100" stroke="#00FF00" stroke-width="4"/><circle cx="450" cy="100" r="40" fill="#E81123"/><text x="450" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">EEVDF</text><text x="300" y="195" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">Virtual Runtime Accounting</text></svg>
</div>

# 4주차: CPU 스케줄링 이론과 현대 리눅스/이종코어 스케줄러

다중 프로그래밍(Multi-programming) 체제에서 한정된 CPU 자원은 단 1ms라도 쉬어서는 안 됩니다. 이 거대한 프로세스의 행렬을 이끄는 지휘자가 바로 **스케줄러(Scheduler)**입니다. 본 강의에서는 FCFS/SJF와 같은 학술적 큐잉 알고리즘의 기초를 다지고, 나아가 현대 리눅스 최신 패러다임(CFS 및 EEVDF)과 데스크탑/모바일 기기의 이종 코어(big.LITTLE) 스케줄링 최적화에 이르는 딥-테크 엔진 코어를 단계별로 탐구합니다.

---

## 🎯 핵심 학습 목표

1. **스케줄러 3계층 아키텍처**: 장기/중기/단기 스케줄러의 역할을 구분하고 큐잉 파이프라인의 구조를 파악한다.
2. **트레이드오프 성과 분석**: 선점(Preemptive) 타이머 강제 할당과 비선점의 성능 차이를 정량 지표(응답 시간 등)로 분석한다.
3. **고전 알고리즘 설계사**: FCFS의 병목 한계와 SJF의 수학적 완벽성을 증명하고 이론의 한계점을 도출한다.
4. **실무형 피드백 큐 (MLFQ)**: 기아 상태(Starvation) 방지를 위한 에이징(Aging) 논리와 다단계 큐 강등 구조를 이해한다.
5. **[엔지니어링 코어] 현대 커널 알고리즘**: O(log N) 복잡도를 지닌 Linux 커널 **CFS(가상 런타임)** 및 P-Core/E-Core 스레딩 제어 명령어(`taskset`)를 활용한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

시간 제어와 스케줄러 아키텍처의 발전을 다룬 이번 챕터는 5개의 상세 블록으로 재구성되었습니다. 아래 링크를 통해 진입하십시오.

1. [스케줄러 파이프라인 아키텍처](./01_architecture/index.md)
   > CPU / IO 버스트의 빈도를 분석하고 중기(Swap) 및 단기 스케줄러의 상호 통신 파이프라인을 체득합니다.
2. [선점성과 성능 평가 지표](./02_metrics/index.md)
   > 1초를 수만 번 쪼개는 타이머 선점(Preemptive) 설계의 존재 이유와 응답 시간(Response) 지표의 중요성을 나열합니다.
3. [스케줄링 고전 설계사 (FCFS/SJF)](./03_classic_algo/index.md)
   > 단순 큐인 FCFS의 병목 원인인 호위 효과(Convoy Effect)와 SJF 모델의 불가능성을 수학적으로 분해합니다.
4. [실전 상용: 다단계 피드백 큐 (MLFQ)](./04_mlfq/index.md)
   > Windows 계열에서 활용하는 다중 계급식 큐 강등/승격(Aging) 모델의 자원 패널티 지배 방식을 뜯어봅니다.
5. [[현대 Linux] CFS와 이종코어 제어](./05_modern_cfs/index.md)
   > O(log N) 가상 런타임을 빚어내는 리눅스 표준 CFS 및 차세대 EEVDF의 철학, 그리고 Intel 빅-리틀 코어(P/E 코어) 친화성 고정 엔지니어링(`taskset`) 환경을 다룹니다.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, J. Wiley.
> * 『Linux Kernel Source Tree』 (kernel/sched/core.c)
> * 구현회, 『운영체제 - 그림으로 배우는 구조와 원리』, 한빛.
