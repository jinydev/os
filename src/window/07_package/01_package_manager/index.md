---
layout: default
title: "1. 패키지 관리자의 도입과 격리"
---

# 1. 패키지 자동 셋업과 분리 공간

여러분은 아직도 브라우저를 열고 `.exe` 설치 파일을 일일이 다운로드한 뒤, 마우스를 클릭해 가며 `Next -> Next -> Finish` 구조로 프로그램을 설치하고 계십니까?

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="150" cy="100" r="50" fill="#0078D7"/><text x="150" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Winget</text><circle cx="450" cy="100" r="50" fill="#4B4B4B"/><text x="450" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Scoop</text><path d="M 220 100 L 380 100" stroke="#00FF00" stroke-width="4" stroke-dasharray="5,5"/><text x="300" y="90" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">User Space Isolation</text></svg>
</div>

이 구시대적인 그래픽(GUI) 인스톨 방식은 다음과 같은 치명적인 한계를 가집니다.
1. 관리자 권한을 매번 탈취하려듭니다(UAC 팝업 점등).
2. 시스템 전역 레지스트리와 PATH를 함부로 오염시켜, 다른 버전의 동일 패키지가 깔려 있을 시 심각한 버전 충돌망(Dependency Hell)을 일으킵니다.

## 코드로 선언하는 인프라 셋업 (Winget, Scoop)
현대적인 엔지니어는 자신이 쓰는 개발 환경을 단 몇 줄의 스크립트 몽둥이 조작으로 자동 셋업합니다. 이를 가능케 하는 것이 윈도우 공식 패키지 매니저 모듈인 **`winget`** 과 사용자 권한 격리망의 최강자인 **`Scoop`** 입니다.

프로그램을 `C:\Program Files` 폴더 같은 최고 권한의 중심 요새에 설치하지 않습니다. 오직 현재 로그인된 내 사용자만의 로컬 환경 파일 구조(User Space) 안에 패키지를 깔끔하게 던져 넣음으로써 권한 충돌과 환경 오염을 완벽하게 통제해 냅니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">$env:JAVA_HOME = "C:\Program Files\Java\jdk-17"</text></svg>
</div>
