---
layout: default
title: "3. Seccomp와 괴물 eBPF"
---

# 3. 제로-데이 방어: Seccomp와 eBPF 구조

MAC 규칙 역시 오탐지나 복잡성 한계가 있습니다. 현대 가용성 높은 클라우드 OS 관찰성 및 보안의 최종 레이어를 장식하는 것은, 단연코 실시간 시스템콜 후킹/필터링 기법입니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="300" cy="100" r="60" fill="none" stroke="#0078D7" stroke-width="4"/><text x="300" y="105" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">seccomp</text></svg>
</div>

## 1. Seccomp (시큐어 컴퓨팅 모드) 필터링
특정 도커나 프로세스가 리눅스에게 제공받는 300개가 넘는 시스템 콜(System Call)을 모두 호출할 필요는 절대 없습니다. `seccomp` 은 해당 컨테이너나 프로세스가 동작할 때 파일 읽기/쓰기/종료 외에 기상천외한 시스템 콜 구동을 시도하면 즉각적으로 커널 트랩 지점에서 실행 자체를 `SIGKILL` 쳐버리는 화이트리스트 검문소입니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">eBPF Security Observability (Cilium)</text></svg>
</div>

## 2. 동맥 직결 괴물 탐지망: eBPF (Extended BPF) 
과거 악성 트래픽을 막으려 커널에 강력한 방화벽 모듈을 박으려면 보안 회사가 이를 직접 컴파일 빌드해서 위험하게 주입(LKM)해야 했습니다. 
하지만 최신 리눅스의 **eBPF 체계**는, C코드 기반의 극소형 샌드박스 가상 머신(JIT 컴파일러)을 커널 안에 통째로 제공합니다.

eBPF는 "서버 커널 쪽에 전혀 충격/재부팅 부담을 안 주면서도, 모든 시스템 콜이 호핑하거나 외부 통신 소켓 패킷이 떨어질 때마다 실시간으로 C코드를 찔러 넣어(Hooking) 이벤트를 적발"하게 만듭니다. 
예를 들어 서버 속의 어떠한 불특정 앱이 몰래 가상 암호화폐 채굴장 IP로 통신을 열려는 그 순간, 그게 실행되기도 전에 밑바닥 eBPF 레이어(현행 Cilium, Falco 모듈 등)가 실시간으로 이를 적발·색출 후 즉각 모가지를 잘라버리는(Drop) 현대 클라우드 네이티브의 진정한 사이버 킬 체인 패러다임입니다.
