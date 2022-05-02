# File Management
---
## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7BD6C155A1-627D-48ED-ACF3-9918DE460520%7D&file=6%20-%20Week%20-%206%20-%20Monday%20-%20File%20management%20-%20Modified.pptx&action=edit&mobileredirect=true)
---

## Understanding File Management System in Operating Systems
- File management is one of the basic and important features of operating systems
- A file is a collection of specific information stored in the memory of a computer system
  - Non-volatile, long-term storage (e.g disk)
    - Must store very large amount of information
    - Must persist beyond process lifetime
    - Must be accessible by multiple processes at once
- File management is defined as the process of manipulating files in a computer system
  - Management includes the process of creating, modifying and deleting file

---

## Tasks Performed by File Management
1. Help create new files in a computer system and place them at a specific location
2. Provide quick look up time for locating files in a computer system
3. Provides mechanisms for sharing files among multiple users (privileges)
4. Maintains a hierarchical structure that consists of root directory and it's subdirectories in which files are stored

---

## OS Provides the Following Functions
- **File Attributes**
  - File type, date of last modification, size, location on disk etc.
  - Helps the user to understand the value and location of files
- **File operations**
  - Specifies the task that can be performed on a file such as opening and closing of a file
- **File access permissions**
  - Read, write, execute for group, owner and other
- **File systems**
  - Specifies the logical method of file storage in a computer system such as File allocation table (FAT)

---

## Data Organization on Disks
- All data organized into equal-sized blocks on disk
- Disk supports two main operations
  - Read block
  - Write block
- Addressing disk blocks directly -> too complex for users

- OS provides simpler abstraction for persistent data
- This abstraction is called <font color="#A72608">file system</font>
  - <font color="#A72608">Files:</font> names collections of related data in file system
  - File split into blocks as well
  - Logical blocks mapped to physical blocks

---

## File Allocation - Contiguous
- File blocks stored contiguously

- **Pros**
  - Simple
  - Read is very fast
- **Cons**
  - Results in external fragmentation
    - Compaction or de-fragmentation very expensive
  - Max file size must be known

---

## File Allocation - Linked List
- File blocks form linked list
- Info about next block stored within disk block itself

- **Pros**
  - No external fragmentation
  - File size can dynamically change
- **Cons**
  - Could have internal fragmentation in last block
  - Entire disk block not used for file content
  - To locate random block in file, several disk accesses needed

- Linked list information stored as <font color="#A72608">**table**</font> in main memory
  - File allocation table (FAT)
  - Disk blocks entirely used for file content
  - External pointers to first and possibly last blocks
  - Each block points to next block (or special EOF value)

- **Pros**
  - To locate random block within file, only memory accesses needed
- **Cons**
  - Entire table must be in main memory

---

## File Allocation - I-Node
- Attributes and disk block addresses of file stored in data structure called i-node
- When file opened its i-node brought into main memory
  - Only i-nodes of open files kept in main memory
