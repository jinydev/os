---
layout: default
title: "1. 가상화와 하이퍼바이저 링(Ring) 레벨"
---

# 1. 하드웨어 가상화와 하이퍼바이저 링 레벨

컨테이너(도커)가 동일한 리눅스 커널을 돌려쓰는 "프로세스 격리 꼼수"라면, 완전한 이종 커널 간의 동시 구동(예: 맥북 안에서 MS 윈도우 커널을 띄우고 리눅스도 같이 돌리는 것)은 물리 하드웨어 가상화 장비인 **하이퍼바이저(Hypervisor)** 계층이 없으면 절대 성립하지 않습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Type 1 Bare Metal (KVM/ESXi)</text><text x="300" y="130" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Type 2 Hosted (VirtualBox)</text></svg>
</div>

## [전공 심화] 하이퍼바이저 링(Ring) -1 패러다임

리눅스 커널이 Ring 0 특권 레벨을 지배할 때, 그 각기 다른 여러 개의 커널들을 밑에서 떠받쳐 가짜 하드웨어 스펙을 분배해주는 또 다른 시스템 황제가 바로 <b>하이퍼바이저</b>입니다.

인텔의 `VT-x` 나 AMD의 `AMD-V` 같은 CPU 전용 가상화 하드웨어 명령어 칩셋이 부팅부터 **Ring -1 레벨 (일반 OS 커널보다 더 밑바닥에 권한이 있는 특권층)**로 깊숙히 개입합니다. 여러 개의 게스트 OS가 충돌을 일으킬 만한 모든 메모리 간섭 현상이나 페이지 폴트를 중간 하드웨어에서 꿀꺽 집어삼킨 뒤, 몰래 CPU 처리를 대리수행(Shadow Paging & EPC) 시켜 줍니다. 
오늘날 아마존 AWS 클라우드 등에 띄워진 무수한 KVM 기반 가상 서버 인스턴스들도 이렇게 정교한 하드웨어 CPU 특권 은폐 트릭으로 초고속 네이티브 성능(99.9%)을 유지할 수 있습니다.
