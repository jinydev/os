---
layout: default
title: "2. 권력을 통제하는 도스 명령어"
---

# 2. 클래식 DOS 명령어의 부활

우리는 여전히 최신 윈도우 11 환경에서도 터미널을 열면 유닉스의 `ls`나 `cp`가 아닌, MS-DOS의 유산인 옛날 명령어를 타이핑해야만 윈도우 커널을 직결적으로 제어할 수 있습니다. 

## 1. 파일/디렉토리 통제 명령
아직도 윈도우 스크립트에는 Unix `ls` 가 아니라 `dir` 이 디렉터리 목록 탐색기로 박혀 있습니다. 디렉터리 파괴 명령인 `rmdir /s /q`, 그리고 옛날 `copy`를 넘어선 확장 고속 파일 복사 로직인 `xcopy` 나 서버 단절에 대비한 초안전 동기화 백업 전술 명령어인 `robocopy`의 파괴력을 체감해야 합니다.

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

## 2. 권력의 제어 (네트워크와 프로세스 킬링)
당신의 귀중한 서버 컴퓨터 전용 포트를 어느 수상한 악성 앱이 갉아먹고 연결하고 있는지 알아내려면, 즉시 `cmd`창을 관리자 권한으로 열고 `netstat -ano` 네트워크 명령을 쳐서 몰래 통신 중인 프로세스 PID를 확보해야 합니다.

그리고 `tasklist` 로 그 악성 프로세스의 본명을 추적하고, 멈춰버려 GUI의 'X' 버튼으로도 안 꺼지거나 몰래 뒷면에서 도는 좀비 프로그램을 즉각적으로 터미널에서 폭파시키는 강력한 처형 명령어 `taskkill /F /PID 4012` 를 사용하는 것은 모든 윈도우 엔지니어의 핵심 서바이벌 스킬입니다.
