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

- Synchronization in real world
    - Bell from kitchen to notify the food is ready

### How synchronization works from examples

- global variable
    - Has a problem with synchronization
    - Use busy waiting

- With file
    - file I/O = Open + Write + Close
        - `Like a key to hotel room`
            - a key to open the hotel room (open)
            - Use hotel room (write)
            - return a key when you check out (close)
    - file description = key
    - Do not provide synchronization
        - use wait()

- With pipe
    - a synchronization that OS provides
    - One-way using global variable
        - 2 pipes in case of duplex
    - while process A tries to read a global variable
        - if a process B has not finished writing to a global variable, request to read goes to wait
        - when writing is done, then synchronization starts and process A can read global variable
    - Anonymous(between related processes), named pipe(between unrelated processes)

- With Socket
    - To communicate with other PC, one has to know
        - Address(IP), port(Process)
    - `During connection, One tries to connect its socket with another PC's socket in parallel`
        - `this is binding`

# Shared Resources & Critical Section

- Shared resources
    - Resources that many processes can access
        - variables, memory, files ...
    - without order, it can be chaotic
        - who access first can result in undesirable result
    - Race condition
        - `more than two process tries to read and write shared resources `
        - When it happens, result can be the one that we do not expect
- Critical section
    - `ONE PROCESS AT A TIME!`
    - Program section that can have different result depending on access order to shared resources
    - This also means that this should not be shared
    - `one has to wait while other in critical section`

    - Producer-Consumer Problem
        - Problem related to critical section for a long time
          `quiz: What is producer-consumer problem?`

    - Critical section also applies to hardware
        - printer

- Conditions for solution of critical section
    - Solution must satisfy the following conditions no matter what 
    1. mutual exclusion
        - `One process at a time in critical section`
    2. bounded waiting
        - no infinite waiting for process
    3. progress flexibility
        - one process cannot interrupt or disturb other's progress
        - one can enter critical section when it's empty without other's progress

**Be able to describe Shared Resources, Race Condition, Critical Section and Producer-consumer problem**

# Critical Section Resolution

1. The simplest way
    -  just lock it
        ```kotlin
        fun doSomething() {
            while(!lock) {
                lock = true
                    ... //critical section
                lock = false
            }
        }
        ``` 
        - This can cause a problem when it comes to CPU timeout between `while and lock =true`
            - `could result in violation of mutual exclusion`
            - busy waiting as well
        
        - Deadlock
            - when it can guarantee bounded waiting
            - wait infinitely while processes are alive
            
        - Lockstep synchronization
            - progress of one disturbs progress of others

2. Solution from hardware
- test-and-set
```
while(testandset())
```
- easy, but still busy waiting

3. Peterson algorithm, Dekker algorithm
- complicated, not used these days

4. Semaphore
- an algorithm that solves critical section issues(producer-consumer problem)
- How semaphore works
    1. turn the switch on before entering into critical section
    2. upcoming process(A) waits until critical section is free
    3. when a process(B) finishes, semaphore signals next process(sync signal) to use critical section
- code snippet
    ```kotlin
        semephore(n)
        p()
            ... critical section ...
        V()
    ```
    - semaphore(n) : init global variable RS with n(number of shared resources)
        - RS contains number of available resources
    - P(): lock and enters critical section
        - RS > 0, decrease by 1
        - RS <=0, wait until it's bigger than 1
    - V(): unlock and synchronize
        - increase RS by 1, send signal(wake_up signal) to waiting process to enter critical section

- Waiting process is stored in semaphore queue
    - when received wake_up signal, get out of queue and enters critical section
    - No busy waiting
- P() and V() both use test-and-set to prevent other code to run
    


6. Monitor
    

# File. Pipe and Socket Programming
