---
layout: default
title: "Windows OS Architecture"
---

# Windows OS Architecture: 관리자와 개발자를 위한 플랫폼의 이해

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="100" height="100" fill="#0078D7" rx="5"/><text x="100" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Windows NT</text><path d="M 160 100 L 240 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/><rect x="250" y="50" width="100" height="100" fill="#4B4B4B" rx="5"/><text x="300" y="105" fill="#00FF00" font-size="20" font-family="monospace" text-anchor="middle">.NET Core</text><path d="M 360 100 L 440 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/><rect x="450" y="50" width="100" height="100" fill="#E95420" rx="5"/><text x="500" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">WSL2 / K8s</text><defs><marker id="arrow" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs></svg>
</div>

전 세계 PC 시장의 지배자이자, 기업용 로컬 생태계부터 Azure 클라우드 인프라에 이르기까지 여전히 거대한 파이를 차지하고 있는 운영체계. 바로 **마이크로소프트 윈도우(Microsoft Windows)**입니다.

리눅스(Linux)가 클라우드 백엔드 배포의 최종 무대라면, 여러분이 매일같이 자판을 두드리고 화려한 툴을 구동하는 베이스캠프는 십중팔구 윈도우 환경 위에 서 있습니다. 
단순히 마우스를 몇 번 클릭해 파란 폴더에서 파일을 옮기는 수준을 너머, 개발자와 인프라 엔지니어라면 이 거대한 운영체제가 디스크를 어떻게 파티셔닝하고(C:\), 메모리와 패키지 모듈을 어떤 방식으로 충돌 없이 제어하며, 권한 에러를 추적해 내는지 그 엔진(NT 커널)의 심연을 정밀 타격할 수 있어야 생존할 수 있습니다.

본 `Windows OS` 커리큘럼은 MS-DOS 시대의 낡은 유산에서 시작해, 최신의 혁신적인 하드웨어 가상화 브릿지(WSL2)에 이르기까지 **"윈도우라는 거대 상용 프레임워크를 터미널(명령줄) 환경에서 완벽하게 해체하고 완전 통제하는 힘"**을 기르기 위한 총 10주간의 마스터 코스입니다.

---

## 📚 윈도우 커리큘럼 전체 목차

무거운 그래픽 유저 인터페이스(GUI)를 버리고, 하드웨어 기계를 직결 제어하는 터미널(Terminal) 환경으로 도약하기 위한 여정 코스입니다. 

