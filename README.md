# 🚀 System OS & Architecture Curriculum

<div align='center' style='margin: 30px 0;'>
  <img src="https://img.shields.io/badge/Course-System_OS-0078D7?style=for-the-badge" alt="System OS"/>
  <a href="https://os.jiny.dev">
    <img src="https://img.shields.io/badge/Website-os.jiny.dev-00B294?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Website"/>
  </a>
</div>

환영합니다! 본 저장소는 현대 소프트웨어 상위 1% 개발자 및 클라우드 인프라 엔지니어(SRE)로 도약하기 위해 반드시 거쳐야 할 **플랫폼 운영체제(OS) 및 시스템 아키텍처** 심화 커리큘럼 문서를 호스팅합니다.

## 🔗 공식 웹사이트 랜딩 페이지
상세한 주차별 코스 내용과 실전 튜토리얼은 아래의 공식 배포 사이트에서 편안하게 학습하실 수 있습니다.
* **[💻 https://os.jiny.dev](https://os.jiny.dev)**

---

## 🗂️ 4대 플랫폼 커리큘럼 구성

이 레포지토리는 단순히 하나의 운영체제 이론을 암기하는 곳이 아닙니다. 실무 서버 및 클라이언트 프로덕션 환경을 지배하는 4가지 거대 플랫폼 생태계의 철학을 뜯어내고, 터미널 환경에서 스크립트 기반으로 시스템을 직결 제어하는 근육을 키웁니다. 문서 소스는 `/src` 디렉터리에 각 챕터별로 모듈화되어 있습니다.

### 1. 🐧 운영체제 (OS Core)
* **목표:** 리눅스(Linux) 철학 기반의 터미널 명령어, 파일/링크 입출력 메커니즘, 메모리 페이징 및 프로세스/쓰레드 통제망. 최종적으로 Docker 컨테이너와 쿠버네티스(K8s) 클라우드 인프라 배포까지 등반.
* **경로:** `/src/os` (1주차 ~ 14주차)

### 2. 🍎 유닉스 데스크탑 (macOS)
* **목표:** 가장 아름다운 유닉스(Unix) 머신인 macOS 기반 로컬 독립 개발망 구성. zsh 오 마이 쉘 튜닝, Homebrew 패키지 생태계와 Nginx/MySQL 데몬 서버 셋업 완전 정복. 
* **경로:** `/src/mac` (1주차 ~ 11주차)

### 3. 🪟 네이티브 시스템 (Windows)
* **목표:** NT 커널 기반 아키텍처와 환경 변수 경로 이해. 객체 쉘인 파워셸(PowerShell)과 `csc.exe` 닷넷 빌드. MS가 만든 최고의 걸작 WSL2 리눅스 하이브리드 엔진과 Remote-VSCode 융합 체계 파밍.
* **경로:** `/src/window` (1주차 ~ 10주차)

### 4. 💾 메타 생태계 및 히스토리 (Others)
* **목표:** 16비트 MS-DOS와 어셈블리 시대, 엔터프라이즈 유닉스(Solaris)와 임베디드 실시간 운영체제(RTOS). 나아가 노드(Node.js) 등 OS의 단계를 위협하는 거대 런타임 플랫폼 아키텍처 조망.
* **경로:** `/src/others` (1주차 ~ 5주차)

---

## ⚠️ 필수 선행 과목 (Prerequisites)

이곳은 **소프트웨어 개발자를 위한 하드코어 심화(Advanced) 코스**입니다.  
터미널 명령어 구조와 기본적인 메모리/캐시/네트워크 하드웨어 블록에 대한 사전 이해가 없다면 커리큘럼 진행 간에 치명적인 패널티를 입게 됩니다.

본 과정에 진입하기 앞서 핏이 맞지 않다고 판단되시면, 아래의 컴공 베이직 코스에서 기초 엔지니어링 체력을 먼저 길러오시길 강력하게 권장합니다.
* 👉 **[웹 개발자 기초 역량 코스: basic.jiny.dev](https://basic.jiny.dev/)**

---

## 🛠️ 사이트 유지보수 및 지킬(Jekyll) 빌드 안내
본 저장소는 `Jekyll` 프레임워크 기반의 정적 웹사이트 제너레이터(SSG)로 구동됩니다.

### 1. 로컬 환경 빌드 및 실행
로컬 환경에서 문서를 수정하고 미리보기 위해 아래 명령어를 사용할 수 있습니다.

```bash
# Ruby v3 이상 및 번들러 환경 필요
bundle install

# 로컬 개발 서버 구동 (실시간 핫리로딩 지원)
bundle exec jekyll serve --port 4001
```

### 2. 아키텍처 구조
* **Documents (`/src/**/*.md`)**: 모든 학습 문서는 마크다운 컴포넌트 형식으로 조각나 있으며 URL 경로와 독립적으로 맵핑 체계를 갖습니다.
* **Navigation (`/src/_data/*.yml`)**: 4개 통합 과정을 관통하는 상/하단, 좌/우측 트리 커리큘럼 라우팅 앵커는 이곳 데이터 파일들에 저장되어 일괄 통제됩니다.
