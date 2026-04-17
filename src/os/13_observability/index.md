---
layout: default
title: "13주차: 성능 분석과 관찰성 (perf·Flame Graph)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="50" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Flame Graph Profiling</text><rect x="250" y="90" width="100" height="20" fill="#E81123"/><rect x="200" y="110" width="200" height="20" fill="#E95420"/><rect x="150" y="130" width="300" height="20" fill="#F4D03F"/></svg>
</div>

# 13주차: 성능 관찰성과 SRE 딥다이브 (perf·Flame Graph)

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_13.png)
<br>

서버가 다운되진 않았는데 원인 모를 병목으로 CPU 사용량은 치솟고 유저 응답 지연율이 5초를 넘어가고 있습니까? 우리는 더 이상 터미널에서 바보같이 `top` 유틸리티 하나만 바라보고 원인을 예측할 수 없습니다.

이번 13주차 렉처는 운영체제 관리를 넘어선 **SRE(Site Reliability Engineering)**의 정수를 향해 달립니다. 하드웨어 CPU 칩셋 자체의 브랜치 캐시 미스를 긁어오는 `perf` 카운터부터, 넷플릭스 아키텍트가 발명한 시각적 킬러 툴 **플레임 그래프(Flame Graph)**, 그리고 수천 대의 MSA 파드들을 엮어 지표를 슬러핑하는 **프로메테우스/그라파나** 관찰성 패러다임까지 분산 서버 시스템의 '시야(Sight)'를 장착합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

블랙박스가 된 서버 커널 트랜잭션을 사람의 눈으로 파싱하기 위한 3단계 시각화 툴 체커 보드입니다.

1. **[`top`의 한계와 perf 프로파일링](./01_perf_profiling/index.md)**
   > 단순 Load Average 측정을 벗어나, 하드웨어 타이머와 L2 레지스터 센서에 직결되어 병목을 탐지하는 `perf`의 활용성.
2. **[플레임 그래프(Flame Graph) 분석 지형](./02_flame_graph/index.md)**
   > 99헤르츠 샘플링된 함수 콜스택을 뚱뚱하게 렌더링 된 블록 SVG로 타겟팅하여 코드 병목을 저격하는 마스터 기술.
3. **[마이크로서비스와 관찰성 지표](./03_observability_trend/index.md)**
   > 단일 서버를 벗어나 OpenTelemetry 로그 추적과 Prometheus/Grafana 지표 대시보드를 구축하는 모던 클라우드 관찰력.

<hr style="margin: 40px 0;">

> **💡 현대 성능 엔지니어링 마인드셋**
> "최고의 최적화는 무작정 코드를 고치는 것이 아니라, 가장 병목이 심한 뜨거운 불꽃(가장 넓은 블록)을 정확히 정밀 타격하여 증명해 내는 시각적 관찰력에서 파생된다."
