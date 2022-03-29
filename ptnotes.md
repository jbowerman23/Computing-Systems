# Processes and Threads
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
      <li>Invoke exec family of system call to change its memory image/li>
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
