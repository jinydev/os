---
layout: default
title: "9주차: 하이브리드 엔진, WSL2 아키텍처"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="80" width="200" height="80" fill="#0078D7" rx="5"/><text x="150" y="125" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows NT Kernel</text><rect x="350" y="80" width="200" height="80" fill="#E95420" rx="5"/><text x="450" y="125" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Linux Kernel</text><rect x="50" y="30" width="500" height="30" fill="#333" rx="5"/><text x="300" y="50" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Hyper-V Hypervisor Layer</text></svg>
</div>

# 9주차: 리눅스를 품은 윈도우, WSL2 엔진

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_09.png)
<br>

윈도우 개발 환경은 편하지만, 세상 99%의 프로덕션 백엔드 서버는 결국 리눅스로 배포됩니다. 그렇다고 코딩할 때마다 거북이 같은 가상머신(VM)을 띄우거나 듀얼 부팅을 하는 것은 엄청난 엔지니어링 낭비입니다.

이번 9주차 렉처는 운영체제 기술의 기적이라고 불리는 **WSL2 (Windows Subsystem for Linux 2)** 의 하드웨어 가상화 아키텍처를 해부합니다. 
윈도우 NT 커널 밑바닥에 Hyper-V 스위치를 달아 진짜 Linux 커널을 동시에 맞물리게 돌리는 미친 구조, 그리고 이 이기종 커널들이 파일 자원을 징그럽게 주고받을 수 있게 하는 `9P 네트워크 프로토콜` 파일 연결 구조를 직관(Inspect)해 냅니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순히 리눅스 커맨드 창 하나 띄우는 것이 아닙니다. 파일 징검다리를 이해해야 퍼포먼스 드랍을 막습니다.

1. [극강 통신 하이브리드 아키텍처](./01_wsl2_architecture/index.md)
   > 단순 명령어 번역(WSL1)을 탈피하고 경량 머신 안에 찐 리눅스 커널을 분리 이식시킨 WSL2의 철학.
   > 윈도우의 `\\wsl$\Ubuntu` 접근과 리눅스의 `/mnt/c/` 접근에 대한 상호 브릿지 구조.

<hr style="margin: 40px 0;">

> **💡 두 커널의 대화**
> "클라우드의 제왕인 리눅스를 안방의 지배자인 윈도우가 가상화로 흡수한 순간, 윈도우는 개발자에게 가장 완벽한 퓨전 하이브리드 머신으로 다시 태어났다."
