---
layout: default
title: "9주차: IO 디바이스 투어와 io_uring (디스크 스케줄링/RAID)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="120" height="80" fill="#5C2D91" rx="5"/><text x="110" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">CPU RAM</text><path d="M 180 100 L 410 100" stroke="#00FF00" stroke-width="4"/><text x="300" y="90" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">DMA Bypass CPU / io_uring</text><rect x="420" y="60" width="120" height="80" fill="#333" rx="5"/><text x="480" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">NVMe SSD PCIe</text></svg>
</div>

# 9주차: I/O 디바이스 모델링 (DMA, 디스크 스케줄링, RAID 및 io_uring)

컴퓨터 시스템의 근본적인 본질은 중앙 연산(CPU/RAM)이 도출해 낸 결과물을 하드디스크나 네트워크, 모니터라는 외부 사용자 세계(I/O Peripheral)로 보내 영구 출력하는 데 있습니다.

하지만 이 밖의 우주(I/O 장비)는 CPU가 지닌 GHz 속도에 비하면 한없이 기어가는 거북이와도 같습니다. 이번 I/O 종단 강좌는 기계식 모터 암(Arm)의 물리적 속도 한계(HDD Seek Time)를 최소 거리로 격파하기 위한 엘리베이터(C-SCAN) 스케줄링부터, 무적의 상용 서버용 조립 부품 RAID 구축법을 해부합니다. 

그리고 종국에는 **비싼 CPU를 완전히 무시/바이패스하고 디스크가 RAM에 직접 직결되는 DMA 버스 패스와 시스템 콜의 벽마저 깨부순 현대 리눅스 백엔드 최강 병기 io_uring 비동기 혁명**까지 다루며 운영체제의 거대한 렉처의 대단원을 내립니다.

---

## 🎯 통합 핵심 학습 목표

1. **디스크 메커니즘과 스케줄링**: 하드 디스크 연산의 90%를 찌르는 모터 탐색 시간(Seek Time) 파멸을 분석하고 운영체제 CPU 스케일링과는 전혀 다른 물리적 타겟을 지닌 디스크 C-SCAN 균등 스케줄링을 비교한다.
2. **트랜잭션 비용 최적화 (Interrupt ➔ DMA)**: 무의미하게 대기하는 폴링(Polling)의 노예에서 벗어나, CPU 없이 스토리지 하드웨어가 시스템 램을 다이렉트로 써 내려가는 DMA(Direct Memory Access) 철학을 배운다.
3. **RAID 시스템 아키텍처**: 디스크 화재나 파손을 즉각 방어하고 I/O 병렬 스트림 속도를 증강시키기 위한 엔터프라이즈 레이드의 스트라이핑(0), 미러링(1), 그리고 패리티 블록 연산(5) 규격을 정복한다.
4. **커널 레벨 I/O 추상화**: 쏟아지는 수만 개의 하드웨어를 전부 블록 디바이스(`/dev/sda`)와 문자 장치 파일 나부랭이로 평준화시켜버리는 유닉스 철학과 포직스 `stat`-`readdir` API 제어를 파악한다.
5. **[엔지니어링 코어] 극한 돌파 io_uring**: 폭증하는 최신 SSD 속도를 못 따라가는 수만 번의 `read()` 시스템 콜 오버헤드, 커널/유저 모드 전환의 멍청한 장벽을 무너뜨린 최신 리눅스 커널 공유 링버퍼(Ring Buffer) AIO 철학의 위력을 체감한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

1~8주 차에서 시스템 상부를 가동하던 이론이 디스크를 만나 현실로 구워지는 종단점 아키텍처, I/O Subsystem의 5가지 최적화 혁명을 체험합니다.

1. **[하드웨어 혈관과 커널 추상화](./01_io_subsystem/index.md)**
   > 모든 기기를 하나의 위장 파일로 평준화시킨 UNIX 철학과 이기종 버스 체계를 통제하는 제어기(Controller)의 위엄.
2. **[전송 철학 (Polling ➔ DMA)](./02_data_transfer/index.md)**
   > 무식한 무한루프 점검을 벗어나 하드웨어가 쏘아올리는 인터럽트, 더 건너뛰어 CPU를 기만하고 직접 입출력하는 DMA.
3. **[디스크 탐색 스케줄링 (C-SCAN)](./03_disk_scheduling/index.md)**
   > 좌우로 오가는 엘리베이터의 한쪽 양 끝단 병목 분쟁을 해소하기 위한 Circular 로비 회기 한 방향 스크래핑 기법.
4. **[서버 파티션: RAID 아키텍처](./04_raid/index.md)**
   > N개의 디스크를 묶어 1처럼 속이는 마법. 속도를 위한 0과 미러링 1, 그리고 현업 실무 대부인 패리티(Parity)의 5 모듈.
5. **[OS API 한계와 io_uring의 도래](./05_api_iouring/index.md)**
   > C언어 기반의 폴더 구조 분해 코드 및 최신 NVMe 드라이브에 맞춰 시스템콜 트랩 자체를 포기해 버려 속도 한계를 부순 링 버퍼 매커니즘.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * Abraham Silberschatz, 『Operating System Concepts』 (I/O & Disk)
> * Jens Axboe 논문, 『Efficient IO with io_uring』, 2019. (Linux Block Layer Creator)
