## Multithreading models

There are 3 main models for how operating systems map user threads to kernel threads.

- Many-to-one: multiple user threads map to one kernel thread.  Obselete approach since it doesn't allow you to use multiple cores.
- One-to-one: separate kernel thread to handle each and every user thread.  Limit on how many threads can be created.
- Many-to-many: multiplexes user threads among a pool of kernel threads.  Will allow more user threads than one-to-one

## Thread local storage

Global variables specific to each thread.  Also called TLS.

## Thread pools

Creating threads is relatively expensive, and having unlimited threads can exhaust system resources.

If you are say building a multithreaded web server, you can create a fixed number of threads at process startup and place them into a pool where they sit and wait for work.  When a request is received, it awakens a thread from the pool (if there is one available) and tells it to serve the request.  If no thread is available, queue it until one becomes free.

## Interprocess communication

Two approaches: shared memory and message passing.

Shared memory:
- region of a process's memory can be accessed by other processes
- system call to create region and have another process attach it, regular access after that
- insecure... harder to program correctly (process synchronization)

Message passing:
- slower than shared memory. requires system calls to send message
- secure
- blocking send: send message and wait for receiver to receive it
- non-blocking send: send message and resume immediately
- blocking receive: stop and wait until a message is received
- non-blocking receive: get a message from queue or null, right now

## Sockets

Socket is an IP address and port number.

OS receives network message, and uses the port number to determine which process to deliver the message to.

Well known ports:

- HTTP: 80