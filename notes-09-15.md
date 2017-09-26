## Threads

For parallel programs, using multiple threads is better than multiple processes:

- More memory efficient
- Easy communication (global variables accessible to all threads)
- Fast to create a new thread
- Faster context switch

Cons:

- Threads can't use exec()
- When a thread crashes (hits an exception), the whole process is killed.  Whereas a process is independent from its parent, and will not cause its to be killed.

## Kernel threads vs. User threads

Thread management operations:
- create thread
- stop thread
- pause thread

You can manage threads without kernel-mode instructions.  These are called user-level threads:

- user threads are fast (no system call needed)
- can only use one core, since all user threads are treated as a single kernel thread and are thus scheduled to one core
- one user thread blocks all other user threads

Kernel-level threads are managed by the OS.

- slower (because you need system calls to create and manage them)
- kernel threads can be allocated to multiple cores
- one kernel thread does not block other threads

