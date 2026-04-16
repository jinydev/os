---
layout: default
title: "3주차: 프로세스와 스레드 (현대 멀티코어 환경의 실행 단위)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="150" height="100" fill="#0078D7" rx="5"/><text x="125" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Process</text><path d="M 210 100 Q 300 20 390 60" fill="none" stroke="#00FF00" stroke-width="4" marker-end="url(#a)"/><path d="M 210 100 Q 300 180 390 140" fill="none" stroke="#00FF00" stroke-width="4" marker-end="url(#a)"/><rect x="400" y="30" width="100" height="60" fill="#333" rx="5"/><text x="450" y="65" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Thread 1</text><rect x="400" y="110" width="100" height="60" fill="#333" rx="5"/><text x="450" y="145" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Thread 2</text><defs><marker id="a" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs></svg>
</div>

# 3주차: 프로세스와 스레드 (현대 멀티코어 환경의 실행 단위)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_03.png)
<br>




## 1. 프로세스와 코어 메모리 구조

[실전 심화 렉처]
여러분이 `python main.py`를 입력하면 OS는 디스크에 있던 바이너리를 읽어 '프로세스(Process)'라는 생명체를 만듭니다. 프로세스는 철저히 격리된 메모리 세그먼트(Text, Data, Heap, Stack)를 부여받습니다. 
이 메모리 뭉치는 PCB(Process Control Block)라는 커널 내부 자료구조로 관리되며 PID 1번(`systemd` 또는 `init`)부터 거대한 트리를 형성합니다.
특히 부모가 `fork()`로 자식을 낳으면, 메모리 공간이 통째로 1:1 무한 복제되는 것이 아니라 CoW (Copy-on-Write) 기술을 사용하여 실제 데이터가 변형될 때까지는 물리 메모리 포인터만 공유하여 엄청난 성능 이득을 봅니다.

## 2. 스레드 (Thread) 스케일 구조

[실전 심화 렉처]
하지만 프로세스끼리 통신(IPC)하는 비용은 무겁습니다. 그래서 현대 프로그래밍은 '스레드(Thread)'라는 경량 단위를 사용합니다.
스레드는 Data와 Heap 메모리를 공유하고, 각자의 Stack 영역과 레지스터만 따로 갖습니다. 즉 같은 전역 변수를 여러 스레드가 동시에 읽고 쓸 수 있는 자유(그리고 락 지옥의 시작)를 갖습니다.
Linux 커널 관점에서는 스레드나 프로세스나 본질적으로 똑같은 `task_struct`로 다뤄지며(NPTL 모델), 그저 '가상 메모리 테이블을 공유하느냐 안 하느냐'의 차이(flag)만 있을 뿐입니다. 이것이 리눅스가 윈도우보다 프로세스 생성에 뛰어난 퍼포먼스를 내는 이유입니다.

## 3. 코루틴과 비동기 논블로킹 I/O

[실전 심화 렉처]
천 개의 스레드를 띄우면 1천 번의 컨텍스트 스위칭(Context Switching) 비용이 CPU 캐시를 날려먹습니다. 
Node.js와 파이썬 `asyncio`는 "스레드는 1개만 쓰고, I/O를 요청해놓고 기다리는 유휴 시간에 다른 코드 조각(코루틴)을 실행시키자"는 초고도화된 비동기(Asynchronous) 이벤트 루프 모델입니다. 
당신이 네트워크 대기 시간을 기다리지 않고 단일 코어에서도 초당 만 건의 쿼리를 날릴 수 있는 이유가 바로 이 유저 레벨 컨텍스트 스위칭 덕분입니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">fork() -> exec()</text></svg>
</div>

## [전공 심화] 주소 공간 독립성과 fork()의 철학

프로세스는 운영체제로부터 배급받은 완벽히 분리된 사유지(사유 메모리 공간)를 갖습니다. 리눅스의 프로세스 생성 방식은 매우 독특한데, 텅 빈 공간을 새로 만드는 창조 행위가 아니라 무조건 기존 부모 프로세스를 똑같이 유전 복제(fork)한 뒤 뇌(코드)만 갈아끼우는(exec) 기법을 취합니다. 이는 환경 설정과 자원의 유전을 انتہائی 간결하게 만듭니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">Python GIL: Single Core Concurrency Limit</text></svg>
</div>

## [전공 심화] 스레드와 Python GIL의 비극

메모리를 통째로 복제하는 것은 무겁기 때문에 힙 메모리를 공유하며 일손만 늘리는 스레드(Thread)가 등장했습니다. 하지만 널리 쓰이는 Python은 객체의 참조 카운터를 보호하기 위한 치명적인 자물쇠(GIL: Global Interpreter Lock)가 존재하여 막강한 10코어 머신에서도 스레드들이 줄을 서서 1코어만 활용하는 비효율을 보여줍니다.
