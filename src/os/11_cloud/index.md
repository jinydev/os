---
layout: default
title: "11주차: 가상화와 클라우드 OS (하이퍼바이저·K8s 개요)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Type 1 Bare Metal (KVM/ESXi)</text><text x="300" y="130" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Type 2 Hosted (VirtualBox)</text></svg>
</div>

# 11주차: 가상화와 클라우드 OS 마스터 (하이퍼바이저·K8s 개요)

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_11.png)
<br>

지난 10주차 컨테이너(Docker)의 세계 너머에는, 아예 물리 하드웨어와 거대한 서버 팜 자체를 통째로 가상 생태계로 덮고 찍어내는 궁극의 **가상화(Virtualization) 인프라**가 기다리고 있습니다. 

이번 11주차 모듈에서는 물리적 CPU 칩셋에 숨겨진 또 다른 절대 권력자 '하이퍼바이저(Hypervisor)'의 링 권한을 분석합니다. 또한 만 대가 넘는 무수한 서버 대군과 도커 컨테이너들을 마치 하나의 유기적인 컴퓨터인 것처럼 자가 치유(Auto-Healing)하며 조율해 내는 클라우드 OS의 진수, **쿠버네티스(Kubernetes) 오케스트레이터의 아키텍처**와 0.1초 만에 부팅하는 **차세대 Micro-VM 체계**를 통합 파악합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단일 유닉스 단말기를 벗어나 대규모 서버 오케스트레이션과 인프라 추상화를 이루는 핵심 기술 3단계를 해부합니다.

1. **[가상화와 하이퍼바이저 링(Ring) 레벨](./01_hypervisor/index.md)**
   > 커널 모드보다 훨씬 아래인 Ring -1 레벨에 스텔스처럼 잠입하여 메모리 폴트를 낚아채는 KVM/VMware의 HW 가상화 원리.
2. **[쿠버네티스(Kubernetes) 오케스트레이터](./02_kubernetes/index.md)**
   > 인프라를 프로그래밍 문서로 서술하는 '선언적(Declarative)' 상태 감시 패러다임과 수만 대 K8s 클러스터의 자가 복원 기술.
3. **[서버리스와 극초기화 마이크로-VM](./03_micro_vm/index.md)**
   > 컨테이너 격리의 한계를 부수고 VM의 단점을 걷어내어 단 150ms 만에 콜드 부팅하는 AWS Firecracker 등 차세대 엔진의 등장.

<hr style="margin: 40px 0;">

> **💡 클라우드 인프라의 철학**
> "클라우드의 본질은 남의 컴퓨터를 쓰는 것이 아니다. 수만 개의 쇠덩이 컴퓨터 칩셋을 논리적 소프트웨어 시스템 코드로 완전히 추상화하여(Infrastructure as Code) 단 한 줄의 코드로 통제하는 사상이다."
