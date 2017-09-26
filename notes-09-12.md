# Forking exercises

## Exercise 1

```
pid_t x;
x = fork();
printf("*");
fork();
printf("?");
```

Produces this process tree:

```
parent *?
|-child *?
 |-child ?
|-child ?
```

Possible outputs:

```
**????
*?*???
*??*??
```

*???*? is impossible

## Exercise 2

```
pid_t x;
printf("one\n");
x = fork();
if (x==0) {
  fork();
  printf("two\n");
}

printf("three\n");
```

```
parent (one, three)
|-child (two, three)
 |- child (two, three)

```

```
one
two
two
three
three
three
```

```
one
three
two
two
three
three
```

```
one
three
two
three
two
three
```

## Process tree

There is an `init` process which spawns all other processes.

## Exit

A process can exit by calling "exit(status_code);".  This will tell the OS to kill the process and free its resources.

It returns a status code which indicates whether it was successful (0 = success, 1 = error, ... 255).

Parent can listen for the status code for a child's exit by calling `wait();`.

When a child process exits, it goes into the TERMINATED state and its PCB is kept around.  It is now known as a zombie process.  When the parent at some point later calls wait();, the OS will return the child's PCB and the zombie process is destroyed.

When a parent exits while there is still a running child (and the parent did not call wait()), the child process is called an orphan.

OS doesn't like orphans.  It has a reaper process which terminates orphans.

Cascading termination: when a parent process is terminated, its descendents are also terminated.

## Threads

Threads allow you to run your code in parallel, at different points of your program.  Threads are way faster than processes, faster to create, use less memory.  OS can distribute threads across multiple cores.