---
layout: default
title: "1. Windows Terminal 아키텍처"
---

# 1. 터미널의 혁신, Windows Terminal 엔진

과거 2010년대까지만 해도 윈도우의 가장 고질적인 악명은 바로 `cmd` 창의 끔찍할 정도로 느린 명령어 렌더링 성능이었습니다. 텍스트 엔진(`conhost.exe`)이 오래되어 글자가 주르륵 올라갈 때 CPU가 한숨을 쉬어야 했습니다.

그러나 마이크로소프트가 칼을 빼들어 새롭게 빌드한 혁신적인 앱, **Windows Terminal(WT)** 은 과거의 흔적을 모조리 지워버렸습니다. WT는 앱의 코어 엔진부터 그래픽카드(GPU) 가속 렌더링(DirectWrite) 기술을 통째로 이식하여 터미널 창을 구동합니다. 게임을 구동할 법한 압도적 속도 로직으로 무수히 쏟아지는 백엔드 로고 텍스트들을 딜레이 제로로 뽑아냅니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="40" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Windows Terminal Architecture</text><rect x="50" y="60" width="150" height="100" fill="#333" rx="5"/><text x="125" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">cmd.exe</text><rect x="225" y="60" width="150" height="100" fill="#005A9E" rx="5"/><text x="300" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PowerShell</text><rect x="400" y="60" width="150" height="100" fill="#E95420" rx="5"/><text x="475" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">WSL2 (Ubuntu)</text></svg>
</div>

## 다중 쉘 융합과 Json 환경 프로그래밍
단순히 빨라지기만 한 것이 아닙니다. 
지금까지 `cmd`, `PowerShell`, `Git Bash`, 그리고 심지어 나중에 배울 리눅스 커널인 `WSL(Ubuntu)` 창까지 각각 정신없이 분리되어 마우스로 켜야 했던 수많은 클라이언트 환경을, 웹 브라우저처럼 **하나의 단일 윈도우 앱 창 안의 탭(Tab)** 으로 완벽하게 통합시켜버렸습니다.

<div align='center' style='margin: 30px 0;'>
  {% raw %}
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="80" y="40" width="440" height="120" fill="#333" rx="5"/><text x="100" y="70" fill="#00FF00" font-size="14" font-family="monospace">"profiles": {{</text><text x="120" y="90" fill="#00FF00" font-size="14" font-family="monospace">"defaultProfile": "{{ubuntu-guid}}",</text><text x="120" y="110" fill="#00FF00" font-size="14" font-family="monospace">"useAcrylic": true</text><text x="100" y="130" fill="#00FF00" font-size="14" font-family="monospace">}}</text></svg>
  {% endraw %}
</div>

더는 GUI 설정 환경에 얽매이지 않고, 터미널 환경을 제어하는 `settings.json` 설정 파일을 직접 코딩하여 뒷배경의 투명도(Acrylic)부터 D2Coding 개발자 폰트, 다크 테마 맵핑까지 전부 커스터마이징합니다. 단축키 하나로 분할 화면(Split Pane) 두 개를 띄워 왼쪽엔 윈도우 파워셸을, 오른쪽엔 리눅스 셸을 동시에 돌리는 극강의 생산성 궤도로 진입하십시오.
