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
