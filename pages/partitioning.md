# Partitioning
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B19828F00-ECE4-40E2-A873-302DEA6D0DFA%7D&file=5-CPSC-3500-Computing-Systems-Memory-Management.pptx&action=edit&mobileredirect=true)
---

# Memory Management - Partitioning
---

## Context
- Processes needs resources for execution
  - CPU cycles, I/O devices, etc
  - Memory resources to store
    - Program code ("text")
    - Data
    - OS structures for process

All process memory recourses = process data

- For process to execute, its data must be in main memory
  - Main memory is volatile
  - Process data stored in non-volatile memory (disk)
  - Process data must be loaded into main memory from disk

---

## Simple Scenario
- Allow only one process to be active at a time
  - Load process data from disk to main memory
  - Once process is done, store its contents to disk
- In reality a process
  - May wait for I/O -> poor CPU utilization
  - May not use all memory -> poor memory utilization


## More Realistic Scenario
- Just like CPU multiplexed among multiple processes
  - ... memory must be multiplexed among multiple processes
- What we need
  - Multiple processes should reside in memory at a time
  - Processes should not collide in memory
  - Processes should not access other process' memory (protection)
  - Processes should be able to share memory if desired
#### We need memory protection and controlled overlap

---

## Memory Partitioning
- Divide memory into multiple paritions
- Allocate processes to partitions
- Ensure protection across partitions

### Questions
- How should memory be divided into partitions?
- Which process should be allocated to which partition?
- Should partitions be allowed to change dynamically?

---

## Static, Equal-Sized Partitions
- Statically divide main memory into equal-sized partitions
- Map each process to one partition
  - May be gaps within each partition -> Internal fragmentation

- If there are more processes than partitions
  - Map multiple processes to same partition
  - Store existing process data to disk & de-allocate its partition
  - Allocate new process to partition & load its data from disk
#### This is called swapping

#### Pros
- Ver simple

### Cons
- Results in interal fragmentation
  - Under-utilization of memory
- Cannot fit process larger than partition size
- Takes a one-size-fits-all kind of approach

---

## Static, Unequal-Sized Partitions
- Statically create partitions of different sizes
- Map each process to a partition that's large enough for it
  - Less internal fragmentation
  - Swapping is still allowed

### Pros
- Supports process of different sizes better
- Less internal fragmentation

### Cons
- Slightly more complex than equal-sized partitions
  - Needs policy for mapping processes to partitions (partition placement)
  - Needs slightly enchanced protection mechanism
- Needs partition to be created statically
  - Chosen sizes may not suit processes that may need to be supported
- Still can't support processes larger than largest partition

---

## Protection
### Ensure
- Ensure process only access location sin its partition
### Store
- Store or base address (BA) for each process
### Check
- Check every address issued by process
  - Must lie between BA & (BA + parition size)

---

## Dynamic, Variable-Sized Partitions
- Start with un-partitioned memory ("free space")
- Create partitions dynamically based on process data size
  - Nymber of partitions changes dynamically
  - Lengths of partitions may be different

- Place initial partitions contiguously in main memory
- As processes get swapped in and out of main memory
  - Memory ends up with "free space"/"holes" between partitions -> external fragmentation

### Consequences
- Need mechanism to keep track of free spaces
- Need policy for partition placement

- Possible mechanism to keep track of free spaces
  - Maintain linked list of free spaces
  - Each list element stores base address and size of free space

### Pros:
- More flexible than static partitioning

### Cons:
- Management more complex than static
- Has external fragmentation (extent varies with policy)

---

## Policies for partition placement
### First Fit (FF)
- Scan list, choose first free space large enough for parition
- Pros: simple; fast
- Cons: partitions may crowd initial regions of main memory

### Next Fit (NF)
- Like FF; however scanning starts where previous scan ended
- Pros: more distributed allocation

### Best Fit (BF)
- Scan entire list; choose smallest free space large enough
- Cons: slow; leaves many small unusable free spaces

### Worst Fit (WF)
- Scan entire list; choose largest free space that fits process
- Pros: Leaves larger free spaces
- Cons: Slow

---

## In practice
- Program uses offsets relative to start address of 0
  - Program uses logical address
  - Range of logical address for process: Logical address space
- System translates relative offset into absolute address
  - System generates physical address
  - Range of absolute address of process: Physical address space
- Translation mechanism
  - Maintain base address & limit for process partition
  - Add base address to logical address issued by program
  - Check whether result is within limit

### Consequence of Relative Addressing
- Process need not be mapped to same physical partition all the time
- Partition relocation is possible
- Very useful, especially when using dynamic partitioning

