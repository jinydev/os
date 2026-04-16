---
layout: default
title: "11~14주차: 인프라 설계 종합"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="100" y="30" width="400" height="140" fill="#333" rx="5"/><text x="300" y="60" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">brew dump --force</text><text x="300" y="100" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">dotfiles / alias / function / PATH</text><text x="300" y="140" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">Zero-touch Provisioning</text></svg>
</div>

# 11~14주차: 인프라 설계 종합

<br>

## 1. 백엔드 생태계 완성 검토

[실전 심화 렉처]
맥은 이제 이동형 클라우드 입니다. 명령어 한방으로 통합 클러스터를 지배할 수 있습니다. 진정한 인프라 엔지니어로 거듭난 최종 퀄리티 인증을 완료하십시오.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#E81123" font-size="24" font-family="monospace" text-anchor="middle">Mac OS Infrastructure CI/CD</text></svg>
</div>

## [심화 렉처] Dotfiles 프로비저닝 (Zero-Touch Setup)

단순히 노트북을 세팅하는 수준을 넘어, 엔지니어의 로컬 랩 자체가 구동 가능한 서버 인프라임을 명심해야 합니다. 1~10주 차까지 쌓아온 `.zshrc`, 홈브루 `.Brewfile`, Nginx/MySQL 설정 파일들을 모두 Github 원격 저장소(`dotfiles`)에 동기화해 관리하는 자동 운영 체계를 확보합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Your Machine is a Server.</text></svg>
</div>

## [심화 렉처] 트러블슈팅과 엔지니어의 자존감

플랫폼 셋업이 무너졌을 때, 단순히 재부팅을 하거나 구글링에서 찾은 의미 모를 설정 값을 복사-붙여넣기 행위는 이제 끝났습니다. OS의 커널 층부터 패키지 데몬 로그 층까지 직접 다이빙하여 권한과 포트 충돌의 원인을 규명해 내고 복구 파이프라인을 쟁취했다면, 완벽한 Senior 레벨로의 관문을 돌파한 것입니다.
