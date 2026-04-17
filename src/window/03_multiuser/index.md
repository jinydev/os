---
layout: default
title: "3주차: 다중 사용자 환경과 시스템 권한 제어"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="150" height="100" fill="#333" rx="5"/><text x="125" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Standard User</text><path d="M 210 100 L 390 100" stroke="#E81123" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="90" fill="#E81123" font-size="14" font-family="monospace" text-anchor="middle">UAC Elevation Request</text><rect x="400" y="50" width="150" height="100" fill="#0078D7" rx="5"/><text x="475" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Administrator</text></svg>
</div>

# 3주차: 관리자 계정 모델(UAC)과 레지스트리 디버깅

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_03.png)
<br>

서버 프로그램 개발 시 빈번하게 터지는 "권한 거부(Permission Denied)"나 화면에 아무 오류도 뜨지 않고 프로그램이 백그라운드에서 죽어버리는 현상의 원인은 무엇일까요?

이번 3주차에서는 컴퓨터 한 대에 파티션을 나눠 관리자와 일반 유저, 그리고 백그라운드 데몬 서비스 계정들이 공존하게 해주는 보안 철학인 **윈도우 UAC (User Account Control)** 패러다임을 분석합니다. 나아가 리눅스의 `/etc/` 텍스트형 설정 폴더를 대체하는 거대 두뇌인 **레지스트리(Registry)** 구조의 맵을 탐험하고, 보이지 않는 스파이웨어 에러를 추적하기 위해 **이벤트 뷰어(Event Viewer)**의 로그를 뜯어보는 디버깅 마스터클래스를 진행합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 프로그램 개발사를 넘어 시스템 권한 통제 계층과 은폐된 에러 추적기를 탐험하는 2부작입니다.

1. [윈도우 다중 사용자 환경과 UAC](./01_multiuser_env/index.md)
   > SYSTEM 관리자 계정과 일반 사용자 격리 시스템. 화면을 어둡게 막아서는 UAC 방어막의 진정한 존재 의미 파악.
2. [이벤트 뷰어와 레지스트리 디버깅](./02_event_viewer/index.md)
   > HKEY_LOCAL_MACHINE 구조 해부 및 보이지 않는 백그라운드 셧다운 원인을 붉은색 Event ID로 파밍해 내는 디버깅 스킬.

<hr style="margin: 40px 0;">

> **💡 권한 분리 철학**
> "최상위 권력(Root/Administrator)을 매 순간 쥐고 컴퓨터를 쓰는 것은 안전망 없는 스포츠카를 타는 것과 같다. 필요할 때만 호출하여 일회용으로 쓰는 것이 현대 운영체제 방어망 설계의 핵심이다."
