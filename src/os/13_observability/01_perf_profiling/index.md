---
layout: default
title: "1. 탑(top)의 한계와 perf 프로파일링"
---

# 1. `top` / `htop` 의 한계 돌파와 `perf`의 등장

여러분이 마주할 실무 운영 서버 환경은 터미널에서 `top` 명령 하나만 치고 가만히 앉아 'Load Average' 숫자만 바라보는 낮은 레벨이 아닙니다. 만약 모니터링상에서 CPU는 100%로 맹렬하게 풀 로드 중인데, 사용자에게 응답하는 쿼리(네트워크) 전송량은 0인 블랙아웃(Blackout) 타임에 빠졌다면 어떻게 해야 할까요?

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">perf stat -e cache-misses</text></svg>
</div>

## 하드웨어 카운터 덤프: perf 체계
엔지니어는 `perf stat` 등 최상위 계층의 리눅스 프로파일링 도구를 즉각 집어넣어야 합니다! 

`perf` 툴셋은 CPU 코어 내부에 하드웨어 레벨로 칩셋에 은밀히 심어진 '이벤트 카운터 센서 레지스터' 값들을 무자비하게 싹 다 긁어들여옵니다. 이를 통해 조건문 분기(Branch Prediction) 예측 실패율이 얼마나 막대한지, `L2/L3` 캐시 미스가 얼마나 빈번하게 발생하여 CPU 병목을 일으키고 굶겨 죽이고 있는가를 가장 적나라하게 하드웨어 분석 데이터로 던져 냅니다.
