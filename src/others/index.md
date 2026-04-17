---
layout: default
title: "Other OS & Frameworks"
---

# 컴퓨팅의 숨겨진 역사: 기타 OS 및 프레임워크 아키텍처

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="80" y="50" width="120" height="100" fill="#333" rx="5"/><text x="140" y="105" fill="#00FF00" font-size="20" font-family="monospace" text-anchor="middle">DOS</text><rect x="240" y="50" width="120" height="100" fill="#005A9E" rx="5"/><text x="300" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">OS/2</text><rect x="400" y="50" width="120" height="100" fill="#E81123" rx="5"/><text x="460" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Solaris</text></svg>
</div>

현대의 서버 시스템은 리눅스(Linux)가, 로컬 데스크톱은 윈도우(Windows)와 맥(macOS)이 삼분할하여 천하를 지배하고 있습니다. 하지만 이 견고한 철옹성 같은 현대 운영체제들의 메커니즘은 하루아침에 하늘에서 뚝 떨어진 것이 아닙니다. 

지금은 패배하여 역사 속으로 사라졌거나, 혹은 스마트폰이나 임베디드라는 특수한 환경 속에서 조용히 세상을 굴리고 있는 '숨겨진 운영체제'들의 치열한 아키텍처 전쟁이 존재했습니다. 모바일 기기의 터치스크린 인터럽트부터 시작해, 기업용 서버 운영체제의 대부격이었던 솔라리스, 그리고 현재 OS의 경계를 위협하고 있는 거대 프레임워크들의 본질까지 넘나듭니다.

본 커리큘럼은 **'기타(Others)'** 라는 외피를 쓰고 있지만, 사실상 현대 운영체제들을 가장 객관적이고 넓은 시각에서 평가할 수 있게 해주는 메타(Meta) 지식의 보고입니다. 기술의 진화론적 관점에서 왜 특정 커널 구조가 생존하고 패배했는지를 추적해 보십시오.

---

## 📚 플랫폼 아키텍처 확장 목차

### [1주차 - DOS의 시대](./01_dos_era/index.md)
마우스도 없고 멀티태스킹도 불가능했던 시절, 단일 쉘 위에서 하드웨어를 직접 두드리며 통제하던 16비트 검은 화면의 시대. 현대 터미널과 커맨드라인 환경의 밑바탕이 된 역사적 발자취를 추적합니다.

### [2주차 - OS/2와 데스크탑 전쟁](./02_os2_wars/index.md)
빌 게이츠와 IBM이 합작하여 만들었던 비운의 명작 운영체제. 지금의 윈도우 NT 커널에 막대한 영향을 끼친 이 멀티태스킹 혁명 아키텍처가 왜 역사 속에서 윈도우 95에게 참패했는지, 기술과 시장 생태계의 뼈아픈 교훈을 복기합니다.

### [3주차 - 솔라리스(Solaris)와 유닉스](./03_solaris_unix/index.md)
현대 클라우드 서버의 조상이자 엔터프라이즈 환경을 지배했던 썬 마이크로시스템즈(Sun Microsystems)의 심장. ZFS 파일 시스템과 시스템 복원력 등 현대 리눅스에서도 감히 넘보지 못한 위대한 유닉스 철학의 정수를 해부합니다.

### [4주차 - 모바일 리눅스와 RTOS](./04_mobile_rtos/index.md)
우리가 주머니 속에 구동하고 있는 스마트폰(안드로이드, iOS)도 결국 기저에는 극도로 커스터마이징된 리눅스와 다윈 커널입니다. 배터리 소모를 극도로 억제하는 전력 스케줄러 메커니즘과, 드론·자동차를 제어하는 실시간 운영체제(RTOS)의 인터럽트 철학을 다룹니다.

### [5주차 - 프레임워크 vs 운영체제](./05_frameworks/index.md)
이제 더 이상 하드웨어 커널만 조립하는 시대는 끝났습니다. Java/JVM 런타임, Node.js 이벤트 루프, 자율주행 로봇(ROS) 등 거의 하나의 운영체제에 버금가는 거대 생태계 역할을 수행하는 **가상 운영(Framework) 플랫폼**들이 기존 OS 패러다임을 어떻게 집어삼키고 있는지 통찰합니다.
