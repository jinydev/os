---
layout: default
title: "4주차: 컴퓨터의 핏줄, 환경 변수와 경로(PATH)"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="40" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Environment Variables Execution Flow</text><rect x="50" y="60" width="500" height="30" fill="#333"/><text x="300" y="80" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">1. C:\Windows\System32</text><rect x="50" y="100" width="500" height="30" fill="#0078D7"/><text x="300" y="120" fill="white" font-size="14" font-family="monospace" text-anchor="middle">2. C:\Python311\bin</text><rect x="50" y="140" width="500" height="30" fill="#E81123"/><text x="300" y="160" fill="white" font-size="14" font-family="monospace" text-anchor="middle">3. C:\Program Files\NodeJS</text></svg>
</div>

# 4주차: 시스템의 동맥망 - 환경 변수와 전역 경로망(PATH)

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_04.png)
<br>

처음 파이썬이나 노드(Node.js), 커스텀 해킹 스크립트 파일을 다운로드 받아 설치한 뒤 시커먼 터미널 창에서 야심 차게 엔터를 쳤을 때 우리를 반기는 건 무심한 `command not found` 빨간색 에러 문구입니다.

이번 4주차 렉처는 터미널 프로그램 라우팅의 고장 원인을 꿰뚫을 수 있는 윈도우 백엔드의 필수 교양, **환경 변수(Environment Variables)**와 그중에서도 명령어 탐색기 엔진인 **PATH** 목록의 스코프 메커니즘을 튜닝하는 실전적 방법을 배우게 됩니다. 모든 실행 엔진의 핏줄(라우팅)을 직접 조작해 봅니다!

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 에러 해결을 넘어 윈도우가 명령어를 스캐닝하는 트리거링 우선 심사 제어망을 구축합니다.

1. **[터미널의 동맥 망, 환경 변수 기초](./01_environment_vars/index.md)**
   > PATH 없이 왜 터미널 명령어는 작동하지 않는가? 실행 모듈을 커널 프로세스에 연결시켜 주는 동맥 망의 철학.
2. **[변수 셋업 튜닝과 스코프 오염 방어망](./02_path_manipulation/index.md)**
   > 엉뚱한 이전 구버전 런타임을 호출하는 스코프(Scope) 충돌 에러의 우선순위를 튜닝하고 터미널 단독 1회성 변수 적용법 분석.

<hr style="margin: 40px 0;">

> **💡 트러블슈터의 관점**
> "명령어가 실행되지 않는 건 엔진이 없어서가 아니라, 커널이 그 오두막(실행 파일)으로 가는 숲길 지도(PATH)를 받지 못해 헤매고 있는 것이다."
