---
layout: default
title: "2. 플레임 그래프(Flame Graph)"
---

# 2. 플레임 그래프(Flame Graph) 분석 지형

아무리 `perf`가 방대한 콜스택 로그 텍스트를 제공한다고 해도, 문자의 홍수만으로는 스파게티처럼 꼬인 수백만 줄의 서버 코드 중 어느 곳이 끔찍한 진짜 병목 포인트(Bottleneck)인지 사람 눈으로 곧장 찾아낼 수 없습니다.

## 시각적 파괴력: 불꽃놀이의 마스터피스
넷플릭스(Netflix)의 전설적인 성능 엔지니어인 브렌단 그레그(Brendan Gregg)가 창시한 **플레임 그래프(Flame Graph)**에 주목하십시오.

`perf record -F 99`와 같은 명령어로 1초에 99번(99헤르츠 비율) CPU 콜스택 조각들을 실시간 표본 추출(Sampling)한 뒤, 이 수학적 스택 데이터를 가로 길이 블록 기반의 시각적 형태, 일명 **"불꽃 모양(Flame)"** SVG 화상 지도로 렌더링 전개합니다!

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="50" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Flame Graph Profiling</text><rect x="250" y="90" width="100" height="20" fill="#E81123"/><rect x="200" y="110" width="200" height="20" fill="#E95420"/><rect x="150" y="130" width="300" height="20" fill="#F4D03F"/></svg>
</div>

위로 치솟은 스택의 가장 넓고 뚱뚱한(가로가 제일 두꺼운) 불꽃 덩어리 블록 구간이 당신의 호스트 서버 성능 CPU를 가장 기형적으로 많이 까먹고 있는 **악성 재귀 함수**이거나 **불필요한 시스템 콜 락(Lock) 무한 경합 블록**입니다. 이제 눈먼 장님이라도 즉각 지연율의 원흉을 가장 빠르게 타겟팅하여 잘라낼 수 있게 됩니다.
