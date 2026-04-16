# 운영체제 (OS) 강의계획서

## 1. 교과목 개요

- **과목 소개**: <컴퓨터 구조(computer)>를 이수하여 하드웨어 원리를 이해한 학생이, 그 하드웨어 위에서 **현대 운영체제가 어떻게 모든 것을 관리하는가**를 배우는 전공 심화 과목입니다. Windows 11·Linux(Ubuntu·Rocky) ·macOS의 실제 동작을 기반으로 학습하며, Docker·컨테이너·가상화·클라우드 OS 개념까지 **오늘날 개발자와 인프라 엔지니어가 반드시 알아야 하는 현대 OS 지식**을 다룹니다.
- **학습 목표**: 시스템 콜에서 컨테이너까지 — OS가 프로세스·메모리·파일·장치·보안을 관리하는 원리를 이론과 실습으로 이해하고, Docker·Linux 관리·클라우드 환경에서 자신의 코드가 어떻게 실행되는지 설명할 수 있습니다.
- **선수 과목**: 컴퓨터 구조(computer) — CPU 내부 원리, 메모리 계층, 인터럽트 개념 이상

---

## 2. 학습 성과(LO)

- 시스템 콜의 구조를 이해하고 `strace`·`dtruss`로 실제 시스템 콜 흐름을 추적할 수 있다.
- 프로세스·스레드·코루틴의 차이를 설명하고, 멀티코어 스케줄링 원리를 이해할 수 있다.
- `top`·`htop`·`perf`로 시스템 리소스를 실시간 모니터링하고 병목을 진단할 수 있다.
- Docker와 Linux 네임스페이스·cgroup으로 컨테이너의 격리 원리를 이해할 수 있다.
- 현대 파일 시스템(ext4·APFS·NTFS·ZFS)의 저널링·CoW 구조를 설명할 수 있다.
- Linux 권한 시스템, SELinux, eBPF 기반 보안의 개념을 설명할 수 있다.

---

## 3. 14주 주차별 강의계획

---

### 1주차
- **대주제**: 운영체제란 무엇인가 — 현대 OS의 역할과 구조
- **세부학습목표**: OS가 하드웨어와 소프트웨어 사이에서 수행하는 역할을 이해하고, 현재 시장의 주요 OS를 사용자·서버·모바일 관점에서 비교한다.

#### 📌 1-1. 운영체제의 핵심 역할
1. 추상화 — 복잡한 하드웨어를 단순한 인터페이스(파일·프로세스·소켓)로 감추는 역할
2. 자원 중재 — CPU·메모리·I/O를 여러 프로그램이 충돌 없이 공유하도록 조정
3. 권한 제어 — 사용자 모드(User Mode) vs 커널 모드(Kernel Mode)로 안전 경계 설정
4. 하드웨어 드라이버 통합 — 다양한 장치를 표준 인터페이스로 통합하는 드라이버 계층
5. 서비스 제공 — 파일 시스템·네트워크 스택·프로세스 관리 등을 API로 제공

#### 📌 1-2. 현대 OS 생태계 비교
1. Windows 11 — NT 커널, DirectX12·WSL2·Hyper-V 통합, 데스크톱·서버 양용
2. Linux (Ubuntu·Debian·Rocky·Fedora) — 오픈소스 모놀리식 커널, 서버·클라우드·AI 인프라 사실상 표준
3. macOS Sequoia — Darwin(XNU) 커널, POSIX 호환, Apple Silicon 최적화 유닉스 계열
4. Android — Linux 커널 기반 모바일 OS, 터치 UI·앱 샌드박스 특화
5. iOS / iPadOS — Darwin 기반, 보안·성능 최우선의 폐쇄적 생태계

#### 📌 1-3. 커널 구조의 종류
1. 모놀리식 커널(Linux·Windows NT) — 모든 핵심 서비스가 커널 공간에서 실행, 성능 우선
2. 마이크로커널(L4·QNX) — 최소 기능만 커널에, 나머지는 사용자 공간 서버, 안전성 우선
3. 하이브리드 커널(macOS XNU·Windows NT) — 모놀리식 + 마이크로커널 절충
4. 커널 모듈(Linux LKM) — 재부팅 없이 드라이버·파일 시스템을 동적으로 로드·언로드
5. 엑소커널·유니커넬 — 클라우드·고성능 환경을 위한 새로운 설계 방향

#### 📌 1-4. 운영체제의 발전 역사
1. 배치 처리(1950s) — 천공 카드에 작업을 적어 일괄 제출, 순서대로 처리하며 대화형 입력 불가능
2. 시분할 시스템(1960s) — CTSS·Multics: CPU 시간을 짧게 나눠 여러 사용자가 동시에 쓰는 것처럼 느끼게 하는 시분할 기법 개발
3. Unix 탄생(1969) — Bell Labs의 Ken Thompson·Dennis Ritchie가 어셈블러 대신 C 언어로 이식 가능한 OS를 설계한 혁신
4. 개인용 PC OS(1981~1984) — MS-DOS(IBM PC)·Apple DOS·맥 OS System 1 등 단일 사용자 CLI 기반 OS의 대중화
5. GUI·멀티태스킹·인터넷 시대(1990s~) — Windows 95·macOS, 이후 모바일(Android·iOS)과 클라우드(Linux 컨테이너)로의 진화

