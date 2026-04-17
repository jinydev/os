---
layout: default
title: "8주차: Windows 네이티브 프로그래밍과 C#"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="120" height="100" fill="#5C2D91" rx="5"/><text x="110" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">C# Source</text><path d="M 180 100 L 250 100" stroke="white" stroke-width="3" marker-end="url(#a)"/><rect x="250" y="50" width="120" height="100" fill="#333" rx="5"/><text x="310" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">csc.exe</text><path d="M 380 100 L 450 100" stroke="white" stroke-width="3" marker-end="url(#a)"/><rect x="450" y="50" width="120" height="100" fill="#0078D7" rx="5"/><text x="510" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Hello.exe</text><defs><marker id="a" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" fill="white"/></marker></defs></svg>
</div>

# 8주차: Windows 네이티브 객체 생태계 - C#

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_08.png)
<br>

파이썬 개발자나 자바 스프링 개발자가 윈도우용 응용 프로그램을 만들고 싶다면 그건 외래종 언어로 커널을 어설프게 건드리는 것에 불과합니다. 만약 윈도우 깊숙한 곳의 메모리와 사용자 화면(GUI)을 극한으로 매끄럽게 통제하고 싶다면 마이크로소프트의 공식 혈통, **C#** 을 만나야 합니다.

이번 시간은 단순히 C# 문법을 배우는 코딩 튜토리얼이 아닙니다. 
무거운 통합 개발 환경(Visual Studio)의 마법 같은 클릭 플레이를 치워버리고, 오직 평문 텍스트 코드 조각이 윈도우 깊은 곳의 `.NET` 컴파일러 엔진(`csc.exe`)을 터미널에서 강제로 거쳐 어떻게 실행 가능한 기계어(`Hello.exe`) 덩어리로 변환되는지 그 원초적 블랙박스를 터미널 환경에서 타격합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

무거운 IDE 도구를 버리고 운영체제의 엔진(CLR)과 직접 맞붙는 빌드업 구조 투어.

1. **[윈도우 네이티브 객체, C#](./01_dotnet_native/index.md)**
   > 객체지향 닷넷(.NET) 공통 언어 런타임(CLR) 과 메모리의 가비지 컬렉션 아키텍처 이해.
2. **[터미널 기반 네이티브 빌드](./02_cli_compile/index.md)**
   > IDE를 거치지 않고 소스코드를 네이티브 윈도우즈의 컴파일러 `csc.exe` 에 직접 던져넣는 .EXE 파일 타격 방식.

<hr style="margin: 40px 0;">

> **💡 개발 환경의 본질**
> "단순히 초록색 '실행' 화살표를 누르고 결과만 기다리는 것은 개발에 종속되는 것이다. 진정한 개발자는 텍스트가 기계어로 응집되는 그 파이프라인의 조종 권한을 터미널에서 제어한다."
