---
layout: default
title: "5. OS API 한계와 io_uring의 도래"
---

# 5. 리눅스 커널 API와 극한의 io_uring 프레임워크

응용 프로그래머들은 블록 장치(SSD)든 문자열 스트림 장치(키보드/tty)든 손쉽게 가상 파일시스템(VFS) 추상화 API를 거쳐 조작력을 행사합니다.

![디렉터리 API 흐름](./img/os13_directory_api.svg)

```c
#include <stdio.h>
#include <sys/stat.h>     // 메타데이터 파서
#include <dirent.h>       // 디렉터리 스트림 제어

int main() {
    struct stat info;
    stat("/dev/sda", &info);  // 대상 디바이스 혹은 대상 텍스트 파일의 메타 덤프 복사 추출

    if (S_ISBLK(info.st_mode)) printf("블록 I/O 장치입니다!\n"); // SSD 블록장치 감지 매크로
    printf("고유 i-node 번호: %ld\n", info.st_ino);

    DIR *dp = opendir("/etc"); // 커널에서 목록(목차) 열람 전용 포인터 스트림 오픈
    struct dirent *dirp;
    while ((dirp = readdir(dp)) != NULL) {
        printf("폴더 내부 요소 이름: %s\n", dirp->d_name);
    }
    
    closedir(dp); // 파일 지향적 자원 반납
    return 0;
}
```

<br>

# 6. [최종 패러다임] 병목의 역전, 한계 돌파 io_uring 

스토리지 I/O 전송 속도가 초광속(PCIe Gen 5급 SSD) 수준이 되어버리자 컴퓨터 공학계에 끔찍한 병목 역전이 발생합니다. 

오히려 I/O 데이터를 파일 시스템에 읽으라 오더를 내리는 옛 기술인 `read() / epoll()` 시스템 콜 인터럽트 과정, 즉 **'유저 권한 모드' ↔ '커널 권한 링 스페이스' 사이의 문맥 강제 전환(Context Switching Overhead)** 그 자체를 1초에 수백만 번 오가는 로스 타임이 SSD 속도보다 훨씬 느려져 전체 시스템 속도를 주저앉히는 주객 전도 사태가 도래했습니다.

### 갓 링커 프레임워크 io_uring
이 참사를 산산조각 낸 것이 리눅스 커널 서브시스템의 창조자 Jens Axboe가 디자인한 커널 5.1의 **io_uring 괴물 비동기(AIO) 프레임워크**입니다.

이 기술은 커널 보안 공간 장벽에 구멍을 뚫고 유저 응용 계층이 공동으로 관람할 수 있는 **메모리 환상 큐고리(Ring Buffer, SQ/CQ)**를 만들어버렸습니다. 
유저 C 소스코드가 디스크 조회 요청명세서를 무자비하게 큐 고리에 밀어넣기만 하면, **CPU 인터럽트 트랩이나 어떠한 시스템 콜 제동 전환 없이** 커널의 백그라운드 I/O 스레드가 혼자 슬쩍 이를 쓸어가고 작업 완료 포인터를 리턴 박스(큐고리 반대편)에 조용히 놔둡니다!

이 제로-오버헤드, 시스템 콜 궤도 완전 생략의 철학적 돌파는 현재 Redis 인메모리 캐시, PosgreSQL, 웹 기반 스케일러 Node.js 라이브러리의 엔진 코어를 완전히 새 역사로 뒤엎어 갈아끼우게 만들었습니다. 시스템 스케줄링과 I/O 레이어 최상단 엔지니어들의 궁극적 로망이 도달한 모습입니다.