#### 📌 1-5. 멀티유저 시스템의 개념과 구조
1. 시분할(Time-Sharing) — 하나의 CPU를 여러 터미널 사용자가 동시에 쓰는 것처럼 느끼게 하는 스케줄링 기법
2. 멀티유저 필수 구성 요소 — 계정(Account)·세션(Session)·파일 권한(Permission)·프로세스 소유권(UID/GID)의 4가지 격리 메커니즘
3. 터미널과 원격 로그인 — 과거 물리 터미널(tty) → Telnet → SSH로 이어지는 다중 동시 접속의 역사와 pts(가상 터미널) 개념
4. Unix 멀티유저 설계 철학 — root(UID 0)만이 시스템 자원을 제어하고, 일반 사용자와 권한 경계를 분리하는 최소 권한 원칙
5. 현대 클라우드 멀티테넌시 — OS의 멀티유저 개념이 컨테이너(네임스페이스)·VM(하이퍼바이저) 단위의 테넌트 격리로 진화한 과정

- **강의 내용**: OS 핵심 역할, 현대 OS 생태계 비교, 커널 구조 종류, OS 발전 역사, 멀티유저 시스템
- **실습 내용**: `uname -a`·`lsb_release -a`·`sw_vers`로 OS 버전 확인, `lsmod`로 Linux 커널 모듈 목록 조회, `who`·`w`·`last`로 현재 로그인 세션·접속 이력 확인
- **과제**: OS 발전 역사 연대표 작성(1950s~현재) + 본인 사용 OS의 커널 버전·멀티유저 설정 상태 확인 캡처 리포트

---

### 2주차
- **대주제**: 시스템 콜 — 소프트웨어가 OS에 요청하는 방법
- **세부학습목표**: 프로그램이 파일을 열거나 메모리를 할당할 때 내부적으로 OS에 무엇을 요청하는지, 시스템 콜의 흐름을 직접 추적한다.

#### 📌 2-1. 시스템 콜의 개념과 필요성
1. 시스템 콜 = 사용자 모드 프로그램이 커널 기능을 호출하는 유일한 공식 창구
2. 사용자 모드 ↔ 커널 모드 전환 — trap 명령어로 CPU 특권 레벨이 바뀌는 과정
3. 시스템 콜이 없다면 — 모든 프로그램이 하드웨어를 직접 제어하는 혼란
4. Linux 주요 시스템 콜 목록 — `open`·`read`·`write`·`close`·`fork`·`exec`·`mmap`·`socket`
5. `syscall` 번호 테이블 — Linux x86-64 시스템 콜 번호표와 각 콜의 의미

#### 📌 2-2. strace·dtruss로 시스템 콜 추적
1. `strace 명령어`(Linux) — 프로그램 실행 시 호출되는 모든 시스템 콜 실시간 출력
2. `strace cat /etc/hostname` 분석 — `openat` → `read` → `write` → `close` 흐름 읽기
3. `dtruss`(macOS) — DTrace 기반 시스템 콜 추적 도구
4. 시스템 콜 오버헤드 — 사용자 모드 ↔ 커널 모드 전환 비용이 성능에 미치는 영향
5. io_uring(Linux 5.1+) — 시스템 콜 오버헤드를 줄이는 비동기 I/O 인터페이스

#### 📌 2-3. 인터럽트와 이벤트 처리
1. 하드웨어 인터럽트 — 키보드·NIC·SSD가 CPU에 작업 완료를 알리는 비동기 신호
2. 소프트웨어 인터럽트(트랩) — 시스템 콜·예외·페이지 폴트를 처리하는 내부 인터럽트
3. IRQ(Interrupt Request) — 인터럽트 우선순위와 라우팅 방식
4. 인터럽트 핸들러(ISR) — 인터럽트 발생 시 커널이 실행하는 최우선 처리 함수
5. 인터럽트 vs 폴링 — CPU가 장치를 능동적으로 확인 vs 장치가 CPU를 호출하는 방식 비교

- **강의 내용**: 시스템 콜 개념·흐름, strace·dtruss 추적, 인터럽트 처리
- **실습 내용**: `strace python3 -c "open('/etc/hostname')"` 실행 → 시스템 콜 목록 분석
- **과제**: `strace ls -la`로 캡처한 시스템 콜 중 10개를 골라 각각의 역할 설명 제출

---

### 3주차
- **대주제**: 프로세스와 스레드 — 현대 멀티코어 환경의 실행 단위
- **세부학습목표**: 프로세스·스레드·코루틴의 차이를 명확히 이해하고, 멀티코어환경에서 병렬성을 어떻게 활용하는지 실습으로 체험한다.

#### 📌 3-1. 프로세스의 구조
1. 프로세스(Process) — 실행 중인 프로그램의 독립적 인스턴스 (메모리·파일 디스크립터·PID)
2. PCB(Process Control Block) — OS가 프로세스 상태를 관리하는 자료구조
3. 프로세스 상태 — Running·Ready·Blocked·Zombie 각 상태와 전환 조건
4. `fork()` — 현재 프로세스를 복제하여 자식 프로세스를 생성하는 UNIX 시스템 콜
5. `exec()` — 현재 프로세스 이미지를 새 프로그램으로 교체하여 실행

#### 📌 3-2. 스레드와 병렬 처리
1. 스레드(Thread) — 같은 프로세스의 메모리를 공유하는 경량 실행 단위
2. 멀티스레딩의 이점 — 멀티코어 CPU의 동시 실행, 응답성 향상
3. Python의 GIL(Global Interpreter Lock) — 멀티스레드를 써도 CPU 연산이 병렬화되지 않는 이유
4. Python `multiprocessing` vs `threading` — CPU-bound 작업 vs I/O-bound 작업 선택 기준
5. 사용자 스레드(Green Thread·Goroutine) vs 커널 스레드 — 경량화와 스케줄링 책임 위치

