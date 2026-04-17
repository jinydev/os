---
layout: default
title: "2. 개발자 셸 셋업과 프로필"
---

# 2. 개발자 셸 환경 구축과 스크립팅

파워셸 명령어의 기본 체계는 `Get-Process`나 `Start-Service`, `Stop-Process` 처럼 **동사-명사 (Verb-Noun)** 구조로 이루어져 있어, 누구나 코드만 읽어도 이 스크립트가 무슨 짓을 하는지 가독성이 뛰어나게 유지됩니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Verb-Noun Convention</text><rect x="100" y="90" width="400" height="60" fill="#333" rx="5"/><text x="300" y="125" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">Get-Process | Stop-Process</text></svg>
</div>

## 일괄 처형 스크립트 작성
위에서 배운 닷넷 객체 파이프라인을 조합하면, `"메모리를 1기가바이트 초과해서 쓰고 있는 앱들을 싹 다 찾아서 한 번에 프로세스 종료시켜버려라"` 라는 위력적인 명령을 단 한 줄로 작성할 수 있습니다. 
`Get-Process | Where-Object WorkingSet -gt 1GB | Stop-Process`

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">Set-ExecutionPolicy RemoteSigned</text></svg>
</div>

## 스크립트 보안 해제와 Profile 셋업
기본적으로 윈도우는 악성 해커 공격을 막기 위해 파워셸 스크립트(`.ps1`) 실행 권한을 엄격하게 차단(`Restricted`)해 두고 있습니다.
이를 로컬 개발자 스크립트는 돌아가도록 단계를 하향 조정하는 `Set-ExecutionPolicy RemoteSigned` 권한 해제 작업이 파워셸 마스터로 가는 첫 관문입니다. 이후 터미널이 켜질 때마다 자동 실행되는 `Profile.ps1` 파일을 건드려 글로벌 `Oh-My-Posh` 테마 플러그인을 깔아 화려하고 가독성 좋은 개발자 콘솔 UI를 구축하게 됩니다.
