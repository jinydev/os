---
layout: default
title: "2. cgroup을 통한 하드웨어 통제"
---

# 2. cgroup(Control Groups)을 통한 하드웨어 통제 구역

네임스페이스를 통해 프로세스의 "시야"를 완전히 차단해 버렸다고 해도 물리적 제어망이 없으면 재앙이 터집니다. 
어느 한 컨테이너에 들어간 악성 백엔드 코드가 호스트 서버의 CPU 자원과 RAM 100%를 무한루프로 독점해 버리면, 같은 서버(노드)에 있는 다른 착한 자식 컴포넌트(서버)들이 전부 질식해 죽어버립니다(Noisy Neighbor 문제).

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="80" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">cgroups v2</text><text x="300" y="120" fill="gray" font-size="16" font-family="monospace" text-anchor="middle">Memory &amp; CPU Throttle Constraints</text></svg>
</div>

## 감옥의 창살: 리눅스 cgroup v2
리눅스 커널은 이런 무법자 프로세스들 파이를 조절하기 위해 **cgroup (Control Groups)** 이라는 무시무시한 서브시스템 트리 구조를 엽니다. 

커널이 엄격히 정해줍니다:
* "Nginx 웹 컨테이너 묶음은 절대 물리적 RAM 2GB를 넘기지 못해!" 
* "이 무거운 배포 스크립트 도커는 오직 0번, 1번 물리 CPU 코어 연산력의 50%만 배당해!"

만약 컨테이너가 폭주하여 자기에게 할당된 제한된 2GB 이상의 메모리를 추가로 점유해 구걸하려 든다면? 
Linux 커널에 상주하는 OOM Finder 조준 시스템이 즉각 개입하여 해당 컨테이너 내부 1번 프로세스에 무자비한 `SIGKILL (-9)` 총알을 박아버립니다. 터미널의 `docker stats` 명령어가 실시간으로 긁어다 출력하는 자원 점유율 표 데이터가 바로 호스트 리눅스의 이 cgroup 트리 메트릭을 파싱해 내는 것입니다.