#### 📌 3-3. 코루틴과 비동기 I/O
1. 코루틴(Coroutine) — `async/await` 문법으로 I/O 대기 시간에 다른 작업을 실행하는 협력형 실행
2. Python `asyncio` — 단일 스레드 이벤트 루프 기반 비동기 프레임워크
3. Node.js 이벤트 루프 — 싱글 스레드 비동기 I/O로 수만 개 동시 연결을 처리하는 원리
4. `async def` vs `def` — 코루틴 함수와 일반 함수가 CPU 스케줄링에 미치는 차이
5. `ps aux` · `top` · `htop` — 실행 중인 프로세스 목록·CPU·메모리 사용량 실시간 확인

- **강의 내용**: 프로세스 구조, 스레드·멀티코어 병렬성, 코루틴·비동기 I/O
- **실습 내용**: Python으로 멀티스레드 vs 멀티프로세스 CPU 연산 속도 비교 실험, htop 분석
- **과제**: CPU-bound(소수 계산) 작업을 스레드·프로세스·asyncio 각 방법으로 구현하고 속도 비교 리포트

---

### 4주차
- **대주제**: 현대 CPU 스케줄링 — 멀티코어·이종코어 환경의 OS 스케줄러
- **세부학습목표**: OS 스케줄러가 멀티코어·P코어·E코어 환경에서 어떻게 작업을 배분하는지 이해하고, 실시간 스케줄링과 리눅스 CFS의 원리를 파악한다.

#### 📌 4-1. 스케줄링의 목표와 지표
1. 처리량(Throughput) vs 응답시간(Latency) — 서버와 데스크톱 OS의 스케줄링 목표 차이
2. 컨텍스트 스위칭(Context Switching) — 프로세스 교체 시 레지스터·PCB를 저장·복원하는 오버헤드
3. 우선순위(Priority) — nice 값(-20~19)과 실시간 스케줄링 클래스(SCHED_FIFO·SCHED_RR)
4. CPU 친화도(CPU Affinity) — 특정 스레드를 특정 코어에 고정하여 캐시 효율을 높이는 방법
5. 스로틀링(Throttling) — 온도·전력 한계에 따라 OS가 클록을 낮추는 자동 조절

#### 📌 4-2. Linux CFS와 현대 스케줄러
1. CFS(Completely Fair Scheduler) — Linux의 기본 스케줄러, vruntime 기준 공정한 시간 배분
2. EEVDF(Earliest Eligible Virtual Deadline First) — Linux 6.6+ 새 스케줄러, latency 개선
3. 이종코어 스케줄링(Intel Thread Director) — P코어·E코어에 작업 유형별로 자동 배분
4. NUMA-aware 스케줄링 — 멀티소켓 서버에서 메모리 로컬리티 고려한 코어 배분
5. cgroups v2 — 프로세스 그룹별로 CPU 사용 비율을 제한하는 리눅스 자원 제어 메커니즘

#### 📌 4-3. 실시간 OS와 임베디드 스케줄링
1. RTOS(Real-Time OS) — 정해진 마감 시간 안에 반드시 응답하는 결정론적 스케줄링
2. RTOS 사례 — FreeRTOS(IoT), VxWorks(항공), QNX(자동차 인포테인먼트)
3. 리눅스에서 실시간 응용 — `SCHED_FIFO` + `PREEMPT_RT` 패치 적용 환경
4. 지연 측정 — `cyclictest`로 리눅스 실시간 응답 지연(latency jitter) 측정
5. 자율주행·드론 OS — 안전 임계 시스템에서 OS 선택이 중요한 이유

- **강의 내용**: 스케줄링 목표와 지표, Linux CFS·EEVDF, 이종코어·RTOS 스케줄링
- **실습 내용**: `nice renice`로 프로세스 우선순위 변경 → `chrt`로 SCHED_FIFO 실행 체험
- **과제**: Python CPU-bound 프로세스의 nice 값 변경 전·후 스케줄링 시간 변화 관찰 리포트

---

### 5주차
- **대주제**: 동기화와 공유 자원 — 현대 병렬 프로그래밍의 안전망
- **세부학습목표**: 멀티코어 환경에서 공유 자원을 안전하게 접근하기 위한 동기화 메커니즘을 이해하고, Python과 Go에서 실제로 활용하는 방법을 체험한다.

#### 📌 5-1. 경쟁 조건과 임계 구역
1. 경쟁 조건(Race Condition) — 두 스레드가 동시에 같은 자원을 수정할 때 발생하는 버그
2. 임계 구역(Critical Section) — 한 번에 하나의 스레드만 실행되어야 하는 코드 영역
3. 원자 연산(Atomic Operation) — CPU 명령 단위로 중간 상태 없이 완결되는 연산
4. `threading.Lock`(Python) — `acquire()`·`release()`로 임계 구역 보호
5. 경쟁 조건 재현 실험 — 락 없이 카운터를 멀티스레드로 증가시켜 결과 불일치 체험

#### 📌 5-2. 현대 동기화 도구
1. 뮤텍스(Mutex) vs 세마포어(Semaphore) — 1개 자원 vs N개 자원 접근 제어 차이
2. 읽기-쓰기 락(RWLock) — 여러 독자(Reader)와 단일 작가(Writer) 동시 처리 최적화
3. 조건 변수(Condition Variable) — 특정 조건이 충족될 때까지 스레드를 대기시키는 메커니즘
4. Go의 채널(Channel) — 공유 메모리 대신 메시지 전달로 안전하게 통신하는 동시성 패턴
5. 락 프리(Lock-Free) 자료구조 — CAS(Compare-And-Swap) 원자 연산 기반 무잠금 설계

