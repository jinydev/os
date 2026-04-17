---
layout: default
title: "3. 마이크로서비스와 관찰성 지표"
---

# 3. 분산 측정과 관찰성(Observability) 모델

이제는 서버가 1대인 시대가 아닙니다! 클라우드 분산 아키텍처 세계관(Kubernetes 클러스터)에서는 단 하나의 유저 요청을 처리하기 위해 수십 개의 컨테이너 서비스 노드가 거미줄처럼 동기화되어 통신 릴레이를 처리합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#0078D7" font-size="18" font-family="monospace" text-anchor="middle">Prometheus &amp; Grafana Observability</text></svg>
</div>

## 분산 추적 (Distributed Tracing)
유저의 버튼 클릭 한 번이 `A 프론트 앱 → B 게이트웨이 → C 인증망 → D 데이터베이스`로 흘러가는 이 거대한 통신 지연 양상을 어떻게 트래킹할까요? 우리는 "OpenTelemetry" 단일표준과 "Jaeger" 추적 엔진을 써서, 요청 객체에 고유한 'Trace ID' 배지를 붙여 날림으로써 시각적 네트워크 지연 랠리를 싹 잡아냅니다.

## 시계열 지표 분석망 (Metrics & Dashboard)
수백 대 분리된 마이크로서비스의 CPU 부하율과 네트워크 지표를 확인하려 일일이 SSH로 `vmstat`을 타이핑하고 있을 수는 없습니다. 

모든 수백 개의 OS 메트릭스(Metrics) 정보를 푸시/풀 기반의 시계열 DB인 **프로메테우스(Prometheus)**가 동기화로 전부 쓸어담고(Slurping), 이를 **그라파나(Grafana) 대시보드**의 화려한 차트로 시각화합니다. 어느 노드 구간에서 Latency 가 심각하게 정체(Spike)되는지를 단박에 잡아내는 **SRE(사이트 신뢰성 엔지니어링)**의 표준 신기술 패러다임입니다.
