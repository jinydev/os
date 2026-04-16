---
layout: default
title: '1주 차 - DOS의 시대'
---

# 1주 차 - DOS의 시대

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="#00FF00" font-size="24" font-family="monospace" text-anchor="middle">A:\> dir</text><rect x="250" y="90" width="100" height="60" fill="#333" rx="5"/><text x="300" y="125" fill="white" font-size="16" font-family="monospace" text-anchor="middle">FAT16</text></svg>
</div>

## [전공 심화] 단일 작업(Single-Tasking) 환경과 메모리 덤프

MS-DOS는 태생적으로 마이크로프로세서(8088/8086) 시대의 산물입니다. 당시 운영체제의 가장 큰 역할은 그저 디스켓의 파일을 읽어서 CPU에 올려주는 기초적인 로더(Loader)일 뿐이었습니다. 프로그램이 한 번 실행되면 커널 역할조차 멈추며, 응용 프로그램이 RAM의 전체 주소 공간을 제어하는 이 위험천만한 설계는 과거의 야생과도 같았습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><rect x="150" y="50" width="300" height="100" fill="#E81123" rx="5"/><text x="300" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Single-Tasking Limit</text></svg>
</div>

## [전공 심화] FAT 파일 시스템과 파티션의 태동

지금 도 펌웨어 업데이트 등 저수준 영역에서 쓰이는 FAT(File Allocation Table)의 원리를 이해합니다. 링크드 리스트(Linked List)로 파일을 연결하는 고전적 방식 때문에 클러스터 체인이 꼬이거나 디스크 조각화가 생기는 본질적인 이유를 파헤칩니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">640KB Ram Barrier & Himem.sys</text></svg>
</div>
