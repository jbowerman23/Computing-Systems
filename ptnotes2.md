# Process Control Boards and Process Creation and Termination
---

# Process Review
---

## Manage multiple processes
- information about each process must be maintained
  - Process control block used for this
    - Process ID
    - Process State
    - Program Counter - address of next instruction to be executed
    - Registers - general purpose registers, stack pointers, etc
    - Scheduling information
    - Memory management information
    - Accounting information - time limits, etc 

## Unix process creation (fork)
- Process invokes fork to initiate creation of new process
- Creating process is parent and new process is child
- System call creates new process
- Data from parent copied to child
  - Memory image, environment settings I/O handles, etc
  - Of course child get its own ID, scheduling info etc


## Fork()
- fork call returns a value
  - Upon success, fork returns child ID to parent
  - ... returns 0 to child

- Parent/chihld process independently continue exeuction from statement after fork

If process spwan fails, fork returns -1 to parent & no child is created

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

## EXEC System call
- Child can change the program it executes
- Invove exec family of system calls to change its memory image
- Stops executing code in parent program & starts new program

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

## CLion Example - Processes.cpp

```c++
#include <iostream>
#include <unistd.h>

void fork_example();

int main() {
    pid_t id = fork();
    if(id == -1) {
        std::cout << "Error creating process\n";
    }
    else if (id == 0) {
        // child process functionality
        char* args[] = {(char *) "echo", (char *) "Hello,", (char *) " World!", NULL};
        execvp(args[0], args);
    }
    else {
        std::cout << "I just became a parent!\n";
        int status;
        waitpid(id, &status, 0);
    }

    //fork_example();
    return 0;
}

void fork_example() {

    //fork() returns 0 to the child and the child's ID to the parent
    //Recap truthy and falsey
    if (fork ()) {
        fork ();
    } else {
        std::cout << "Hello";
    }
}

```
