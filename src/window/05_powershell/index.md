---
layout: default
title: "5주차: 차세대 프레임워크, PowerShell 객체 셸"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="40" width="200" height="120" fill="#333" rx="5"/><text x="150" y="75" fill="white" font-size="16" font-family="monospace" text-anchor="middle">bash (Text)</text><text x="150" y="105" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">grep / awk</text><rect x="350" y="40" width="200" height="120" fill="#005A9E" rx="5"/><text x="450" y="75" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PowerShell (Object)</text><text x="450" y="105" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">.WorkingSet > 1GB</text><path d="M 260 100 L 340 100" stroke="white" stroke-width="4"/></svg>
</div>

# 5주차: 차세대 객체 프레임워크 셸 - PowerShell

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_05.png)
<br>

CMD 환경의 치명적 설계 단점은 바로 셸의 응답 결과가 파싱하기 어려운 그저 '글자의 나열(Text Stream)'이라는 데 있습니다. 리눅스의 강력한 bash 스크립터들조차 문자열 파싱을 위해 지저분한 정규식에 의존해야 합니다. 

이번 5주차에는 마이크로소프트의 역작이자 현대 윈도우 인프라를 지배하는 **PowerShell** 딥다이브에 돌입합니다. 문자가 아닙니다! 실행 즉시 **오브젝트(Object)** 를 반환하여 개발자가 `.WorkingSet` 속성을 직접 접근해 메모리를 조작해 버릴 수 있는 차세대 닷넷(.NET) 터미널의 위력과, `Profile.ps1`을 통한 커스텀 진입 셋업 구성을 마스터합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 명령어 타이핑 구역을 벗어나 완전한 프로그래밍 언어로 승급한 PowerShell의 기초 2부작입니다.

1. **[객체기반 셸의 탄생](./01_powershell_intro/index.md)**
   > 단순 텍스트(String)를 버리고 닷넷 객체(Object Pipeline)를 반환함으로써 시스템 제어의 뎁스를 바꿔버린 철학 전환.
2. **[개발자 셸 셋업과 프로필](./02_dev_shell/index.md)**
   > 윈도우 보안 ExecutionPolicy 해방과 `Verb-Noun` 스크립트 작성법, Oh-My-Posh 프로프트 테마 기반 환경 구축법.

<hr style="margin: 40px 0;">

> **💡 차세대 쉘 아키텍처**
> "파워셸의 진짜 공포이자 파괴력은 텍스트 정규식 노가다를 없애 버렸다는 것이다. 당신은 그저 시스템이 던져준 객체의 속성값 배열을 조립하기만 하면 된다."
