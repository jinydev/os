---
layout: default
title: "7주차: 파일 시스템 총정리 (ext4·ZFS·APFS)"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="60" fill="white" font-size="20" font-family="monospace" text-anchor="middle">The inode Structure</text><circle cx="300" cy="120" r="50" fill="#0078D7"/><text x="300" y="125" fill="white" font-size="16" font-family="monospace" text-anchor="middle">Index 281</text></svg>
</div>

# 7주차: 파일 시스템 총정리 (ext4·ZFS·APFS)


![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_07.png)
<br>




## 1. Inode와 루트 폴더부터 타고 내려가기

[실전 심화 렉처]
화면에 보이는 '폴더 아이콘'과 'test.txt' 파일명은 인간을 위한 허구입니다.
Linux 커널에게 진정한 파일의 이름은 **아이노드(inode) 번호**입니다. 디렉토리(폴더)라는 건 단지 "문자열 파일명 -> inode 번호"를 매치해 놓은 텍스트 장부 파일에 불과합니다.
파일 권한이 꼬이거나 디스크 공간은 널널한데 "No space left on device" 에러가 뜬다면, 백발백중 너무 작은 파일 수백만 개를 생성하여 디스크의 전체 Inode 개수 고갈 한계점에 부딪힌 것입니다. `df -i`로 모니터링해야 하는 심화 관리 포인트입니다.

## 2. 하드 링크(Hard Link) vs 심볼릭 링크(Soft Link)

[실전 심화 렉처]
하드 링크는 아주 독특한 복제 메커니즘입니다. 원본 파일을 다른 폴더에 `ln` 복사하면, 데이터 블록을 2배로 쓰지 않고 "동일한 inode 번호"를 가리키는 디렉토리 이름표만 새로 발급합니다! 양쪽 파일 중 하나를 수정하면 데이터 원본이 같으므로 다른 쪽도 100% 동일하게 실시간 반영됩니다. `ls -l`에서 보이는 링크 카운트(숫자)가 바로 이를 식별하는 증표입니다.
반면 단축 아이콘 격인 심볼릭 링크(Soft Link)는 원본의 '경로 문자열'만 가리키고 있기 때문에 원본 파일을 날려버리면 "Broken Link(빨간색 폴더)"가 되는 극단적 차이를 가집니다.

## 3. 저널링, CoW, 스냅샷 (ZFS, APFS, ext4)

[실전 심화 렉처]
파일 1GB를 저장하다 전원이 뚝 끊기면 데이터는 어떻게 보장될까요?
현대 파일 시스템(ext4 등)은 실제 디스크에 쓰기 전에 `저널(Journal)` 영역에 "지금부터 이런 작업을 할 거야"라고 스케줄 로그를 선기록합니다. 부팅 시 저널을 검사해 누락된 작업을 마저 이행하는 안전 장치(Recovery)입니다.
더 나아가 APFS(애플)나 Btrfs, ZFS 등은 파괴적 덮어쓰기를 절대 허가하지 않는 CoW (Copy-on-Write) 아키텍처를 가집니다. 특정 블록을 수정할 때 쓰던 블록을 밀어버리지 않고, 새 위치에 쓴 뒤 인덱스만 싹 교체하므로 단 1초 만에 전체 디스크 시점 백업을 복사(Snapshot)해낼 권능을 가질 수 있습니다.

---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="#E81123" font-size="24" font-family="monospace" text-anchor="middle">Journaling vs FAT32</text></svg>
</div>

## [전공 심화] 인덱스 노드(inode) 구조의 분별

하드디스크에서 '파일의 입구'는 파일 이름이 아니라 번호(inode)입니다. 이름표는 디렉터리 테이블에 텍스트 데이터로서 번호와 매핑될 뿐입니다. 그래서 하나의 파일에 수십 개의 다른 이름을 부여하는 하드 링크(Hard Link) 같은 분신술이 가능해지는 구조를 파악합니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">Copy-on-Write (ZFS, Btrfs, APFS)</text></svg>
</div>

## [전공 심화] Journaling 과 CoW 의 진화

컴퓨터 코드를 저장하던 도중 플러그가 뽑혀버린다면 파일 시스템은 어떻게 살아남을까요? 미리 저장할 내역을 외상장부(Journal)에 적고, 부팅 시 복원하는 방식 기반인 ext4/NTFS에서 나아가, 아예 원본 파일블록을 덮어쓰지 않고 최신 블록에 신규 내용을 쌓은 뒤 포인터만 교체하는 현대 스냅샷의 완성체 CoW(APFS / ZFS) 파일 시스템의 진화를 체험합니다.
