# 운영체제(Operating System) - Ewha W. Univ. 반효경 교수님

KOCW 운영체제(이화여자대학교, 반효경 교수님) 강의 듣고 정리  

http://www.kocw.net/home/search/kemView.do?kemId=1046323



## 3차시



### 3-1. Process1



#### 프로세스의 개념

"Process is **a program in execution**"

프로세스는 실행 중인 프로그램을 의미  

- 프로세스의 문맥(context)
  - CPU 수행 상태를 나타내는 하드웨어 문맥
    - Program Counter
    - 각종 register
  - 프로세스의 주소 공간
    - code, data, stack
  - 프로세스 관련 커널 자료 구조
    - PCB(Process Control Block)
    - Kernel stack



#### 프로세스의 상태(Process State)

프로세스는 상태(state)가 변경되며 수행된다.

- Running
  - CPU를 잡고 instruction을 수행중인 상태
- Ready
  - CPU를 기다리는 상태(in memory)
- Blocked(wait, sleep)
  - CPU를 주어도 당장 instruction을 수행할 수 없는 상태
  - Process 자신이 요청한 event(예: I/O)가 즉시 만족되지 않아 이를 기다리는 상태
  - (예) 디스크에서 file을 읽어와야 하는 경우

(추가)

- New
  - 프로세스가 생성중인 상태
- Terminated
  - 수행(execution)이 끝난 상태

<img src="https://user-images.githubusercontent.com/86271759/154794142-4dabc61d-c37a-4678-bdb4-4327c10f482e.jpg" width="450" height="350">

<img src="https://user-images.githubusercontent.com/86271759/154794148-eacfe048-b672-4b8e-b813-6ab68b24df38.jpg" width="450" height="350">

<img src="https://user-images.githubusercontent.com/86271759/154794149-be66f67a-113a-4cbd-96e7-36ae4e78f6f9.jpg" width="450" height="350">



#### Precess Control Block(PCB)

운영체제가 각 프로세스를 관리하기 위해 data 영역에다가 프로세스당 유지하는 정보  

다음의 구성 요소를 가진다. (구조체로 유지)

1. OS가 관리상 사용하는 정보
   - Process state, Process ID
   - scheduling information, priority
2. CPU 수행 관련 하드웨어 값
   - Program conter, registers
3. 메모리 관련
   - Code, data, stack의 위치 정보
4. 파일 관련
   - Open file descriptors... 

<img src="https://user-images.githubusercontent.com/86271759/154794204-7022a50c-95a6-4df5-b891-21f56820e690.jpg" width="300" height="350">



#### 문맥 교환(Context Switch) (★ 중요!)

CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정  

CPU가 다른 프로세스에게 넘어갈 때 운영체제는 다음을 수행  

- CPU를 내어주는 프로세스의 상태를 그 프로세스의 PCB에 저장

- CPU를 새롭게 얻는 프로세스의 상태를 PCB에서 읽음

<img src="https://user-images.githubusercontent.com/86271759/154794247-9744b04e-0dd6-4975-8396-13fbfe74725b.jpg" width="450" height="350">

<img src="https://user-images.githubusercontent.com/86271759/154794249-7977a8cf-decc-4875-954c-e2301aa93c84.jpg" width="450" height="350">

그림 (1)과 (2)의 경우를 잘 비교!



#### 프로세스를 스케줄링하기 위한 큐

- Job queue
  - 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready queue
  - 현재 메모리 내에 있으면서 **CPU**를 잡아서 실행되기를 기다리는 프로세스의 집합
- Device queues
  - **I/O device**의 처리를 기다리는 프로세스의 집합

프로세스들은 각 큐들을 오가며 수행된다.



#### 스케줄러(Scheduler)

- Long-term Scheduler(장기 스케줄러 or job scheduler)
  - 시작 프로세스 중 어떤 것들을 **ready queue**로 보낼지 결정
  - 프로세스에 **memory(및 각종 자원)**을 주는 문제
  - **Degree of Multiprogramming**을 제어
  - **Time sharing system에는 보통 장기 스케줄러가 없음(무조건 ready), 지금의 시스템은 중기 스케줄러로 Degree of Multiprogramming을 조절함** 
- **Short-term Sceduler(단기 스케줄러 or CPU scheduler)**
  - 다음번에 어떤 프로세스를 **running**시킬지 결정
  - 프로세스에 **CPU**를 주는 문제
  - 충분히 빨라야 함(millisecond 단위)
- **Medium-term Scheduler(중기 스케줄러 or Swapper)**
  - **여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄**
  - 프로세스에게서 **memory**를 뺏는 문제
  - **Degree of Multiprogramming**을 제어



