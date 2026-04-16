---
layout: default
title: "12주차: 현대 OS 보안 (Linux 권한·SELinux·eBPF)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">MAC (Mandatory Access Control)</text><rect x="150" y="90" width="300" height="50" fill="#E81123" rx="5"/><text x="300" y="120" fill="white" font-size="16" font-family="monospace" text-anchor="middle">SELinux Enforcing</text></svg>
</div>

# 12주차: 현대 OS 보안 (Linux 권한·SELinux·eBPF)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_12.png)
<br>




## 1. 심층 DAC 권한과 SetUID 비트

[실전 심화 렉처]
리눅스의 기초 rwxrwxrwx (소유자, 그룹, 기타) 9자리 신분 제약 권한은 DAC(임의 접근 제어) 방식입니다.
일반 유저가 비밀번호를 바꿀 때 쓰이는 `passwd` 파일이나 `sudo` 명령체계는 본질적으로 루트(Root)만 접근 권한이 있어야 합당합니다. 여기서 등장하는 것이 **SetUID(s비트)**의 마법입니다! 이 비트가 켜진 프로그램은 실행되는 그 순간(찰나의 프로세스타임)에만 파일의 원래 주인(root) 레벨인 초인 권한을 획득했다가 종료 시 권한을 즉각 반납합니다. 이것이 바로 리눅스 보안 권한 관리의 숨겨진 트릭 오케스트라입니다.

## 2. MAC 강제 제어 (SELinux와 AppArmor)

[실전 심화 렉처]
그런데 해커가 뚫고 들어온 웹 서버가 시스템 전체 /etc/passwd 파일을 털어버리면 어떻게 될까요?
현대 시스템 보안은 여기서 멈추지 않고 MAC(강제 제어 규칙) 감옥을 이중으로 깔아버립니다. NSA가 주도해 만든 RedHat의 `SELinux` 나 우분투 베이스의 `AppArmor`는 "비록 웹 데몬이 소유 권한이 있더라도, 사전에 정의한 룰북(Policy)에 없으면 /bin/sh 같은 치명적 쉘 호출이나 임의 포트 바인딩을 무조건 커널단에서 원천 거절해버립니다". 즉 커널 단에 정책 지배 모듈을 삽입해버린 무적 방패입니다.

## 3. eBPF: 괴물 같은 관찰 및 보안 동맥 추적

[실전 심화 렉처]
현대 OS 관찰성 및 보안의 최종 레이어는 단연코 eBPF(Extended BPF) 기법입니다!
과거엔 커널에 방화벽 모듈을 박으려면 보안 프로그램을 직접 커널 소스로 코딩해 컴파일 빌드해서 위험하게 주입(LKM)해야 했습니다. 하지만 eBPF 체계는 C코드 기반 작은 eBPF 샌드박스를 제공하여 "커널 공간에 전혀 충돌(Panic) 부담을 안 주면서 모든 시스템 콜이 발생하거나 백엔드 통신 패킷이 떨어질 때마다 즉석으로 JIT 후킹"을 수행하게 해줍니다.
특정 도커 앱이 외부 IP로 수상한 소켓 통신을 열면 이가 수행되기도 전에 eBPF 레이어(Cilium, Falco 등)가 실시간 적발·색출 후 즉각 폭파(Drop) 처리하는 괴물 같은 현대 사이버 킬 체인이 여기에 존재합니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="300" cy="100" r="60" fill="none" stroke="#0078D7" stroke-width="4"/><text x="300" y="105" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">seccomp</text></svg>
</div>

## [전공 심화] DAC을 넘어선 강제 통제 MAC (SELinux)

리눅스 시스템에 익숙해진 여러분이 마주할 가장 단단한 보안벽은 NSA(미 국가안보국)가 개발한 모듈, SELinux입니다. 아무리 루트 권한을 취득하여 DAC(파일 소유자 권한) 폴더를 파먹으려 한들, 각 프로세스와 파일 단위에 붙은 MAC 보안 컨텍스트 라벨이 일치하지 않으면 Kernel 단계에서 접근 시도를 강제 파괴해버리는 극한의 샌드박스입니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">eBPF Security Observability (Cilium)</text></svg>
</div>

## [전공 심화] Seccomp 와 eBPF 보안 탐지망

모든 시스템 콜을 허용할 필요는 없습니다. 시큐어 컴퓨팅 모드(seccomp)는 특정 실행 파일의 시스템 콜 진입을 화이트리스트로 검문합니다. 나아가 커널을 재컴파일하지 않고도 커널 내부 C코드 이벤트를 후킹해 의심스런 Shellcode 실행과 포트 바인딩을 잡아채는 eBPF 기술은 현대 사이버 관제 플랫폼의 신기술입니다.
