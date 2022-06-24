# CS study : 04 OS scheduling

> [Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner)/**OS**/
>
> [[운영체제] 스케줄러(scheduler)](https://dheldh77.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACScheduler)

- 위 repository 를 읽고 정리한 글입니다.

## Scheduler

> 한정적인 메모리를 여러 프로세스가 효율적으로 사용할 수 있도록 다음 실행 시간에 실행할 수 있는 프로세스 중에 하나를 선택하는 역할

*프로세스를 스케줄링하기 위한 Queue 에는 세 가지 종류가 존재한다.*

- Job Queue(Batch Queue) : 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready Queue : 현재 메모리 내에 있으면서 CPU 를 잡아서 실행되기를 기다리는, ready 상태의 프로세스의 집합
- Device Queue : Device I/O 작업을 대기하고 있는 프로세스의 집합



스케줄러의 종류는 3가지로 나눌 수 있다. 

1. **장기 스케줄러(Long-term scheduler)** / 잡 스케줄러(Job scheduler)

   - 프로세스의 상태
     new -> ready(in memory)
   - 메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리(일반적으로 디스크)에 임시로 저장된다. 
     - 이 pool 에 저장되어 있는 프로세스 중 어떤 프로세스에 메모리를 할당하여 ready queue 로 보낼지 결정하는 역할을 한다.

   - 디스크와 메모리 사이의 스케줄링 담당
   - degree of multiprogramming (실행 중인 프로세스의 수) 제어

2. 단기 스케줄러(Short-term scheduler) / CPU 스케줄러(CPU scheduler)

   - 프로세스의 상태
     ready -> running -> waiting -> ready

   - Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
   - 메모리와 CPU 사이의 스케줄링 담당

3. **중기 스케줄러(Mid-term scheduler)** / 스와퍼(Swapper)

   - 프로세스의 상태
     ready -> suspended (외부적인 이유로 프로세스의 수행이 정지된 상태로 메모리에서 내려간 상태, 스스로 돌아갈 수 없다.)

   - 여유 공간을 마련하기 위해 프로세스를 통째로 메모리에서 디스크로 쫓아내는 역할(swap out)
   - 프로세스에게서 memory 를 deallocate
   - degree of multiprogramming 제어

## CPU scheduler

**Preemptive** vs **Non**-**preemptive**

- 선점형 vs 비선점형 
- 비선점형 스케쥴링 
  -  프로세스가 자발적으로 CPU 점유를 멈출 때 까지, 기다려야 한다. (프로세스가 스스로 종료되거나, waiting 상태로 진입할 때까지 )
- 선점형 스케쥴링
  - a process can be preempted by the scheduler
  - 프로세스를 쫓아낼 수 있다. 

---

#### FCFS(First Come First Served)

![img](https://www.studytonight.com/operating-system/images/fcfs.png)

특징

- 가장 간단한 방법, FIFO Queue 로 쉽게 구현 가능.

- 비선점형(Non-Preemptive) 스케줄링
  일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU 를 반환하지 않는다. 할당되었던 CPU 가 반환될 때만 스케줄링이 이루어진다.

단점

- convoy effect: 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.
- 하나의 거대한 CPU-bound process 때문에, 작은 CPU 작업만을 요하는  I/O-bound process 까지 오랜 시간 기다려야 하는 비효율성 발생 

---

#### SJF(Shortest - Job - First)

![img](https://www.studytonight.com/operating-system/images/sjf-preemptive.png)

특징 

- 다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
- 비선점형(Non-Preemptive) 스케줄링

문제점

- starvation: 효율성을 추구하는게 가장 중요하지만 특정 프로세스가 지나치게 차별받으면 안된다. 이 스케줄링은 극단적으로 CPU 사용이 짧은 job 을 선호하므로, 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.

---

#### SRTF(Shortest Remaining Time First)

![img](https://www.studytonight.com/operating-system/images/sjf.png)

특징

- Preemptive SJF scheduling (선점형 SJF 스케줄링)

- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
- 선점형 (Preemptive) 스케줄링
  현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.
- average waiting time 이 가장 적다. 

문제점

- starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

---

#### Priority Scheduling

![img](https://www.studytonight.com/operating-system/images/priority-scheduling.png)

특징

- 우선순위가 가장 높은 프로세스에게 CPU 를 할당하는 스케줄링이다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
- 선점형 스케줄링(Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
- 비선점형 스케줄링(Non-Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.

문제점

- starvation: 무기한 봉쇄(Indefinite blocking), 실행 준비는 되어있으나 CPU 를 사용못하는 프로세스를 CPU 가 무기한 대기하는 상태

해결책

- aging: 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.

---

#### Round Robin

![img](https://www.studytonight.com/operating-system/images/round-robin.png)

특징

- 현대적인 CPU 스케줄링
- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다. (generally from 10 to 100 milliseconds)
- 할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.
- `RR`은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
- `RR`이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.

장점

- `Response time`이 빨라진다.
  n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
- 프로세스가 기다리는 시간이 CPU 를 사용할 만큼 증가한다.
  공정한 스케줄링이라고 할 수 있다.

---

#### Round Robin + Priority 

우선 순위 기준으로 프로세스를 실행하고, 

프로세스 간의 우선 순위가 같은 경우엔  Round Robin 스케쥴링을 사용한다. 

#### Multi-Level Queue(MLQ) Scheduling

 ![image-20220623201148819](2022-06-23-CS_study04_OS.assets/image-20220623201148819.png)

#### Multi-Level Feedback Queue(MLFQ) Scheduling

high priority 만 계속해서 실행하는 것을 막고자, 점점 더 많은 time quantum, CPU-burst time 을 할당한다.

 ![image-20220623201203909](2022-06-23-CS_study04_OS.assets/image-20220623201203909.png)

### etc 

CPU burst ?

![image-20220623194238183](2022-06-23-CS_study04_OS.assets/image-20220623194238183.png)
