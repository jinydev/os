---
layout: default
title: "5. 실습 환경 준비"
---

# 5. 실습 환경 준비

본 운영체제 수업의 실습은 **리눅스(Linux)** 환경 기반으로 진행됩니다. 

별도의 C 언어 기반 시스템 레벨 제어를 훈련하고 커널 내부를 들여다보기 위해서는 쉘(Shell) 조작과 패키지 관리자의 활용이 필수적입니다.
수강생 여러분은 개인 PC에 아래의 방법 중 하나를 택하여 **Ubuntu Linux** 중심의 쉘 기반 전용 환경을 구축하시기 바랍니다.

## 실습 권장 환경 (선택)

1. **WSL2 (Windows Subsystem for Linux)**
   * 최신 윈도우 10/11 사용자에게 가장 권장되는 네이티브에 가까운 리눅스 서브시스템 환경입니다.
   * 터미널에서 `wsl --install` 명령어만으로 최신 Ubuntu 배포판이 즉시 설치됩니다.
2. **가상 머신 (Virtual Machine)**
   * VirtualBox, VMware 등을 이용하여 Ubuntu Desktop/Server 이미지를 부팅하는 전통적 방식입니다.
3. **Mac Terminal (macOS)**
   * macOS 사용자의 경우 자체 커널이 Unix 기반이므로 기본 `Terminal.app` 이나 `iTerm2` 터미널 위에서 Homebrew 패키지 매니저를 통해 실습 도구 대다수를 동일하게 활용할 수 있습니다.
4. **클라우드 서버 인스턴스**
   * AWS(EC2), GCP 단기 무료 티어를 활용하여 클라우드상에서 Ubuntu 원격 접속(SSH) 실습 환경을 구축하는 것도 훌륭한 실무 연습입니다.
