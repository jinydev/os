---
layout: default
title: "4주차: 컴퓨터의 핏줄, 환경 변수와 경로(PATH)"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="40" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Environment Variables Execution Flow</text><rect x="50" y="60" width="500" height="30" fill="#333"/><text x="300" y="80" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">1. C:\Windows\System32</text><rect x="50" y="100" width="500" height="30" fill="#0078D7"/><text x="300" y="120" fill="white" font-size="14" font-family="monospace" text-anchor="middle">2. C:\Python311\bin</text><rect x="50" y="140" width="500" height="30" fill="#E81123"/><text x="300" y="160" fill="white" font-size="14" font-family="monospace" text-anchor="middle">3. C:\Program Files\NodeJS</text></svg>
</div>

# 4주차: 컴퓨터의 핏줄, 환경 변수와 경로(PATH)

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_04.png)
<br>

- **대주제**: 컴퓨터의 핏줄, 환경 변수와 경로(PATH)
- **세부학습목표**: 프로그램 개발에서 가장 많이 발생하는 "command not found" 에러를 원천적으로 해결하는 환경변수 시스템을 실습한다.

#### 📌 4-1. 전역 및 사용자 환경 변수
1. `%USERPROFILE%`, `%APPDATA%`, `%TEMP%` 숨겨진 폴더의 역할
2. 시스템 변수 vs 윈도우 사용자 변수 우선순위
3. GUI(Advanced System Settings)와 레지스트리를 통한 안전한 환경 변수 조작

#### 📌 4-2. PATH 라우팅 실습
1. 터미널은 당신의 명령어를 어디서 찾는가?
2. 윈도우 PATH 에러 분석: 우선순위 오작동으로 인한 엉뚱한 Python 버전 호출 해결
3. 실습: CMD/Powershell에서 동적으로 임시 환경 변수 셋업

---


<div align='center'>
  <img src='img/toon2.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Concept Art' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">set PATH=C:\Temp;%PATH%</text><text x="300" y="140" fill="gray" font-size="16" font-family="monospace" text-anchor="middle">(Temporary Session Override)</text></svg>
</div>



---

## [심화 렉처] 터미널의 동맥 망, 환경 변수

`python -V` 명령어가 안 먹힌다면, 윈도우 터미널 환경이 고장 난 것입니다. 윈도우 터미널은 당신이 입력한 명령어를 오직 `PATH` 라는 환경 변수의 세미콜론(`;`) 목록 안에서만 순서대로 찾습니다.


<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="50" cy="60" r="20" fill="#0078D7"/><text x="300" y="65" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Global (System) PATH + Local (User) PATH</text></svg>
</div>


## [심화 렉처] 변수 조작과 오염 방지망

패키지를 이것저것 깔면 오염된 시스템 PATH 라우팅을 복구해야 합니다. 고급 시스템 속성(GUI)에서 사용자 변수와 시스템 변수의 스코프를 분리하고, 터미널 1회성 변수인 `set MY_KEY=val` 동작을 이해해야 합니다.
