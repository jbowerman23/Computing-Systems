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
