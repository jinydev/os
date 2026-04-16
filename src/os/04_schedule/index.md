---
layout: default
title: "4주차: 현대 CPU 스케줄링 (멀티코어·이종코어 스케줄러)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="150" cy="100" r="40" fill="#0078D7"/><text x="150" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">CFS</text><path d="M 210 100 L 390 100" stroke="#00FF00" stroke-width="4"/><circle cx="450" cy="100" r="40" fill="#E81123"/><text x="450" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">EEVDF</text><text x="300" y="195" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">Virtual Runtime Accounting</text></svg>
</div>

# 4주차: 현대 CPU 스케줄링 (멀티코어·이종코어 스케줄러)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_04.png)
<br>




## 1. CPU 스케줄러의 타임 퀀텀

[실전 심화 렉처]
한 번에 한 가지 연산밖에 못 하는 싱글 코어 CPU가 수십 개의 프로그램을 '동시에' 돌리는 것처럼 속일 수 있는 비결은 무엇일까요?
OS 내부의 스케줄러(Scheduler)가 1초를 수백 조각으로 쪼개서(Time Quantum, 슬라이스) A 프로세스 실행 - B 프로세스 실행을 교대로 강제 할당하기 때문입니다. 
만약 어떤 프로그램이 무한 루프 `while(1)`에 빠져 CPU를 내놓지 않아도, 하드웨어 타이머 인터럽트가 강제로 제어권을 뺏어서 OS에게 되돌려줍니다(선점형 스케줄링). 

## 2. Linux CFS 및 EEVDF 알고리즘

[실전 심화 렉처]
서버 시장을 지배하는 리눅스는 어떻게 이 스케줄링을 최적화했을까요? 
Linux의 CFS(Completely Fair Scheduler)는 레드-블랙 트리(Red-Black Tree) 알고리즘을 사용해 각 프로세스의 실행된 가상 시간(`vruntime`)을 추적합니다. 가장 적게 실행된 프로세스가 항상 트리 가장 왼쪽에 배치되어 다음 실행 티켓을 가져가게 되므로 구조적으로 O(log N) 탐색 속도와 절대적 공정성을 보장합니다.
최근 커널 6.6 버전부터는 EEVDF(Earliest Eligible Virtual Deadline First) 알고리즘이 도입되어 지연 시간(Latency) 민감도를 획기적으로 낮추었습니다.

## 3. 멀티 코어와 이종 코어(P-Core/E-Core) 지배

[실전 심화 렉처]
최신 인텔 칩셋이나 모바일 AP들은 고성능을 내는 거대한 P(Performance) 코어와 전성비가 좋은 작은 E(Efficiency) 코어가 섞여 있습니다. 
초창기 OS 스케줄러들은 코어가 다르면 당황했습니다. 이제 현대 OS들은 `Thread Director`라는 하드웨어 텔레메트리를 읽어내어 게임 렌더링 스레드는 P코어에 즉각 매핑하고, 백그라운드 다운로드나 압축 프로세스는 E코어로 몰아넣는 초고도의 부하 분산 스케줄링을 실시간으로 연산합니다. 
`chrt`, `taskset` 명령어를 통해 엔지니어인 여러분들이 직접 이 코어 친화도(Affinity)를 핀-포인트로 배당할 수 있습니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">Context Switch Overhead</text></svg>
</div>

## [전공 심화] 리눅스 스케줄러: CFS에서 EEVDF로의 진보

초당 수억 번의 연산이 가능한 CPU를 천 개의 프로세스에게 초 단위 파편으로 잘라주는 시계열 마술이 프로세스 스케줄링입니다. 가장 적게 실행된 프로세스를 레드블랙 트리구조에서 찾아 우선권을 부여하던 리눅스의 명작 CFS(Completely Fair Scheduler)는, 최근 지연(Latency) 이슈 축소에 집중한 최신 EEVDF 스케줄러 체계로 완전히 세대 교체를 이룩했습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#0078D7" font-size="20" font-family="monospace" text-anchor="middle">Intel Thread Director: P-Core / E-Core</text></svg>
</div>

## [전공 심화] 이종 코어 시대의 스케줄링 붕괴점

과거 모든 CPU 코어의 속도는 동일했습니다. 그러나 현재의 데스크톱(Intel 13, 14세대)과 스마트폰(ARM)은 강한 코어(P)와 약한 코어(E)가 섞인 이종 코어(big.LITTLE) 아키텍처입니다. 백그라운드 영상 렌더링은 E코어에, 마우스나 게임 연산은 P코어로 스케줄러가 알아서 갈라치기 해주지 않으면 끔찍한 버벅임이 발생합니다. OS의 스케줄러는 점점 모바일 프로세서 구조를 닮아가고 있습니다.
