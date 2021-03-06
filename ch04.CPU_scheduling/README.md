# CPU Scheduling

1. [Intro and Recap](#Intro-and-Recap)
2. [CPU scheduling consideration](#CPU-scheduling-consideration)
3. [Multiple queue](#Multiple-queue)
4. [Scheduling algorithm](#Scheduling-algorithm)
5. [Interrupt handling](#Interrupt-handling)

# Intro and Recap

1. Recap
    ```
    Q: So what is a process lifecycle?
    A: Process lifecycle is how process goes through stages from creation to termination.
       it consists of create, ready, running, blocking, and terminate status
   ``` 

2. What is CPU scheduler?
    - `Part of OS that controls CPU allocation based on context(i.e., status of other processes, allocattion of CPU and resources)`

3. In real life, what is equivalent to CPU Scheduling?
    - Restaurant manager
        - manages reservations, change cooking order, respond to customer

4. Levels of scheduling
    - High level
        - job scheduling, or admission scheduling
        - `High level scheduling determines total number of works`
        - if there are too many jobs running, system overloaded!
            - Like restaurant accepting too many customers despite ths number of seats
        - `When job requests come, scheduler decide whether to accept or decline, based on context`
    - Mid level
        - Between high and low level
        - `Act as a buffer`
        - `Even though high level system controls total number of process, sometimes it does not work idealy`
        - `By limiting the number of active process, this prevents system overloads`
            - Using suspend and active
    - Low level
        - short-term scheduling
        - `Determines which process needs to take CPU, and which to set as blocking status and as such`
            - This means, `Dealing with process status`
    - ![process scheduling by level](./res/process-scheduling-by-level.png)

5. Purpose of scheduling
    - Fairness
        - Every process will be equally allocated
    - Efficiency
        - No down-time
    - Stability
        - allocate resource based on priority, protect system from malfunctioning process
    - Scalability
        - Scalable when number of process increases
    - Response time
        - Respond within designated time
    - Prevent infinite postpone

# CPU scheduling consideration

`How CPU scheduler allocate CPU resources to process primarily?`

### Preemptive vs non-preemptive

1. Preemptive scheduling
    - `OS can take CPU from a running process if it has to`
        - How? `through intterrupt`
    - Can be wasteful in context switch and other additional work perspective
    - `However, since one process can take CPU forever, preemptive suits for time-sharing system`
2. Non-preemptive scheduling
    - `No one can take CPU from running process unless it terminates or blocks itself`
    - Can be efficient since less context switching or other additional work
    - `However, not efficient since other process has to wait`

### Process Priority

- Every process has its own priority
    - it's like normal customers vs customers with reservation
- Higher priority = frequent occupation of CPU
    - `Kernel process has higher priority than normal process`
- `Priority is present in PCB`

### Which process has higher priority, CPU bound vs I/O bound process?

- Process goes to various stages(creation, ready, running, blocking, termination)
- running status: a process actually taking CPU and execute computation -> CPU bound
- blocking status: request I/O and wait for its completion -> I/O bound

```
If CPU bound has higher priority, it is going to take CPU more frequently.
thus, I/O bound process has higher priority
```

### Which process has higher priority, foreground vs background process?

- foreground process
    - a process that user actively interacts with
    - has I/O operation
- background process
    - a process that user does not actively interact with
    - downloading, zipping file
- `Foreground process has higher priority than background process`

# Multiple queue

### Multiple queue in ready status

- `What if number of process are wait for allocation of CPU without order?`
    - CPU has to walk through every process to allocate CPU based on priority

- `It would be easier for scheduler allocate CPU if processes are sorted by priority `
    - `Yes, have multiple queue based on priority!!`
    - **# of queue, allocating CPU depend on scheduling algorithm**

- How is priority of a process set?
    - static priority
        - Does not change once set
        - Hard to keep up with change
    - dynamic priority
        - Dynamically change its priority
        - Easy to keep up with change, but hard to implement
        - priority inversion

### Multiple queue in blocking status

- `Multiple queue based on same I/O work`
    - Queue based on HDD, LAN, CD-ROM

### Multiple queue from ready status vs blocking status

- In ready status, `allocate CPU to process one by one`
- In blocking status, `Take multiple PCB and move to ready status, if multiple I/O work finish`

![multiple-queue-through-process-lifecycle](./res/mutiple-queue-through-process-lifecycle.jpg)

# Scheduling algorithm

- preemptive and non-preemptive
- preemptive algorithm is mostly used
    - Again, it is best for time-sharing system

## How to measure efficiency of scheduling algorithm?

1. CPU utilization
    - `time CPU used / total time`
    - The higher number is, the more efficient
    - hard to measure
2. Throughput
    - `number of processes that finish tasks per unit time / total time`
    - The higher number is, the more efficient
    - hard to measure
3. Waiting time
    - time it takes between request and actual execution
    - shorter the better
4. Response time
    - How fast it respond to client request
5. Turnaround time
    - time between process creation and termination

- Since it's hard to measure algorithm's efficiency, people tend to calculate `average waiting time`
    - This can vary with work pattern
      ![waiting, executing, response, turnaround time](res/different-types-of-time.jpg)

# non-preemptive

## FCFS(First Come First Serve)

- `non-preemptive scheduling`
- FIFO scheduling
- Like restaurant with only one table
- `Since only one queue, all process has same priority`
- Used in batch system
- Simple & fair, but with long-running task, avg waiting time could become longer
    - convoy effect

## SJF(Shortest Job First)

- `Allocate CPU to process with the shortest running time`
- non-preemptive
- an order changes if it finds a process which is shorter than upcoming process
- Better than FCFS scheduling, But
    - `How does OS predict exact termination time of processes of modern computers?`
        - Was easy to predict with batch system
    - Fairness problem
        - `What if processes with shorter time keeps being added to queue?? : Starvation`

## HRN

- Highest Response Ratio Next
- non-preemptive scheduling to solve starvation noticed in SJF
- schedule based on priority = (Waiting time + Running time) / Running time
- Better than SJF, but still violates Fairness

# Preemptive

## Round Robin(RR)

- `preemptive scheduling`
- `circular`
- `allocate CPU for time slice`
    - When it's not done, that task will be added to the tail of a queue
- No priority applied
- Similar to FCFS, but has time slice
    - minimized convoy effect
- `Has frequent context switch`
    - right time slicing is needed since Round robin has frequent context switch
- Bigger time slice
    - less frequent context switch, but almost identical to FCFS
- Smaller time slice
    - too much frequent context switch

## SRT(Shortest remaining time)

- SJF + RR
- preemptive
- use RR in general case
    - However, when allocating CPU, select process with the shortest remaining time
- has to calculate each process's remaining time + context switch

## Priority Scheduling

- `Process has its priority based on importance`
- `Priority based scheduling can vary on how to set priority`
- `Can be applied to both preemptive and non-preemptive`
    - Example
        - SJF: priority based on its execution time
        - SRT: priority based on its remaining time
- Dynamic vs Static priority scheduling
    - `Does priority of process change or not?`
    - Static
        - Priority does not change once set
        - Does not reflect current context
    - Dynamic
        - Priority does change based on current context
        - Complex but efficient

- May cause starvation if OS continuously neglect a process with lower priority
- May cause overhead and be inefficient during frequent change in priority

> Priority is set based on importance of the process, rather efficiency

## Multilevel queue in ready status

- have multiple queue in ready status based on priority
- RR based
- process in queue all have same priority
- OS adds process in a queue where other processes have same priority
    - Static priority
- when all processes in one queue finishes, then it moves to next queue with lower priority
    - preemptive scheduling

> However, process with lower priority still has to wait util a process with higher priority is done
>
> How do we solve it?

## Multilevel feedback queue

- In multilevel queue, process with lower priority has disadvantage of allocating CPU
- multiple queue with same processes
- `a process with a higher priority has changed its priority to low after execution`
    - `After execution, a process will be added to a queue with lower priority`
- `Has different time-slice based on priority`
    - lower the priority, longer the time-slice

# Interrupt handling

## What is interrupt?

- Notify OS when action occurs
    - Just like event driven
    - When I/O work completes, it notifies OS that the work is done
    - `CTRL + C` to tell OS to stop the process while it's in infinite loop
    - Cause error to arise when one process intrudes memory area that others occupy
- Used to handle I/O and to protect system
- Multiple interrupts can occur at the same time
    - interrupt vector

## Synchronous and Asynchronous interrupt

- Synchronous Interrupt
    - Caused by Command
    - Errors from program(overflow, underflow)
    - intentional stoppage of a process(CTRL + C)
    - Interrupt from peripherals(I/O)
    - Interrupt from arithmetic (A/0)
- Asynchronous Interrupt
    - Hardware related interrupt(read HDD failure, Memory issue)

## What OS handles interrupt

- Simple
- How to handle interrupt is also predefined, because
    - `Interrupt consists of interrupt number(IRQ) and function(interrupt handler) as a key-value pair`
- Predefined action can also be customizable

- `Flow`
    - a running process causes interrupt(s)
    - Process is in suspend and save current context temporarily for restart
    - Interrupt controller starts running
        - determine what interrupt(s) to handle based on priority
        - Higher the sooner
    - invoke interrupt handler(function) predefined from interrupt vector
    - After interrupt handler, process either continues or terminates

## Interrupt and dual mode

## Dual Mode
- OS moves between user mode and kernel mode to execute task
    - User process use system call to execute task(I/O), then User process goes to wait
    - Kernel process is now in charge of executing the request
        - `How? through API`

## Why dual mode?
- To protect resource if user process access resource directly


## Two possible ways from user mode to kernel mode
- Use API(system call)
- Through interrupt

