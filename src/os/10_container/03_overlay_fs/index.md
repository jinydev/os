---
layout: default
title: "3. OCI 규격과 Layered FS"
---

# 3. OCI 규격과 이미지 레이어(Layered FS)

도커 허브에서 1GB짜리 Ubuntu 베이스 이미지를 하나 다운받고, 거기에 Node.js를 얹어 빌드한 1.1GB짜리 또 다른 파생 커스텀 컨테이너 이미지를 다운로드한다고 해서 여러분의 하드디스크가 2.1GB(1+1.1)로 뻥튀기되지 않습니다! 

## 중첩의 마법: Union Mount FileSystem
OverlayFS나 AuFS 같은 리눅스 유니온 마운트(Union Mount) 파일 시스템 기능 덕분에, 컨테이너 **이미지는 얇디얇은 유리판(Layer)들의 단순 중첩 탑차 구조(Layered FS)**를 띕니다. 

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_10.png)

1. 하단의 이전 단계 공통 레이어들(Ubuntu 베이스 등)은 읽기 전용(Read-Only) 상태로 디스크에 단 한 벌(1개)만 캐시 보관되어 1,000개의 컨테이너 코어들 사이에 완벽히 공유됩니다.
2. 실행 시점에 컨테이너 상층부에 투명한(Writable) 임시 유리판이 덮어씌워지고 오직 그 **상단 레이어 블록에만 최신 파일 변경의 기록(Diff)이 차곡차곡 기록**됩니다.

이 기술 때문에 수십 개의 대규모 컨테이너 서비스들을 마이크로 서비스(MSA)망에 던져 순식간에 올렸다 내렸다 부팅시켜도, 디스크 저장 메인 공간 점유율 낭비가 제로에 가깝게 수렴하는 무적의 스케일업(Scale-up) 고속 배포망 엔진을 완성시키게 되었습니다.
