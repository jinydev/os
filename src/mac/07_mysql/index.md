---
layout: default
title: "7주차: RDBMS 1 (MySQL 셋업 및 보안)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">MySQL InnoDB Volume Layout</text><rect x="150" y="100" width="300" height="40" fill="#333" rx="5"/><text x="300" y="125" fill="#E81123" font-size="16" font-family="monospace" text-anchor="middle">/opt/homebrew/var/mysql</text></svg>
</div>

# 7주차: RDBMS 1 (MySQL 셋업 및 보안)

<br>

## 1. MySQL 엔진 터미널 셋업

[실전 심화 렉처]
GUI 버튼에 의존하면 데이터베이스 커넥션 포트가 꼬일 때 복구를 못 합니다! 터미널 기반의 `mysql -u root -p` 명령 진입 후 권한 분리로 포트 바인딩 방어를 세팅합니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="300" cy="100" r="60" fill="#005A9E"/><text x="300" y="105" fill="white" font-size="24" font-family="monospace" text-anchor="middle">utf8mb4_</text></svg>
</div>

## [심화 렉처] RDBMS(MySQL) 데몬의 영속성(Persistence)

데이터베이스 프로세스가 메모리 상에 떠 있는 것과 물리 디스크에 플러시되는 구조를 이해합니다. Mac Homebrew의 기본 MyISAM, InnoDB 엔진 폴더 레이아웃을 파악하고, 시스템 설정(`my.cnf`) 오버라이딩을 적용해 최대 커넥션 수와 대용량 쿼리 캐시 정책을 튜닝합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">CREATE USER 'jiny'@'localhost' IDENTIFIED BY 'pwd';</text></svg>
</div>

## [심화 렉처] 유니코드와 콜레이션(Collation) 오류 정복

초기 MySQL 셋업 시 Emoji 이모티콘 저장에 실패하는 근본 원인은 utf8 제약(3바이트)입니다. 진정한 4바이트 렌더링인 `utf8mb4` 문자셋 지정과 대소문자 구문 정렬 방식(collation)을 시스템 수준에서 패치하여 백엔드 로직 오류를 사전에 봉쇄합니다.
