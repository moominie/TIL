# 운영체제(Operating System) - Ewha W. Univ. 반효경 교수님

KOCW 운영체제(이화여자대학교, 반효경 교수님) 강의 듣고 정리  

http://www.kocw.net/home/search/kemView.do?kemId=1046323



## 4차시



### 4-1. Process Management1



#### 프로세스 생성(Process Creation)

- 부모 프로세스(Parent process)가 자식 프로세스(Children process)를 생성
- 프로세스의 트리(계층 구조) 형성
- 프로세스는 자원을 필요로 함
  - 운영체제로부터 받는다.
  - 부모와 공유한다.
- 자원의 공유
  - 부모와 자식이 모든 자원을 공유하는 모델 
  - 일부를 공유하는 모델 (효율적)
    - (예) Copy-on-write(COW) 기법 : 그 이전까지는 program counter만 새로 copy해서 자식 프로세스를 생성하고 부모 것을 그대로 공유하다가 write가 발생할 때(내용이 바뀔 때) 그 부분만 부모의 code, data, stack을 copy해서 새로운 걸 만든다.
  - **전혀 공유하지 않는 모델 (원칙)**
- 수행(Execution)
  - 부모와 자식이 공존하며 수행되는 모델
  - 자식이 종료(terminate)될 때까지 부모가 기다리는(wait) 모델

- 주소 공간(Address space)
  - 자식은 부모의 주소 공간을 그대로 복사함(binary and OS data)
  - 자식은 그 공간에 새로운 프로그램을 올림
- 유닉스의 예
  - 1단계 : **fork() 시스템 콜**이 새로운 프로세스를 형성
    - **부모를 그대로 복사** (OS data except PID + binary)
    - 주소 공간 할당
  - 2단계 : fork 다음에 이어지는 **exec() 시스템 콜을 통해 새로운 프로그램을 메모리에 올림**



#### 프로세스 종료(Precess Termination)

- 자발적 종료 : 프로세스가 마지막 명령을 수행한 후 운영체제에게 이를 알려줌**(exit** 시스템 콜)
  - 자식이 부모에게 output data를 보냄(via **wait**)
  - 프로세스의 각종 자원들이 운영체제에게 반납됨
- 비자발적 종료(강제 종료) : 부모 프로세스가 자식을 수행 종료시킴(**abort**)
  - 자식이 할당 자원의 한계치를 넘어섬
  - 자식에게 할당된 태스크가 더 이상 필요하지 않음
  - 부모가 종료(exit)하는 경우
    - 운영체제는 부모 프로세스가 종료하는 경우 자식이 더 이상 수행되지 않도록 한다.
    - 단계적인 종료







### 4-2. Process Management2



#### 프로세스와 관련한 시스템 콜

- fork() : create a child (copy)
- exec() : overlay new image
- wait() : sleep until child is done
- exit() : frees all the resources, notify parent  



#### fork() 시스템 콜

- **A process is created by the `fork()` system call.**
  - **creates a new address space that is a duplicate of the caller.**

<img src="https://user-images.githubusercontent.com/86271759/155334934-31ead692-b8e3-40d3-973c-40df5373ec95.jpg" width="450" height="300">

fork()를 통해 자식 프로세스를 생성하면 **자식 프로세스는 fork() 이후 코드부터 실행**함

fork()가 일어나게 되면 자식은 부모의 context를 그대로 복제하는데, 부모의 program counter가 fork()를 가리키고 있으므로 자식 프로세스는 fork() 이후의 코드부터 실행하게 됨   

**부모 프로세스는 fork() 결과값이 양수(자식의 pid값)이고, 자식은 0**이므로 부모와 자식 프로세스는 서로 원본과 복제본을 구분할 수 있음  

fork() 결과값이 다른 것을 이용해서 이후 서로 다른 일을 수행하게 할 수 있음   

<img src="https://user-images.githubusercontent.com/86271759/155335566-82a6626f-b218-4d7a-9176-4ff237beb9a5.jpg" width="450" height="300">

부모 프로세스는 "Hello, I am child!" 출력 후에 "Hello, I am parent!"를 출력  

자식 프로세스는 fork() 이후의 코드를 실행하기 때문에 "Hello, I am child!"만 출력  



#### exec() 시스템 콜

- **A precess can execute a different program by the `exec()` system call.**
  - r**eplaces the memory image of the caller with a new program.**

<img src="https://user-images.githubusercontent.com/86271759/155335485-8cce9057-8b4f-4902-861e-7f4cef2025c8.jpg" width="450" height="300">

