---
layout: default
title: "2. 터미널 기반 네이티브 빌드"
---

# 2. 터미널 기반 Hello World 네이티브 컴파일

보통 C#을 처음 공부하게 될 경우 수 기가바이트(GB)에 육박하는 거대하고 무거운 `Visual Studio` 통합 툴을 깔고 마법의 `빌드 및 실행(F5)` 초록색 화살표 버튼을 클릭해서 프로그래밍을 합니다.

그러나 이런 식의 구동은 코드가 도대체 컴퓨터 내부에서 어떤 컴파일 파이프라인(Compilation Pipeline)을 거쳐 윈도우가 읽어 들이는 기계어 `.exe` 파일로 압축되는지 그 블랙박스 내부 과정을 철저히 은폐시킵니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe</text></svg>
</div>

## `csc.exe` 터미널 빌드 엔진 조작
우리는 이런 무거운 편의성 IDE 툴을 쓰지 않습니다. 그저 가장 원초적인 메모장(VS Code 등 빈 껍데기 파일) 하나만을 열어 `Program.cs` 원시 코드를 타이핑한 뒤, 윈도우즈 디렉터리 아주 싶은 곳에 박혀 숨 쉬고 있는 순수 네이티브 닷넷 컴파일러인 **`csc.exe`** 빌드 훅(Build Hook)을 터미널 환경에서 직접 타격합니다! 

코드를 강제 압축시켜 `Hello.exe` 라는 실행 파이프라인 파일을 내 손으로 깎아내려 보며 닷넷 코어 엔진의 체계를 깨부수는 실증에 도달합시다.