#### 📌 5-3. 교착 상태(Deadlock) 이해와 현대적 회피
1. 교착 상태 4가지 필요 조건 — 상호 배제·점유 대기·비선점·순환 대기
2. 교착 상태 실제 사례 — 데이터베이스 트랜잭션 잠금, 멀티스레드 파일 접근에서의 데드락
3. 락 순서 일관성(Lock Ordering) — 항상 동일한 순서로 락을 획득하여 순환 대기 방지
4. 타임아웃(Timeout) 기반 회피 — 락 획득에 시간 제한을 두어 데드락 탈출
5. `asyncio`와 데드락 — I/O 기반 비동기 코드에서 데드락이 거의 발생하지 않는 이유

- **강의 내용**: 경쟁 조건·임계 구역·원자 연산, 현대 동기화 도구, 교착 상태와 회피
- **실습 내용**: Python Lock 없이 카운터 증가 → 데이터 불일치 재현 → Lock 추가 후 수정 확인
- **과제**: 철학자 식사 문제(Dining Philosophers)를 Python으로 구현하고 데드락 발생·회피 방법 제출

---

### 6주차
- **대주제**: 현대 메모리 관리 — 가상 메모리·mmap·메모리 보안
- **세부학습목표**: 현대 OS가 메모리를 가상화하여 프로세스를 격리하는 원리를 이해하고, mmap·huge page·ASLR 등 현대 메모리 관리 기술을 학습한다.

#### 📌 6-1. 가상 메모리와 페이징
1. 가상 주소 공간 — 모든 프로세스가 독립적인 0~최대 주소를 가지는 환상
2. 페이지 테이블 — 가상 주소를 물리 주소로 변환하는 OS 관리 자료구조
3. TLB(Translation Lookaside Buffer) — 페이지 테이블 탐색 가속을 위한 CPU 내장 캐시
4. 페이지 폴트(Page Fault) — 요청한 페이지가 물리 메모리에 없을 때 OS가 개입하는 과정
5. 요구 페이징(Demand Paging) — 실제 접근 시점에만 물리 페이지를 할당하여 메모리 효율화

#### 📌 6-2. 현대 메모리 관리 기술
1. `mmap()` — 파일 또는 익명 메모리를 가상 주소 공간에 직접 매핑하는 고성능 I/O
2. Huge Page(2MB·1GB) — TLB 미스를 줄여 DB·ML 프레임워크 성능을 향상하는 대형 페이지
3. ASLR(Address Space Layout Randomization) — 메모리 레이아웃을 무작위화하여 공격 방어
4. Copy-on-Write(CoW) — `fork()` 후 부모·자식 프로세스가 실제 수정이 일어날 때만 메모리를 복사
5. OOM Killer(Out-of-Memory Killer) — 메모리 부족 시 OS가 프로세스를 강제 종료하는 메커니즘

#### 📌 6-3. 메모리 진단 도구
1. `free -h`(Linux) — 총 RAM·사용·여유·버퍼·캐시 현황 한눈에 확인
2. `vmstat 1`(Linux) — 1초 간격으로 메모리 스왑·페이지 폴트·컨텍스트 스위치 실시간 출력
3. `smem`·`/proc/pid/maps` — 특정 프로세스의 세부 메모리 매핑 분석
4. `Activity Monitor`(macOS)·`Resource Monitor`(Windows) — GUI 기반 메모리 사용량 분석
5. Valgrind·ASan(Address Sanitizer) — C/C++ 코드의 메모리 누수·버퍼 오버플로우 탐지

- **강의 내용**: 가상 메모리·페이징·페이지 폴트, mmap·Huge Page·ASLR·CoW, 메모리 진단 도구
- **실습 내용**: Python `mmap`으로 대용량 파일 매핑 후 처리 속도 비교, `/proc/meminfo` 분석
- **과제**: 메모리 사용이 많은 프로세스를 `smem`으로 분석하고 메모리 구성(코드·힙·스택·매핑) 설명

---

### 7주차
- **대주제**: 파일 시스템 — 구조·역사·현대 파일 시스템 총정리
- **세부학습목표**: 파일 시스템의 내부 자료 구조를 이해하고, 플로피·HDD 시대부터 현대 NVMe SSD까지 저장 미디어와 파일 시스템이 함께 진화한 역사를 파악한다.

#### 📌 7-1. 파일 시스템의 핵심 구조
1. inode — 파일 이름이 아닌 번호로 파일 메타데이터(권한·크기·타임스탬프·블록 위치)를 저장
2. 디렉토리 엔트리 — 파일 이름 → inode 번호 매핑 테이블
3. 하드 링크 vs 심볼릭 링크 — inode를 공유(하드) vs 경로를 가리키는 경량 포인터(심볼릭)
4. 블록(Block)·클러스터(Cluster) — 파일 시스템이 데이터를 할당하는 최소 단위, 내부 단편화가 발생하는 이유
5. 마운트(Mount) — 파일 시스템을 디렉토리 트리에 연결하는 원리 (`/etc/fstab`·`mount` 명령어)

#### 📌 7-2. 저장 미디어의 역사 — 플로피·HDD·SSD
1. 자기 테이프(1950s~) — 순차 접근 전용, 릴(Reel) 단위 교체, 현재도 LTO 테이프로 장기 냉동 백업에 사용
2. 플로피 디스크(1970s~2000s) — 자기 코팅 유연 원판, 8인치(1971) → 5.25인치(1.2MB) → 3.5인치(1.44MB) 소형화, USB에 밀려 소멸
3. HDD(하드디스크, 1956~현재) — 금속 플래터(Platter) 회전, 자기 헤드(Read/Write Head)와 액추에이터 암(Actuator Arm)의 물리 구조
4. HDD 주소 체계 진화 — CHS(Cylinder-Head-Sector, 실린더·헤드·섹터) → LBA(Logical Block Addressing, 논리 블록 번호) 추상화 전환
5. SSD와 NVMe의 등장 — NAND Flash로 물리 이동 부품 제거, 충격 저항·속도 혁명, HDD 대비 랜덤 접근 지연 100배 이상 단축

