---
layout: default
title: "2주차: 명령 프롬프트(CMD)와 DOS 명령어의 부활"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <rect x="50" y="40" width="500" height="40" fill="#333" rx="5"/>
  <text x="70" y="65" fill="#00FF00" font-size="18" font-family="monospace">C:\> dir /w /s</text>
  <rect x="50" y="100" width="500" height="40" fill="#333" rx="5"/>
  <text x="70" y="125" fill="#00FF00" font-size="18" font-family="monospace">C:\> xcopy "SRC" "DEST" /E /H /C /I</text>
</svg>
</div>

# 2주차: 명령 프롬프트(CMD)와 DOS 명령어의 부활

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_02.png)
<br>

- **대주제**: 명령 프롬프트(CMD)와 DOS 명령어의 부활
- **세부학습목표**: GUI 마우스를 버리고, 현재까지도 위력을 발휘하는 쉘인 CMD 환경에서 필수 DOS 명령어들을 다듬어 낸다.

#### 📌 2-1. 명령 프롬프트 엔진
1. `cmd.exe` 프로세스의 한계 및 작동 원리
2. 배치 스크립트(`.bat`)의 문법 체계

#### 📌 2-2. 클래식 DOS 명령어 실전
1. 디렉토리 탐색기: `dir`, `cd`, `mkdir`, `tree`
2. 파일 복사/이동 종결자: `copy`, `xcopy`, `robocopy` 의 성능 차이
3. 네트워킹과 포트 점검: `ipconfig`, `ping`, `tracert`, `netstat -ano`
4. 프로세스 제어: `tasklist`, `taskkill`

---


<div align='center'>
  <img src='img/toon2.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Concept Art' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <circle cx="200" cy="100" r="40" fill="#E81123"/>
  <text x="200" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PID: 4012</text>
  <path d="M 250 100 L 350 100" stroke="white" stroke-width="4"/>
  <rect x="360" y="70" width="180" height="60" fill="#4B4B4B" rx="5"/>
  <text x="450" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">taskkill /F /PID 4012</text>
</svg>
</div>



---

## [심화 렉처] 전통을 지배하는 도스 명령어

아직도 윈도우 서버 스크립트에는 Unix `ls` 가 아니라 `dir` 이 박혀 있습니다. 이전의 레거시 DOS 명령어를 모르면 구형 유지보수가 불가능합니다.
`mkdir` 과 디렉토리 파괴(`rmdir /s /q`), 그리고 빠른 파일 복사 로직인 `xcopy` 나 단선 네트워크 서버 백업 전술인 `robocopy` 를 체감해야 합니다.


<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Networking: netstat -ano | findstr :8080</text>
</svg>
</div>


## [심화 렉처] 권력의 제어

당신의 컴퓨터 포트를 누가 갉아먹고 있는지 알아내려면 `netstat -ano` 와 `tasklist` 로 PID를 추적해야 합니다. 멈춰버린 프로세스를 터미널에서 즉시 폭파시키는 `taskkill /F /PID 2043` 은 모든 윈도우 엔지니어의 핵심 스킬입니다.
