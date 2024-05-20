# [과제2] README 파일 작성하기

리눅스 명령어 중에서 top, ps, jobs, kill 명령어에 대해서 조사해보자!

## top

- top 명령어는 __현재 OS의 상태를 나타내주는 CLI 어플리케이션__
  > CLI : Command-Line Interface

- 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)
- 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌

### top 실행 전 옵션
- 순간의 정보를 확인하려면 `-b` 옵션 추가(batch 모드)
  > 이 조건만 줄 시 계속해서 화면을 갱신하니 `ctrl + c` 로 강제 종료
- `-n` : top 실행 주기 설정(반복 횟수)

### top 실행 후 명령어
- `shift + p` : CPU 사용률 내림차순
- `shit + m` : 메모리 사용률 내림차순
- `shift + t` : 프로세스가 돌아가고 있는 시간 순
- `k` : kill. `k` 입력 후 `PID 번호` 작성. signal은 9
- `f` : sort field 선택 화면 -> `q` 누르면 RES순으로 정렬
- `a` : 메모리 사용량에 따라 정렬
- `b` : Batch 모드로 작동
- `1` : CPU Core별로 사용량 보여줌
  
### 나의 OS 상태
  
`
/# top
`

![image](https://github.com/wjpark4430/ossw_assignment2/assets/170320686/c8d93491-1f85-44e3-b9e5-ad186f49cd37)

`
/# top -b -n 2
`

![image](https://github.com/wjpark4430/ossw_assignment2/assets/170320686/d6901fd1-f374-4038-96ae-300c15fb8163)

- 33m : 33분 동안 서버가 구동
- load average : 현재 시스템이 얼마나 일을 하는지를 나타냄.
  - 3개의 숫자는 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수.
  - CPU 코어수 보다 적으면 문제 없음
- Tasks : 프로세스 개수
- KiB Mem, Swap : 각 메모리의 사용량
- PR : 실행 우선순위
- VIRT, RES, SHR : 메모리 사용량 => 누수 check 가능
- S : 프로세스 상태(작업중, I/O 대기, 유휴 상태 등)
---
#### 자료 출처
> ___https://zzsza.github.io/development/2018/07/18/linux-top/___


## ps

- ps 명령어는 _Process State_ 의 약자로 __현재 실행 중인 프로세스와 상태를 출력하는 명령어__

## ps 명령어 옵션

- `-A` : 모든 프로세스를 출력

- `a (BSD)` : 터미널과 연관된 프로세스를 출력, x 옵션과 같이 사용하여 모든 프로세스를 출력할 때 사용

- `-a` : 세션 리더를 제외하고 데몬 프로세스처럼 터미널에 종속되지 않은 모든 프로세스를 출력

- `-e` : 커널 프로세스를 제외한 모든 프로세스를 출력

- `-f` : 출력을 풀 포맷으로 표기 (유닉스 스타일) UID, PID , PPID 등이 함께 표시

- `-l (System V)` : 출력을 긴 포맷으로 표기
  
- `l (BSD)` : 프로세스의 정보를 길게 보여주는 옵션으로 우선순위와 관련된 PRI 값과 NI 값을 확인

- `-o` : 출력 포맷을 지정

- `-M` : 64비트 프로세스들을 출력

- `-m` : 프로세스뿐만 아니라 커널 스레드도 출력

- `-p` : 특정 PID를 지정하여 출력

- `-r` : 현재 실행 중인 프로세스 출력

- `u (BSD)` : 프로세스의 소유자를 기준으로 출력

- `-u [사용자]` : 특정 사용자의 프로세스 정보를 출력, 사용자를 지정하지 않는다면 현재 사용자 기준으로 출력

- `x (BSD)` : 데몬 프로세스처럼 터미널에 종속되지 않은 프로세스를 출력

- `-x` : 로그인 상태에 있는 동안 아직 완료되지 않은 프로세스를 출력

### 현재 실행 중인 프로세스와 상태

`
/# ps
`

![image](https://github.com/wjpark4430/ossw_assignment2/assets/170320686/0af87a55-0ec6-4e23-a391-2c9443c27239)

### 많이 사용되는 명령어

`
/# ps -ef | head
`

![image](https://github.com/wjpark4430/ossw_assignment2/assets/170320686/26745487-cda3-4fd3-83fd-3ee58e593f5c)

### ps 명령어 출력 항목

- USER(BSD)/UID(System V) : 프로세스 소유자의 이름
- PID : 프로세스의 식별 번호
- PPID : 부모 프로세스의 PID
- %CPU : CPU 사용 비율의 추정치 (BSD)
- %MEM : Memory 사용 비율의 추정치(BSD)
- VSZ : K 단위 또는 페이지 단위의 가상 메모리 사용량
- RSS : 실제 메모리 사용량
- TTY : 프로세스와 연결된 터미널
- S (System V)/STAT (BSD) : 현재 프로세스의 상태 코드
- TIME : 총 CPU 사용 시간
- COMMAND : 프로세스의 실행 명령행
- STIME : 프로세스가 시작된 시간 혹은 날짜
- C (System V)/CP (BSD) : 짧은 기간 동안의 CPU 사용률
- F : 플래그
- PRI : 실제 실행 우선순위
- NI : nice 우선순위 번호

#### 자료 출처
> ___https://blog.naver.com/tmk0429/222318530824___

## jobs
- 현재 실행하는 작업의 상태를 표시하는 명령어