#### 📌 7-3. 레거시 파일 시스템 — FAT·exFAT와 파티션 구조
1. FAT(File Allocation Table) — 파일이 저장된 클러스터 번호 목록(연결 리스트), FAT12(플로피)·FAT16(초기 HDD)·FAT32(USB·SD카드) 진화
2. FAT32의 한계 — 단일 파일 최대 4GB, 볼륨 최대 2TB, 저널링 없어 전원 차단 시 파일 시스템 손상 위험
3. exFAT — SD카드·USB 플래시용 경량 현대 포맷, 4GB 파일 제한 없음·크로스 플랫폼(Win·Mac·Linux) 표준
4. MBR(Master Boot Record) — 디스크 첫 512바이트에 부트로더와 파티션 테이블 저장, 최대 4개 파티션·2TB 볼륨 한계
5. GPT(GUID Partition Table) — UEFI 기반 현대 표준, 최대 128개 파티션·9.4ZB 볼륨, `fdisk`·`gdisk`·`diskutil` 도구로 확인

#### 📌 7-4. 현대 파일 시스템 비교
1. ext4(Linux 표준) — 저널링, 최대 16TB 파일·1EB 볼륨, 지연 할당(Delayed Allocation)으로 쓰기 성능 향상
2. APFS(Apple) — Copy-on-Write, 스냅샷, 암호화 내장, SSD 정렬 최적화, macOS Monterey 이후 Time Machine 기본
3. NTFS(Windows) — 저널링, ACL 세분화 권한, 압축·암호화 내장, 4KB 클러스터 기준 설계
4. ZFS(OpenZFS) — 체크섬 기반 데이터 무결성·RAID-Z·자동 비트 오류 복구·무한 스냅샷, TrueNAS·FreeBSD 표준
5. Btrfs(Linux) — CoW·서브볼륨·스냅샷·인라인 압축, RHEL 9·SUSE·Fedora 기본 파일 시스템으로 확산

#### 📌 7-5. 저널링·CoW·스냅샷과 복구 원리
1. 저널링(Journaling) — 데이터 쓰기 전 저널(Journal)에 변경 예정 사항을 기록, 전원 차단 후 재마운트 시 미완료 작업 복구
2. CoW(Copy-on-Write) — 기존 블록을 덮어쓰지 않고 새 위치에 기록한 뒤 메타데이터 원자적 교체, 충돌 안전·스냅샷 기반
3. 스냅샷(Snapshot) — CoW 덕분에 특정 시점의 메타데이터 루트만 저장하면 전체 파일 시스템 상태를 즉시 보존 가능
4. APFS 스냅샷 vs ZFS 스냅샷 — macOS Time Machine(APFS)·TrueNAS(ZFS) 동작 비교, 스냅샷 복원 실습
5. ZFS 자동 비트 복구 — 읽기 시 체크섬 불일치 감지 → RAID-Z의 패리티로 자동 교정, 사일런트 데이터 손상(Silent Corruption) 방지

- **강의 내용**: inode·디렉토리·블록 구조, 플로피·HDD·SSD 역사, FAT·exFAT·MBR·GPT, ext4·APFS·NTFS·ZFS·Btrfs 비교, 저널링·CoW·스냅샷
- **실습 내용**: `stat 파일명`으로 inode 정보, `df -hT`로 파일 시스템 목록, `fdisk -l` / `diskutil list`로 파티션 구조 확인
- **과제**: FAT32·exFAT·NTFS·ext4·APFS·ZFS 비교표(최대 파일 크기·저널링·CoW·플랫폼) 작성 + HDD CHS 주소체계를 직접 계산하는 연습 문제 풀이 제출

---

### 8주차
- **대주제**: 중간고사 (평가 주간)
- **세부학습목표**: 1~7주차 (OS 구조·시스템 콜·프로세스·스케줄링·동기화·메모리·파일 시스템) 전반기 성취도 측정
- **강의 내용**: 이론 필기 (시스템 콜 흐름·파일 시스템 비교·스케줄링 지표) + `strace`·`top`·`stat` 실기
- **실습 내용**: 없음
- **과제**: 없음

---

### 9주차
- **대주제**: 장치 관리와 I/O — 현대 드라이버 모델과 비동기 I/O
- **세부학습목표**: OS가 USB·NVMe·GPU 등 다양한 장치를 추상화하여 관리하는 드라이버 모델과 현대 비동기 I/O 인터페이스를 이해한다.

#### 📌 9-1. 장치 드라이버 모델
1. 장치 드라이버 — 하드웨어와 OS 커널 사이의 번역기 역할을 하는 소프트웨어 계층
2. Linux 장치 유형 — 블록 장치(SSD·HDD), 문자 장치(키보드·터미널), 네트워크 장치
3. `/dev` 디렉토리 — Linux에서 모든 장치를 파일로 추상화한 장치 파일 목록 (`/dev/sda`, `/dev/nvme0n1`)
4. `udev` — USB 연결 시 드라이버 자동 로드·장치 파일 자동 생성을 처리하는 Linux 데몬
5. `lsblk`·`lsusb`·`lspci` — 블록 장치·USB·PCIe 장치 목록 확인 명령어

