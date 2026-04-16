---
layout: default
title: "6주차: 현대 메모리 관리 (가상 메모리·mmap·ASLR)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="100" height="80" fill="#005A9E" rx="5"/><text x="100" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Virtual Mem</text><path d="M 160 100 L 260 100" stroke="#00FF00" stroke-width="4"/><rect x="270" y="40" width="60" height="120" fill="#333" rx="5"/><text x="300" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">MMU</text><path d="M 340 100 L 440 100" stroke="#00FF00" stroke-width="4"/><rect x="450" y="60" width="100" height="80" fill="#4B4B4B" rx="5"/><text x="500" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Physical</text></svg>
</div>

# 6주차: 현대 메모리 관리 (가상 메모리·mmap·ASLR)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_06.png)
<br>




## 1. 가상 메모리(Virtual Memory)의 위대한 환상

[실전 심화 렉처]
운영체제 역사상 가장 마법 같은 추상화입니다!
여러분이 개발하는 프로그램은 자신이 마치 거대한 16헥사바이트(64비트 시스템) 메모리를 혼자서 모두 독점하고 있다고 착각하게 만듭니다. 실제 RAM 칩이 8GB밖에 없더라도 말입니다.
OS는 '페이지 테이블(Page Table)'이라는 맵핑 장부를 통해 가짜 주소(Virtual Address)를 진짜 RAM 주소(Physical Address)로 실시간 번역해 줍니다. 
메모리가 진짜 부족하면 쓰지 않는 페이지를 디스크로 잠시 빼돌려(Swap Out) 감쪽같이 시스템을 연명시킵니다.

## 2. 페이지 폴트(Page Fault)와 mmap()

[실전 심화 렉처]
물리 메모리에 데이터가 없는 가짜 주소를 읽으려고 할 때, CPU(MMU 장치)는 즉각 에러 인터럽트(Page Fault)를 날립니다. 이때 커널이 쏜살같이 개입해서 디스크에서 데이터를 RAM으로 퍼 올린 뒤 프로세스를 재개시킵니다.
`mmap()` 시스템 콜은 이를 역이용한 천재적인 함수입니다. 10GB짜리 거대 파일을 메모리에 `mmap()` 치면 파일을 변수에 직접 복사하지 않습니다! 그저 파일의 주소를 가상 메모리 포인터에 연결해두고(Zero-Copy 접근), 프로그래머가 포인터를 읽으려 할 때만 Page Fault가 발생해 필요한 블록만 RAM으로 가져오기 때문에 엄청난 I/O 퍼포먼스를 뽐냅니다. 다수의 NoSQL DB가 이 아키텍처를 사용합니다.

## 3. OOM Killer와 메모리 보안 (ASLR)

[실전 심화 렉처]
모든 스왑 파티션마저 고갈되어 시스템 붕괴 직전에 몰리면, Linux 커널은 비장의 무기를 꺼냅니다: 바로 **OOM (Out-of-Memory) Killer**입니다.
`badness()` 점수를 매겨 가장 뚱뚱하고 덜 중요한 프로세스를 찾아 자가 처형(SIGKILL) 시켜버립니다. 여러분의 `java`나 `python` 서버가 아무 로그도 없이 강제 종료되었다면 커널 로그 `dmesg`를 뒤져 OOM 발생 이력을 반드시 확인하십시오.
또한, 이 가상 메모리 체계 덕택에 OS는 매번 프로그램이 실행될 때마다 코드와 스택의 메모리 주소를 랜덤으로 마구 뒤섞어버릴 수 있습니다. (ASLR) 해커가 버퍼 오버플로우 공격 시 타겟 주소를 예측하지 못하게 만들어 시스템을 수호하는 핵심 방어벽입니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">Page Fault / mmap()</text></svg>
</div>

## [전공 심화] 가상 메모리 매핑의 마술

모든 프로세스는 자기가 램을 1TB쯤 혼자 다 쓴다고 착각하고 있습니다. 이 장대한 환상을 만드는 곳이 CPU의 MMU(메모리 매니지먼트 유닛) 단과 OS의 페이지 테이블 설계입니다. 메모리가 단편화되어 찢어져 있어도 가상 구역에선 한 줄로 나타나고, 실행할 때서야 부리나케 물리 램으로 페이지 크기만큼 복사되는 Page Fault 기법의 우아함을 탐색합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">TLB Miss Penalty</text></svg>
</div>

## [전공 심화] mmap과 OOM Killer

100GB짜리 로그 파일을 어떻게 메모리에 올려 분석할까요? 파일 구조를 그대로 램에 '사상' 시켜버리는 `mmap()` 함수는 극강의 스토리지 I/O 부스터 역할을 담당합니다. 하지만 시스템 메모리가 파탄에 이르렀을 때, 리눅스 커널이 점수(OOM Score)를 매겨 무작위 프로세스의 뒤통수를 쏴 죽여버리는 OOM Killer의 메커니즘을 숙지하여 상용 DB 폭파 사태를 예방합니다.
