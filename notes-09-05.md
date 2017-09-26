## Process states

```
new
ready
running
waiting
terminated
```

When a process is first created, it is in the `new` state.  The OS will start allocating memory, loading instructions, data, etc.

When the process is ready to use the CPU, it is put on to the *ready queue* and then is in the `ready` state.

When the process is finished running, it goes into the `terminated` state.  The OS will free the resources (memory, etc.) belonging to that process.

OS may force a process to give up the CPU, this is called pre-emption.

Processes waiting to use an I/O device are placed on an I/O queue.  Each I/O device has its own queue.

If a process is waiting (sleep) or waiting on an I/O queue, it is kicked out of the CPU and placed into the "waiting" state.  After it's done waiting, it'll be put back on the ready queue.

```

new --> ready queue -> CPU --> terminated
    | <- preemption <---|
    | <- I/O queue  <---|
    | <- waiting    <---|
```

## Process control block

Every process has a process control block.  It represents information about the process.

PCB usually contains:

- Process ID (pid)
- Process state
- program counter, CPU registers
- CPU related information (includes priority, total time spent using CPU)
- Memory information (what areas of memory were allocated)
- I/O status info: list of I/O devices allocated to process, files opened
- list of interrupts waiting for
- threads

## Context switching

P1, P2, OS running.  Assume P1 is currently running.  To switch to P2, this is the procedure:

1. Pause P1
2. Store register contents (known as context) in P1's PCB
3. Load P2's register contents from P2's PCB
4. Restart P2

Store and load of CPU registers is supported at the hardware level to reduce overhead.

OS want to reduce context switches as much as possible, since they are expensive.