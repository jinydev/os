---
layout: default
title: "운영체제(OS) 심화 과정"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="250" viewBox="0 0 800 250" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="15"/>
  <text x="400" y="50" fill="white" font-size="28" font-weight="bold" font-family="monospace" text-anchor="middle">Software Engineer Curriculum</text>
  
  <rect x="100" y="80" width="150" height="120" fill="#E81123" rx="10"/>
  <text x="175" y="145" fill="white" font-size="20" font-weight="bold" font-family="monospace" text-anchor="middle">CS Basic</text>
  <text x="175" y="175" fill="rgba(255,255,255,0.7)" font-size="14" font-family="monospace" text-anchor="middle">(basic.jiny.dev)</text>

  <rect x="325" y="80" width="150" height="120" fill="#0078D7" rx="10"/>
  <text x="400" y="145" fill="white" font-size="20" font-weight="bold" font-family="monospace" text-anchor="middle">System OS</text>
  <text x="400" y="175" fill="rgba(255,255,255,0.7)" font-size="14" font-family="monospace" text-anchor="middle">(Kernel/Infra)</text>

  <rect x="550" y="80" width="150" height="120" fill="#00B294" rx="10"/>
  <text x="625" y="145" fill="white" font-size="20" font-weight="bold" font-family="monospace" text-anchor="middle">Network</text>
  <text x="625" y="175" fill="rgba(255,255,255,0.7)" font-size="14" font-family="monospace" text-anchor="middle">(Protocol/Web)</text>

  <path d="M 260 140 L 310 140" stroke="#00FF00" stroke-width="6" marker-end="url(#arrow)"/>
  <path d="M 485 140 L 535 140" stroke="#00FF00" stroke-width="6" marker-end="url(#arrow)"/>
  
  <defs>
    <marker id="arrow" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
      <path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/>
    </marker>
  </defs>
  </svg>
</div>

# 🚀 운영체제 (OS) 심화 과정

환영합니다! 본 과정은 상위 1% 소프트웨어 개발자와 인프라(SRE) 엔지니어가 반드시 꿰뚫고 있어야 할 **현대 컴퓨터 플랫폼의 핵심 제어 메커니즘**을 파고드는 곳입니다. 

단순히 언어의 문법을 아는 수준의 '코더(Coder)'를 넘어서, 자신이 짠 코드가 어떻게 수십만 대의 서버 하드웨어 메모리를 점유하고, 커널 시스템 콜(System Call)을 타격하며, Docker 컨테이너의 네임스페이스와 클라우드에 자동 배포(Deploy)되는지 그 거대한 생태계의 지배권을 이 커리큘럼을 통해 당신의 손안에 쥐어 드립니다.

---

## ⚠️ [필수 안내] 선수 과목 (Prerequisites) 확인

> [!WARNING]
> 본 운영체제(OS) 과정은 **소프트웨어 엔지니어를 위한 중고급(Advanced) 과정**입니다. 
> 파일 시스템 입출력, 터미널 명령어 구조, 기본적인 하드웨어 지식에 대한 사전 이해도가 없으면 학습에 치명적인 어려움을 겪을 수 있습니다.

본격적인 딥다이브에 앞서, 개발자로서의 가장 기초적인 체력 훈련이 부족하다 느끼시는 분들은 **반드시 아래의 컴퓨터 과학 베이직 코스를 먼저 이수한 후** 이 운영체제 과정에 합류하시길 강력하게 권장합니다.

* 👉 [개발자 역량 기본기: 컴퓨터 과학 프레임 (basic.jiny.dev)](https://basic.jiny.dev/)
  * 컴퓨터 구조 (CPU, RAM, 메인보드)와 데이터 단위의 이해
  * 터미널/쉘(Shell) 명령어의 기본 사용법과 권한 체계
  * 웹/네트워크 통신의 아주 기초적인 기저 메커니즘

---

## 🗂️ 플랫폼 아키텍처 맵 (커리큘럼)

본 저장소는 크게 4가지 대주제 플랫폼으로 나뉘어 구성되어 있습니다. 상단의 전역 내비게이션 바 혹은 우측 사이드바를 통해 관심 있는 분야로 직집 진입해 보십시오.

1. [운영체제(OS) 코어 엔지니어링](/os/01_intro/)
   * *추천 대상: 백엔드/인프라 지망생* 
   * 리눅스 커널 프로세스 스케줄링부터 페이징 기법, Docker 가상화 기술, 그리고 쿠버네티스(K8s) 클라우드 환경 배포까지 14주간 파고드는 하드코어 여정입니다.
2. [맥(macOS) 터미널 및 유닉스 생태계 방어](/mac/)
   * *추천 대상: 모든 실무 IT 개발자* 
   * 스타벅스에서 멋 부리기 위한 용도를 넘어, 왜 전 세계 개발자들이 Mac을 찬양하는가. zsh 오 마이 쉘, Homebrew, Nginx 웹 서버 커널 독립 구축 등 백엔드 유닉스 로컬 뼈대 완성 프로젝트입니다.
3. [윈도우(Windows) 네이티브와 WSL2 하이브리드](/window/)
   * *추천 대상: 게임/클라이언트/C# 개발자 및 보편 시스템 사용자* 
   * NT 커널 아키텍처와 치명적인 터미널 환경 변수 셋업 제어. 나아가 MS가 칼을 갈고 내놓은 가상화 WSL2 브릿지 연결과 Remote-VSCode 융합 체계를 파밍합니다.
4. [기타 시스템 및 거대 프레임워크 생태계](/others/)
   * *추천 대상: 아키텍터 및 테크 긱스* 
   * MS-DOS, OS/2부터 모바일용 RTOS는 물론 최신 노드(Node.js) 이벤트 루프와 자율주행 등 운영체제의 한계를 돌파하는 새로운 메타 세계관들을 꿰뚫어 봅니다.
