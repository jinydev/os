---
layout: default
title: "1. 객체기반 셸의 탄생"
---

# 1. 파워셸(PowerShell)의 닷넷( .NET) 객체 지향성

MS-DOS의 `cmd`를 넘어서 터미널의 모든 것을 갈아엎기 위해 마이크로소프트가 내놓은 차세대 역작, 바로 PowerShell입니다. 

기존의 리눅스 `bash`나 윈도우 `cmd`의 가장 큰 한계는 모든 명령어의 결괏값이 단순한 "텍스트 긴 뭉텅이 문자열(Text String)"로 반환된다는 것이었습니다. 이 때문에 개발자들은 `grep` 이나 `awk` 와 같은 정규식 파서를 써서 눈 빠지게 문자열을 자르고 파싱해야 시스템 지표를 얻을 수 있었습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="40" width="200" height="120" fill="#333" rx="5"/><text x="150" y="75" fill="white" font-size="16" font-family="monospace" text-anchor="middle">bash (Text)</text><text x="150" y="105" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">grep / awk</text><rect x="350" y="40" width="200" height="120" fill="#005A9E" rx="5"/><text x="450" y="75" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PowerShell (Object)</text><text x="450" y="105" fill="#00FF00" font-size="14" font-family="monospace" text-anchor="middle">.WorkingSet > 1GB</text><path d="M 260 100 L 340 100" stroke="white" stroke-width="4"/></svg>
</div>

## 패러다임 전환: 객체 파이프라인(Object Pipeline)
그러나 파워셸은 근본 철학 자체가 다릅니다. 파워셸 명령어가 뱉어내는 모든 결과는 텍스트가 아니라 완전한 형태를 갖춘 **닷넷(.NET) 객체(Object)**입니다! 

예를 들어 `Get-Process` 명령을 치면 단순 텍스트가 나오는 게 아니라, 현재 실행 중인 프로세스들의 객체 배열이 튀어나옵니다. 따라서 우리는 지저분한 정규식 없이 그저 `.WorkingSet` (메모리 사용량)이라는 속성(Property) 메서드를 우아하게 호출하여 곧바로 1GB를 넘게 처먹고 있는 프로세스 배열만 추출할 수 있게 됩니다. 이것이 파워셸 코어의 극강의 유지보수성입니다.
