---
layout: default
title: "10주차: 컨테이너 딥다이브 (Linux 네임스페이스와 cgroup)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="30" width="500" height="40" fill="#333" rx="5"/><text x="300" y="55" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Linux Kernel (host)</text><rect x="50" y="100" width="230" height="80" fill="#E81123" rx="5"/><text x="165" y="145" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Container 1 (PID 1)</text><rect x="320" y="100" width="230" height="80" fill="#0078D7" rx="5"/><text x="435" y="145" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Container 2 (PID 1)</text><path d="M 165 70 L 165 100" stroke="white" stroke-width="4"/><path d="M 435 70 L 435 100" stroke="white" stroke-width="4"/></svg>
</div>

# 10주차: 컨테이너 딥다이브 (Namespace와 Cgroup의 비밀)

가상 머신(VM)의 하이퍼바이저 패러다임을 박살 내고 현대 클라우드 서버 생태계를 송두리째 잡아먹은 **컨테이너(Container)** 패러다임. 혹시 여러분은 아직도 도커(Docker)를 '초경량 리눅스 OS 에뮬레이터'라고 생각하고 계신가요?

이번 10주차 렉처에서는 도커의 허상과 외피를 벗겨내고, 오직 하나의 호스트에서 공유 커널 기반으로 작동하면서도 타 컨테이너를 절대 침범하지 못하게 막아버리는 실질적 리눅스 커널 격리 핵심 기법—네임스페이스(Namespace)와 물리 자원 상한선 통제 그룹인 Cgroup, 그리고 용량 낭비를 기적적으로 타파시킨 Layered File System—의 진정한 정체를 디코딩합니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

도커 마법의 실체를 3단계의 리눅스 커널 심화 핵심 모듈 컴포넌트로 해부했습니다. 

1. [도커의 정체와 네임스페이스 격리](./01_namespace_isolation/index.md)
   > VM의 한계를 무너뜨린 "서로 사기를 당하고 있는 격리 프로세스". PID 통제와 시야 차단의 매직.
2. [cgroup(Control Groups) 하드웨어 통제](./02_cgroup_control/index.md)
   > 호스트 CPU/RAM 100% 점유 폭주를 막는 물리적 오버헤드 감옥(Cgroup)과 OOM 개입 체계.
3. [OCI 규격과 이미지 레이어 (Layered FS)](./03_overlay_fs/index.md)
   > Union Mount 기술로 읽기 전용 베이스를 공유하여 파생 이미지를 무한 증식해도 디스크 낭비율이 제로인 설계.

<hr style="margin: 40px 0;">

> **💡 컨테이너 아키텍트의 명언**
> "컨테이너는 존재하지 않는다. 단지 커널 단에서 이름표(Namespace)가 달린 프로세스들만이 무한히 오케스트레이션 연주를 할 뿐이다."
