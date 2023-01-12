### PCB & Context Switching

### Process Management
> CPU 가 프로세스가 여러개일 때, CPU 스케줄링을 통해 관리하는 것  



CPU는 각 프로세스의 정보(특징)들을 갖고 있음 = `process metadata`
  
<br>

**Process Metadata**
- Process ID  (프로세스 구분자)
  - 새로운 프로세스에 시스템이 할당해주는 고유 id
- Process State
  - 프로세스의 생명 주기와 관련된 상태
  - waiting, running, ready, blocked, end, suspend-wait, suspend-ready 등이 있다.
- Process Priority
  - 프로세스 스케줄링을 위한 우선 순위
- CPU Registers
  - context switch가 발생하면 이 때의 레지스터 정보를 기억해서 다시 프로세스가 CPU 할당을 받으면 사용한다. accumulator, index, stack pointer 와 같은 레지스터의 값이 저장된다
- Owner
- CPU Usage
- Memory Usage

<br>

이러한 메타데이터는 프로세스가 생성되면, PCB(Process Control Block) 이라는 곳에 저장됨.


### PCB(Process Control Block)
> 프로세스의 각 메타 데이터들을 저장해 놓는 장소,  
> 하나의 PCB 에는 하나의 프로세스 정보가 담김.


![img.png](Downloads/doha/CS_STUDY/OS/image/PCB & ContextSwitching.png)

정리 :
1. 프로그램 실행
2. 프로세스 생성
3. 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 
4. 이 프로세스 메타 데이터들이 PCB 에 저장

<br>

**PCB 가 필요한 이유**  
- CPU 에서는 프로세스의 상태에 따라 교체 작업이 이루어진다.
- 만약 인터럽트가 발생해서, 다른 프로세스를 실행해야 한다면,
대기 상태의 프로세스 정보를 PCB 에 저장해 놓고,
다음에 다시 해당 프로세스가 CPU 를 할당받을 때 PCB 에서 정보를 가져와서 실행한다.


**PCB 관리 방법**
- 링크드 리스트 방식으로 관리됩니다.
- PCB List Head 라는 곳에 PCB 들이 연결되어 있습니다.
- 주소 값으로 연결이 이루어져 있는 연결리스트이기 때문에 삽입 삭제가 용이하다.
- 즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.


## Context Switching
> 현재 수행 중인 프로세스의 상태 정보를 PCB에 저장하고, 다음 수행할 프로세스의 PCB에서 정보를 읽어와 CPU 레지스터를 세팅하는 과정이다.

보통 인터럽트가 발생하거나, CPU의 사용 허가 시간을 모두 소모한 경우, 입출력을 위해 대기해야 하는 경우
Context Switching 이 발생한다.


### Context Switching 의 오버헤드
프로세스 작업 중에는 오버헤드를 감수해야 하는 상황이 있다.

```markdown
프로세스를 수행하다가 입출력 이벤트가 발생해서 대기 상태로 전환시킴
이때, CPU를 그냥 놀게 놔두는 것보다 다른 프로세스를 수행시키는 것이 효율적
```

즉, CPU 에 프로세스를 계속 수행시키도록 하기 위해 다른 프로세스를 Context Switching 하는 것
