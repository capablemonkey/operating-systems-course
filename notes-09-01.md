## Processes

A program is a static list of commands.

A process is a program in execution. It's a *dynamic* entity, consisting of:
- the list of instructions
- the data associated with it
- the memory allocated for the process
- the list of files open for the process

## Dual Mode

CPU instruction set is split into 2 categories: *user mode* (safe) and *kernel mode* (unsafe) instructions.  This prevents malware from wrecking havoc on the system.

User mode instructions:

- artithmetic
- control flow: jump, branch
- load, store

Kernel mode instructions:
- I/O operations
- execution
- file and disk storage (write file, read file)

Each time a user program wants to run a kernel mode instruction, it must ask the operating system to execution the instruction for it via a *system call*.  OS has the sole right to run kernel mode instructions.

When a system call is made by a user process, CPU will pause execution of process and switch to the OS to handle the system call.  After that, it will switch back to the process.  This context switch is not free, there is overhead for the CPU to switch execution.

Dual mode is enforced by by a register which keeps track of whether it's in user mode or kernel mode.  The instruction to switch from user to kernel mode is a kernel mode instruction itself... This can happen when a user process is finished.

When an interrupt is received, the exeuction mode will switch to kernel (hardware mechanism), and the CPU will run the OS.  Interrupts can also happen on a timer.

## API

System calls are very low level and tedious to use.  The OS exposes an API to make programming easier.

- Windows API
- POSIX API for linux

## Kernel

The kernel is the core of the operating system.  It always remains in memory.  Kernels can load modules.

## Approaches to OS development

Two extremes described below, but modern OS architecures use a mix of both.

#### Monolithic kernel

Very large kernel which handles most of OS functions.  Tends to be fast, because lower communication between sub-components.  Harder to extend, debug.

#### Micro kernel

Small kernel which works with smaller, specific modules.  Easier to update, since you can update modules without updating the whole kernel.  Slower because more inter-module communication.  Example of module: CPU scheduler

#### Exokernel

Gives application total control over hardware.  Fastest.