# Communication between Processes

## What is it

- `Processes in computer work solely or work together by sending and receiving data`
    - This is called `IPC`, inter-process communication
- Does IPC happen in computer?
    - No, it can also be from computer to computer via network

## IPC can be done with or without OS

1. within a process
    - `threads` communicate via shared data(global variable, file)
    - No need OS
2. within a PC
    - `Processes communicate via shared file or Pipe that OS provides`
3. Via network
    - Send and receive data via socket
    - Networking?
        - communication via socket
        - RPC is a one example

## How IPC works?

- Simple: `send & receive data`
- However, complicate in detail
    - How to make sure data has sent and received?

## IPC classification by

### direction

- Simplex
    - one-way(Unidirectional)
    - Data can be sent one-way
    - Global variable, pipe
- Duplex
    - Bidirectional
    - Most common one
    - Each process can send data
    - Example: Socket
- Half-duplex
    - `Each process can send data, but not at the same time`
    - only one-way in certain time
    - walkie-talkie

### by synchronization

- busy waiting
    - wait by executing infinite loop to check the changes of states
    - example of busy waiting
        - in simplex IPC, many threads can have access to global variable
        - assume one thread changes global variable
        - Do other thread knows about this? `NO`
        - `for that, thread has to check frequently`
    - `an example of wasting resource`

- To solve busy waiting, OS use `synchronization`
    - just like notification when you receive a message
- With synchronization, process doesn't have to check frequently because OS notifies automatically

|Classification|Example|
|--------------|-------|
|IPC with Sync |Pipe, Socket|
|IPC w/o Synchronization|Global variable, file|

# Shared Resources & Critical Section

# Critical Section Resolution

# File. Pipe and Socket Programming