#### 📌 9-2. DMA와 고속 I/O
1. DMA(Direct Memory Access) — CPU를 거치지 않고 장치가 직접 RAM에 데이터를 전송하는 메커니즘
2. NVMe DMA 동작 — CPU 개입 없이 SSD가 RAM에 데이터를 바로 쓰는 경로
3. `io_uring`(Linux 5.1+) — 시스템 콜 없이 I/O 작업을 큐에 제출하는 초저지연 비동기 I/O
4. SPDK(Storage Performance Development Kit) — 커널 우회 방식으로 NVMe를 직접 제어
5. GPU 직접 접근(GPUDirect) — NIC·SSD가 GPU 메모리를 CPU RAM 없이 직접 채우는 기술

#### 📌 9-3. I/O 스케줄링 현황
1. Linux I/O 스케줄러 — mq-deadline(SSD 기본)·BFQ(처리량 우선)·None(NVMe 최신 표준)
2. NVMe 큐 모델(MQ) — 단일 큐 SATA vs 64K 큐 NVMe의 병렬 I/O 처리 차이
3. 불연속 I/O vs 순차 I/O — SSD는 랜덤 접근 비용이 HDD와 달라 스케줄러 역할 변화
4. `iostat -x 1`(Linux) — I/O 장치별 읽기·쓰기 속도·대기 시간 실시간 모니터링
5. Windows StorNVMe 드라이버 vs 오픈소스 NVMe 드라이버 비교

- **강의 내용**: 장치 드라이버 모델, DMA·io_uring·GPUDirect, I/O 스케줄링 현황
- **실습 내용**: `lsblk`·`lsusb`·`lspci` 장치 목록 확인, `iostat -x`로 SSD I/O 성능 실시간 관찰
- **과제**: `/dev` 디렉토리 주요 장치 파일 목록 조사 + io_uring이 기존 시스템 콜 방식보다 빠른 이유 설명 제출

---

### 10주차
- **대주제**: 컨테이너 — Docker와 Linux 네임스페이스·cgroup
- **세부학습목표**: Docker 컨테이너가 VM과 어떻게 다른지 Linux 커널 기능(네임스페이스·cgroup)으로 설명하고, 실제 컨테이너를 만들고 실행한다.

#### 📌 10-1. 컨테이너의 정의와 등장 배경
1. "내 컴퓨터에선 됐는데요" 문제 — 환경 불일치가 컨테이너를 탄생시킨 핵심 동기
2. 가상 머신(VM) vs 컨테이너 — 하이퍼바이저+Guest OS 포함 vs 커널 공유·프로세스 수준 격리
3. Docker 아키텍처 — Docker Daemon·Client·Registry·Image·Container·Volume
4. OCI(Open Container Initiative) — 컨테이너 이미지·런타임 표준으로 Docker 종속 탈피
5. containerd·Podman — Docker 없이 컨테이너를 실행하는 대안 런타임 생태계

#### 📌 10-2. Linux 네임스페이스와 cgroup
1. 네임스페이스(Namespace) — PID·Mount·Network·IPC·UTS·User 6가지로 자원 뷰를 격리
2. PID 네임스페이스 — 컨테이너 내부에서 PID 1번이 따로 존재하는 이유
3. Network 네임스페이스 — 컨테이너마다 독립적인 가상 네트워크 인터페이스를 가지는 원리
4. cgroups v2 — CPU·메모리·I/O·네트워크 대역폭을 컨테이너 단위로 제한하는 커널 기능
5. `docker run --cpus 0.5 --memory 256m` — cgroup 제한이 실제로 컨테이너에 적용되는 방법

#### 📌 10-3. Docker 실전 활용
1. `Dockerfile` 작성 — `FROM`·`COPY`·`RUN`·`EXPOSE`·`CMD` 핵심 지시어
2. `docker build`·`docker run`·`docker ps`·`docker exec` — 이미지 빌드에서 컨테이너 접속까지
3. Docker 레이어 캐시 — 이미지 빌드 시 변경된 레이어만 재빌드하는 캐시 동작 원리
4. Docker Compose — 멀티 컨테이너 서비스(앱+DB+캐시)를 YAML로 정의하고 한 번에 실행
5. Docker Hub·GHCR — 이미지를 공유하는 컨테이너 레지스트리 활용법

- **강의 내용**: VM vs 컨테이너, Linux 네임스페이스·cgroup 원리, Docker 실전
- **실습 내용**: Python 웹 앱을 Dockerfile로 컨테이너화 → 빌드 → 실행 → 포트 매핑으로 브라우저 접속
- **과제**: Dockerfile로 본인 Python 프로젝트 컨테이너 이미지 작성 + Docker Hub에 push한 URL 제출

---

### 11주차
- **대주제**: 가상화와 클라우드 OS — 하이퍼바이저·Kubernetes 개요
- **세부학습목표**: 현대 클라우드 인프라의 기반인 가상화 기술(Type1·Type2 하이퍼바이저)과 컨테이너 오케스트레이션(Kubernetes)의 개념을 이해한다.

#### 📌 11-1. 하이퍼바이저 유형과 사례
1. Type 1 하이퍼바이저(Bare-metal) — 하드웨어 위에 직접 실행, VMware ESXi·Microsoft Hyper-V·Xen
2. Type 2 하이퍼바이저(Hosted) — 호스트 OS 위에서 실행, VMware Workstation·VirtualBox·Parallels
3. KVM(Kernel-based Virtual Machine) — Linux 커널 자체가 Type 1 하이퍼바이저로 동작하는 구조
4. WSL2(Windows Subsystem for Linux 2) — Hyper-V 기반 경량 VM으로 Linux 커널 실행
5. Apple Virtualization Framework — macOS에서 Linux·Windows를 경량화하여 실행하는 Apple 공식 API

