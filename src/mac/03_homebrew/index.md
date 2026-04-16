---
layout: default
title: "3주차: 패키지 관리자 혁명 (Homebrew 아키텍처)"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Mac Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="50" y="50" width="150" height="100" fill="#333" rx="5"/><text x="125" y="105" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">/opt/homebrew</text><path d="M 210 100 L 390 100" stroke="#E81123" stroke-width="4" stroke-dasharray="2,2"/><text x="300" y="90" fill="#E81123" font-size="14" font-family="monospace" text-anchor="middle">Symlink (ln -s)</text><rect x="400" y="50" width="150" height="100" fill="#0078D7" rx="5"/><text x="475" y="105" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Cellar/nginx/1.24</text></svg>
</div>

# 3주차: 패키지 관리자 혁명 (Homebrew 아키텍처)

<br>

## 1. Homebrew 시스템의 기적과 Cellar

[실전 심화 렉처]
`brew install nginx` 엔터 한 방이 내부적으로 어떻게 동작할까요? Homebrew 는 루비(Ruby) 스크립트를 다운받은 후, 컴파일 빌드하여 무조건 `/usr/local/Cellar`(또는 `/opt/homebrew/Cellar`)라는 격리된 폴더에 처박아 버립니다.

## 2. Brew Cask와 셋업 자동화

[실전 심화 렉처]
크롬, 슬랙, VSCode 마저도 Brew로 깔 수 있습니다. `brew install --cask google-chrome` 은 마우스를 클릭해 dmg 파일을 다운받는 모든 삽질을 날려줍니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">brew install --cask google-chrome</text></svg>
</div>

## [심화 렉처] Homebrew: 누락된 패키지 관리자의 해결사

리눅스의 `apt`, `yum` 과 달리 맥에는 자체 CLI 패키지 관리자가 없습니다. Max Howell은 Ruby 언어로 컴파일 스크립트 모음을 작성해 GitHub에 공유했고, 이것이 Homebrew가 되었습니다. Apple의 C 컴파일러(xcode-select)를 동원해 소스코드를 Celler 디렉토리 안에 격리 빌드하고, 그 결과물을 `bin/` 폴더에 '심볼릭 링크'하는 방식은 버전 충돌을 원천 차단하는 마법입니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#E81123" font-size="18" font-family="monospace" text-anchor="middle">ruby -e "$(curl -fsSL https://raw.githubusercontent...)"</text></svg>
</div>

## [심화 렉처] Cask와 Brewfile의 강력함

GUI 애플리케이션조차 `Cask`라는 형태로 패키징되어 브라우저에서 버튼을 누를 필요가 없어집니다. `brew bundle dump` 명령어로 현재 맥의 상태를 Brewfile로 추출해두면, 새 노트북을 샀을 때 스크립트 한 줄로 기존 업무 환경 100%를 복구할 수 있는 클라우드급 인프라코드(IaC)를 경험하게 됩니다.
