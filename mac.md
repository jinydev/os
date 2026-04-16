# 맥(macOS) 개발 프레임워크 강의계획서

## 1. 교과목 개요

- **과목 소개**: macOS는 전 세계 실무 개발자들의 사실상 표준(De-facto Standard) 데스크톱 환경입니다. 본 과목은 단순한 GUI 사용법을 넘어, Unix(Darwin) 기반 시스템으로서의 본질을 이해하고 터미널과 패키지 관리자를 통해 전문가 수준의 백엔드/프론트엔드 통합 개발 환경을 구축하는 방법을 다룹니다.
- **학습 목표**: Homebrew를 통해 모든 종속성을 설치 및 통제하고, PHP/Node.js/Python/Java 멀티 버전을 관리하며, Nginx와 MySQL/PostgreSQL을 백그라운드 서비스로 다룰 수 있는 풀스택 로컬 랩(Local Lab) 환경을 구축한다.

---

## 2. 14주 주차별 강의계획

---

### 1주차
- **대주제**: macOS의 본질과 기원 — Darwin과 Unix
- **세부학습목표**: macOS가 어떻게 BSD Unix 호환 시스템이 되었는지 아키텍처를 이해하고, 개발자 진영에서 대세가 된 이유를 파악한다.

#### 📌 1-1. NeXTSTEP과 OS X의 역사
1. 스티브 잡스와 NeXT — 객체지향 OS의 탄생
2. Mach 마이크로커널과 FreeBSD 유저랜드의 결합
3. Darwin 아키텍처 — XNU 커널의 구조적 이해
4. 개발자 생태계 장악 — 네이티브 터미널과 상용 GUI의 완벽한 결합

#### 📌 1-2. 기본 조작과 단축키 해부
1. Command(⌘), Option(⌥), Control(⌃) 키의 철학 차이
2. 텍스트 에디팅 시스템 단축키 (Emacs 바인딩)
3. Spotlight와 Alfred — 생산성을 극대화하는 런처 시스템
4. 가상 데스크톱(Mission Control) 기반 멀티태스킹 

---

### 2주차
- **대주제**: 터미널과 셸 스크립팅 — zsh 완벽 제어
- **세부학습목표**: 기본 셸인 zsh의 특성을 파악하고, 터미널 생산성을 극대화하는 `oh-my-zsh` 플러그인 생태계를 구축한다.

#### 📌 2-1. 터미널 환경 해부
1. 터미널 에뮬레이터 기본 — Terminal.app vs iTerm2
2. bash에서 zsh로의 전환 — Apple이 셸을 바꾼 이유
3. `.zshrc` 와 `.zprofile` — 환경 변수 파일의 호출 순서
4. `PATH`의 이해 — 명령어가 어디서 실행되는가

#### 📌 2-2. 생산성 플러그인 (Oh-My-Zsh)
1. 기본 환경 세팅 — 테마(Agnoster, Powerlevel10k) 적용
2. auto-suggestions, syntax-highlighting 플러그인 연동
3. 디렉토리 이동 최적화 (`z`, `fzf`)
4. Alias 커스터마이징 전략

---

### 3주차
- **대주제**: 패키지 관리자 혁명 — Homebrew 아키텍처
- **세부학습목표**: 애플 생태계에 없는 오픈소스 컴파일 도구를 체계적으로 공급해 주는 Homebrew의 원리를 이해한다.

#### 📌 3-1. Homebrew 시스템의 작동 원리
1. 왜 AppStore 대신 Homebrew인가?
2. `Cellar` 디렉토리와 심볼릭 링크(Symlink)의 마법
3. Ruby 스크립트로 동작하는 패키지 설치 메커니즘
4. ARM (Apple Silicon) 시대의 Homebrew 경로 변경 (`/opt/homebrew`)

#### 📌 3-2. Brew Cask — GUI 앱의 명령어화
1. `brew cask` — Chrome, VSCode, Slack 까지 명령어로
2. 랩탑 자동화 셋업 스크립트 작성 (Brewfile 연동)
3. 오래된 캐시 비우기 및 의존성 문제 복구 (`brew doctor`)
4. 컴파일 툴체인(Xcode Command Line Tools)의 연관성

---

### 4주차
- **대주제**: 멀티 버전 매니저 1 — Python과 Node.js
- **세부학습목표**: 버전 충돌로 인한 패닉을 방지하기 위해, 사용자 공간에서 언어 버전을 동적으로 교체하는 툴링을 도입한다.

#### 📌 4-1. Node.js NVM / FNM 관리체계
1. npm의 전역(Global) 설치 오염 문제
2. NVM(Node Version Manager) 구조
3. Rust 기반 초고속 매니저 FNM (Fast Node Manager) 셋업
4. `.nvmrc`로 프로젝트별 노드 버전 자동 스위칭

#### 📌 4-2. Python Pyenv와 가상환경
1. 맥 기본 설치 Python의 한계와 사용 금지 이유
2. `pyenv` 셋업 — 껍데기(shim)를 통한 버전 스위칭
3. `venv` 모듈로 격리된 라이브러리 사이트 만들기
4. Poetry 툴링 소개

---

### 5주차
- **대주제**: 멀티 버전 매니저 2 — PHP, Ruby, Java
- **세부학습목표**: 고전적 엔터프라이즈 및 스크립트 언어들의 버전 관리 기법(rbenv, shivam)을 익힌다.

#### 📌 5-1. PHP 개발 환경 세팅
1. PHP-FPM 구조와 Nginx 연동 체계 이해
2. `shivam/php` (또는 수동 brew) 패키징을 활용한 PHP 버전 관리
3. Composer — PHP 세계의 종속성 제어
4. `php.ini` 로컬 커스터마이징 위치와 반영

