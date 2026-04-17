---
layout: default
title: "1. 원격-WSL 이원화 메커니즘"
---

# 1. VS Code Remote-WSL 껍데기 분리 아키텍처

우리는 방금 전 챕터에서 윈도우 안쪽에 리눅스(WSL2)를 심었습니다. 그러면 윈도우 쪽에 깔려 있는 화려한 `VS Code` 그래픽 편집기 안에서, 도대체 어떻게 저 컴컴한 파이썬이나 노드(Node) 소스코드는 저 안쪽 리눅스 커널에 가두어 놓고 돌릴 수 있을까요?

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="60" width="200" height="80" fill="#0078D7" rx="5"/><text x="150" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code GUI (Windows)</text><path d="M 260 100 L 340 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="2,2"/><text x="300" y="90" fill="#00FF00" font-size="12" font-family="monospace" text-anchor="middle">Socket Tunnel</text><rect x="350" y="60" width="200" height="80" fill="#E95420" rx="5"/><text x="450" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">VS Code Server (.vscode)</text><text x="450" y="125" fill="white" font-size="12" font-family="monospace" text-anchor="middle">(Linux Subsystem)</text></svg>
</div>

## 에디터 프론트와 컴파일 서버 백엔드의 분리 철학
그 비밀은 바로 VS Code의 **분산-원격(Remote) 아키텍처**에 있습니다.

여러분이 윈도우에서 `VS Code` 를 열고 WSL에 연결하는 순간, 윈도우에 깔려 있던 VS Code는 자신의 컴파일 처리 엔진인 `VS Code Server (.vscode)` 조각 모듈을 WSL2 우분투 리눅스 안으로 은밀하게 배포하여 침투시킵니다.
그러면 진짜 컴파일과 소스코드 I/O(입출력) 분석은 100% 우분투 안의 엔진 서버가 수행하며, 윈도우에 떠 있는 우리 눈앞의 VS Code는 **그저 화면과 마우스 클릭만을 중계받는 일개 껍데기(Thin Client) 프론트 뷰어**로 전락하게 됩니다. 통신은 소켓 터널로 아주 빠르게 연결됩니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="80" fill="gray" font-size="16" font-family="monospace" text-anchor="middle">Do NOT place Code in C:\Drive</text><text x="300" y="120" fill="#00FF00" font-size="22" font-family="monospace" text-anchor="middle">git clone internally at ~/project</text></svg>
</div>

이것이 왜 중요할까요? 만약 윈도우의 `C:\` 폴더에 소스를 둔 채 파일 프로토콜 브릿지를 넘어 리눅스 커널더러 해석해 달라고 넘기게 되면 어마어마한 파일 번역 딜레이(퍼포먼스 쇼크)가 오기 때문입니다. 그래서 소스는 무조건 리눅스 내부(`~/`) 에 클론해 두고, 컴파일은 그 안에서 끝낸 뒤 윈도우 GUI로는 껍데기만 쏘게 하는 환상적인 이원화 체계가 탄생한 것입니다.
