---
layout: default
title: "1. 윈도우 다중 사용자 환경과 UAC"
---

# 1. 윈도우 다중 사용자 환경

리눅스에 `root`가 있다면 윈도우에는 최고 관리자 권한을 상징하는 `Administrator` 계정 그룹이 존재합니다. 컴퓨터 한 대에 여러 명이 RDP(원격 데스크톱)로 각자 접속하여 자기만의 화면을 띄워 독립된 프로그램을 각기 실행시킬 수 있는 윈도우의 멀티 유저 세션 관리(Multi-User Session Control)의 본질을 이해해야 합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="150" height="100" fill="#333" rx="5"/><text x="125" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Standard User</text><path d="M 210 100 L 390 100" stroke="#E81123" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="90" fill="#E81123" font-size="14" font-family="monospace" text-anchor="middle">UAC Elevation Request</text><rect x="400" y="50" width="150" height="100" fill="#0078D7" rx="5"/><text x="475" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Administrator</text></svg>
</div>

## UAC의 불편하지만 안전한 방패
또한, 우리가 윈도우를 쓰다 보면 화면이 어두워지며 "이 앱이 디바이스를 변경하도록 허용하시겠습니까?" 라는 UAC (사용자 계정 컨트롤) 경고 팝업이 수시로 뜹니다. 
이 팝업이 뜨는 본질적인 이유는, 해당 실행 프로세스가 C드라이브 프로그램 폴더에 파일을 쓰거나 시스템 레지스트리를 변조하기 위해 관리자(Administrator) 그룹으로 권한 승급(Elevation)을 시도했기 때문입니다.

윈도우 시스템 내부 눈에 보이지 않는 저 깊은 곳에는 서버 백그라운드 웹 데몬 서비스용으로 격리된 `SYSTEM`, `LOCAL SERVICE`, `NETWORK SERVICE` 같은 특수한 특권 아이디가 백그라운드로 돌아가고 있다는 사실을 간과하고 코딩을 하게 되면 권한 거부 에러의 늪에 빠집니다.
