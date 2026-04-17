---
layout: default
title: "7주차: 파일 시스템 아키텍처 (i-node부터 ZFS/APFS까지)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="50" fill="white" font-size="20" font-family="monospace" text-anchor="middle">UNIX i-node Architecture</text><circle cx="150" cy="120" r="40" fill="#0078D7"/><text x="150" y="125" fill="white" font-size="14" font-family="monospace" text-anchor="middle">Direct</text><circle cx="300" cy="120" r="40" fill="#E81123"/><text x="300" y="125" fill="white" font-size="14" font-family="monospace" text-anchor="middle">Indirect</text><circle cx="450" cy="120" r="40" fill="#00FF00"/><text x="450" y="125" fill="#333" font-size="14" font-family="monospace" text-anchor="middle">Double Ind.</text></svg>
</div>

# 7주차: 파일 시스템 아키텍처 (i-node, 블록 할당, CoW/ZFS)

여러분이 데스크탑 화면에서 더블 클릭하는 화려한 '폴더 아이콘'과 '텍스트 파일명'은 인간의 인지 편향을 유도하기 위해 빚어낸 위대한 허구(Abstraction)에 불과합니다. Linux 커널에게 진정한 파일의 실체는 오직 **아이노드(inode) 고유 번호표**뿐이며, 화려한 폴더계층은 그저 번호들을 나열한 색인표일 뿐입니다. 

이번 주차에서는 디지털 파일 데이터가 자력선형 디스크 블록 위에 어떤 전략적 할당으로 심어지는지 추적하고, 갑작스러운 하드웨어 전원이 끊겨도 데이터를 완벽하게 수호하는 데에서 나아가 타임머신 스냅샷까지 찍어버리는 현대 OS의 최전선 **저널링(Journaling)** 및 **CoW(Copy-on-Write)** 철학을 배웁니다.

---

## 🎯 통합 핵심 학습 목표

1. **디렉터리와 링크**: 비순환 그래프 모델에 종속된 Linux 디렉터리 파싱 구조와 하드 링크/소프트 링크의 참조 카운팅 분자 구조를 체득한다.
2. **UNIX 인덱스 트리**: 141바이트 고정된 메타데이터 블록(i-node) 정체가 어떻게 간접(Indirect) 포인터 확장을 통해 수백 기가바이트의 파일을 오차 없이 즉시 색인해 내는 원리를 설명한다.
3. **블록 할당 트레이드오프**: 연속 할당(단편화 낭비), 연결 할당(디스크 색인탐색 지연율), 색인 할당(인덱스 결합 구조) 방식의 스토리지 파편화 병목 장/단점을 분석한다.
4. **저수준 C 커서 제어**: OS 커널의 파일 지정자 자원 반환과 오프셋 포인터 레코드를 임의 조작, 점프하는 `lseek()` C언어 인터페이스 기법을 익힌다.
5. **[엔지니어링 코어] 스토리지 안전망 진화**: 예고 없는 치명적 정전(Power Loss) 참사에 대비해 트랜잭션 기록을 남는 ext4/NTFS 저널(Journal) 기법과 APFS 스냅샷(CoW) 덮어쓰기 무력화 엔진의 본질을 분해한다.

<br>

---

## 📚 하위 문서 목차 (Sub-Chapters)

물리 매체와 파일 시스템 사이의 논리적 괴리를 파헤치는 7주차 렉처는 5개의 상세 파이프라인으로 구성되었습니다.

1. **[디렉터리 시스템과 링크 아키텍처](./01_directory_link/index.md)**
   > 낭비적인 트리 모델을 극복한 비순환 그래프의 공용 권한과 '하드 링크 / 소프트 링크' 바로가기의 차이를 분석.
2. **[UNIX 메타데이터: i-node 색인](./02_inode/index.md)**
   > 거대한 볼륨 폭증을 대비해 직접/1중/2중/3중 포인터로 디스크 할당을 기적적으로 확장해 내는 핵심 트리 철학.
3. **[디스크 블록 공간 할당 모델](./03_allocation/index.md)**
   > 외부 단편화 방식을 남기는 연속 배열형, 꼬리잡기식 연결 할당, 색인 파일 할당 3대장의 트레이드 오프.
4. **[포인터 제어 lseek 시스템 콜](./04_lseek/index.md)**
   > C언어 개발자가 직접 파일 디스크립터(FD)에 접근하여 임의의 번지로 오프셋 스캔/수정을 날리는 핵심 매커니즘.
5. **[저널링과 현대 CoW 스냅샷](./05_journal_cow/index.md)**
   > 커밋 로그를 남겨 디스크 박살을 피하는 ext4의 저널과 원본 비파괴 참조 스냅샷을 0.1초 만에 떠버리는 최신 APFS 기술.

<hr style="margin: 40px 0;">

> **📚 참고문헌**
> * A. Silberschatz 등 3인, 『운영체제(Operating System Concepts)』, J. Wiley & Sons. 
> * M. McKusick, 『The Design and Implementation of the 4.4BSD Operating System』 (UFS/inode)
