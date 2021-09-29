# Ch3. Process and Thread

# Section

[Process Intro](#Process-Intro)

[PCB and context switch](#PCB-and-context-switch)

[Process Calculation](#Process-Calculation)

[Thread](#Thread)

[Dynamic Allocation and System call](#Dynamic-Allocation-and-System-call)

# Goal

- State of the process after initialization
- Understand how PCB and context switch works
- Understand process creation, copy and transformation
- Understand thread, multi-thread

# Process Intro

### What is process?

- `To CPU, a process is a unit of task`
- `When we double-click a program, program becomes a process`
- Program vs Process
    - Program: Static state that stored in storage
    - Process: Dynamic state that is loaded on memory for execution
    - `Write a program` and `Run process`
    - If someone writes code is executed, it becomes a process
    - `Program = Recipe whereas process = food`

### How Process Works, State of process

- A process goes through various state under OS
- Learn by Example: Restaurant
    - How restaurant operates
        - Restaurant takes order from each table
        - What to order, table number, how many people, how food should be cooked, etc
        - Waiter takes orders from tables, and hand it over to kitchen
        - Then chef start cooking
    - `Cooking under batch system`
        - Only one table
        - One order only
        - Start new one only after new customer comes in
        - While customers are eating, kitchen takes rest
        - Even if restaurant takes orders in advance(Queue), it still has to wait
    - `Cooking under time-sharing system`
        - Cooking under batch system in a Restaurant is not efficient
        - While customers are eating, kitchen has to cook for other tables
        - Under time-sharing system, chef distributes time for every order in order to serve every table
            - This is like CPU allocate time for every process
        - Then how?
            - Restaurant takes `orders`
            - Kitchen allocate time for `cooking entrée for table A`
            - When it's done, `mark it as done` and place it all the way to the bottom
            - Start `cooking entrée for table B`
            - When it's done, `mark it as done`, place it all the way to the bottom
            - `Start main dishes for table A`
            - and so on ...
    - Importance of Orders
        - `It contains information about`
            - How food should be cooked, current status, what to do next and etc
        - When it is done, it gets removed from orders list
- Takeaways from Restaurant Case
    - Orders listed on list = start of cooking
    - While cooking, orders go through either `stay in list` or `chef cooking` status
    - When it is done, it gets removed from the list

- Exceptions in cooking
    - In restaurant, All procedures listed above do not work smoothly
    - If vegies are not washed, then chef needs to wait to cook lo mein
    - `Waiting without cooking something else is not efficient`
    - If in case of smart chef, `put that in wait list and cook something else`
    - What if vegies are washed? Should chef stop what he/she is cooking and start cooking lo mein?
        - No, it's inefficient
        - `put that in order list from wait list`
    - What if customer want it slow?
        - Expected time of cooking can be tracked whereas customer's request is not
        - In this case, put order in `pending list`
        - `Different from wait list`
- Exceptions in Process
    - Works same as cooking
    - `It has order list, wait list, pending list and current working list`

### Program to process

- Recap
    - `Process is an unit of work called task`
- How program is transformed into process
    1. OS load program onto memory
    2. At the same time, OS creates PCB, or order in restaurant
        - PCB contains information needed to handle process
    3. As chef cannot cook without order, Program cannot be transformed into process without `PCB`
- Key elements in PCB
    - PID
        - Since memory has numbers of processes, it needs to identify each process
        - PID is used to identify each process
    - Memory information
        - CPU needs memory information to run where process is loaded
        - PCB contains information about memory location of process, as well as limit register, bound register
    - Medians
        - This is similar to `what has done so far` in cooking
        - Under time-sharing system, CPU changes current working process after certain time
        - `Before switching, PCB stores PC(program counter) and other registers that hold medians`
        - When process takes CPU again, it starts from where it has left off

- Sum up
    - In order to transform a program in to process,
        - `It has to manage PID, memory information and medians`, and the data structure that holds this is called `PCB`
    - `This also means that PCB has to be created when transforming a program into process`
    - `PCB is created in OS`
    - When a process finishes, process is removed from memory and PCB is disposed
    - `A program to process = acquiring PCB from OS`
    - `Process termination = disposing PCB`

- OS?
    - OS has to be run as a process
    - Bootstrap loads OS onto memory
    - Bootstrap starts many other OS related processes
    - `Computer thus runs kernel process and user process`

### Process Status

- Status of process changes in many reasons
- Batch system
    - One process at a time :point_right: thus, status will be `create, run, terminate`
- Time-sharing
    - Many process run simultaneously :point_right: more complicated

    1. Create
        - Process loaded on memory, PCB created
    2. Ready
        - Status that wait to acquire CPU
    3. Running
        - Process acquires CPU and starts running
        - Process runs for certain period of time
        - When process did not finish during that time :point_right: it goes back to ready status, wait for next turn
        - Process goes back and forth between `ready` and `running` status until it finishes
    4. Terminate
        - When process finishes its work
        - PCB is disposed

- Q: Who decides what process as next?
    - A: `CPU Scheduler`
    - CPU scheduler sends PCB to CPU in order for process to take CPU
        - `Dispatch`: Work that changes status from `ready` to `running`
    - CPU scheduler is involved in every status of process to manage processes to work seamlessly

# PCB and context switch

# Process Calculation

# Thread

# Dynamic Allocation and System call