---
layout: default
title: "2주차: 시스템 콜 (소프트웨어가 OS에 요청하는 방법)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">System Request (INT 0x80 / SYSCALL)</text><rect x="250" y="90" width="100" height="50" fill="#E81123" rx="5"/><text x="300" y="120" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Trap!</text></svg>
</div>

# 2주차: 시스템 콜 (소프트웨어가 OS에 요청하는 방법)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_02.png)
<br>




## 1. 시스템 콜 (System Call) 작동 원리

[실전 심화 렉처]
시스템 콜은 여러분의 코드가 OS의 세계로 진입하는 유일한 출입구이자 다리입니다.
유저 스페이스에서 `write(fd, buf, len)` 호출 시, 컴파일된 라이브러리는 CPU의 범용 레지스터(rax, rdi, rsi 등)에 시스템 콜 번호와 인자를 적재하고 `syscall` 명령어(또는 과거의 `int 0x80`)를 날립니다. CPU는 이 순간부터 유저 모드 권한을 박탈당하고 특권 레벨 코드를 실행하며 커널 모드로 점프합니다.
이 비용은 생각보다 큽니다. 매번 커널 링과 유저 링을 오가는 왕복 티켓(Context Switch - Mode Transition) 비용이 발생하기 때문입니다.

## 2. strace와 디버깅 예술

[실전 심화 렉처]
여러분이 마주하는 "원인을 알 수 없는 에러"의 90%는 `strace`로 추적 가능합니다.
파이썬 스크립트가 갑자기 멈췄다고요?
```bash
$ strace -p <파이썬 PID>
```
이걸 치면 현재 이 스크립트가 어떤 파일을 열려다 권한 거부(EACCES)를 당했는지, 아니면 어떤 소켓 파이프에서 영원히 `read()` 대기 중(Blocked)인지 초당 수천 줄의 시스템 콜 로그로 쏟아집니다.
`strace ls -la`를 직접 실행해 보세요. `ls` 명령어가 화면에 출력되기도 전에 어떤 동적 라이브러리(.so)들을 `mmap`으로 메모리에 로드하고, 어느 디렉토리 `openat()`을 날렸는지 숨겨진 뼈대가 적나라하게 드러납니다.

## 3. 소프트웨어 인터럽트와 하드웨어 인터럽트

[실전 심화 렉처]
`syscall`이 소프트웨어에 의해 촉발되는 자발적 트랩(Trap)이라면, 마우스를 클릭하거나 네트워크 패킷이 도착할 때 발생하는 것은 하드웨어 인터럽트(Hardware Interrupt)입니다.
수만 건의 트래픽이 밀려오는 서버에서 이 인터럽트를 처리하는 방식은 매우 정교해야 합니다. ISR(Interrupt Service Routine)은 너무 오래 실행되면 시스템 전역이 마비되므로 Linux 커널은 이를 Top Half(즉시 처리)와 Bottom Half(나중에 큐잉되어 천천히 처리)로 나누어 처리하는 철학을 개발했습니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">strace python3 app.py</text></svg>
</div>

## [전공 심화] Syscall 101: 트랩(Trap)과 권한 상승

C 프로그램 안에서 `printf` 함수를 호출한다면, 내부적으로는 `write()` 시스템 콜이 실행됩니다. 이 순간 CPU 내부에서는 예외(Exception)와 동일하게 생긴 소프트웨어 인터럽트(트랩)가 발생합니다. 레지스터에 시스템 콜 번호(가령 Linux x64의 경우 1번 write)를 올려둔 채 CPU 모드 비트를 3에서 0으로 뒤집어 진정한 커널 모드로 진입하는 문턱을 넘게 됩니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">User Space <-> Kernel Space Transition Overhead</text></svg>
</div>

## [전공 심화] strace를 통한 셜록 홈즈식 디버깅

서버 프로그램이 멈췄을 때 로그조차 찍히지 않는다면 어떻게 원인을 찾을까요? `strace -p [PID]` 명령은 프로세스를 낚아채어, 현재 커널과 어떤 대화를 나누고 있는지 `sys_read()`, `sys_nanosleep()` 등의 순서로 화면에 폭포수처럼 디스플레이해 줍니다. 장애 분석의 엔드게임이라 할 수 있습니다.
