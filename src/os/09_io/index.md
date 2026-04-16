---
layout: default
title: "9주차: 장치 관리와 I/O (현대 드라이버 모델과 io_uring)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="120" height="80" fill="#5C2D91" rx="5"/><text x="110" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">RAM</text><path d="M 180 100 L 410 100" stroke="#00FF00" stroke-width="4"/><text x="300" y="90" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">DMA Bypass CPU</text><rect x="420" y="60" width="120" height="80" fill="#333" rx="5"/><text x="480" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">NVMe SSD</text></svg>
</div>

# 9주차: 장치 관리와 I/O (현대 드라이버 모델과 io_uring)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_09.png)
<br>




## 1. 모든 것은 파일이다 (Everything is a file)

[실전 심화 렉처]
마우스 커서 데이터, 네트워크 소켓 스트림 로그, SSD 파티션 구조. 이 셋의 공통점은 과연 무엇일까요? 유닉스(Linux) 철학에서는 이들 모두가 단지 `/dev` 폴더 안의 '파일'로 취급된다는 점입니다. 
당신은 파이썬으로 `/dev/sda` 파일을 `open()`하여 디스크의 자기 섹터(MBR/GPT 파티션 테이블 영역)를 다이렉트로 읽거나 밀어버릴(파괴) 수 있습니다! 즉, 장치 드라이버는 본질적으로 특정한 메타 명령을 물리 인터페이스(GPIO/PCIe 버스)로 변환 전송하는 마법의 파이프 번역기에 불과합니다.

## 2. DMA(Direct Memory Access)와 인터럽트 전술

[실전 심화 렉처]
초고속 10Gbps 광랜 카드나 Gen5 NVMe SSD가 데이터를 쏠 때 CPU가 이를 하나하나 받아 적는다면 칩이 녹아내릴 것입니다.
현대 하드웨어는 OS의 승인 하에 DMA 컨트롤러를 통해 CPU를 완전히 무시한 채 메인 메모리(RAM)의 지정된 주소 공간에 통째로 데이터를 다이렉트로 갖다 때려(Write) 붓습니다. 다 붓고 나면 최후에 "작업 끝"이라는 하드웨어 인터럽트를 한 줄 날려 통보하는 경이로운 효율성을 달성합니다. PCIe 레인(Lane) 아키텍처의 혁명적 비결입니다.

## 3. io_uring: 괴물 같은 비동기 패러다임

[실전 심화 렉처]
전통적인 `epoll()`과 AIO(비동기 I/O)는 뛰어났지만 잦은 커널 시스템 콜 왕복(Context Switch)의 비용 한계에 다다랐습니다.
최신 Linux 5.1 커널부터 도입된 `io_uring`은 이를 산산조각 내버렸습니다. 공유 메모리 링버퍼(Ring Buffer)를 유저 스페이스와 커널 스페이스 양쪽이 함께 보며(Mmap Ring), 유저는 수백 개의 I/O 제출을 링 큐에 집어넣고 시스템 콜 한 번 없이 커널이 이를 집어가서 알아서 백그라운드로 처리해주는 초과격한 제로 오버헤드 퍼포먼스를 뽐냅니다. Redis나 DB 시장은 현재 이 엔진 하나로 대대적 프레임워크 개조를 치르고 있습니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#E81123" font-size="24" font-family="monospace" text-anchor="middle">io_uring vs epoll</text></svg>
</div>

## [전공 심화] DMA와 초고속 I/O 패스

초당 수 기가바이트를 쏘아붙이는 NVMe SSD의 데이터를 일일이 CPU가 받아서 복사하면 컴퓨터는 마비됩니다. 칩셋과 메모리 버스 사이에 심겨진 DMA(Direct Memory Access) 하드웨어 컨트롤러가 CPU를 우회하여 램에 테라바이트 데이터를 알아서 밀어 넣는 우회 메커니즘을 배웁니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#0078D7" font-size="18" font-family="monospace" text-anchor="middle">SPDK: Zero-Copy Userspace I/O</text></svg>
</div>

## [전공 심화] io_uring, 리눅스 I/O의 최종 혁명

스토리지 속도가 빛의 속도에 가까워지면서, `read()` 시스템 콜 오버헤드 자체가 가장 느린 병목이 되었습니다. 커널 5.1 부터 도입된 `io_uring` 은 유저 메모리와 커널 메모리 공간에 공유된 고리(Ring) 원형 큐를 만들어 놓고, 트랩/문맥전환 오버헤드 없이 수만 개의 디스크 읽기 요청을 한 번에 배달하는 극강의 비동기 파이프라인입니다.
