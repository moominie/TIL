# 운영체제(Operating System) - Ewha W. Univ. 반효경 교수님

KOCW 운영체제(이화여자대학교, 반효경 교수님) 강의 듣고 정리  

http://www.kocw.net/home/search/kemView.do?kemId=1046323



## 2차시



### 2-1. System Structure & Program Execution1



#### 컴퓨터 시스템 구조

<img src="https://user-images.githubusercontent.com/86271759/154608907-77061fe5-5368-4a31-8836-3802986ed21f.jpg" width="400" height="300"/>

| Computer (host) | I/O device                                  |
| --------------- | ------------------------------------------- |
| CPU             | Disk(input, output device의 역할 모두 수행) |
| Memory          | input device : 키보드, 마우스 등            |
|                 | output device : 모니터, 프린터 등           |

memory : CPU의 작업 공간

CPU : memory 접근을 해서 instruction을 실행함



#### Mode bit

사용자 프로그램의 잘못된 수행으로 다른 프로그램 및 운영체제에 피해가 가지 않도록 하기 위한 보호 장치 필요   

Mode bit을 통해 하드웨어적으로 두 가지 모드의 operation 지원

`1 사용자 모드 : 사용자 프로그램 수행`   

`0 모니터 모드(= 커널 모드 = 시스템 모드) : OS 코드 수행`  

- 보안을 해칠 수 있는 중요한 명령어는 모니터 모드에서만 수행 가능한 '특권명령'으로 규정
- interrupt나 execution 발생 시 하드웨어가 mode bit을 0으로 바꿈
- 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 셋팅



#### Interrupt(인터럽트)

**현대의 운영체제는 인터럽트에 의해 구동됨**  

- 인터럽트
  - 인터럽트 당한 시점의 레지스터와 program counter를 save한 후 CPU의 제어를 인터럽트 처리 루틴에 넘긴다.
- Interrupt(넓은 의미)
  - **Interrupt(하드웨어 인터럽트) : 하드웨어가 발생시킨 인터럽트 (일반적인 의미)**
  - **Trap(소프트웨어 인터럽트)**
    - **Exception : 프로그램이 오류를 범한 경우**
    - **System call : 프로그램이 커널 함수를 호출하는 경우**
- Interrupt 관련 용어
  - **인터럽트 벡터**
    - 해당 인터럽트의 처리 루틴 **주소**를 가지고 있음
  - **인터럽트 처리 루틴(=interrupt Service Routine, 인터럽트 핸들러)**
    - 해당 인터럽트를 처리하는 **커널 함수 (실제 하는 일)**



#### Timer

- 타이머
  - 정해진 시간이 흐른 뒤 사용자 프로그램으로부터 운영체제로 제어권이 넘어가도록 interrupt를 발생시킴
  - 타이머는 매 클럭 틱 때마다 1씩 감소
  - 타이머 값이 0이 되면 타이머 interrupt 발생
  - **CPU를 특정 프로그램이 독점하는 것으로부터 보호**
- 타이머는 time sharing을 구현하기 위해 널리 이용됨
- 타이머는 현재 시간을 계산하기 위해서도 사용



#### Device Controller

- I/O device controller
  - **해당 I/O 장치 유형을 관리하는 일종의 작은 CPU**
  - 제어 정보를 위해 control register, status register를 가짐
  - local buffer를 가짐(일종의 data register로 데이터를 담음)
- I/O는 실제 device와 local buffer 사이에서 일어남
- Device controller는 I/O가 끝났을 경우 interrupt로 CPU에 그 사실을 알림

###### device driver(장치구동기)

OS 코드 중 각 장치별 처리 루틴 -> software  

###### device controller(장치제어기)

각 장치를 통제하는 일종의 작은 CPU -> hardware  



#### DMA Controller(Direct Memory Access)  

CPU 뿐만 아니라 직접 Memory에 접근할 수 있는 컨트롤러  

CPU를 더 효율적으로 쓰기 위한 장치  

- I/O device가 중간 중간 작업을 끝낼 때마다 interrupt를 걸면 CPU에 overhead 문제가 발생할 수 있으므로 DMA Controller가 I/O device의 local buffer에 접근해 완료된 작업을 Memory에 복사하는 일까지 해줌  
- 모든 작업 후에 DMA Controller는 CPU에 interrupt를 한 번만 걸어서 보고하면 됨  



#### Memory Controller

CPU와 DMA Controller가 특정 메모리 영역에 동시 접근하면 문제가 발생할 수 있음  

Memory Controller가 그걸 중재하는 역할을 담당



#### 입출력(I/O)의 수행

