---
layout: default
title: "1주차: 윈도우 컴퓨터란? 시작과 역사적 배경"
---

<div align='center'>
  <img src='img/toon1.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Webtoon Splash' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <rect x="50" y="50" width="100" height="100" fill="#005A9E" rx="5"/>
  <text x="100" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">Hardware</text>
  <path d="M 160 100 L 240 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/>
  <rect x="250" y="50" width="100" height="100" fill="#0078D7" rx="5"/>
  <text x="300" y="105" fill="white" font-size="20" font-family="monospace" text-anchor="middle">NT Kernel</text>
  <path d="M 360 100 L 440 100" stroke="#00FF00" stroke-width="4" marker-end="url(#arrow)"/>
  <rect x="450" y="50" width="100" height="100" fill="#4B4B4B" rx="5"/>
  <text x="500" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">User App</text>
  <text x="300" y="30" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">The HAL (Hardware Abstraction Layer)</text>
  <defs><marker id="arrow" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#00FF00"/></marker></defs>
</svg>
</div>

# 1주차: 윈도우 컴퓨터란? 시작과 역사적 배경

![OS Core Architecture](/Users/hojin/.gemini/antigravity/brain/28d2e8ff-2bf4-4b06-8f22-23880f1f7300/ai_window_01.png)
<br>

- **대주제**: 윈도우 컴퓨터란? 시작과 역사적 배경
- **세부학습목표**: 마이크로소프트와 윈도우 운영체제의 탄생 배경, IBM PC 호환 기기 위에서의 진화 과정을 파악한다.

#### 📌 1-1. MS-DOS에서 NT 커널까지
1. 1980년대: IBM PC와 MS-DOS 1.0의 시작
2. Windows 95~98: DOS 위에서 돌아가던 GUI 껍데기의 한계
3. Windows NT 등장: 기업용 서버 시장을 노린 진정한 커널(추상화 계층) 시스템
4. 현대의 Windows 11 아키텍처와 레거시 호환성

#### 📌 1-2. 파일 시스템과 디렉터리 철학
1. 왜 `C:\` 드라이브부터 시작하는가? (A, B 플로피 디스크의 역사)
2. 백슬래시(`\`) 기호 경로 구분자의 역사적 기원 (리눅스와 차이점)
3. 무대소문자 구분의 양면성 (NTFS 파일 시스템)

---


<div align='center'>
  <img src='img/toon2.png' width='70%' style='border-radius: 10px; margin-bottom: 20px;' alt='Concept Art' />
</div>

<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="200" viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <circle cx="150" cy="100" r="50" fill="none" stroke="#E81123" stroke-width="5"/>
  <text x="150" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows 95/98</text>
  <text x="150" y="130" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">(DOS Core)</text>
  <circle cx="450" cy="100" r="60" fill="none" stroke="#0078D7" stroke-width="5"/>
  <text x="450" y="105" fill="white" font-size="18" font-family="monospace" text-anchor="middle">Windows NT</text>
  <text x="450" y="130" fill="gray" font-size="14" font-family="monospace" text-anchor="middle">(Protected Mod)</text>
</svg>
</div>



---

## [심화 렉처] MS-DOS: 윈도우의 기원

여러분은 윈도우(Windows)를 단순히 파란 배경의 GUI 시스템으로만 알 것입니다. 윈도우 키+R을 눌러 `cmd` 를 타이핑해 보십시오. 나타나는 시컴한 콘솔은 과거 1980년대 빌 게이츠가 IBM 시스템에 납품했던 디스크 운영체제(MS-DOS)의 근본 유산입니다.
파일 경로가 왜 `C:\` 부터 시작할까요? 초창기 A와 B 드라이브는 디스켓(플로피)의 몫이었습니다. 비싼 하드디스크가 등장하자 가장 남는 문자열인 C가 지정되었고 지금도 유지되고 있습니다.


<div align='center' style='margin: 30px 0;'>
  <svg width="100%" height="120" viewBox="0 0 600 120" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="#1E1E1E" rx="10"/>
  <text x="300" y="50" fill="white" font-size="24" font-family="monospace" text-anchor="middle">C:\ : HDD / SSD Core</text>
  <text x="300" y="90" fill="#00FF00" font-size="16" font-family="monospace" text-anchor="middle">A: / B: (Floppy Disk Legacy History)</text>
</svg>
</div>


## [심화 렉처] NT커널과 진정한 플랫폼

Windows 95, 98 은 여전히 DOS 쉘 위에서 겉도는 그래픽 프로그램이었습니다. 그러나 기업 시장을 타겟으로 한 Windows NT 커널의 등장은 무소불위의 권력을 지닌 드라이버를 격리시킨 진정한 아키텍처였습니다.
