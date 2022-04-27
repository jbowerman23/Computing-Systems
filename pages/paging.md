# Paging
---
## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B6FF6EA02-1447-44A3-A455-A1DAAE980872%7D&file=5-%20paging.pptx&action=edit&mobileredirect=true)
---

# Memory Management - Paging
---

## External fragmentation
- Reduces memory utilization
  - Even if enough free memory exists to allocate new process...
  - ... not useful since memory is not contiguous

- Possible approaches
  - Reduce external fragmentation using compaction
  - Find way to allow non-continguous partitions
    - Split process footprint into multiple parts

---

## Compaction
- Move partitions to together to create a new parition
  - Free space is collected in a large memory chunk to make some space available for processes.
- Need partition relocation

- This allows for non-contiguous allocation

- We now need a more sophisticated memory management mechanism
- Maintain information for multiple parts of process

---

## Paging
- Divide physical memory into equal-sized blocks: page frames
- Divide logical memory into same sized blocks: pages
- Process pages mapped to physical page frames
- Page frame sizes are powers of 2
  - 4096 bytes (2^12), 8192 bytes (2^13)

- Mapping of process pages could end up being contiguous
  - BUT dont need to be
- Depends on: 
  - State of memory when process is allocated
  - Policy used for allocation

- OS maintains page to page frame mappings -> page tables (one per process)
- OS keeps track of free page frames -> linked list
- To allocate process that needs n pages

1. Find n free page frames
2. Allocate process pages to frames

- Internal fragmentation possible due to fixed-sized frames
- Manageable by carefully choosing size of page/page frame

- Part of OS that takes care of mapping, address translation etc -> memory management unit

- Page table itself stored in main memory
  - Expensive to access it for each memory request
- Solutions -> cache subset of page table entries
- Translation look-aside buffer (TLB)
  - Small set of associative registers
  - Provides fast access

---

## Address translation in paged systems
- Logical address includes two parts
  1. Page numeber (pn)
  2. Offset within page (off)
- Physical address includes corresponding parts
  1. Page frame number (fn)
  2. Offset within frame (off)

---

## In a computer
- Addresses represented in binary
  - Main memory and page frame sizes are powers of 2
  - Hexadecimal -> more compacts

- 2 bits: 4 (2^2) combinations
- 3 bits: 8 (2^3) combinations
- n bits: 2^n combinations

---

## Memory System
- 32KB (2^15) main memory
  - 15 bit physical address
- 16KB (2^14) logical address space
  - 14 bit logical address
- 4KB (2^12) page frame/page
  - 12 bit offset (LSB)
  - 2^15 / 2^12 = 2^3 page frames
    - 3 bit page frame number
  - 2^14 / 2^12 = 2^2 pages
    - 2 bit logical page number

### Page table entry structure
- Structure is dependent on system

---

## One restrictive assumption
- All process pages must be in main memory to execute process
  - Limits num processes in main memory and process data size
- Observation
  - Process does not use all its data all the time
- Better option
  - Keep only subset of process pages in main memory
  - Bring others as needed
  - This is called __demand paging__

---

## Demand paging
- When process requests for data
  - Check if page with data already in main memory
  - If yes proceed as usual
  - If not, page fault is set to occur

- When page fault occurs  
  - Load missing page into main memory
    - May add <font color='red'>TLB</font> entry for new page
  - Restart instruction that caused page fault

### Consequence of demand paging
- Process data not limited to physical main memory size
  - Size of process virtually unlimited

- Virtual memory
  - Did not support this in our earlier examples

- Allow more logical pages in process than physical page frames
- Logical page # can be longer than physical page frame #
- Logical (virtual) address can be longer than physical address

---

## Memory system (Virtual Memory)
- - 32KB (2^15) main memory
  - 15 bit physical address
- 64KB (2^16) logical address space
  - 16 bit logical address
- 4KB (2^12) page frame/page
  - 12 bit offset (LSB)
  - 2^15 / 2^12 = 2^3 page frames
    - 3 bit page frame number
  - 2^16 / 2^12 = 2^4 pages
    - 4 bit logical page number

---
