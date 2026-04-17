---
layout: default
title: "2. 중간고사 실기 평가 안내"
---

# 2. 중간고사 실기 평가 및 문항 안내

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#E81123" font-size="24" font-family="monospace" text-anchor="middle">Summary Assessment</text></svg>
</div>

## 이론-실기 병합 평가 지침

상반기 평가는 종이 위에서 끝나는 암기 테스트가 아닙니다. 터미널 프롬프트에서 벌어지는 시그널을 해석하는 실무와 결합됩니다.

* **프로세스 궤적 추적**: `fork()`와 `exec()`가 파생시키는 메모리 PCB 스냅샷의 계산식 해결 문항.
* **스케줄러 튜닝 이슈**: 백그라운드 서버 프로세스들이 O(logN) CFS 스케줄러 환경 하에서 선점율(nice 값)에 따라 겪게 되는 CPU 지연율 지표 도출.
* **가상 메모리 한계점**: 외부/내부 단편화와 요구 페이지 폴트를 분석하고, 터미널의 `free -m`이나 `top` 스크린샷에 찍힌 증상을 판독하는 분석형 문항.

단순 정답보다 "왜 이런 시스템 에러가 발생했으며 하드웨어의 병목 지점은 어디인가?"를 논리적으로 서술해 내는 능력이 채점의 기준이 됩니다.