### [1주차: 윈도우 컴퓨터란? 시작과 역사적 배경](./01_history/index.md)
왜 세상 모든 하드디스크 드라이브는 항상 `C:\` 라는 알파벳으로 굳어졌으며, 경로 구분자로 리눅스와 달리 역슬래시(`\`)를 고집할까요? 불안정했던 MS-DOS의 근간을 박살 내고 지금의 윈도우를 지배하는 강철의 통제망인 **NT 커널**의 철학과 역사적 등장 배경을 추적합니다.

### [2주차: 명령 프롬프트(CMD)와 DOS 명령어의 부활](./02_cmd/index.md)
유닉스의 `ls`와 `rm` 명령어 대신 윈도우 서버 시스템을 지탱하는 `dir` 과 `xcopy`, 그리고 권력을 쥐고 흔드는 강제 프로세스 처형 명령어인 `taskkill /F` 가 난무하는 원초적 생존 명령 체계 생태계를 다룹니다.

### [3주차: 다중 사용자 환경과 시스템 권한 제어](./03_multiuser/index.md)
수많은 개발자를 눈막음하는 암살자, '권한 거부(Permission Denied)'. 화면을 즉각 가려버리는 윈도우 특유의 방어막 **UAC(관리자 권한 승급)** 메커니즘을 뚫어야 합니다. 나아가 윈도우에서 아무런 오류 화면 없이 앱이 죽어버릴 때 흔적을 남기는 블랙박스인 **이벤트 뷰어(Event Detail)**와 **레지스트리(Registry)** 구조를 딥다이브합니다.

### [4주차: 컴퓨터의 핏줄, 환경 변수와 경로(PATH)](./04_path/index.md)
`command not found` 터미널 구동 에러의 명백한 본질. 윈도우 커널이 수백만 개의 폴더 속에서 실행 파일을 딱딱 찾아 배포해 주는 파이프라인인 전역 및 사용자 **PATH(환경 변수)** 설정법과, 복잡하게 뒤엉킨 패키지의 스코프(Scope) 우선순위 해결법을 파밍합니다.

### [5주차: 차세대 프레임워크, PowerShell 객체 셸](./05_powershell/index.md)
구닥다리 텍스트 문자열(String) 정규식에서 해방되십시오! 리눅스의 bash 조차 구현하지 못한 방식. 명령어의 모든 결과값을 온전한 `.NET` 객체(Object Property)로 리턴하여 메모리 속성에 곧장 직접 접근(e.g., `.WorkingSet`) 가능하게 해주는 윈도우 최후의 무기 **PowerShell** 환경 스크립팅의 권력을 거머쥡니다.

### [6주차: 터미널의 혁신, Windows Terminal](./06_terminal/index.md)
느리고 답답했던 기존 시커먼 콘솔 렌더링 엔진(`conhost.exe`)의 태생적 한계를 부수고, 게임 엔진처럼 GPU 하드웨어 가속기를 직결 장착해 압도적인 I/O 렌더링을 내뿜는 **Windows Terminal** 혁신. 리눅스/파워셸 쉘을 병렬로 융합하고 다크테마와 `settings.json`을 단축키 분할 탭으로 맵핑하는 실전 구축기입니다.

### [7주차: 패키지 관리자의 도입과 개발 환경 렌더링](./07_package/index.md)
여전히 브라우저상에서 `Next`를 번갈아 누르며 언어를 다운로드합니까? 윈도우의 심장부인 레지스트리를 오염시키지 않는 안전한 유저 사용자 격리 환경 내에 텍스트 스크립트 단 한 줄로 개발 런타임 수십 개(Node.js, Python, Java)를 완전 연동 배포하는 현대판 윈도우 데브옵스 **Winget / Scoop** 엔진을 장착합니다.

### [8주차: Windows 네이티브 프로그래밍과 C#](./08_csharp/index.md)
윈도우 시스템의 RAM 메모리와 커널 객체를 가장 매끄럽게 교감하며 파고들 수 있는 코어 오피셜 언어, 바로 **닷넷(.NET)과 C#** 의 실체입니다. 몇 기가바이트에 육박하는 거대한 도구를 사용하지 않고 백엔드 터미널의 커맨드 내에서 네이티브 컴파일러인 `csc.exe` 훅을 찔러 자체 실행 파일(`Hello.exe`) 엔진을 직접 압축시켜 내며 블랙박스를 풀어봅니다.

### [9주차: 하이브리드 엔진, WSL2 아키텍처](./09_wsl2/index.md)
윈도우가 마침내 오픈소스를 발목부터 집어삼켰습니다! 눈속임 에뮬레이터 수준에 불과했던 WSL1의 굴레를 찢고, 윈도우의 가장 밑바닥 Hyper-V 경량 가상 머신 슬롯에 진짜 순정 **리눅스 백엔드 커널**을 병렬 이식시켜버린 WSL2 구조. 그리고 이종 플랫폼 간의 벽을 허물어 버린 극강의 `9P 파일 네트워크 쉐어망` 아키텍처를 해부합니다.

### [10주차: 궁극의 퓨전 — VS Code Remote 아키텍처](./10_vscode/index.md)
어떻게 윈도우 바탕화면 겉에 껍데기로 깔려 있는 에디터가, 가상화 안에 갇혀 있는 WSL2 우분투 리눅스 속 파일을 그토록 빠르게 수정하고 소팅해 버리는 것일까요? 윈도우는 화려한 화면 송출 클라이언트로만 분리시키고, 소스 코드 입출력과 파싱 메모리는 오직 리눅스에 전가하는 **Remote-WSL 이원화 소켓 프레임워크 퓨전 구조**를 최종 수료합니다.
