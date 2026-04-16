---
layout: default
title: "9주차: RDBMS 2 (PostgreSQL)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">PostgreSQL vs MySQL 메모리 구조</text><rect x="100" y="90" width="150" height="60" fill="#0078D7" rx="5"/><text x="175" y="125" fill="white" font-size="16" font-family="monospace" text-anchor="middle">PG: Multi-Process</text><rect x="350" y="90" width="150" height="60" fill="#E81123" rx="5"/><text x="425" y="125" fill="white" font-size="16" font-family="monospace" text-anchor="middle">MySQL: Multi-Thread</text></svg>
</div>

# 9주차: RDBMS 2 (PostgreSQL)

<br>

## 1. PostgreSQL - 객체 관계형 심층 전개

[실전 심화 렉처]
단순 관계형(RDBMS)을 벗어난 외계 스펙. JSONB 타입, 지리 공간좌표 분석 등 현대 스택의 끝판왕입니다. MySQL 과는 테이블 철학까지 다름을 꿰뚫어 보세요.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><circle cx="300" cy="100" r="60" fill="#333"/><text x="300" y="105" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">JSONB</text></svg>
</div>

## [심화 렉처] 진보된 ORDBMS, PostgreSQL의 차별점

대규모 트래픽 시대에 스키마 없는 NoSQL과 RDBMS의 간격을 메워주는 것이 PostgreSQL의 바이너리 JSON(JSONB) 인덱싱 능력입니다. 클라이언트 연결마다 '스레드'가 아닌 거대한 '프로세스'를 포킹하여 격리 안정성을 추구한 PG의 메모리 할당 정책을 구조적으로 탐구합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">psql -U postgres -d postgresdb</text></svg>
</div>

## [심화 렉처] 사용자 정책 및 Peer Authentication

MySQL의 Password Authentication 과 확연히 대비되는 것은 `pg_hba.conf` 라우팅 파일에 기반한 유연한 보안 정책입니다. Mac 로컬 시스템 터미널 사용자 계정과 DB 내부 최고 관리자(postgres) 간의 일대일 매핑 구조(Peer Trust)를 우회하거나 제어하는 네트워크 접근 통제 방식을 마스터합니다.
