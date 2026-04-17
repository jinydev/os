---
layout: default
title: "1. 도커의 정체와 네임스페이스"
---

# 1. 도커(Docker)의 정체와 네임스페이스 격리

초보자들이 겪는 가장 흔한 착각이 "컨테이너 = 가벼운 가상 머신(VM)" 이라는 논리입니다. 이 개념은 철저히 틀린 멘탈 모델입니다!

도커엔 가상 머신(HW Hypervisor)이 존재하지 않습니다. 리눅스 컨테이너의 본질은 **"서로 거짓말을 당하고 있는 유저 권한 안의 단일 프로세스 그룹"**에 불과합니다. 단지 호스트 컴퓨터에 이미 띄워진 공유 커널(Linux 껍데기)이 제공하는 특수한 시각 차단막 공간에 갇힌 애플리케이션일 뿐, 풀 부팅된 OS가 아닙니다.

## [전공 심화] 네임스페이스 (Namespace) 격리
Linux의 네임스페이스(Namespace) 기능은 PID, Network, Mount 트리를 감쪽같이 위장시킵니다. 
컨테이너를 구동하면 해당 앱은 자기가 이 리눅스 시스템 우주의 1번 프로세스(PID 1) 권한이며, 컴퓨터가 가질 수 있는 유일한 네트워크 포트 랜카드(eth0)를 완전히 독점한 것처럼 리눅스 최상위 커널에게 사기를 당하여 홀로 외딴방에 갇혀 실행됩니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#0078D7" font-size="20" font-family="monospace" text-anchor="middle">Namespaces: IPC, Network, Mount, UTS</text></svg>
</div>

무거운 게스트 OS 커널이 이중 탑재되지 않으므로 성능 손실(VM Hypervisor Tax)이 문자 그대로 "0%"(Zero) 인 무자비한 퍼포먼스가 컨테이너 혁명의 핵심입니다.
