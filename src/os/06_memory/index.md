---
layout: default
title: "6주차: 현대 메모리 관리와 가상 메모리 매핑 설계"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="100" height="80" fill="#005A9E" rx="5"/><text x="100" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Virtual Mem</text><path d="M 160 100 L 260 100" stroke="#00FF00" stroke-width="4"/><rect x="270" y="40" width="60" height="120" fill="#333" rx="5"/><text x="300" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">MMU</text><path d="M 340 100 L 440 100" stroke="#00FF00" stroke-width="4"/><rect x="450" y="60" width="100" height="80" fill="#4B4B4B" rx="5"/><text x="500" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Physical</text></svg>
</div>

# 6주차: 현대 메모리 관리와 가상 메모리 매핑 설계

소프트웨어 시스템 구조에서 가장 거대하고 위대한 마술은 단연코 **가상 메모리(Virtual Memory)**입니다. 여러분이 다루고 프로그래밍하는 최신 애플리케이션들은 프로그램 스스로가 수십 기가바이트의 거대한 메모리 영역 전체를 통째로 오롯이 혼자서 장악해버렸다고 착각합니다. 그들의 실제 하드웨어 서버 RAM은 4GB나 8GB밖에 없더라도 말입니다.

본 강의 모듈에서는 기초적인 물리/논리 주소 맵핑부터 치명적인 단편화 패널티를 돌파하는 기법인 페이징(Paging)을 거쳐, 현대 Linux의 `mmap` 백엔드 엔진과 최후 방어선인 OOM Killer 강제 탈환 시스템에 이르기까지 메모리 아키텍처의 세계를 딥 다이브 파이프라인으로 해부합니다.

---

## 🎯 통합 핵심 학습 목표

1. **물리 주소와 단편화(Fragmentation)**: MMU의 하드웨어 주소 변환 원리와 내부/외부 단편화 메모리 낭비 패턴을 규명한다.
2. **페이징과 세그먼테이션의 융합**: 현대 페이지화된 세그먼트 아키텍처가 메모리 권한 보호와 외부 단편화 방지를 어떻게 동시 달성하는지 파악한다.
3. **요구 페이징 체계 (Demand Paging)**: Page Fault 발생 시 디스크에서 필요한 코드만 끌고 오는 지연 적재와 `mmap()`의 제로 카피 I/O 성능을 엮어 이해한다.
4. **추방자 선출과 LRU 메커니즘**: 램 메모리가 가득 찼을 때 어떤 페이지를 퇴출할 것인지, 스왑 공간 교체 교리 LRU의 위력을 입증한다.
5. **[엔지니어링 코어] 스래싱과 OOM Killer**: 커널이 다중 프로세스를 넘다 스래싱 붕괴로 치닫는 것을 막고 최후 방어벽 OOM Killer의 `badness` 타겟 선정 로직을 학습한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

물리 반도체의 한계를 무한대로 확장시키는 기적의 논리, 가상 메모리 서브시스템 아키텍처를 5개 분류로 모듈화했습니다. 아래 챕터 링크로 접근하십시오.

1. [물리 주소 맵핑과 메모리 단편화](./01_physical_mapping/index.md)
   > CPU의 논리적 주소와 RAM의 물리 공간을 이어주는 칩셋 MMU와 고질적인 단편화 빈칸의 병목을 규명합니다.
2. [가상 메모리: 페이징과 세그먼테이션](./02_paging_segmentation/index.md)
   > 외부 단편화를 100% 박살내는 고정 블록 썰기 '페이징'과 권한을 통제하는 페이지화된 세그먼트 융합 체제.
3. [요구 페이징과 mmap() 시스템 콜](./03_demand_paging/index.md)
   > 모든 걸 한 번에 올리지 않고, CPU 지연인 Page Fault 인터럽트를 유도하여 디스크를 긁어오는 현대 엔진 `mmap`의 신비.
4. [페이지 대치 (Replacement) 알고리즘](./04_replacement_algo/index.md)
   > 공간이 파열되었을 때 어떤 과거 기록물 프레임을 하드디스크 스왑으로 쫓아 희생양을 삼을지 결정짓는 LRU 전략 지표.
5. [스래싱, 워킹 셋과 커널 OOM Killer](./05_working_set_oom/index.md)
   > 너무 잦은 자리 교체로 CPU가 멈춰버리는 스래싱 굴레와, 램이 고갈되었을 때 커널이 메모리 괴물을 강의 총살시키는 OOM 디버깅 분석.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, J. Wiley & Sons. 
> * Linux Kernel Documentation (`mm/oom_kill.c` & `mmap(2)`)