#### 📌 5-2. Ruby와 Java 생태계 구축
1. `rbenv`를 통한 Ruby 온보딩 — Jekyll 테마, CocoaPods 구동
2. Gem 관리 — rbenv 하위의 보석들
3. Java `SDKMAN!` 도입 — JDK 버전을 손쉽게 이동하기
4. `.zshrc` 환경변수 연동 최종 디버깅

---

### 6주차
- **대주제**: 로컬 웹 서버 셋업 — Nginx 아키텍처
- **세부학습목표**: macOS 내부 포트를 점유하여 Nginx 웹 엔진을 구동하고, 동적 도메인 라우팅을 실습한다.

#### 📌 6-1. Nginx 코어 아키텍처 분석
1. 아파치(Apache)의 한계와 Nginx Event-Driven 비교
2. Nginx 설정 파일 `nginx.conf` 해부 (worker, events)
3. Reverse Proxy 기본 개념 이해
4. 80번 포트 권한 이슈 (루트 유저 vs 일반 유저)

#### 📌 6-2. 로컬 도메인 서버 라우팅 실습
1. `/etc/hosts` 파일 강제 변조 매커니즘
2. Nginx Server Block(Virtual Host) 생성
3. `*.test` 도메인을 로컬 애플리케이션으로 포트 포워딩
4. 로컬 TLS/SSL 인증서 (mkcert) 발급 및 적용

---

### 7주차
- **대주제**: 관계형 데이터베이스 1 — MySQL 셋업
- **세부학습목표**: 터미널 기반으로 MySQL을 설치, 접근 통제하고 데이터 볼륨을 관리하는 방법을 터득한다.

#### 📌 7-1. MySQL 엔진과 서버 구조
1. RDBMS 클라이언트/서버 구조의 이해
2. Homebrew 기반 MySQL 설치 및 보안 초기화 (`mysql_secure_installation`)
3. `my.cnf` 설정 — 캐릭터셋(utf8mb4), 최대 커넥션 풀 조정
4. 데이터 저장 디렉토리(`/usr/local/var/mysql`) 관측

#### 📌 7-2. 터미널 및 GUI 클라이언트 연동
1. 터미널 MySQL 셸 명령어 기본 탐험
2. TablePlus, Sequel Ace 등 Mac 전용 DB 툴 소개
3. 사용자 권한(GRANT) 분리와 로컬 호스트(`127.0.0.1`) 보안 바인딩
4. SQL 덤프 생성을 통한 스키마 백업

---

### 8주차
- **대주제**: 백그라운드 데몬 통제 — Brew Services
- **세부학습목표**: 설치된 서버 프로그램들을 Mac이 재부팅될 때마다 자동 실행하게 만드는 macOS Launchd 데몬 시스템을 다룬다.

#### 📌 8-1. macOS Launchd 서브시스템
1. 리눅스 `systemd` 와 맥 `launchd` 의 차이
2. `~/Library/LaunchAgents` 의 plist 파일 해부
3. `launchctl` 명령어 작동 방식

#### 📌 8-2. Brew Services 생태계
1. `brew services start/stop/restart` 마법의 비밀
2. 백그라운드로 돌아가는 MySQL, Nginx, Redis 런타임 제어
3. 상태 출력 `brew services list` 및 오류 진단
4. 로그 파일 꼬리 물기 (`tail -f`)를 통한 서버 트러블슈팅

---

### 9주차
- **대주제**: 관계형 데이터베이스 2 — PostgreSQL 셋업
- **세부학습목표**: 최신 백엔드 스택 포스트그레스큐엘의 차별점을 파악하고 설치 및 확장 기능을 다룬다.

#### 📌 9-1. PostgreSQL 특징 및 생태계
1. 객체 관계형 데이터베이스(ORDBMS)의 위상
2. PostGIS, pgvector 등 플러그인 확장 기능
3. JSONB 타입 처리에 있어 MySQL과의 핵심 차이점
4. 커넥션 모델(프로세스 포크)에 따른 메모리 관리

#### 📌 9-2. 셋업 및 권한 제어
1. Homebrew 기반 PostgreSQL 16 셋업
2. 기본 사용자(postgres) 정책과 Peer Authentication
3. `psql` 셸과 기본 메타 명령어(`\d`, `\l`) 체득
4. GUI 관리 도구 (pgAdmin, Postico) 연동 전략

---

### 10주차
- **대주제**: Apple Silicon (ARM)과 크로스 컴파일
- **세부학습목표**: M1/M2/M3 이후의 아키텍처 대격변 속에서 x86 소프트웨어를 제어하고 컨테이너를 구동하는 방법을 다룬다.

#### 📌 10-1. x86에서 ARM으로의 대전환
1. CISC (Intel) vs RISC (ARM) 코어 철학
2. 왜 x86 빌드 파일을 ARM 맥에서 돌릴 수 없을까?
3. Rosetta 2 아키텍처 — 실시간 및 AOT(사전 컴파일) 명령어 번역
4. 터미널의 두 얼굴 (Rosetta Terminal vs Native Terminal)

#### 📌 10-2. Mac-on-Docker
1. 리눅스 네이티브가 아닌 Mac에서 Docker 데몬이 구동되는 원리 (Linux VM)
2. `docker buildx` 명령어로 멀티 아키텍처(amd64, arm64) 클라우드 이미지 빌드
3. Lima / Colima — 무거운 Docker Desktop을 피하는 대체 런타임
4. 포트포워딩시 발생하는 macOS 네트워크 브리지 체계

---

### 11~14주차 (종합 프로젝트 등은 커리큘럼 성격에 맞게 융합)
- Mac 개발 환경 마스터 피스, 인프라 배포 등 고급 유즈케이스 시뮬레이션
- 실무자 트러블슈팅 시나리오 분석
