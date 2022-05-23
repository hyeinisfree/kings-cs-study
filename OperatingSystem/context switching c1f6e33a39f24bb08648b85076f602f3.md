# context switching

### PCB 개념

프로그램이 커널에 등록되고 커널의 관리를 받으면서 프로세스가 된다. 이때 프로세스 관리 블록(이하 PCB)을 할당받는다. PCB는 메모리의 커널영역에 존재하고 각 프로세스들에 대한 정보를 관리한다.

![untitled](https://github.com/imim-seung/test1/issues/3#issue-1244969360)

- PCB 가 관리하는 정보 (OS 별로 상이)
    1. process-id : 새로운 프로세스에 시스템이 할당해주는 고유 id
    2. process- state : 프로세스의 라이프 타임과 관련된 상태로, waiting, running, ready, blocked, end, suspend-wait, suspend-ready 가 있다.
    3. priority : 프로세스 스케줄링을 위한 우선순위이다.
    4. Process Accounting Information : CPU를 사용한 시간, CPU 할당 시간 등이 있다.
    5. Program Counter : 이전에 배운 PC로 다음 작업할 명령어 위치를 기억한다.
    6. List of Open Files : 실행 중에 프로그램에 필요한 모든 파일의 정보를 포함한다.
    7. Process I/0 status information : 해당 프로세스가 실행 중에 할당을 요구한 I/O 장치에 대한 정보를 담는다.
    8. **CPU 레지스터 : context switch가 발생하면 이 때의 레지스터 정보를 기억해서 다시 프로세스가 CPU 할당을 받으면 사용한다. accumulator, index, stack pointer 와 같은 레지스터의 값이 저장된다.**
    9. PCB Pointer : 준비중인 다음 프로세스의 주소를 가리킨다. 준비 상태나, 대기 상태의 큐를 구현할 때 다음을 가리키는 포인터로 사용된다.
    10. Memory management information : 메모리 관리 정보로 프로세스가 메모리의 어디에 있는 지 나타내는 메모리 정보와 메모리 보호를 위한 경계 레지스터, 한계 레지스터 값등이 저장된다. 또한, segmentation table , page table 등 정보도 보관한다.
    11. PPID, CPID : 부모 프로세스를 가리키는 PPID, 자식 프로세스를 관리하는 CPID가 저장된다.

### Process state transition diagram, Memory

![IMG_633435723C9F-1](https://user-images.githubusercontent.com/46683113/169802951-6a548129-dc9e-467c-8e69-d107e123ab9d.jpeg)

![IMG_D106604ED505-1](https://user-images.githubusercontent.com/46683113/169803194-81c8faff-41b3-4345-bbdf-7da7d958f643.jpeg)

### context switching 흐름

임의의 프로세서 Pa 와 Pb가 있다고 하자.  Pa에게 프로세서가 할당되어 running 상태이다. 근데 이때 어떤 인터럽트가 발생했다. 이때 커널이 개입해서 인터럽트가 어디서 왜 일어났는지 확인한다 (이를 interrupt handling 이라 한다. ) 그리고 특정한 서비스루틴을 호출(interrupt service)한다. 이 과정에서 프로세서에 있는 Pa의 레지스터 정보가 메모리 커널영역에 있는 Pa의 PCB에 저장되고 ready queue에 있는 Pb가 프로세서를 할당 받으면서 Pb의 pcb에 저장되어 있는 문맥이 복구(context restoring)된다. 그리고 Pb running 상태가 괸다. 

- context : 프로세스와 관련된 정보들의 집합
- context saving
- context restoring
- context switching : 커널의 개입으로 saving, restoring

### context switching Overhead

-context switching마다 소요되는 비용 —> 스레드 사용으로 이를 줄일 수 있다.

- 스레드의 사용으로 overhead 를 줄인다?
    
    프로세스 1,2가 자원 A를 사용한다면 자원 A를 사용하기 위해 1,2 사이에 context switching 이 필요하다. 하지만 스레드 1,2 둘이 자원 A를 사용한다면 자원을 공유하기 때문에 context switching를 안해도 된다.
    
- context switching overhead 가 증가하는 경우
    
    : 빈번하게 context switching 이 일어나는 경우. 프로세스 스케줄링에서 중요한 개념이 된다.
    
    다중 프로그래밍 환경에서 자원을 할당할 프로세스를 선택해야 한다. 이를 스케줄링이라 한다. 이 때 ready 상태에 있는 프로세스 중 running 으로 전이할 때 short-term  scheduling 이라 하고 이 정책에 의해 context switching overhead 가 결정된다. 이 스케줄링 정책 중 non-preemptive(비 선점) scheduling 은  할당 받은 자원을 스스로 반납할 때까지 사용하므로 overhead 가 적고, preemptive(선점) 방식은 할당시간의 종료 혹은 우선순위가 높은 프로세스의 등장 등으로 인해 자원을 뺏길 수 있으므로 overhead가 크다.
    
    또, 스케줄링 알고리즘(FCFS, RR, SPN,SRTN,HRRN,MLQ등.. )을 비교할 때 RR(Round-Robin )방식에서 time quantum 이 짧아질 수록 context switch가 빈번하게 발생된다.
