# Linux top, ps, jobs, kill
### 20214021박윤채


---
### top
- 리눅스 시스템의 운용 상황을 실시간으로 전반적인 상황을 모니터링하거나 프로세스 관리를 할 수 있는 유틸리티 `CPU, Memory, Process`
- 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌
  - top 실행 전 옵션


### 세부 정보 필드별 항목
|항목 |내용|
|:---|:---|
|PID|프로세스 아이디(Process ID)|
|USER|프로세스를 실행시킨 사용자 ID|
|PRI|프로세스의 우선순위(priority)|
|NI|NICE값, 일의 nice value값(마이너스를 가지는 nice value는 우선순위가 높음)|
|VIRT|가상 메모리의 사용량(SWAP+RES)|
|RES|현재 페이지가 상주하고 있는 크기(Resident Size)|
|SHR|분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합|
|S|프로세스의 상태 `S(sleeping),R(running),W(swapped out process),Z(zombies)`|
|%CPU|프로세스가 사용하는 CPU의 사용율|
|%MEM|프로세스가 사용하는 메모리의 사용율|
|TIME+|프로세스가 시작된 이후 경과된 총 시간|
|COMMAND|실행된 명령어|

`Load average`
- 세 개의 숫자는 각각 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수를 나타냄.
- `uptime` 명령어로도 확인할 수 있으며 시스템 부하를 모니터링 할 수 있음(숫자가 높을 수록 시스템에 부하가 있다는 뜻이며 Load average 값은 CPU의 코어 수를 같이 확인해야 하며 코어 수 보다 적으면 문제가 없음)


### top 실행 후 사용할 수 있는 옵션
    * shift + t	: 실행된 시간이 큰 순서로 정렬
    * shift + m	: 메모리 사용량이 큰 순서로 정렬
    * shift + p	: cpu 사용량이 큰 순서로 정렬
    * k		: Process 종료
       o k 입력 후 종료할 PID를 입력한다
       o signal을 입력하라 표시되면 9를 넣어준다
    * c 		: 명령 인자 표시 / 비표시
    * l(소 문자) 	: uptime line(첫번째 행)을 표시 / 비표시
    * space bar	: Refresh
    * u		: 입력한 유저 소유의 Process만 표시
       o which user	: 와 같이 유저를 입력하라 표시될때 User를 입력
       o blank(공백) 입력시 모두 표시
    * shift + b	: 상단의 uptime 및 기타 정보값을 블락선택해 표시
    * f 		: 화면에 표시될 프로세스 관련 항목 설정
    * i			: idle 또는 좀비 상태의 프로세스는 표시 되지 않음
    * z		: 출력 색상 변경
    * d [sec]		: 설정된 초단위로 Refresh
    * c 		: command뒤에 인자값 표시
    * q		: 명령어 종료


### top 실행 전 옵션: _top의 정보들을 서식으로 출력하기 위한 옵션
     * -b		: 배치모드 옵션 
     * -n		: top 실행 주기를 설정
     * -p		: process ID 
---

### ps
- ps는 process status의 줄인말이며 현재 실행 중인 프로세스 목록과 상태를 출력하여 보여주는 기능을 함
   - 윈도우의 작업 관리자와 비슷함

### ps 명령어
- ps 옵션 사용법
```
$ps [option]
```
- ps 도움말
```
$ps --help all
```

### 자주 사용되는 ps 명령어 옵션 사용 예시
|명령어 옵션 |내용|
|:---|:---|
|||
|||
|||
|||
|||


### kill
- 리눅스에 여러 개의 프로세스가 사용 중인 경우 계속해서 CPU와 메모리를 사용하게 됨
- 이를 막기 위해 기존 프로세스를 중지(kill)하는 명령어 사용
### kill확인
- 현재 사용 중인 프로세스 찾기
- PID(Process ID)를 사용하여 중지


### kill 
```
$kill -9 PID
```
- 프로세스(Process)를 끄는 명령어
- kill의 단점은 Process ID로만 종료할 프로세스를 지정할 수 있다는 점
- `-9` kill 신호를 보내라는 뜻
  - `-9` 옵션은 다른 옵션과 따로 지정해야 하는 점에 주의


#### Proscess ID(PID) 
- `ps` 명령으로 Proscess list 출력해 찾을 수 있음
- `pidof [Process_Name]` 명령을 이용하면 바로 알아낼 수 있음


### kill process 일치하는 경우(kill all)
```
$killall -9 [process_name]
```


### process 매개변수를 참고해야 하는 경우 (pkill -f)
```
$pkill -9 -ef [my_process]
```
- 프로세스명만으로는 원하는 프로그램을 참조할 수 없는 경우 `pkill` 명령에 `-f` 옵션을 주어 명령어 전체를 참조해 `my_process` 찾기
- `-e` 로그 출력 옵션
- `-f` 명령행 전체 참조 옵션


### kill

- 프로세스 종료 명령이 아닌 프로세스에 신호를 보내는 명령
- 단 9번 신호(KILL)의 경우엔 신호를 보내지 않고 커널이 바로 프로세스를 정리해 버리기 때문에 프로세스를 바로 정리하고 싶다면 신호 9번을 사용해야 함
