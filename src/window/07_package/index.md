---
layout: default
title: "7주차: 패키지 관리자의 도입과 개발 환경 렌더링"
---

<div align='center'>
  <img src='../01_history/img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="150" cy="100" r="50" fill="#0078D7"/><text x="150" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Winget</text><circle cx="450" cy="100" r="50" fill="#4B4B4B"/><text x="450" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Scoop</text><path d="M 220 100 L 380 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="90" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">User Space Isolation</text></svg>
</div>

# 7주차: 실무 개발망 자동 병합 (패키지 관리자)

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_07.png)
<br>

"내가 짠 코드가 내 컴퓨터에서는 잘 되는데, 네 컴퓨터에서는 안 돼!" 
개발자라면 누구나 한 번쯤 겪는 환경 변수에 얽힌 끔찍한 악몽입니다. 이는 각자의 컴퓨터에 깔려 있는 파이썬 버전이나 자바 엔진이 시스템 레지스트리를 오염시키며 복잡하게 충돌하기 때문입니다.

이번 7주차 렉처에서는 아직도 마우스를 몇 번씩 클릭하며 무식하게 개발 패키지를 디렉토리에 설치하는 구습을 탈피합니다. 시스템 권한 자체를 완전히 벗어나 나만의 분리망(User Space) 안에 패키지를 자동 설치하고 디펜던시 헬(Dependency Hell)을 통제해 내는 `winget`과 `Scoop` 패키지 관리자의 강력한 인프라 스크립팅 매력을 겪어봅니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단순한 프로그램 설치가 아닙니다! 레지스트리를 보호하기 위해 패키지 환경망을 격리시키는 현대 개발자 데브옵스.

1. [패키지 관리자의 도입과 격리](./01_package_manager/index.md)
   > 그래픽 인스톨러(.exe)의 폐해를 끊어내고 터미널 스크립트 명령(Scoop) 하나로 유저 환경망을 깨끗하게 관리하는 파이프라인.

<hr style="margin: 40px 0;">

> **💡 개발 환경 통제**
> "포맷 후 컴퓨터를 부팅하여 10분 만에 명령줄 스크립트 단 한 줄로 개발 런타임을 완벽하게 동일 복사해 낼 수 없다면, 당신은 시스템 환경에 지배당하고 있는 것이다."