- 모든 입출력 명령은 특권 명령
- 사용자 프로그램은 어떻게 I/O를 하는가?
  - **System call(시스템콜)**
    - **사용자 프로그램은 운영체제에게 I/O 요청**
  - trap을 사용하여 인터럽트 벡터의 특정 위치로 이동
  - 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동
  - 올바른 I/O 요청인지 확인 후 I/O 수행
  - I/O 완료 시 제어권을 System call 다음 명령으로 옮김



#### System call

사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것







### 2-2. System Structure & Program Execution2

#### 동기식 입출력과 비동기식 입출력

<img src="https://user-images.githubusercontent.com/86271759/154608985-38f432a5-033b-4c2c-a0fa-9960dba995e3.jpg" width="400" height="300"/>

- 동기식 입출력(Synchronous I/O)
  - I/O 요청 후 입출력 작업이 완료된 후에야 제어가 사용자 프로그램에 넘어감
  - 구현 방법1
    - I/O가 끝날 때까지 CPU를 낭비시킴
    - 매시점 하나의 I/O만 일어날 수 있음
  - 구현 방법2
    - I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗음
    - I/O가 처리를 기다리는 줄에 그 프로그램을 줄 세움
    - 다른 프로그램에게 CPU를 줌
- 비동기식 입출력(Asynchronous I/O)
  - I/O가 시작된 후 입출력 작업이 끝나기를 기다리지 않고 제어가 사용자 프로그램에 즉시 넘어감

*두 경우 모두 I/O의 완료는 인터럽트로 알려줌*  



#### DMA(Direct Memory Access)

- 빠른 입출력 장치를 메모리에 가까운 속도로 처리하기 위해 사용
- CPU의 중재 없이 device controller가 device의 buffer storage의 내용을 메모리에 block 단위로 직접 전송
- Byte 단위가 아니라 block 단위로 인터럽트를 발생시킴



#### 서로 다른 입출력 명령어

- I/O를 수행하는 special instruction에 의해   

​		: Memory Addressess, Device Addressess 따로

- Memory Mapped I/O에 의해

​		: Memory Addressess에 디바이스 주소까지 저장



#### 저장장치 계층 구조

<img src="https://user-images.githubusercontent.com/86271759/154609057-516830d2-2ca5-403d-946c-e9481cacfa1b.jpg" width="400" height="300"/>

*Executable : CPU가 직접 접근 가능* 

위로 올라갈수록

- Speed(빠름)
- Cost(비쌈)
- Volatility(휘발성)



#### 프로그램의 실행(메모리 load)

<img src="https://user-images.githubusercontent.com/86271759/154609094-464cebd4-b54e-4965-b8d0-1f5ef203a851.jpg" width="400" height="300"/>

###### File System

각 프로그램은 File System에 실행파일로 저장되어 있음   

비휘발성(전원이 나가도 내용이 유지됨)  



###### Virtual memory

각 프로그램(프로세스)마다 stack, data, code로 구성된 독자적인 주소 공간(Address space)이 만들어짐   

프로그램 실행시 만들어졌다가 종료하면 사라짐  



###### Physical memory

메인 메모리에는 주소 공간 중 꼭 필요한 부분만 올라옴  



###### Swap area

메모리 용량 한계 때문에 Physical memory의 연장 공간으로서 사용



#### 커널 주소 공간의 내용

- code
  - 커널 코드
    - 시스템콜, 인터럽트 처리 코드
    - 자원 관리를 위한 코드
    - 편리한 서비스 제공을 위한 코드
- data
  - 운영체제가 사용하는 여러 자료 구조들이 저장됨
  - 하드웨어(CPU, Memory, disk) 종류별 자료구조
  - PCB(Process Control block) : 각 프로세스(프로그램)마다 그것을 관리하기 위한  PCB가 하나씩 만들어짐 
- stack
  - 함수를 사용하거나 리턴할 때 스택 영역을 사용함  
  - 사용자 프로세스마다 커널 스택을 따로 둠
  



#### 사용자 프로그램이 사용하는 함수

- 함수(function)
  - 사용자 정의 함수
    - 자신의 프로그램에서 정의한 함수
  - 라이브러리 함수
    - 자신의 프로그램에서 정의하지 않고 갖다 쓴 함수
    - 자신의 프로그램의 실행 파일에 포함되어 있음
  - 커널 함수
    - 운영체제 프로그램의 함수
    - 커널 함수의 호출 = 시스템 콜



#### 프로그램의 실행

<img src="https://user-images.githubusercontent.com/86271759/154609291-1ef7b944-8c25-457e-a232-6ccd8b15f7bb.jpg" width="400" height="300"/>

프로그램은 user mode와 kernel mode를 반복





