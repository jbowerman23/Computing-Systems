# Process and Threads
---

## Process
<ul>
  <li>Abstraction for a running program instance</li>
  <li>A process is not equivalent to a program</li>
  <li>More to process than just a program</li>
</ul>

---
## Program Execution
<ul>
  <li>To execute a program, corresponding process must be created</li>
  <ul>
      <li>Others are created or needed as needed/requested</li>
    </ul>
  <li>After creation, process becomes active or ready for execution</li>
</ul>

---
## Key Process Terms
<ul>
  <li>The process is the major OS abstraction of a running program</li>
  <li>Processes exists in one of many difference process states, including running, ready, and waiting/blocked</li>
  <li>A process list contains information about all processes in the system</li>
</ul>

---
## Process creation steps
- Assign unique identifier to new process
- Allocate & setup memory space for process(process memory image)
  - Process control block(PCB)
  - Program & data -> organized into regions
    - Code/text space
    - Global data space
      - Stored in its own region 
    - Heap (dynamically allocated data) space
    - Stack (local function data) space
- Set up memory management structures for process
  - We will look at details of these structures later...
- Other structures OS may keep for performance monitoring, etc.

---
## Process creation mechanisms
- 1st option -> cloning
  - Process spawns process that is a copy of itself
    - Adopted by Unix based Oss  fork() system call
- 2nd option  creation from scratch
  - Process creates new process with appropriate parameters
    - Adopted by Windows - CreateProcess() system call

---
## Unix process creation (fork)

- Process invokes fork to initiate creation of new process
- Creating process is parent & new process is child
- System call creates new process
- Data from parent process copied to memory of child process
  - Memory image, environment settings, l/0 handles, etc.
  - Of course, child gets its own ID, scheduling info, etc.


---
### Fork Call
<ul>
  <li>Upon sucess, fork returns child ID to parent process</li>
  <li>...and returns 0 to child process</li>
</ul>

<ul>
  <li>Parent/child processes independently continue execution from statement after fork</li>
  <li>(If process spawn fails, fork returns -1 to parents and no child is created)</li>
</ul>

```c++
pid_t id = fork();
if(id == -1){
  cout << "Error creating process\n";
} else if (id == 0) {
  cout << "I'm a child process!\n";
} else {
  cout << "I just became a parent!\n";
}
```

- ...return value to enable conditional execution after fork
  - So, even though program is same, paths can be different!
  - Different behavior can thus be achieved in parent and child
---

### Alternate Fork Call

<ul>
  <li>Child can change the program it executes</li>
    <ul>
      <li>Invoke exec family of system call to change its memory image</li>
      <li>stops executing code in parent program and starts new program</li>
    </ul>
</ul>


```c++
pid_t id = fork();
if(id == -1){
  cout << "Error creating process\n";
} else if (id == 0){
  // child process functionality
  char* args[] = {"echo", "hello", NULL};
  execvp(args[0], args);
} else {
  cout << "I just became a parent!\n";
}
```

---
### On Unix based systems...

* OS maintains notion of process hierarchy
  * A process, its children, their children, etc
* Parent must be allowed to read child's exit status
* If parent terminantes before child...
  * Child is now an orphan process
  * Orphan processes are adopted by init process

---
### Zombie process
- If a child process terminated before parent
  - System will still need to keep child's PCB
  - Child process becomes a zombie process
    - "Dead" but not "reaped"
  - Parent process con reap children by waiting for them to terminate
    - OS provides system call for this -> wait

---
### Process switching/context switching
- Example scenarios that may trigger process switch
  - Processtermination(voluntary/involuntary)
  - New process activation
  - Executingprocessgetsblocked (e.g., due to system call)
  - Eventcompletion
  - Time slice expiration
- Process switching mechanism needs hardware & OSsupport
  - Requires transition to kernel mode -> uses interrupt
  - Overhead to switch depends on hardware support

---
### Limited Direct Execution (LDE) Protocol
- "Direct Execution" - run programs directly on CPU
- Two issues
  - If we just run a program, how can OS make sure the program doesn't do anything that we don't want it to do, while still running it efficiently?
  - When we are running a process, how does OS stop it from running and switch to another process(i.e., how does OS implement time sharing)?
- Without limits on running programs, the OS would not be in control of anything

---
### Context Switch and Mode Switch

- An interrupt, exception or syscall results in a mode switch
- Context switch: An operating system may choose to save a process' state and restore another process' state -> preemption
- Context switch
  - Switch to kernel mode
  - Save hardware execution state so that it can be restored later
  - Load another processes's hardware execution state
  - Return (to the restored process)
