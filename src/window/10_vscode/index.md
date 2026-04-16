---
layout: default
title: "10주차: 궁극의 퓨전 — VS Code Remote 아키텍처"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="200" height="80" fill="#0078D7" rx="5"/><text x="150" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code GUI (Windows)</text><path d="M 260 100 L 340 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="2,2"/><text x="300" y="90" fill="#00FF00" font-size="12" font-family="monospace" text-anchor="middle">Socket Tunnel</text><rect x="350" y="60" width="200" height="80" fill="#E95420" rx="5"/><text x="450" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code Server (.vscode)</text><text x="450" y="125" fill="white" font-size="12" font-family="monospace" text-anchor="middle">(Linux Subsystem)</text></svg>
</div>

# 10주차: 궁극의 퓨전 — VS Code Remote 아키텍처

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_10.png)
<br>

- **대주제**: 궁극의 퓨전 — VS Code Remote 아키텍처
- **세부학습목표**: 윈도우에 코드를 깔지 않고 에디터만 켠 뒤, 리눅스 서버 엔진에서 소스코드를 컴파일하는 '원격' 체계를 배운다.

#### 📌 10-1. 에디터 껍데기 분리 이론
1. 윈도우의 파일 시스템 속도 방어: 소스는 반드시 우분투에 둔다
2. VS Code Server가 WSL2 프로세스로 침투하여 소켓을 연결하는 방식

#### 📌 10-2. localhost 포트의 마법
1. WSL2 에서 띄운 Node 서버가 왜 윈도우 Edge 브라우저의 로컬호스트(`127.0.0.1:3000`)로 접속되는가?
2. `wsl --shutdown` 과 네트워크 재시작 장애 극복 트러블슈팅

---


<div align='center'>
  <img src='img/toon2.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Concept Art' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="80" fill="gray" font-size="16" font-family="monospace" text-anchor="middle">Do NOT place Code in C:\Drive</text><text x="300" y="120" fill="#00FF00" font-size="22" font-family="monospace" text-anchor="middle">git clone internally at ~/project</text></svg>
</div>

### 11~14주차
- Windows Docker 구조 및 포트 포워딩, 최종 Windows 인프라 종합 배포
- 터미널 융합, 파워셸 닷넷 프로그래밍 심화 등

---

## [심화 렉처] Remote-WSL 아키텍처

코드 컴파일은 우분투 내부에서 전개하십시오. 윈도우에서 소스코드를 읽으면 I/O 번역 지연으로 속도가 치명적으로 떨어집니다. 리눅스 백엔드 상에서 `code .` 을 입력하면 윈도우로 화면만 중계됩니다. 에디터 프론트와 실행 서버 백엔드의 이원화 스위치 체계입니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="20" font-family="monospace" text-anchor="middle">[.wslconfig] memory=16GB processors=4</text></svg>
</div>

