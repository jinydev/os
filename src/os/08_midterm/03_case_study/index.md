---
layout: default
title: "3. 시스템 장애 디버깅 케이스"
---

# 3. [리포팅] 시스템 장애 복서 케이스 리뷰

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="65" fill="#00FF00" font-size="18" font-family="monospace" text-anchor="middle">Review 1~7 Weeks</text></svg>
</div>

## 실전 디버깅 케이스 스터디

현업에서 가장 빈번하게 발생하는 서버군의 핵심 장애 케이스들을 복기하며 엔지니어 뇌 구조를 형성합니다.

1. **Deadlock (교착 상태) 시뮬레이션 복기**
   * 두 스레드가 서로의 자원을 점유하고 타임아웃 없이 무한 대기하던 양상.
   * C/Java 백엔드 단에서 타임아웃(`tryLock()`)과 락 오더링 패러다임을 부여해 회피했던 과제 검토.
2. **리눅스 OOM Killer 출동 이력 분석**
   * 스래싱 현상으로 인한 서버 중단. `dmesg` 명령어로 커널 커맨드를 뜯어보고 워킹 셋(Working Set) 제한을 설정했던 복구 프로세스 리뷰.
3. **i-node 고갈 한계 돌파**
   * 잔여 하드디스크 용량이 수십 GB나 남아있음에도 임시 세션 쪼가리 파일들로 메타데이터 색인이 거덜 났을 때 `df -i` 추적을 통하여 장애를 규명했던 실무 에피소드.
