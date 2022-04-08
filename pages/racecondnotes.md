# Race Conditions
---

## Prior Notes  

- Each stack gets their own thread


---
## Data Sharing

- Thread of a process share process data
  - Multiple threads read/write same data
  - Consider banking proces
    - Thread 1: Withdraw money
    - Thread 2: deposit money
  - Account shared by threads 1 and 2


---
## Banking process operation
- Thread 1: Withdrawing
- Thread 2: Deposit

### Scenario where final result depends on order of execution is called race condition

---
## Understanding race conditions
- Threads must not be interleaved during access to shared data
  - This property is called mutual exclusion among threads
- Region of code during which shared data is accessed
  - Critical section/critical region
- No two threads may simultaneously be inside critical sections accessing same shared data

---
## Rule to avoid race conditions
- There are more rules in place from system perspective
  - Must consider fairness, efficiency, etc.
- Overall mutual exclusion requirements are
  - No two threads/processes may simultaneously be in critical sections accessing same shared data
  - No assumptions must be made about hardware (#procs, speed, etc.)
  - A thread/process not in critical section must not prevent other thread/process from entering critical section
  - No thread/process should have to wait for ever to enter critical section

---
## Strict Alternation
- Must take turns even if other process doesn't want a turn

- Bob
- Susan
  - Two people are sharing DS
- Bob gets the play with DS
  - Once Bob is finished, Susan can play with the DS

### __Susan can't take another turn till Bob takes his turn__

```c++
turn = 0; // thread/process 0 execute
turn = 1; // thread/process 1 execute

// Thread/Process 0

  while(turn != 0);
  critical_region_0();
  turn = 1;
  non_critical_region_0();
  

// Thread/Process 1
 while(turn != 1); // Spin locked, stuck till it is susan's turn
 critical_region_1();
 turn = 0;
 non_critical_region_1();
```

- Pros
  - Mutual Exclusion correctly maintained
    - Doesn't satisfy overall requirements though

- Cons
  - Busy waiting required
  - Thread/process forced to wait even if other thread/process executing is in a noncritical region
  - Should not block thread is one is not interested
  - Makes method unsuitable for use in **practice**
  - Gets worse as number of competing threads/processes increase


---
## Peterson's Solution
- Peterson's solution is restricted to two processes that alternate execution between their critical sections and remainder sections
- The processes are numbered 0 and 1
- Peterson's solution requires the two processes to share two data items:
```c++
int turn;
int interested[2];
```

---

```c++
#define FALSE 0;
#define TRUE 1;
#define N 2;

int turn;
int interested[N];

void enter_region(int process){
  int other;
  other = 1- process;
  
  interested[process] = TRUE;
  turn = process;
    while (turn == process && interested[other] == TRUE);
}

void leave_region(int process){
  interested[process] = FALSE;
}
```

- Pros
  - Mutual Exclusion correctly maintained
  - No strict alternation

- Cons
  - Busy waiting required



  
