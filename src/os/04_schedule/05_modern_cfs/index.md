---
layout: default
title: "5. [현대 Linux] CFS와 이종코어 제어"
---

# 5. 현대 Linux 스케줄러: CFS에서 EEVDF 및 이종코어(big.LITTLE) 최적화로

일반적인 큐잉 방식을 넘어, 지금 여러분이 쓰고 있는 리눅스 클러스터 서버는 수학적 자료구조를 토대로 O(M) 성능의 한계를 넘어버렸습니다.

## 🐧 CFS(Completely Fair Scheduler) 구조
리눅스의 명작 **CFS(Completely Fair Scheduler)**는 자료구조인 레드-블랙 트리(Red-Black Tree)를 사용해 각 프로세스의 실행된 가상 계산시간(`vruntime`)을 회계 장부처럼 철저하게 추적합니다. 
가장 적게 혜택을 받은(vruntime이 낮은) 프로세스가 언제나 트리의 맨 왼쪽에 적재되므로 구조적으로 `O(log N)` 처리 탐색 속도와 완벽한 분할 시간 공정성을 증명했습니다.

최근(커널 6.6 버전 이후) 이 CFS 체계마저 한 단계 진보하여, 극한의 레이턴시(지연) 이슈를 없앤 **EEVDF(Earliest Eligible Virtual Deadline First)** 스케줄러로 세대를 진화시켜 게임이나 실시간 응답성(Tick Delay) 분야를 완전히 갈아엎고 있습니다.

## 🦾 거대한 멀티 코어와 이종 코어(big.LITTLE) 스케줄링 패러다임

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#0078D7" font-size="20" font-family="monospace" text-anchor="middle">Intel/ARM Thread Director: P-Core / E-Core</text></svg>
</div>

과거 2010년대에는 모든 물리적 CPU 단일 패키지 안의 코어 클럭 속도가 동일했습니다. 그러나 현재 초고출력 데스크톱(Intel)과 스마트폰/M1칩셋(ARM)은 괴물 같은 계산력을 가진 **P(Performance) 코어**와 전성비가 매우 뛰어난 절전형 **E(Efficiency) 코어**가 뒤섞인 이종 코어(big.LITTLE) 아키텍처 환경입니다.

만약 영상 백그라운드 렌더링이 P코어로 가버리고 정작 화면 UI 랜더링이 E코어로 떨어지면 스터터링(버벅임) 현상이 발생합니다. 
때문에 최신 OS 스케줄러는 하드웨어 텔레메트리인 `Thread Director` 의 피드백을 실시간 감시해 능동적으로 부하를 분산합니다.

* 엔지니어인 여러분들은 언제든지 터미널에서 `taskset` (코어 친화도 고정) 명령어를 직접 호출하여 특정 프로세스가 특정 코어 렌즈에서만 구동되도록 가둘 수 있습니다.