execlp()를 만나면 자식 프로세스는 execlp 안의 새로운 프로그램을 덮어씌워서 실행함  

<img src="https://user-images.githubusercontent.com/86271759/155334928-effab9cd-a520-4bc2-a6c8-d4ea083d57f2.jpg" width="450" height="300">

- echo : Linux 명령어, 이 명령어 뒤에 나오는 argument(""안에 작성)들을 그대로 화면에 출력해줌, C언어의 printf와 비슷한 기능

맨 처음 "1"을 출력하고, 자식 프로세스가 생성된 후 echo 명령어를 수행하여 "3"을 출력하고 종료된다.



#### wait() 시스템 콜

- 프로세스 A가 wait() 시스템 콜을 호출하면
  - **커널은 child가 종료할 때까지 프로세스 A를 sleep시킨다. (block 상태)**
  - Child process가 종료되면 커널은 프로세스 A를 깨운다. (ready 상태) 

<img src="https://user-images.githubusercontent.com/86271759/155336214-23b7f86c-026c-4cc3-bf8d-4920e63e9c3d.jpg" width="450" height="300">  

부모 프로세스의 실행 코드에 wait() 시스템 콜을 작성하면 부모 프로세스는 blocked 상태가 되어 CPU를 얻지 못 하고 기다림  

자식 프로세스가 자신의 코드를 다 실행하고 종료되면 그때 부모 프로세스는 wait() 시스템 콜을 빠져 나가서 그 다음 코드들을 실행할 수 있음  



#### exit() 시스템 콜

- **프로세스의 종료**
  - 자발적 종료
    - 마지막 statement 수행 후 exit() 시스템 콜을 통해
    - 프로그램에 명시적으로 적어주지 않아도 main 함수가 리턴되는 위치에 컴파일러가 넣어줌
  - 비자발적 종료
    - 부모 프로세스가 자식 프로세스를 강제 종료시킴
      - 자식 프로세스가 한계치를 넘어서는 자원 요청
      - 자식에게 할당된 태스크가 더 이상 필요하지 않음
    - 키보드로 kill, break 등을 친 경우
    - 부모가 종료하는 경우
      - 부모 프로세스가 종료하기 전에 자식들이 먼저 종료됨  



#### 프로세스 간 협력

- 독립적 프로세스 (Independent process)
  - 프로세스는 각자의 주소 공간을 가지고 수행되므로 원칙적으로 하나의 프로세스는 다른 프로세스의 수행에 영향을 미치지 못함
- 협력 프로세스 (Cooperation process)
  - 프로세스 협력 메커니즘을 통해 하나의 프로세스가 다른 프로세스의 수행에 영향을 미칠 수 있음
- 프로세스 간 협력 메커니즘 (IPC : Interprocess Communication)
  - 메시지를 전달하는 방법
    - **message passing** : 커널을 통해 메시지 전달
  - 주소 공간을 공유하는 방법
    - **shared memory** : 서로 다른 프로세스 간에도 일부 주소 공간을 공유하게 하는 shared memory 메커니즘이 있음
    - **★ thread** : thread는 사실상 하나의 프로세스이므로 프로세스 간 협력으로 보기는 어렵지만 동일한 process를 구성하는 thread들 간에는 주소 공간을 공유하므로 협력이 가능



#### Message Passing

- Message system

  - 프로세스 사이에 공유 변수(shared variable)를 일체 사용하지 않고 통신하는 시스템

- Direct Communication

  - 통신하려는 프로세스의 이름을 명시적으로 표시

  <img src="https://user-images.githubusercontent.com/86271759/155336435-a1568452-2ea1-4d7a-9760-f8ab59b18ea2.jpg" width="450" height="100">

- Indirect Communication

  - mailbox (또는 port)를 통해 메시지를 간접 전달

  <img src="https://user-images.githubusercontent.com/86271759/155336444-66e7007a-17bc-46e7-81e2-c9fc15759330.jpg" width="450" height="100">

*Direct든 Indirect든 프로세스끼리 직접 메시지 전달은 불가능하며 반드시 중간에 운영체제(커널)을 통해서 전달해야 한다. 다만 interface 측면에서 메시지를 받는 대상을 표시하느냐 아니면 mailbox를 통해서 간접적으로 전달하느냐의 차이가 있을 뿐!*

<img src="https://user-images.githubusercontent.com/86271759/155336450-13456b94-f18b-438e-883e-4eaee46ad55f.jpg" widht="450" height="300">





