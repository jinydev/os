---
layout: default
title: "1. 터미널의 동맥 망, 환경 변수"
---

# 1. 터미널의 동맥 망과 PATH의 비밀

서버나 개발 환경을 구축하다 보면 1순위로 만나는 오류가 바로 `command not found` (명령어를 찾을 수 없습니다) 입니다. 분면 파이썬을 C드라이브 어딘가에 설치했는데, 터미널(cmd) 창을 열고 `python`이나 `node`를 치면 먹통이 됩니다.

## 시스템의 방향키, PATH
윈도우 터미널이 고장 난 게 아닙니다. 터미널은 빙충맞게 운영체제 전체 하드디스크를 알아서 샅샅이 뒤져 스크립트 실행 파일을 찾아내 주지 않습니다. 
터미널은 입력한 명령어를 오직 **`PATH` (경로)** 라고 이름 붙여진 거대한 "환경 변수"의 세미콜론(`;`) 목록 안에서만 기계적으로 순서대로 찾습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="50" cy="60" r="20" fill="#0078D7"/><text x="300" y="65" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Global (System) PATH + Local (User) PATH</text></svg>
</div>

새로운 개발 언어나 패키지 모듈을 다운로드 받았다면, 반드시 그 위치를 윈도우 커널이 인식하는 이 `PATH` 변수 리스트에 등록해 주어야만 터미널의 어느 위치 폴더(`C:\temp` 든 `D:\work` 든)에서건 자유자재로 해당 패키지 명령어를 호출할 수 있습니다. 이것이 윈도우 애플리케이션 실행 아키텍처의 가장 근본적인 연결 혈관입니다.
