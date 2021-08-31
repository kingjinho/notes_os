
# Section

[Components of Computer](#Components)

[Von Neumann Architecture](#Von-Neumann-Architecture)


# Components
- CPU, Main memory
- Keyboard, Mouse, Printer, Monitor, Hard-drive ...
- Main memory loses data when power goes off :point_right: need something to store permanently(Hard-drive, USB)
    - Main memory - first storage
    - Hard-drive or USB - second storage


- CPU and Memory
    - Human brain
    - Memory stores program and data, `divided into byte`

- I/O Devices
    - Input: Keyboard, mouse, scanner etc
    - Output: Speaker, Monitor, Printer
    - In the past, CPU calculates graphical calculation, but these days GPU does that

- Storage
    - Primary Storage & Second Storage
    - Primary storage is faster but expensive

- Main Board(motherboard)
    - All these pieces of hardware are installed on motherboard, and connected by `Bus`
    - What is `Bus`?
        - `Is a communication pathway that allows data to travel between different components`


- Some hardware spec-related terms
    - Clock
        - `Rhythm, Speed of CPU`
        - `CPU performs tasks in clock`
        - Clock produce certain thing called `Pulse, or Clock tick at regular interval`
        - Pieces of hardware are connected with Bus
            - Every time clock in main board sends clock tick, hardware receives and send data
    - Hz
        - `How many clock ticks in a second?`
        - Represents speed of clock occurrence in a second
        - 3.2 GHz = 3,400,000,000 clocks in a second
    - System bus(FSB - front-side bus)
        - `Bus between memory and peripherals`
        - If main board has 1,333MHz system bus whereas memory has 800MHz :point_right: main board works as 800MHz  
    - Internal CPU bus(Back Side Bus)
        - Bus reside in inside of CPU
        - Speed of internal CPU bus is way faster than system bus
    - `How to deal with speed difference between System and Internal CPU bus?` 

# Von Neumann Architecture

<img src="./res/Von_Neumann_Architecture.svg.png" width="500" height="500" />

- Computers these days are made based on von Neumann Architecture
- Computer before Von Neumann Architecture,
  - Manually hard-wired everything to re-program
- It basically suggested Basic Structure of Computer,
    1. CPU(CU & ALU)
    2. Memory(Program memory & Data memory)
    3. I/O Device
  - Connected by bus
- `Leave the hardware, switch program by using memory and having program loaded on memory`
- A.k.a. `stored-program computer`: Instruction data and program data are stored in same memory
- Anytime we need calculation, we send program and data from memory to CPU and let CPU do the job
    - Order
    1. `Fetch` data, instruction from memory
        - Instruction fetch and data operation cannot occur at the same time(They share common bus)
            - Cause von Neumann bottleneck(performance issue)
    2. `Decode` instruction
    3. `Execute` instruction
    4. `Store` result

- Bottleneck?
    - Limited throughput between CPU and memory
        - `Data and program memory share same common bus`
        -  `Can only access one of two classes of memory one at a time`
    - Solution?
        - Harvard Architecture
            - Set separate bus for each data and program memory
            - Cache...
- One instruction at a time?
    - Inefficient
    - Multiprogramming, Asynchronous...   


- Von Neumann Architecture and Restaurant?
    - Chef: CPU
    - Cutting Board: Memory
    - Food: Program or Data
    - Fridge: Storage
    - `For chef(CPU) to cook(Operate), Food(Program, or Data) must be out from Fridge(Storage) 
      and set it on Cutting Board(Memory)` 

[CPU and Memory](#CPU-and-Memory)

## CPU components and operation

#### `CPU = ALU + CU + Register`
- These works together to finish tasks
- ALU(Arithmetic & Logic Unit)
    - Place where `actual calculation occurs`(+, -, *, /, AND, OR)        
- CU(Control Unit)
    - Place where `orders, or commands instructions`
    - CU send signal after interpreting instructions, Control data flow
    - `assembly code below`: Load, Add, Move 
- Register(or Process Register)
    - `Temporary storage for data processed or processing`


### How CPU handles instructions?(or How ALU, CU and Register work together?)

- Simple Programming with C: Addition
    ```c
    int d2 = 2, d3 = 3, sum
    sum = d2 + d3
    ```
**d2, d3, sum are another name of memory address, since it is difficult to remember actual memory address
`This is a definition of variable`**  
- Since computer only understand 0,1, we have to turn this code into assembly code
    ```
    //assembly
    
    LOAD mem(100), register 2; //load value from memory address 100 to register 2
    LOAD mem(120), register 3; //load value from memory address 120 to register 3
    ADD register 5, resister 2, register 3; //perform addition of register2 and 3, put result in register 5
    MOVE register 5, mem(160); // move value stored in register 5 into memory address 160
    ```

- To perform operation, CPU needs to data and store in temporary place
    - This is what register is for
    
`!!!!!Load data into register, perform operations, put result back into register, register to memory!!!!!!!!`

- Important to know
    1. CPU orders loading data from memory into register
    2. CPU orders performing data
    3. CPU orders storing result into register
    4. CPU orders storing result from register into memory




[Performance boost technology](#Performance-boost-technology)


[Parallel Processing](#Parallel-Processing)


[Moore's law and Amdahl's law](#Moore's-law-and-Amdahl's-law)



---

# Components of Computer



# CPU and Memory


# Performance boost technology


# Parallel Processing


# Moore's law and Amdahl's law


# What's Next

Go to [Chapter3. Process and Thread](../ch3.process_and_thread)

# Links and images
[Computer Organization | Von Neumann architecture](https://www.geeksforgeeks.org/computer-organization-von-neumann-architecture/)