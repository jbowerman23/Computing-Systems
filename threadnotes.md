# Threads
---

## POSIX Thread Library

- Once return zero is reach thread/process is terminated

```c++
int main() {
  cout << "Hello World" << endl;
}
```
---

```c++
int main() {
  printHelloWorld();
  
  //other ops
  return 0;
}
```
---

- Once function ends, thread is termintated

```c++
int main() {
  //op
  //start thread 1
  //op
}
```

```c++
//thread 1
{ //op
  //start thread 2
  //op
  //op
  //op
}
```

```c++
//thread 2
{ //op
  //op
}
```

---
## Important Notes

- Include file pthread.h
- Linker flag: -lpthread
  - If program file is test_pthread.cpp different command

---
## Need to...

- Set up sequence of instructions
  - Create function with desired sequence of intructs
- Create new thread to execute sequence of intructs


---
## Thread Creation

```c++
int pthread_create(pthread_t *id, 
                    const pthread_attr_t *attr, 
                    void *(*start_func)(void *), 
                    void *arg);
```

---
## Only termintate calling thread

```c++
void pthread_exit(void * retval)
```

---
## Parameters and Return Values

#### Any parameter to be passed must be converted to void*

```c++
int arg;
void* to_pass = (void*)&arg;
```

#### Return vals must also be converted

```c++
char retval;
void* to_return = (void*)retval;
```

#### More than 1 param to pass

```c++
struct my_args{
  int arg_1;
  char arg_2;
}
```

```c++
my_args a;
a.arg_1 = 10;
a.arg_2 = 'Y';
void* to_pass = (void*)&a;
```


