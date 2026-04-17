---
layout: default
title: "8주차: 전반기 기술 점검 및 중간고사"
---

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="#1E1E1E" rx="10"/><text x="300" y="100" fill="white" font-size="28" font-family="monospace" text-anchor="middle">OS Midterm Checkpoint</text></svg>
</div>

# 8주차: 전반기 딥테크 기술 점검 및 중간고사

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_os_08.png)
<br>

지난 7주 간의 상반기 일정을 통해, 우리는 그저 애플리케이션 코드를 짜는 유저 생태계를 벗어나, 거대한 메인보드 칩셋과 하드웨어 레지스터를 직결 제어하는 **시스템 마스터(System Master)**의 시야를 확보했습니다.

이번 8주차 중간고사 주간은 단순한 지식의 나열과 암기를 테스트하는 시간이 아닙니다. 지금까지 누적해 온 `프로세스-메모리-스케줄러-동기화-디스크`의 5단계 파이프라인이 하나의 서버 인프라 위에서 어떻게 맞물려 돌아가는가를 총체적으로 검증하는 실전 엔지니어링 리포팅 타임입니다.

---

## 📚 하위 문서 목차 (Sub-Chapters)

단편적인 지식을 결합해 전반적인 아키텍처 장애 추적(Troubleshooting) 능력을 점검하기 위해 3개의 가이드 문서를 할당했습니다.

1. **[전반기 아키텍처 복습](./01_architecture_review/index.md)**
   > 1강의 시스템 레이어부터 파일시스템 구조까지 이어지는 거시적 연결선 파이프라인 리뷰.
2. **[중간고사 실기 평가 안내](./02_assessment_guide/index.md)**
   > 메모리 Fault와 스레드 스케줄링 로그를 분석해 내는 이론/실무 복합 문항 오버뷰.
3. **[시스템 장애 디버깅 케이스](./03_case_study/index.md)**
   > 커널 데드락, i-node 파열, 메모리 스래싱 등 현업 운영체제 핵심 병목 트러블슈팅 복기.

<hr style="margin: 40px 0;">

> **🔥 튜터 격려사**
> 중간고사의 난도가 매우 높습니다만, 이 관문을 통과하고 나면 더 이상 에러 로그가 두렵지 않은 시스템 엔지니어의 강력한 디버깅 눈을 가지게 될 것입니다. 행운을 빕니다!
