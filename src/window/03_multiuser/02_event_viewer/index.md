---
layout: default
title: "2. 이벤트 뷰어와 레지스트리 디버깅"
---

# 2. 이벤트 뷰어로 에러 뚫어보기

당신이 만든 백엔드 프로그램이나 배치 파일이, 터미널에서는 잘 되는데 시스템 서비스(Background Service)로 백그라운드에서 구동시켰을 때 아무런 오류 메시지도 없이 그냥 고요하게 시스템 다운 증상을 겪고 죽어버린다면 어떻게 할 참입니까? 그냥 포기하고 재부팅하실 건가요?

해답은 **레지스트리(Registry)**를 이해하고 **이벤트 뷰어(Eventvwr.msc)** 시스템 로그를 뜯어보는 것에 있습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="80" y="50" fill="#00FF00" font-size="20" font-family="monospace">Event Viewer (eventvwr.msc)</text><rect x="80" y="70" width="440" height="90" fill="#333"/><text x="100" y="100" fill="white" font-size="14" font-family="monospace">[Error] Event 1000 - Application Crash</text><text x="100" y="125" fill="#E81123" font-size="14" font-family="monospace">Faulting module name: ntdll.dll</text></svg>
</div>

## 레지스트리 (Windows Registry)의 거대한 뇌 구조
윈도우는 리눅스처럼 단순 텍스트 파일(e.g., `/etc`) 환경설정에 의존하지 않고, 컴퓨터 모든 설정의 두뇌인 **레지스트리 데이타베이스** 폴더 계층망을 씁니다. 크게 전역 컴퓨터 머신에 종속된 `HKEY_LOCAL_MACHINE (HKLM)` 와 현재 로그인한 해당 유저에게만 유효한 정보체계인 `HKEY_CURRENT_USER (HKCU)` 로 나누어져 충돌을 막습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">HKEY_LOCAL_MACHINE (HKLM) vs HKEY_CURRENT_USER (HKCU)</text></svg>
</div>

## 이벤트 뷰어 에코
화면에 에러가 안 보인다고 없는 게 아닙니다. 모든 치명적인 모듈 충돌이나 보안 권한 거부, 백그라운드 셧다운 이벤트는 `이벤트 뷰어(Event Viewer)`의 'Windows 로그 / 시스템 응용 프로그램' 탭에 붉은색 엑스표(이벤트 ID 1000 번호대 등)로 반드시 흔적을 남깁니다. 이것을 읽어내야만 원인을 도출하고 아키텍트 시스템 엔지니어로 살아남을 수 있습니다.
