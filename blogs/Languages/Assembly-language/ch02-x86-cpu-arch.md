# x86-cpu architecture

### General Concepts
* Basic Microcomputer Design: **clock** + **control unit(CU)** + **arithmetic logic unit(ALU)**. Cpu is attached to computer via pins. Most pins connect to the data bus, the control bus and the address bus. 
    - Bus: a group of wires that transfer data from one part of the computer to another. 
    - Clock: operation or system bus is synchronized by an internal clock pulsing at a constant rate.
* Instruction Execution cycle: the execution of a single machine instruction can be divided into a sequence of individual operations called the instruction execution cycle. 
    - Fetch: CU fetches the next instruction from the instruction queue and increments the instruction pointer(IP).
    - Decode: CU decodes the instruction to determine what to do. The instruction's input operands are passed to the ALU, and signals are sent to the ALU indicating the operation to be performed.
    - Fetch operands(optional): If the instruction uses an input operand located in memory, the CU uses a read operation to retrieve the operand and copy it into internal register.
    - Execute: The ALU executes the instruction using the named registers and internal registers as operands and sends the output to named register and/or memory. The ALU updates status flags providing information about the processor state.
    - Store output operand(optional): If the output operand is in memory, the CU uses a write operation to store the data.
```
loop
    fetch next instruction
    advance the instruction pointer (IP)
    decode the instruction
    if memory operand needed, read value from memory
    execute the instruction
    if result is memory operand, write result to memory
continue loop
```
* Reading from Memory: speed slower than CPU clock. CPU must wait one or more clock cycles until operands have been fetched from memory before the current instruction can complete its execution. The wasted clock cycles are called *wait stats*. 
* How Programs Run: 
    - OS search file, if exists, OS retrieves the basic information.
    - OS determine the next available location in memory and loads the program file into memory. It allocates memory to the program and enters information about the programs's size and location into a table. Additionally, the OS may adjust the values of pointers within the program so they contain addresses of program data.
    - OS begins execution of the program's first machine instruction. It create a process. A PID is assigned to keep track of it.
    - The process runs by itself. OS response to requests for system resources. 
    - When the process ends, it is removed from memory. 
* Multitasking: run multiple tasks at the same time. A task is a process or a thread of execution. A process has its own memory area and may contain multiple threads. A thread shares its memory with other threads belonging to the same process. A scheduler allocates a slice of CPU time to each task. By rapidly switching tasks, the processor creates the illusion they are running simultaneously. The processor saves the state of each task before switching to a new one. A task's state consists of the contents of the processor registers, program counter, and status flags, along with references to the task's memory segments. A *preemptive* multitasking OS (Windows XP or Linux) permits a higher-priority task to interrupt a lower-priority one, leading to better system stability. 

### x86 Architecture Details
* Modes of Operation: 
    - Protected mode: the native state of the processor. Programs are given separate memory areas named *segments*, and the processor prevents programs from referencing memory outside their assigned segments. 
    - Virtual-8086 mode: 
    - Real-Address mode: implements the programming environment of the Intel 8086 processor with a few extra features, such as the ability to switch into other modes. This mode is available in Windows 98, and can be used to run an MS-DOS program that requires direct access to system memory and hardware devices. System may crash in this mode.
    - System Management mode: provides an OS with a mechanism for implementing function such as power management and system security.
* Basic Execution Environment:
    - Address Space: 32-bit protected mode, a task or program can address a linear address space of up to 4 GB. Extended Physical Addressing allows a total of 64 GB of physical memory to be addressed. Read-address mode program can only address a range of 1 MB.
    - Basic Program Execution Register: 8 general-purpose registers, 6 segment registers, a process status flags register, and an instruction pointer (EIP).
    - EAX used by multiplication and division instructions. ECX used as loop counter. ESP addresses data on the stack. ESI and EDI are used by high-speed memory transfer instructions. EBP is used by high-level languages to reference function parameters and local variables on the stack. 
    - Segments registers hold pointers to segment descriptor tables. 
    - EIP contains the address of the next instruction to be executed. 
    - EFLAGS register consists of individual binary bits that control the operation of the operation of the CPU or reflect the outcome of some CUP operation. Control flags control the CPU's operation. Status flags reflect the outcomes of arithmetic and logical operations performed by the CPU, such as Overflow, Sign, Zero, Auxiliary Carry, Parity, and Carry flags.
    - MMX registers: 8 64-bit MMX registers improve the performance. MMX supports single-instruction, multiple-data(SIMD) instructions. 
    - XMM registers: 8 128-bit used by streaming SIMD extensions to the instruction set.
* Floating-point unit: FPU performs high-speed floating-point arithmetic. From the Intel486 onward, the FPU has been integrated into the main processor chip. 8 floating-point data registers in the FPU.
* Multi-core processor. Hyper-Threading technology. Dual Core.
* CISC and RISC: complex instruction set computer(CISC). Complex instruction sets permit compiled programs to contain a relatively small number of instruction, but take longer time to decode and execute. Reduced Instruction Set(RISC) consists of a relatively small number of short, simple instructions that execute relatively quickly. 

### x86 Memory Management
* Real address mode:
* Protected mode:
    - Flat segmentation model:
    - Multi-segment model:
    - Paging: segments to be divided into 4 Kb blocks of memory called pages. Pages can be swapped to disk, which is slower but much larger, virtual memory. 

### Components of a Typical x86 Computer
* Motherboard: 
    - Traditionally must have: CPU socket, Memory slots, BIOS computer chips, CMOS RAM, Connectors for mass-storage devices, USB connectors, Keyboard and mouse ports, PCI bus. 
    - Optional: integrated sound processor, parallel and serial device connectors, integrated network adapter, AGP bus connector for a high-speed video card.
    - PCI and PCI express bus architectures: peripheral component interconnect(PCI) bus provide connection between CPU and other system devices.
    - Chipset: 
* Video output: video adapter has video controller and video display memory.
* Memory: 
    - ROM: read-only memory. permanently burned into a chip and cannot be erased.
    - EPROM: erasable programmable read-only memory. Erased slowly with ultraviolet light and reprogrammed.
    - DRAM: dynamic random-access memory. Main memory, where programs and data are kept when a program is running. 
    - SRAM: static RAM. Used primarily for expensive, high-speed cache memory. 
    - VRAM: video RAM. Holds video data. Dual port, one refreshes the display while another writes data to the display.
    - CMOS RAM: complimentary metal oxide semiconductor RAM. On motherboard to store system setup information. 
* Input-Output Ports and Device Interfaces:
    - USB
    - Parallel port
    - ATA Host Adapter
    - SATA Host Adapter
    - FireWire
    - Serial Port
    - Bluetooth
    - Wi-Fi

### Input-Output System
* Levels of I/O Access
    - High-level language functions: These function are portable.
    - OS: Call from a library known as API.
    - BIOS: Low-level subroutines that communicate directly with hardware devices.
    - Device driver: programs that permit the OS to communicate directly with hardware devices. 
    - Hierarchy of I/O request from application to device: L3 - Application program, L2 - OS function, L1 - BIOS function, L0 - Hardware.
* Programming at multiple level: 
    - Level 3: Call library functions to perform generic text I/O and file-based I/O.
    - Level 2: Call OS functions to perform generic text I/O and file-based I/O.
    - Level 1: Call BIOS functions to control device-specific features such as color, graphics, sound, keyboard input, and low-level disk I/O.
    - Level 0: Send and receive data from hardware ports, having absolute control over specific devices. 
    - Lower-level programming need to be more concrete, more device-specific, less portable, while high-level programming is more abstract, less device-specific, more portable. 