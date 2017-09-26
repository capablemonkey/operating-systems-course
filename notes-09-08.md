## Memory space for process

```
 ______________
|  stack       |
|     |        |
|     v        |
|______________|
|              |
|              |
|______________|
|              |
|   ^          |
|   |          |
|  heap        |
|______________|
|              |
| data         |
|______________|
|              |
| code         |
|(instructions)|
|______________|
```

Stack: static memory allocation

Heap: dynamic memory allocation (malloc)

## Process creation

`fork()` creates a new process.  It returns the pid of the newly created child process to the parent, while the child gets 0.  The child is a copy of the parent.  After the fork, the parent will keep running after the fork command, and the child will also resume execution from the forking point.

Forking in C:

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

int main() {
  pid_t pid;
  pid = fork();

  if (pid == 0) {
    printf("I'm a child!\n");
  } else {
    printf("I'm a parent!\n");
  }
}

```

`exec()` takes a path to an executable file.  Replaces the current process in memory with the given executable.  Typically used with fork.

`spawn()` forks a new child process and calls exec() in it.