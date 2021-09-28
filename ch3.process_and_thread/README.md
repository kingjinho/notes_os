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
    




# PCB and context switch

# Process Calculation

# Thread

# Dynamic Allocation and System call