---
layout: default
title: "6주차: 터미널의 혁신, Windows Terminal"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="40" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Windows Terminal Architecture</text><rect x="50" y="60" width="150" height="100" fill="#333" rx="5"/><text x="125" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">cmd.exe</text><rect x="225" y="60" width="150" height="100" fill="#005A9E" rx="5"/><text x="300" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PowerShell</text><rect x="400" y="60" width="150" height="100" fill="#E95420" rx="5"/><text x="475" y="115" fill="white" font-size="16" font-family="monospace" text-anchor="middle">WSL2 (Ubuntu)</text></svg>
</div>

# 6주차: GPU 가속기 융합과 Windows Terminal

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_06.png)
<br>

과거 파란색 창과 검은색 창이 분리되어 개발자를 괴롭히던 지저분한 레거시 콘솔 호스트 환경은 이제 죽었습니다.

이번 6주차 세션에서는 게임 그래픽 엔진을 본떠 만든 **GPU 하드웨어 가속 렌더링**을 탑재하여 미친 출력 속도를 자랑하는 다중 콘솔 렌더링 앱, **Windows Terminal (WT)** 의 구조를 탑재합니다. 
터미널 설정 자체를 GUI 툴이나 마우스가 아니라 **JSON 포맷**으로 직접 코딩하고, 파워셸·명령프롬프트·리눅스 쉘을 하나의 탭 인프라 안에 모두 융합시켜버리는 워크스페이스 분할 구축 스킬을 시연합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 화면 꾸미기를 넘어서, 커스터마이징 가능한 JSON 환경 맵핑과 다중 셸 병합의 궁극적인 아키텍처 원 포인트를 소개합니다.

1. [Windows Terminal 아키텍처](./01_terminal_engine/index.md)
   > 꽉 막혔던 conhost.exe의 한계를 부수고 GPU 가속기를 태워 압도적인 속도를 내뿜는 윈도우 터미널 통합 탭 엔진의 내부 구조와 Split Pane 셋업.

<hr style="margin: 40px 0;">

> **💡 개발 툴링 환경에 대하여**
> "자신이 하루 종일 타이핑을 하는 무대(터미널)의 폰트 렌더링 속도와 테마에 투자하지 마는 것은 칼을 갈지 않는 무사와 같다."
