---
layout: home
---

# 대용량 저장장치





## 학습목표

* 디스크의 구조에 대해서 설명할 수 있다.
* 디스크의 성능을 향상시키기 위한 다양한 스케줄링 기법을 이해할 수 있다.
* 저장장치의 성능을 향상시키기 위한 다양한 방법을 제안할 수 있다.





## 학습내용

* [디스크의 구조](01)
* [디스크 스케줄링](02)
* [저장장치의 성능 향상 방안](03)
* [디렉터리 접근 실습](04)







## 퀴즈로 확인하기









## 정리하기

* 그래에는 다양한 저장장치가 등장하여 하드 디스크나 CD-ROM이외에도 SSD나 각종 메모리 카드 혹은 프래시 드라이브가 등작하고 있다.
* 하드 디스크의 구조는 트랙, 섹터, 실린더로 구성된다.
* 디스크의 속도는 탐색시간, 회전지연시간, 그리고 전송시간으로 구분한다.
* 디스크의 입출력 요청의 처리 방법을 디스크 스케줄링이라고 하며, FCFS, SSTF, SCAN, C-SCAN,LOOK,C-LOOK등의 알고리즘을 사용하여 디스크 큐의 순서를 변경하여 성능을 개선한다.



* 디스크 저장 밀도를 높이거나 회전속도를 증가시켜서 혹은 SSD나 RAID를 사용하여 저장장치의 성능을 향상시킨다.
* RAID는 데이터 중복을 통하여 신뢰성을 향상시키거나, 병렬화를 통하여 디스크 성능을 향상시킨다.



* opendir() / closedir() 함수를 이용하여 디렉터리를 열어서 디렉터리 구조체의 포인터를 획득하거나 반납한다.
* readdir 함수는 개방된 디렉터리에서 디렉터리 엔트리를 하나씩 읽어서 반환한다. 디엑터리 엔트리에는 아이노드 번호 및 파일 이름을 갖고 있다.










