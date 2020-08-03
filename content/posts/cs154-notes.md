---
date: "2020-06-07"
tags:
- uchicago
- notes
title: CS 154 Notes
---

These are notes for CS 154, taught by Yanjing Li, Junchen Jiang, and Haryadi Gunawi. The code for the class can be found [here](https://github.com/deblnia/CS154).

## Lecture 21: Synchronization 

- Each thread’s program counter points to a different address in the same code segment 
- All threads share data and heap 
  - Data = all static and global variables 
  - Heap = malloc’d and dynamically allocated data 
- Pass by Reference into Main Stack dangerous => can lead to read / write conflict 
- Think about _shared variables_ and _atomicity_ in concurrency 
  - Which variables are shared? **Follow the pointers.** If multiple threads reference it, must be shared! 
  - Atomic means run to completion or not at all – cannot be interrupted in the middle 
    - `i++` is not atomic – can be interrupted 
- To guarantee automaticity: 
  - Use locks – mutual exclude threads 
    - `init()`, `acquire()`, `unlock()` 
- Synchronization kills (underutilizes) parallelism
  - Exploit parallelism by creating embarassingly parallel subtasks (tasks independent to each other that do not synchronize too often) 

## Lecture 20: Concurrent Programming 

- Without `fork()` in server, can only serve on request at a time 
- With `fork()` **concurrent**: make child processes to accept new connections and serve prior clients 
- Two main functions: `listenfd()` and `connfd()` 
  - `listenfd()` handles connection requests 
  - `connfd()` handles child process / data transfer 
- **Parent needs to close `connfd()`** – otherwise memory leak 
  - Correct –> parent only points to `listenfd()` and child points to own `connfd()` 
- Threads are another way to create concurrency (as opposed to new processes as in above)
  - I/O multiplexing in the book – also a way of implementing concurrency 
  - Processes can only talk through IPC (complicated)
- Threads allow easy sharing of heap and global variables and file descriptor tables 
  - Thread has it’s own stack and program counter 
  - A thread belong to a process  (live in process address space)
- Interface with threads through `Pthreads` 
- Three ways to pass arguments between to thread from process: 
  - Pass by reference to main stack
    -  `pthread_create(...,&connfd);`
  - Pass by reference to heap (must `free()` later)
    - Malloc space, accept and then just pass 
  - Pass by Value
    - Just pass 
- Race condition is when outcome depends on arbitrary scheduling decisions elsewhere in the system 

## Lecture # 19: Dynamic Memory Allocation 

- Manage free blocks through implicit list (linking all blocks) or explicit list (linking free blocks using pointers)
- 
