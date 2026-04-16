---
layout: default
title: "7주차: 패키지 관리자의 도입과 개발 환경 렌더링"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="150" cy="100" r="50" fill="#0078D7"/><text x="150" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Winget</text><circle cx="450" cy="100" r="50" fill="#4B4B4B"/><text x="450" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Scoop</text><path d="M 220 100 L 380 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="90" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">User Space Isolation</text></svg>
</div>

# 7주차: 패키지 관리자의 도입과 개발 환경 렌더링

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_07.png)
<br>

- **대주제**: 패키지 관리자의 도입과 개발 환경 렌더링
- **세부학습목표**: 브라우저에서 'Next' 버튼을 누르는 대신, 스크립트 한 줄로 필수 개발 언어를 다운하고 PATH를 맞추는 실무 데브옵스를 배운다.

#### 📌 7-1. Winget 과 Scoop
1. 터미널 패키지 디펜던시의 장점 — 시스템 레지스트리 오염 방지
2. `winget` (Windows Package Manager) 설치와 레포지토리 관리
3. `Scoop`: 관리자 권한 없이 유저 스페이스에 독립 배포망 셋업

#### 📌 7-2. 백엔드/프론트엔드 언어 툴체인 융단폭격
1. 소스 컨트롤러: `Git for Windows` 와 credential manager 구성
2. 웹/스크립트 런타임: `Node.js` 및 `Python` (Scoop 기반 격리 환경)
3. 레거시 및 엔터프라이즈 환경: `PHP` 와 `Ruby` 바이너리 다운로드 구동 실습
4. 자바 생태계: `Java JDK` 세팅 및 `JAVA_HOME` 시스템 변수 동기화 확인

---


<div align='center'>
  <img src='img/toon2.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Concept Art' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="70" width="500" height="60" fill="#333" rx="5"/><text x="300" y="105" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">scoop install nodejs python ruby php</text></svg>
</div>

---

## [심화 렉처] 패키지 자동 셋업과 분리 공간

아직도 브라우저에서 `Next` 를 클릭하며 설치하십니까? `winget` 과 `Scoop` 패키지 매니저를 통해 레지스트리와 PATH 등록을 터미널로 자동화하십시오. Node.js 와 Python, Ruby 등의 버전 충돌 꼬임(Dependency Hell)을 사용자 공간(User Space) 격리로 막아냅니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">$env:JAVA_HOME = "C:\Program Files\Java\jdk-17"</text></svg>
</div>

