---
layout: default
title: "8주차: 백그라운드 제어 (Brew Services, launchd)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="150" height="80" fill="#0078D7" rx="5"/><text x="125" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">brew services start</text><path d="M 210 100 L 390 100" stroke="#E81123" stroke-width="4" stroke-dasharray="2,2"/><rect x="400" y="60" width="150" height="80" fill="#333" rx="5"/><text x="475" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">launchctl load .plist</text></svg>
</div>

# 8주차: 백그라운드 제어 (Brew Services, launchd)

<br>

## 1. Launchd 데몬과 Brew Services

[실전 심화 렉처]
Apple 의 초기화 시스템인 `launchd`가 여러분의 파일들을 감시하며 서버를 살려놓습니다. `brew services list` 명령은 바로 이 launchd 시스템에 Homebrew 파일들을 자동으로 스케줄링 시켜버립니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="20" font-family="monospace" text-anchor="middle">~/Library/LaunchAgents/</text></svg>
</div>

## [심화 렉처] macOS의 심장, Launchd 서브시스템 파헤치기

리눅스에 `systemd`가 존재한다면, 애플 운영체제 군단에는 `launchd`가 마스터 프로세스(PID 1) 권한을 지고 있습니다. 단지 터미널을 열었을 뿐인데 자동으로 서비스가 백그라운드에 상주할 수 있는 이유는 XML 형태의 프로퍼티 리스트(`.plist`) 설정 스크립트 덕분입니다. Brew Services 명령어 세트가 내부적으로 launchctl에 어떻게 명령을 치환해 보내는가를 파악합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">tail -f /opt/homebrew/var/log/nginx/error.log</text></svg>
</div>

## [심화 렉처] 로그 테일링과 모니터링 (Observability)

서버 구동에 실패했다고 Homebrew를 탓해서는 안 됩니다. PID 생성이 죽어버린 데몬의 흔적을 쫓는 유일한 단서는 로컬 하드 상단의 Error Log 뿐입니다. `tail -f` 연속 읽기 파이프라인 처리를 통해 Nginx 포트 충돌, MySQL 권한 소거 등의 장애를 실시간 디버그합니다.
