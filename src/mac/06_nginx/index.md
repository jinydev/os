---
layout: default
title: "6주차: 로컬 웹 서버 셋업 (Nginx, 로컬도메인)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="120" height="80" fill="#E81123" rx="5"/><text x="110" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Port 80</text><path d="M 180 100 L 260 100" stroke="#00FF00" stroke-width="4"/><rect x="270" y="40" width="100" height="120" fill="#333" rx="5"/><text x="320" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Nginx</text><path d="M 380 100 L 450 100" stroke="#00FF00" stroke-width="4"/><rect x="460" y="60" width="100" height="80" fill="#0078D7" rx="5"/><text x="510" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Node 3000</text></svg>
</div>

# 6주차: 로컬 웹 서버 셋업 (Nginx, 로컬도메인)

<br>

## 1. Nginx 웹 서버 커널

[실전 심화 렉처]
Nginx 는 싱글 스레드 Event-Driven 워커 구조로 접속을 제어합니다. 로컬에 brew 로 nginx 를 설치하면 `8080` 포트로 뜹니다.

## 2. 로컬 도메인(/etc/hosts) 해킹

[실전 심화 렉처]
`/etc/hosts` 파일의 `127.0.0.1 mysite.test` 레코드는 맥 내부 DNS를 기만합니다. 나아가 `mkcert` 툴을 통해 루트 인증서를 발급하여 `https` 인프라를 로컬에서 구동하면 실서버 디버깅 환경이 완성됩니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">sudo nano /etc/hosts</text></svg>
</div>

## [심화 렉처] Nginx의 비동기 이벤트 루프 워커

스레드 1개가 요청 1개를 처리하던 시절(Apache HTTPD)은 C10K Problem에 부딪혀 무너졌습니다. Nginx는 C언어로 구현된 극단적으로 가벼운 비동기 I/O 이벤트 처리를 통해 워커 당 수만 개의 요청을 다룹니다. Mac 장비의 포트 80을 리스닝하여, 백엔드 로컬 서버(localhost:3000 등)로 데이터를 실시간 중계하는 Reverse Proxy 매커니즘을 체험합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">Event-Driven Asynchronous I/O</text></svg>
</div>

## [심화 렉처] 가상 호스팅과 SSL 해킷(Hack)

`/etc/hosts` DNS 가로채기 파일 조작은 가장 고전적이지만 가장 확실한 로컬 개발망 설계법입니다. `mysite.test` 라는 임의 도메인을 부여하고, Nginx의 Server Block과 맵핑한 뒤 TLS 보안 인증서를 `mkcert` (시스템 CA 신뢰 체인 강제 등록) 로 가짜 서명하여 브라우저에서 '안전함' 딱지를 뛰우는 전체 과정을 실습합니다.
