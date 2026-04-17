---
layout: default
title: "1. 극강 통신 아키텍처"
---

# 1. WSL2 의 극강 통신 하이브리드 아키텍처

우리는 개발을 원활하게 하기 위해 결국은 전 세계 서버 표준인 **"리눅스(Linux)"** 환경으로 도달해야만 합니다. 그러나 노트북을 포맷하고 리눅스를 설치하거나, 느려터진 가상머신(VMware, VirtualBox)을 띄우는 것은 끔찍한 제약입니다.

마이크로소프트의 최후의 카드이자 최고의 발명품, **WSL2 (Windows Subsystem for Linux 2)**는 이 모든 굴레를 박살 냅니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="80" width="200" height="80" fill="#0078D7" rx="5"/><text x="150" y="125" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows NT Kernel</text><rect x="350" y="80" width="200" height="80" fill="#E95420" rx="5"/><text x="450" y="125" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Linux Kernel</text><rect x="50" y="30" width="500" height="30" fill="#333" rx="5"/><text x="300" y="50" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Hyper-V Hypervisor Layer</text></svg>
</div>

## MS의 결단: 찐 리눅스 머신을 가볍게 때려 박다
과거 명령어 번역기에 불과했던 WSL1과 달리, WSL2는 윈도우 OS 커널 맨 밑바닥에 `Hyper-V` 라는 경량 가상화 하이퍼바이저 층을 깔고 그 위에 윈도우와 **진짜 완전한 마이크로 리눅스 커널**을 병렬로 나란히 올려버린 미친 구조를 지닙니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><path d="M 200 100 Q 300 20 400 100" fill="none" stroke="#00FF00" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="60" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">9P Network Protocol Share</text><text x="150" y="140" fill="white" font-size="20" font-family="monospace" text-anchor="middle">\\wsl$\Ubuntu</text><text x="450" y="140" fill="white" font-size="20" font-family="monospace" text-anchor="middle">/mnt/c/</text></svg>
</div>

우리는 윈도우 탐색기에서 `\\wsl$\Ubuntu` 라는 특수한 네트워크 드라이브 주소를 단숨에 타이핑하여 리눅스의 ext4 포맷 내부로 파일 입출력을 다이렉트 브릿지하는 놀라운 파일 공유 프로토콜(`9P`) 아키텍처 세계관에 거주하게 됩니다. 윈도우와 리눅스 커널 간 극강의 융합 엔진, 이것이 현대 윈도우 개발망의 결정체입니다.