#### 다시 프로세스의 상태(Process State)

프로세스는 상태(state)가 변경되며 수행된다.

- Running
  - CPU를 잡고 instruction을 수행중인 상태
- Ready
  - CPU를 기다리는 상태(메모리 등 다른 조건을 모두 만족한 상태)
- Blocked(wait, sleep)
  - I/O 등의 event를 (스스로) 기다리는 상태
  - (예) 디스크에서 file을 읽어와야 하는 경우
- Suspended(stopped)
  - 외부적인 이유로 프로세스의 수행이 정지된 상태
  - 프로세스는 통째로 디스크에 swap out된다.
  - (예1) 사용자가 프로그램을 일시 정지시킨 경우 (break key)  
  - (예2) 시스템이 여러 이유로 프로세스를 잠시 중단시킨 경우 (메모리에 너무 많은 프로세스가 올라와 있을 때)

*Blocked : 자신이 요청한 event가 만족되면 Ready*

*Suspended : 외부에서 resume해주어야 Active*

<img src="https://user-images.githubusercontent.com/86271759/154794297-e4c12032-5b8a-4ebc-a27c-487a6624a23f.jpg" width="450" height="350">







### 3-2. Process2



#### (2장 리뷰) 동기식 입출력과 비동기식 입출력

- 동기식 입출력(Synchronous I/O)
  - 프로세스가 I/O 요청 후 입출력 작업이 완료된 후에야 제어가 사용자 프로그램에 넘어감
  - 구현 방법1
    - I/O가 끝날 때까지 CPU를 낭비시킴
    - 매시점 하나의 I/O만 일어날 수 있음
  - 구현 방법2 (일반적인 방법)
    - I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗음
    - I/O 처리를 기다리는 줄에 그 프로그램을 줄 세움
    - 다른 프로그램에게 CPU를 줌
- 비동기식 입출력(Asynchronous I/O)
  - I/O가 시작된 후 입출력 작업이 끝나기를 기다리지 않고 제어가 사용자 프로그램에 즉시 넘어감

*두 경우 모두 I/O의 완료는 interrupt로 알려줌*



#### Thread

"A **thread** (or **lightweight process**) is a basic unit of CPU utilization"  

프로세스 내부에 CPU 수행 단위가 여러 개 있는 경우 그 CPU 수행 단위를 thread라고 부름  

<img src="https://user-images.githubusercontent.com/86271759/154794319-54762c1a-cb8e-41b8-9514-b4bbdf8caec1.jpg" width="450" height="350">

- Thread의 구성
  - program counter
  - register set
  - stack space
- 프로세스 내부에서 thread가 동료 thread와 공유하는 부분 (=task)
  - code section
  - data section
  - OS resources
- 전통적인 개념의 heavyweight process는 하나의 thread를 가지고 있는 task로 볼 수 있다.

- Thread 사용의 장점
  - 다중 스레드로 구성된 태스크 구조에서는 하나의 서버 스레드가 blocked(waiting) 상태인 동안에도 동일한 태스크 내의 다른 스레드가 실행(running)되어 빠른 처리를 할 수 있다.  
  - 동일한 일을 수행하는 다중 스레드가 협력하여 높은 처리율(throughput)과 성능 향상을 얻을 수 있다.  
  - 스레드를 사용하면 병렬성을 높일 수 있다.(CPU가 여러 개인 경우)  







### 3-3. Process3



#### Benefits of Threads

- **응답성 (Responsiveness)** 

  (예) multi-threaded Web

  - If one thread is blocked (eg network) another thread continues (eg display)  

- **자원 공유 (Resource Sharing)** 

  - n threads can share binary **code, data, resource** of the process  

- **경제성 (Economy)**

  - **creating & CPU switching thread** (rather than a **process**)
  - Solaris의 경우 위 두 가지 overhead가 각각 30배, 5배  

- **병렬성 (Utilization of Multiprocessor Architectures)**

  - each thread may be running in **parallel** on a **different processor**  



#### Implementation of Threads

- Some are supported by **kernel** -> **Kernel Threads**

  운영체제(커널)가 thread가 여러 개가 있다는 사실을 알고 있음   

  하나의 thread에서 다른 thread로 CPU를 넘겨주는 것을 커널이 CPU scheduling하듯이 수행해줌  

  - Windows 95/98/NT
  - Solaris
  - Digital UNIX, Mach

- Others are supported by **library** -> **User Threads**

  운영체제는 thread가 여러 개 있다는 사실을 모름  

  사용자 프로그램이 library의 지원을 받아서 스스로 여러 thread를 관리함  

  - POSIX P-threads
  - Mach C-threads
  - Solaris threads

- Some are real-time threads





