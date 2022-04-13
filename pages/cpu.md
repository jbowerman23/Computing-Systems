# CPU Scheduling 
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/g/personal/bowermanjess_seattleu_edu/ESSUP8KsOHRGmUuOEAuXrhMBK4IELe1HQEwwsXW2GaYAGQ?e=FFlFcz)
---

## What is CPU Scheduling?
- When a system has multi-programming
  - Several jobs may be ready for execution
  - Ready jobs compete for CPU usu
- Need to decide which job to run
  - Part of OS that performs scheduling -> scheduler
  - Algorithm used to make decision -> scheduling algorithm
- Our focus will be on policies for scheduling!

---
## What kind of policy should be used?
- Depends on system or environment
  - Batch system
    - Set of jobs submitted to system
    - Can optimize policy for overall system performance
- Interactive system
  - Users directly waiting for results of jobs or commands
  - Policies must optimize user-perceived performance
- Real-time system
  - Jobs have deadlines by which they must complete
  - Policies must ensure predictability

---
## Objectives of scheduling algorithm
- Interactive Systems
  - Response time
    - Minimize time between issue & completion of interactive jobs
  - Proportionality
    - Users
      - Accept that long jobs may have long response times
      - Expect short jobs to have short response times
  - Maintain this perception

- Real-time systems
  - Predictability
  - Deadline
    - Ensure that job deadlines are met
      - Deadline miss could
        - Be catastrophic(hard-real-time system)
        - Degrade Quality of Service or result in data loss (soft-real-time system)
  - Priorities
    - Priorities need to be considered in scheduling decisions

---
## When should scheduling be done?
- Depends on type of environment
- In general, scheduling can be done when
  - New process is created
  - Process terminates
  - Process gets blocked
    - Waiting for V/O
    - Waiting for lock on shared resource
  - Interrupt occurs
    - I/O completion
    - Timer expiration

---
## Types of Scheduling
- Preemptive scheduling
  - Executing job can be interrupted & other job scheduled
- Non-preemptive scheduling
  - Once job is chosen for execution, it continues until it completes, blocks or voluntarily yields CPU

---
## Job Characteristics
![Computing Systems!](images/Scheduling.png)

---
# Scheduling Policies for Batch Systems

---
## First come first served (FCFS)
- Scheduler maintains queue
  - Incoming job added to end of queue
  - Job at head of queue chosen for exeuction
- Jobs scheduled in non-preemptive manner
  - Once job starts it continues until it blocks/terminates/yields
  - Blocked job removed from queue
  - Upon unblocking, job added to end of queue
- Pros: very simple
- Cons: short jobs may have long wait times

---
## Shortest Job First (SJF)
- Scheduler chooses shortest job for execution at any given time
- Two versions of SJF may be used
  - Version I: Non-preemptive
    - Once job is scheduled, it cannot be preempted until it completes CPU burst
  - Version II: Preemptive
    - New iob with shorter CPU burst than remaining time of current job arrives
      - Preempt current job & schedule new job
      - A.k.a. Shortest-Remaining-Time-First (SRTF)
- Pros: Good for short jobs
- Cons:
  - Needs prior knowledge of execution times of CPU bursts
  - Long jobs may starve


---
# Scheduling Policies for Interative Systems

---
## Round Robin (RR)
- Active jobs kept in ready queue
- Each job gets small unit (quantum) of CPU time
  - Quantum usually 10-100 milliseconds
- After quantum, job is preempted and next job in queue is scheduled
- Pros: simple; ensures fairness
- Cons: assumes all jobs are equally important
- Need to choose quantum carefully!
  - Too short -> too much switching overhead
  - Too long -> systme not responsive

---
## Priority Based Scheduling
- Priority value (integer) associated with each job
- Job with highest priortiy is scheduled
- Schedule could be preemptive or non-preemptive
- Priority assignment based on external factor
  - Importance of job to user [typically static assignment]
  - Cons: low-priority jobs can starve
- Priority assignment based on internal factor
  - Agine
  - %CPU time used in last X hours

---
## Hybrid approaches may be used for mixed job types

---
## Multilevel scheduling
- Ready queue partitioned into separate queues
  - E.g., system processes, foreground (interactive), background (batch)
- Each queue has its own scheduling algorithm
  - Example: foreground (RR), background (FCFS)
- Scheduling must be done between queues
  - Fixed priority - e.g., serve all foreground, then background
    - Possibility of starvation!
  - Time slice - e.g.; 80% foreground (RR), 20% background (FCFS)

