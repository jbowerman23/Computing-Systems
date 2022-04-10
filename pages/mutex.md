# Mutex Variables
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/g/personal/bowermanjess_seattleu_edu/EbkUmz959UNLqvqoHW_q1_8Bnor80yM2_Am2GHAxlwEpXQ?e=lRsTA6)
---

## Solution to Busy Waiting

- Thread/process can be blocked
- Wake up sleeping signal once it is eligible to enter crtical section

---

- Share variable mutex that can be in one of two states
- Locked or 1
- Unlocked or 0
- Can be used to implement software lock without busy waiting!

```c++
mutex_lock:
  TSL REGISTER, MUTEX
  CMP REGISTER,#0
  JZE ok
  CALL thread_yield
  JMP mutex_lock
 Ok:
  RET
  
mutex_unlock:
  MOVE MUTEX,#0
  RET
```
- Similar to entry and leave region software
## No busy waiting

---
## Pthread mutex

![Computing Systems!](https://github.com/jbowerman23/Computing-Systems/blob/55ca57d0ef7fc2e92f90f3c7730b03210f91a263/images/mutex_1.png)
![Computing Systems!](https://github.com/jbowerman23/Computing-Systems/blob/55ca57d0ef7fc2e92f90f3c7730b03210f91a263/images/mutex_2.png)

---
## Header Section

```c++
#include <pthread.h>
#include <iostream>
using namespace std;
int account balance;
pthread mutex_t mutex = PTHREAD MUTEX INITIALIZER;

void* deposit(void* arg){
  int amount = *((int*(arg);
  cout << "Depositing $" << amount << endl;
  pthread_mutex_lock(&mutex);
  account_balance += amount;
  pthread_mutex_unlock(&mutex);
  
  pthread_exit(NULL);
}

void* withdraw(void* arg){
  int amount = *((int*(arg);
  cout << "Withdrawing $" << amount << endl;
  pthread_mutex_lock(&mutex);
  account_balance -= amount;
  pthread_mutex_unlock(&mutex);
  
  pthread_exit(NULL);
}

int main(){
  pthread_t id1, id2;
  int d, w;
  int* pa;
  account_balance = 100;
  
  cout < "Initial balance: $" << account_balance;
  d = 50;
  pa = &d;
  pthread_create(&id1, NULL, deposit, (void*)pa);
  
  w = 60;
  pa=&w;
  pthread_create(&id2, NULL, withdraw, (void*)pa);
  
  pthread_join(id1, NULL);
  pthread_join(id2, NULL);
  
  cout << "Final balance: $" << account_balance;
  pthread_exit(NULL);
}
```




