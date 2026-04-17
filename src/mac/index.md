---
layout: default
title: "macOS Developer Architecture"
---

# macOS Architecture: 개발자를 위한 유닉스 생태계 마스터

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="100" height="100" fill="#E81123" rx="5"/><text x="100" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Darwin</text><path d="M 160 100 L 240 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/><rect x="250" y="50" width="100" height="100" fill="#005A9E" rx="5"/><text x="300" y="105" fill="#00FF00" font-size="20" font-family="monospace" text-anchor="middle">Unix</text><path d="M 360 100 L 440 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/><rect x="450" y="50" width="100" height="100" fill="#4B4B4B" rx="5"/><text x="500" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Homebrew</text><defs><marker id="arrow" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs></svg>
</div>

스타벅스 창가 자리에서 눈에 띄게 빛나는 애플 로고는 단순한 디자인적 유행이나 감성의 전유물이 아닙니다. 백엔드/프론트엔드, 인프라를 가리지 않고 전 세계 상위 1%의 실리콘밸리 개발자들이 구태여 비싼 맥북을 프로그래밍 머신으로 채택하는 데에는 가장 본질적이고 치명적인 이유가 존재합니다.

바로 **macOS가 지구상에서 가장 완벽하게 다듬어진 상용 유닉스(UNIX) 머신**이라는 사실입니다. 
서버 생태계의 패왕인 리눅스와 터미널/쉘 생태계를 거의 100% 흡사하게 공유하면서도, 윈도우 못지않은 극강의 서드파티 그래픽 앱 구동을 보장하는 이 아름다운 하이브리드 커널 공간은 오직 Mac만이 보여줄 수 있는 특권입니다.

본 커리큘럼은 단순히 '맥을 쓰는 방법'을 알려드리지 않습니다. `Homebrew`라는 거대한 패키지 툴체인을 통해 언어 런타임(Node, Python, Java)을 버저닝하고 쪼개며, Nginx와 데이터베이스(MySQL)를 로컬 백그라운드 데몬 시스템(Launchd)으로 통제하는 **'완전한 백엔드 독립 개발망'**을 여러분의 Mac 터미널 속에 깎아 짓는 11주간의 하드코어 훈련 코스입니다.

---

## 📚 macOS 커리큘럼 전체 목차

그래픽 화면을 넘어 맥 터미널을 열방의 도구로 사용하는 유닉스 환경 조율법을 배웁니다.

### [1주차: macOS의 기원과 터미널 기초 (Darwin, 단축키)](./01_intro/index.md)
macOS는 단순한 예쁜 껍데기가 아닙니다! 그 밑바닥에 흐르는 무자비한 오픈소스 유닉스 커널인 다윈(Darwin) 아키텍처의 기원을 파헤치며 개발자로서 터미널과 단축키 기반 생산성을 극한으로 끌어올리는 첫 시작 지점입니다.

### [2주차: 터미널과 zsh 완벽 제어 (Oh-My-Zsh)](./02_terminal/index.md)
기본 `bash` 쉘을 버리고, 가장 진보한 뎁스를 지닌 **`zsh`** 쉘 아키텍처 환경으로 돌입합니다. `Oh-My-Zsh` 커스텀을 테마 꾸미기 용도가 아니라, 막강한 자동완성 플러그인 생태계를 끌어다 쓰는 터미널의 무기화 전술로 이해합니다.

### [3주차: 패키지 관리자 혁명 (Homebrew 아키텍처)](./03_homebrew/index.md)
인터넷에서 `dmg` 파일을 다운로드해 휴지통으로 버리던 설치 방식을 원천적으로 파괴합니다. 맥 OS 필수 교양이자 프로덕션 생태계를 지배하는 **Homebrew**의 `Cellar` 심볼릭 링크 구조를 이해하고 각종 환경 셋업을 스크립트로 자동화합니다.

### [4주차: 멀티 버전 매니저 1 (Node.js & Python)](./04_nodejs_python/index.md)
프로젝트마다 요구하는 노드와 파이썬의 버전이 전부 다릅니다. 이를 브루(brew)에서 한 번에 엎어치는 것이 아니라, 유저 스페이스 내에서 버전을 실시간으로 갈아끼우는 **NVM/FNM** 과 **Pyenv** 버저닝 지옥 탈출기의 원리.

### [5주차: 멀티 버전 매니저 2 (PHP, Ruby, Java)](./05_php_java/index.md)
엔터프라이즈 환경에서 필수적인 PHP 환경(`shivam`, `rbenv`)과 Java/Kotlin 등의 거대 JVM 생태계를 통제하는 **SDKMAN!** 통제 시스템 도입. 수많은 언어 런타임이 격리망 안에 공존하는 인프라 맵을 렌더링합니다.

### [6주차: 로컬 웹 서버 셋업 (Nginx, 로컬도메인)](./06_nginx/index.md)
그저 `localhost:8080` 으로만 서버 테스트를 하시나요? 실전 배포처럼 **Nginx** 웹서버 커널을 로컬에 심고, `/etc/hosts` 로컬 DNS 파일 해킹을 통해 내 맥북 안에서 `.dev` 와 같은 가상 도메인을 라우팅하는 네트워크를 세팅합니다.

### [7주차: RDBMS 1 (MySQL 셋업 및 보안)](./07_mysql/index.md)
DB 관리 툴을 돌리기 전에, 실제 Mac 터미널을 이용해 **MySQL** 엔진 바이너리를 설치하고 보안 툴(`mysql_secure_installation`) 기동부터 소켓 파일 충돌 방지 세팅까지 밑바닥 서버 지식을 체득합니다.

### [8주차: 백그라운드 제어 (Brew Services, launchd)](./08_services/index.md)
터미널을 끄면 내가 띄운 서버도 꺼집니다. 맥 안의 심장부 데몬 프로세스 컨트롤러인 **`launchd`** 의 원리를 배우고, 이를 한 줄로 통제하는 `brew services` 명령어를 통해 로컬 머신을 진정한 무중단 서버로 돌변시킵니다.

### [9주차: RDBMS 2 (PostgreSQL)](./09_pgsql/index.md)
오픈소스 및 모던 백엔드 진영의 지배자 **PostgreSQL**. MySQL 과 무엇이 다른지 아키텍처 전개를 비교하며 로컬 터미널에서 객체 관계형 파이프라인 컴포넌트를 이식해 봅니다.

### [10주차: Apple Silicon과 Docker 가상화](./10_arm/index.md)
인텔맥(x86)에서 종말을 고하고, 폭발적인 전성비를 지닌 **Apple Silicon (ARM M/시리즈)** 구조로 전환되며 가상화 생태계가 어떻게 뒤집혔는지. 리눅스 이미지를 Mac 내부에서 네이티브하게 돌려주는 Docker 아키텍처의 혁명을 이해합니다.

### [11~14주차: 인프라 설계 종합 (백엔드 생태계 완성)](./11_final/index.md)
거대하게 쪼개어져 있던 언어/서버/DB 모듈들을 유기망으로 연결합니다. 구축한 macOS 환경이 실제 AWS, Linux 클라우드 환경으로 넘어갈 때 1%의 괴리 없이 무결점 코딩을 발휘할 수 있는 풀스택 인프라 환경 설계의 완성.