#### 📌 11-2. Kubernetes 기초 개념
1. Kubernetes(K8s) — 컨테이너를 수천 대 서버에서 자동 배포·스케일링·복구하는 오케스트레이터
2. Pod — 하나 이상의 컨테이너를 함께 묶어 배포하는 K8s의 최소 실행 단위
3. Service·Ingress — Pod에 안정적인 네트워크 진입점(IP·도메인)을 제공하는 K8s 리소스
4. Deployment·ReplicaSet — Pod 개수를 자동 유지·롤링 업데이트하는 선언적 배포 방식
5. kubectl 기초 — `kubectl get pods`·`kubectl describe`·`kubectl logs` 실무 명령어

#### 📌 11-3. 클라우드 네이티브 OS 개념
1. 불변 인프라(Immutable Infrastructure) — 서버를 수정하지 않고 새 이미지로 교체하는 운영 철학
2. CoreOS·Flatcar — 컨테이너 전용으로 설계된 최소화 Linux OS
3. Serverless(서버리스) — OS·서버 관리 없이 함수 단위로 코드를 실행하는 AWS Lambda·Cloud Functions
4. eBPF(Extended Berkeley Packet Filter) — 커널 수정 없이 네트워크·성능·보안을 실시간 관찰·제어
5. 서비스 메시(Service Mesh) — Istio·Linkerd로 마이크로서비스 간 트래픽·보안·관찰성 관리

- **강의 내용**: Type1·Type2 하이퍼바이저, KVM·WSL2, Kubernetes 기초, 클라우드 네이티브 OS
- **실습 내용**: Minikube 또는 K3s로 로컬 K8s 클러스터 실행 → Pod 배포 → `kubectl` 기본 명령어 체험
- **과제**: Docker Compose로 만든 앱을 K8s Deployment·Service YAML로 변환하여 Minikube에 배포 제출

---

### 12주차
- **대주제**: 현대 OS 보안 — 권한·SELinux·eBPF·컨테이너 보안
- **세부학습목표**: 현대 OS에서 보안이 어떻게 구현되는지 Linux 권한 모델부터 컨테이너 런타임 보안까지 이해한다.

#### 📌 12-1. Linux 권한 모델과 PAM
1. UID·GID·파일 권한(rwx) — 소유자·그룹·기타에 대한 읽기·쓰기·실행 권한 체계
2. `chmod`·`chown`·`umask` — 권한·소유자 변경과 기본 마스크 설정 명령어
3. SetUID·SetGID 비트 — 실행 시 파일 소유자 권한으로 실행되는 특수 권한 (`passwd` 명령 사례)
4. PAM(Pluggable Authentication Modules) — 로그인·인증 정책을 모듈로 유연하게 교체하는 시스템
5. `sudo`·`visudo` — 특정 명령에만 root 권한을 부여하는 안전한 권한 위임 설정

#### 📌 12-2. SELinux·AppArmor·seccomp
1. MAC(Mandatory Access Control) — 기존 DAC(임의접근제어) 위에 강제 정책을 추가하는 보안 계층
2. SELinux — 프로세스·파일에 보안 레이블 부착, 정책에 명시적으로 허용된 동작만 실행(Red Hat·Android)
3. AppArmor — 경로 기반의 단순화된 MAC, Ubuntu·SUSE 기본 (Docker 컨테이너 프로파일)
4. seccomp(secure computing mode) — 컨테이너 내 프로세스가 사용할 수 있는 시스템 콜을 화이트리스트로 제한
5. Docker의 기본 보안 기능 — ReadOnly 루트 파일 시스템·비특권 모드(`--user`)·Capabilities 제거

#### 📌 12-3. eBPF 기반 현대 보안 관찰
1. eBPF(Extended BPF) — 커널 수정·모듈 삽입 없이 커널 이벤트를 실시간 감시·제어하는 기술
2. Cilium — eBPF 기반 Kubernetes 네트워크 정책·보안·가시성 플랫폼
3. Falco — 컨테이너 내 이상 동작(파일 열기·쉘 실행 등)을 eBPF로 실시간 탐지하는 CNCF 프로젝트
4. 공급망 보안(Supply Chain Security) — 컨테이너 이미지의 취약점 스캔 (Trivy·Snyk)
5. 제로 트러스트(Zero Trust) — 네트워크 위치와 무관하게 모든 접근을 재인증하는 현대 보안 철학

- **강의 내용**: Linux 권한 모델·PAM, SELinux·AppArmor·seccomp, eBPF 기반 보안 관찰
- **실습 내용**: Trivy로 Docker 이미지 취약점 스캔, `strace`로 비정상 시스템 콜 패턴 탐지 실습
- **과제**: 본인이 만든 Docker 이미지를 Trivy로 스캔한 결과 분석 + 취약점 1개 수정 과정 제출

---

### 13주차
- **대주제**: 성능 분석과 현대 OS 관찰성 — perf·eBPF·flame graph
- **세부학습목표**: 현대 OS 관찰(Observability) 도구로 시스템 병목을 찾아내고, 코드 또는 설정 변경으로 성능을 개선하는 엔지니어링 프로세스를 체험한다.

#### 📌 13-1. 시스템 성능 모니터링 도구
1. `top`·`htop`·`btop` — CPU·메모리·스왑·부하 실시간 대시보드
2. `vmstat 1` — 메모리·스왑·IO·컨텍스트 스위치·CPU 사용률 1초 간격 스트리밍
3. `iostat -x 1` — 장치별 읽기·쓰기·대기 시간·처리량 실시간 모니터링
4. `netstat -s`·`ss -tunp` — 소켓·TCP 상태·포트별 연결 현황 확인
5. `sar`(System Activity Reporter) — 시간 구간별 CPU·메모리·I/O 사용 이력 기록·조회

