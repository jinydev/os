---
layout: default
title: "2. 변수 셋업 튜닝과 오염 방어"
---

# 2. 변수 조작과 스코프 오염 방어망

파이썬(Python) 3.8 버전을 깔고 쓰다가 최신의 파이썬 3.11 버전을 또 C 드라이브에 깔았다고 가정해 봅시다. 터미널 창을 열고 `python -V`를 쳤는데 기대와 달리 예전 버전인 3.8 이 출력됩니다! 왜 그럴까요?

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">set PATH=C:\Temp;%PATH%</text><text x="300" y="140" fill="gray" font-size="16" font-family="monospace" text-anchor="middle">(Temporary Session Override)</text></svg>
</div>

## 스코프 충돌과 PATH 우선순위
`PATH` 환경 변수는 단일 값이 아니라 수많은 경로들의 **리스트 집합 체계(Array)**입니다. 먼저 등록되어 배지 1번을 달고 있는 상단 리스트 경로인 파이썬 3.8 폴더에서 `python.exe`를 먼저 찾아버렸기 때문에 커널 엔진이 하단 스캔을 즉시 중단해 버린 것입니다.

패키지를 이것저것 지저분하게 깔다 보면 이처럼 오염된 시스템 환경 변수 `PATH`의 라우팅 순서를 복구 튜닝해야만 합니다. 고급 시스템 속성(GUI)에서 사용자 단일 변수와 글로벌 시스템 변수의 스코프(Scope)를 분리하여 우선순위를 정리하는 기술, 나아가 영구 반영치 않고 잠깐의 디버깅 테스트를 위해 현재 열린 터미널 콘솔창에서 1회성 세션으로만 임시 변수를 덧씌우는 `set MY_KEY=val` 조작 패러다임을 이해해야 합니다.
