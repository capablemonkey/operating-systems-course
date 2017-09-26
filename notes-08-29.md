## Interrupt

Interrupt: when input happens, I/O device notifies OS using a signal.  OS interrupts execution of program and sends signal to it.  All programs are interrupted.

There is a hierarchy which handles interrupt signals.

## OS functions:

1. Executing programs
2. managing CPU
3. managing RAM
4. managing I/O devices
5. managing storage
6. networking
7. user interface
8. security
9. IPC

### virtual memory

When RAM runs out of space, program memory is moved to virtual memory on HDD in order to make space for other programs.  OS can profile programs to try to load most used parts of a program to memory, instead of the whole program.  OS tries very hard to avoid virtual memory usage since it's slow.

### drivers

Drivers are an interface for the OS to control a I/O device.

### file system

OS maintains a mapping of file name to location on disk