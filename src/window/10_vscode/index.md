---
layout: default
title: "10주차: 궁극의 퓨전 — VS Code Remote 아키텍처"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="200" height="80" fill="#0078D7" rx="5"/><text x="150" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code GUI (Windows)</text><path d="M 260 100 L 340 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="2,2"/><text x="300" y="90" fill="#00FF00" font-size="12" font-family="monospace" text-anchor="middle">Socket Tunnel</text><rect x="350" y="60" width="200" height="80" fill="#E95420" rx="5"/><text x="450" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code Server (.vscode)</text><text x="450" y="125" fill="white" font-size="12" font-family="monospace" text-anchor="middle">(Linux Subsystem)</text></svg>
</div>

# 10주차: 궁극의 퓨전 — VS Code 원격 아키텍처

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_10.png)
<br>

모든 환경은 분리되었습니다. 하지만 어떻게 내 윈도우 그래픽 편집기에서, 고립되어 있는 리눅스 공간(WSL2)의 소스코드를 딜레이 전혀 없이 자유자재로 편집할 수 있는 걸까요?

이번 마지막 10주차 렉처는 모던 윈도우 개발 생태계의 최고 정점인 **VS Code Remote 아키텍처**를 낱낱이 파헤칩니다. 프로그램 구동 시 엔진과 프론트 화면을 아예 별개의 커널로 쪼개버리고 소켓 터널로 두 세계관을 연결시켜, GUI 편집이라는 껍데기 시연은 윈도우가, 무거운 소스 I/O와 컴파일 구동은 온전히 리눅스가 전담하는 철저한 이원화 통제 시스템을 이해합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 에디터 사용법이 아닙니다. 왜 C:\ 드라이브에 git clone을 하면 I/O 딜레이 패널티를 입게 되는지를 깨닫는 공간.

1. [원격-WSL 컴파일러 이원화 메커니즘](./01_vscode_remote/index.md)
   > VS Code 핵심 엔진을 WSL 안에 박아 넣고, 윈도우 앱은 껍데기가 되어 소켓 터널로 UI만 중계하는 진보된 Thin Client 셋업 철학.

<hr style="margin: 40px 0;">

> **💡 로컬호스트 포트의 마법**
> "리눅스 포드에서 띄운 백엔드 서버가, 전혀 다른 세상인 윈도우의 3000번 포트로 곧장 튀어나오게 해주는 마법의 연결망, 이것이 최신 OS 간 브릿지 엔지니어링의 위력이다."
