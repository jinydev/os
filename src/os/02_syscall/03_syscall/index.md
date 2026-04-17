---
layout: default
title: "3. 시스템 콜과 디버깅 (strace)"
---

# 3. 시스템 콜 전환 비용과 인터럽트 디버깅 메커니즘

하드웨어 구조 위에서 동작하는 운영체제의 세계로 진입하는 과정을 소프트웨어 관점에서 해부합니다.

## 🛡️ [전공 심화] 시스템 콜 101과 전환 오버헤드

시스템 콜은 여러분의 코드가 OS 보호 영역 안으로 진입하는 유일한 출입구이자 다리입니다. C 프로그램 안에서 `printf`를 호출하면 내부적으로 `write()` 시스템 콜이 실행되며, 예외(Exception)와 동일한 **소프트웨어 트랩(Trap)**이 발생합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">User Space <-> Kernel Space Transition Overhead</text></svg>
</div>

유저 스페이스에서 시스템 호출을 날리면 컴파일된 `libc` 라이브러리는 CPU 범용 레지스터(rax, rdi 등)에 매핑된 특수 콜 번호와 인자를 적재하고 곧장 `syscall` 명령어를 쏩니다. 이 찰나의 순간 CPU는 링 3(User Mode) 권한을 버리고 링 0(Kernel Mode)로 모드 스위칭을 시작합니다.

* **전환 비용(Overhead)의 주의점**: 이 권한 상승 비용은 매우 무겁습니다. 매번 커널 링과 유저 링을 오가는 모드 전환(Mode Transition) 시 방대한 문맥 정보 저장/복원 비용이 발생하기 때문에 과도한 시스템 콜 남용은 엔터프라이즈 시스템 퍼포먼스 붕괴의 주범입니다.

<br>

## ⚡ [실전 심화] 인터럽트 분리와 strace 디버깅

위에서 살펴본 커널 모드 체제의 격리를 역이용하면 시스템 장애 분석에 필요한 가장 강력한 디버깅 도구를 얻어낼 수 있습니다.

### 커널 처리: 인터럽트 분리 철학
`syscall`이 코드에 의해 발현되는 얌전한 트랩이라면, 외부 마우스 클릭이나 네트워크 통신 등은 100% 하드웨어 인터럽트로 발동됩니다. 리눅스 수만 대를 이끄는 커널에서 인터럽트 루틴(ISR)이 오래 막혀 있으면 시스템 전체가 일시 마비됩니다. 리눅스는 이를 **Top Half**(즉시 처리해야 할 일)와 **Bottom Half**(나중에 천천히 할 일)로 쪼개어 처리하는 디자인 최적화를 통해 응답성을 극대화했습니다.

### 셜록 홈즈식 시스템 디버깅 툴: strace
개발자가 마주하는 "디버거로도 안 잡히는 원인 불명 에러"의 90%는 결국 시스템 콜 충돌에서 발생합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="150" viewBox="0 0 600 150" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="80" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">$ strace -p <PID></text></svg>
</div>

여러분들의 파이썬 앱이나 JVM 스레드가 갑자기 아무 로그도 뱉지 않고 먹통이 되었다면 즉각 접속해 위 명령어를 입력해보십시오. 시스템 콜을 훔쳐보는 유틸리티입니다. 데이터베이스 소켓을 열려다 파일 설명자(FD)가 없어서 죽었는지, 디렉터리 권한 거부(EACCES)를 맞고 대기 중인지 커널 내부와의 모든 통신 내역이 터미널에 적나라하게 추적됩니다.
