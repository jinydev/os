---
layout: default
title: "2. NT 커널과 진정한 OS 아키텍처"
---

# 2. NT커널과 진정한 플랫폼

DOS(도스)는 훌륭한 프로그램이었지만, 진정한 의미의 현대적 '운영체제'라 부르기엔 결격 사유가 컸습니다. 

왜냐하면 어떤 게임이나 프로그램 하나가 메모리를 잘못 건드리거나 무한 루프에 빠지면, 커널이 이를 중재하지 못하고 컴퓨터 전체가 그대로 먹통이 되어 재부팅(블루스크린)을 해야만 했기 때문입니다. 즉 자원 격리(Isolation) 기능이 불완전했습니다. 심지어 대성공을 거둔 초창기 Windows 95, 98 조차도 여전히 밑바닥에는 이 불안정한 DOS 쉘이 메모리를 전부 통제하고 그 위에서 겉도는 예쁜 그래픽 껍데기 프로그램에 불과했습니다.

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <circle cx="150" cy="100" r="50" fill="none" stroke="#E81123" stroke-width="5"/>
  <text x="150" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows 98</text>
  <text x="150" y="130" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">(DOS Core)</text>
  <circle cx="450" cy="100" r="60" fill="none" stroke="#0078D7" stroke-width="5"/>
  <text x="450" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows NT</text>
  <text x="450" y="130" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">(Protected Mode)</text>
</svg>
</div>

## 진정한 패러다임 전환: Windows NT 커널의 도래
이를 근본적으로 뒤엎기 위해 마이크로소프트는 기업/서버 시장을 타겟으로 바닥부터 완전히 새로운 하드웨어 격리 통제 시스템을 새롭게 빌드업했습니다. 그것이 바로 **Windows NT (New Technology) 커널**입니다.

NT 커널 아키텍처의 핵심은 무소불위의 권력을 지닌 드라이버 층을 유저 애플리케이션(User App)과 완벽히 격리(Protected Mode)시켰다는 데 있습니다. 유저가 짠 아무리 쓰레기 같은 코드가 메모리를 파괴하려 들더라도 절대 시스템 셧다운으로 직결되지 않고, 커널이 오직 그 프로그램만 깔끔하게 `Kill` 시킬 수 있는 진정한 의미의 현대적 OS 아키텍처 토대를 완성시켰습니다. 현대 우리가 쓰는 무수한 윈도우 10/11 모두가 근간에 이 단단한 NT 아키텍처 혈통을 잇고 있습니다.