#### 📌 13-2. perf와 Flame Graph
1. `perf stat` — CPU 사이클·캐시 미스·브랜치 예측 실패를 하드웨어 카운터로 측정
2. `perf record`·`perf report` — 프로그램 실행 중 함수별 CPU 사용 비율 샘플링
3. Flame Graph — 함수 호출 스택과 시간 비율을 불꽃 모양 그래프로 시각화
4. `bpftrace` — eBPF 기반으로 커널·사용자 공간 이벤트를 원라이너로 추적
5. 병목 유형 분류 — CPU-bound·I/O-bound·Memory-bound·Network-bound 구분 진단법

#### 📌 13-3. 클라우드 환경 관찰성
1. Prometheus + Grafana — 메트릭 수집·시각화 표준 오픈소스 스택
2. OpenTelemetry — 트레이스·메트릭·로그를 표준화하여 수집하는 CNCF 관찰성 프레임워크
3. 분산 추적(Distributed Tracing) — 마이크로서비스 요청이 여러 서버를 거치는 경로 추적 (Jaeger·Zipkin)
4. Linux OOM 이벤트 분석 — `dmesg | grep -i oom`으로 OOM Killer 발동 이력 확인
5. SLO/SLA/SLI — 서비스 레벨 목표·협약·지표: 클라우드 운영의 기준 측정 체계

- **강의 내용**: top·vmstat·iostat 모니터링, perf·Flame Graph, Prometheus·OpenTelemetry 개요
- **실습 내용**: CPU 부하 스크립트 실행 → `perf stat`으로 캐시 미스 측정 → Flame Graph 생성
- **과제**: 본인 시스템에서 부하 테스트 후 Flame Graph 생성 + 병목 유형 분류 및 개선 방법 리포트

---

### 14주차
- **대주제**: 기말고사 및 종합 발표 — 현대 OS 지식의 통합
- **세부학습목표**: 한 학기 동안 학습한 시스템 콜·프로세스·스케줄링·메모리·파일 시스템·컨테이너·보안·관찰성을 통합하여 실제 시스템 설계 시나리오를 발표한다.

#### 📌 14-1. 전체 범위 복습
1. 시스템 콜 → 프로세스 생성 → 스케줄러 배분 → 메모리 할당 → 파일 I/O 완전한 흐름
2. 컨테이너의 격리 원리 — 네임스페이스·cgroup·seccomp·AppArmor의 역할 분담
3. ZFS vs ext4 — 어느 상황에서 어떤 파일 시스템을 선택하는가
4. eBPF 기반 관찰성 도구의 공통 원리와 차이
5. 현대 OS 보안의 계층 구조 — DAC → MAC → 컨테이너 샌드박스 → eBPF 감시

#### 📌 14-2. 팀별 시스템 설계 발표
1. 주제 선택 — "AI 서빙 서버 설계" / "마이크로서비스 컨테이너 배포" / "고성능 데이터 파이프라인" / "IoT 엣지 OS 구성" 중 택1
2. OS 관점의 설계 요소 — 스케줄링 정책·메모리 설정·파일 시스템·컨테이너·보안 레이어
3. 병목 예측 — 선택한 시나리오에서 CPU·메모리·I/O·네트워크 중 어디가 먼저 포화될지 분석
4. 모니터링 계획 — 어떤 지표를 Prometheus로 수집하고 어떤 임계값에서 경보를 울릴지
5. 동료 피어 리뷰 + 교수 최종 피드백

#### 📌 14-3. 다음 단계 안내
1. 이번 학기 핵심 키워드 셀프 점검표 완성
2. 인프라·Site Reliability Engineering(SRE) 직군 진입 로드맵 안내 (LFCS·CKA 자격증)
3. Linux Foundation·Red Hat 공식 학습 자료 소개
4. 오픈소스 기여 입문 — Linux 커널 패치·Docker 이슈 리포팅·CNCF 참여
5. "한 학기 후 내가 이해하게 된 것" 개인 회고

- **강의 내용**: 전체 복습, 팀별 시스템 설계 발표
- **실습 내용**: 팀 발표 + 교수 라이브 질의응답
- **과제**: 최종 시스템 설계 문서(도식+설계 의사결정 이유) + 개인 학습 회고 제출

---

## 4. 평가 방식

| 항목 | 비율 | 설명 |
|------|------|------|
| 출석 | 10% | 성실한 참여 |
| 주간 과제 | 25% | 실습 실험·도구 분석·컨테이너 구성 리포트 |
| 중간고사 | 30% | 1~7주차: 시스템 콜·프로세스·스케줄링·메모리·파일 시스템 이론+실기 |
| 기말고사 | 35% | 9~13주차: 장치·컨테이너·가상화·보안·관찰성 + 팀 시스템 설계 발표 |

---

## 5. 교수자 유의사항

- **현대 도구 중심 실습**: `strace`·`htop`·`perf`·`docker`·`kubectl`을 매주 직접 사용하는 실습이 핵심입니다. OS 이론만으로는 체감이 어렵습니다.
- **컨테이너가 VM 아닌 이유 강조**: 학생들이 "Docker = 가상머신"으로 이해하는 것이 가장 흔한 오개념입니다. 10주차에서 네임스페이스·cgroup 실습으로 직접 확인하게 하세요.
- **고전 알고리즘 비중 최소화**: FCFS·SJF 등 고전 스케줄링 알고리즘은 개념 언급으로 한정하고, Linux CFS·EEVDF·이종코어 스케줄링에 시간을 더 배분하세요.
- **클라우드 연결 고리 항상 제시**: AWS EC2가 결국 KVM 기반 VM이며, EKS가 결국 Kubernetes라는 것을 명시적으로 연결하면 실무 동기를 높일 수 있습니다.
