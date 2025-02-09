# Magic-1-Architecture-and-software-knowledge-base
Magic-1 is a completely homebuilt minicomputer created by <a href="https://www.magic-1.org/">Bill Buzbee</a>. <br> The CPU was designed using only TTL and microcode. 
The computer uses a specially modified version of <a href="https://minix1.woodhull.com/">Minix</a>  2.0.4.

<pre>
  Important note: the following data is not official data but my attempt to understand and summarize how Magic 1 works.
  There may be errors in the text - if one is found - please let me know about it so that I can make corrections in it. 
  The official source of data on Magic 1 architecture is available here: <a href="https://www.magic-1.org/">www.magic-1.org</a>

  At the moment, the Minix system is an integral part of the Magic 1 architecture (as it is necessary to use some of 
  the computer's functions), as Minix has been released under the BSD-3-Clause license since April 2000, for the sake 
  of unification of the    whole project, the rest of the data such as the description of the architecture/software will 
  be released under the same license. 
</pre>

<b>Below is the 24-point summary of the Magic 1 computer architecture:</b>
<br>

    1. The architecture is based on a one-address model, where one operand is implicit, simplifying instruction design.
>[!NOTE from Bill]
>Yes, it started off that way - but I expanded it somewhat.  In a true one-address accumulator model, register A would be involved in nearly all instructions.  
>However, for more efficiency I added B and C registers.  C is pretty limited, but B acts as an added accumulator for loads/stores as well as limited arithmetic 
>using the “lea” instruction.

    2. The system supports data operations in 8-bit and 16-bit widths, offering computational flexibility.
    3. Each process has a virtual address space with a capacity of up to 128KB.
    4. The virtual address space is divided into 32 data pages and 32 code pages, each sized at 2KB.
    5. The physical address space primarily uses a 22-bit address; however, when considering device mappings, it effectively uses 23-bit.
    6. Each process uses a dedicated page table consisting of 64 entries, each 16-bit in size.
    7. The page table is stored in separate memory and is accessed via a base pointer allocated for each process.
    8. Memory implementation is realized through memory mapping, where peripheral devices share the same address space as main memory.
    9. The system supports external interrupts, allowing rapid response to hardware events.
    10. Direct Memory Access (DMA) is integrated, enabling direct data transfers without CPU intervention.
    11. The processor employs a microcode-driven control mechanism for fine-tuned instruction sequencing and optimization of performance.
    12. There is a balanced trade-off between simplicity (one-address architecture) and performance (additional registers and complex addressing modes).
    13. The design includes both atomic operations and complex data manipulation, supporting efficient parallel and multi-threaded computing.
    14. Sophisticated scheduling of microcode instructions allows the system to adapt to various programming paradigms.
    15. The system's memory management unit (MMU) efficiently handles virtual-to-physical address translations.
    16. Hardware-level support for concurrency ensures effective multitasking and high throughput under multiple process loads.
    17. The architecture integrates specialized control units to manage IO devices and system buses.
    18. The instruction set architecture (ISA) is optimized for modern high-level programming languages, facilitating efficient translation of high-level code into hardware operations.
    19. The system is designed to balance the simplicity of hardware logic with the complexity required by modern applications.
    20. Dedicated registers and specialized addressing modes enhance the speed and accuracy of operations.
    21. The architecture anticipates flexible memory management, which is crucial for implementing multiprocessing.
    22. Microcode scheduling technologies allow the system to adapt to changing workloads.
    23. The system design considers data security aspects through strict management of the memory address space.    
    24. The overall compromise between theoretical elegance and practical implementation ensures future development and enables deployments in modern computing systems.

This summary provides a detailed technical overview highlighting both the strengths of the Magic 1 architecture and its constructive compromises.<br><br>
<pre>
The primary goal is to collect as much information as possible about this computer and present it 
in a way that makes it easier to understand its architecture and how it functions.
  
<b>Construction and Operation</b>

In a nutshell, this computer is built with 5 cards (Double Eurocard format):

  <b>ALU/Register:</b> 74LS374, 74F381, 74LS244, 74F382
  <b>Control:</b> 5x 27C256
  <b>Device:</b> ICs 8255, 16550, boot-ROM, 1.482 MHz
  <b>Memory:</b> HM628512ALP-7 4M SRAM (512 KWORD X 8 BIT), UM61256FK-15 61256 32K x 8-Bit High Speed SRAM
  <b>Front Panel</b>

Each card is connected by 2 DIN 41612 (type C, 96-pin) connectors to 2 BUS cards equipped with connectors for 
linking the cards, acting as a bus connecting signals from all the cards. The entire computer can be powered 
using any +5V 2A power supply; I use an old ATX 200W computer power supply.

The computer uses two IC 16550s serving as serial ports: 
one for communication (telnet, for receiving and entering data), 
and the other (SLIP, Serial Line Internet Protocol - for the computer's communication 
with the world, such as the Internet).

The microcode is located in high-speed EPROMs like AMD 27C256-55.5V 32kx8, DIP-28, 55ns.
  
The basic code is located in three places:

  1.<b>Bootloader:</b> Code that loads the monitor, operating system, and IDE driver.
  2.<b>EPROM/PROM:</b> A set of micro-instructions loaded into the computer's RAM during Magic-1 startup.
  3.<b>CF/IDE:</b> A set of partitions and the modified version of the Minix 2.0.4 operating system, 
      which the user uses to boot the computer, load the system, and log in to the system operator console.

<b>Tools</b>

The system would not be complete without a set of tools that allow the development of new software for 
this architecture. In this case, we have two sets of tools: one that can be used, for example, 
on a laptop equipped with Linux, and the second set of tools available on the Magic-1 computer itself.
  
<b>ISA (Instruction Set Architecture)</b>

ISA, or Instruction Set Architecture, is part of the abstract model of a computer that defines how the CPU is 
controlled by the software. The set of instructions is divided into groups (according to their application type). 
I will describe their functions, such as data type/addressing method and the possibility of combining instructions.

</pre>
  
Here’s a detailed explanation of the verified facts regarding the "Magic Architecture" as described in the text:
<pre>
   One-Address Architecture:
        This means that the architecture uses a single address in its instruction set to specify the operand for operations. 
        In a one-address architecture, instructions typically involve a single memory address, which is used for both the 
        source and destination of data. 
        The operations can be either 8-bit or 16-bit, indicating the size of the data being processed.

    Address Space:
        The architecture provides each process with a virtual address space of up to 128K bytes. 
        This space is organized into 32 pages for data and 32 pages for code, with each page being 2K bytes in size. 
        This organization allows for efficient memory management and access, as the system can easily map these pages into 
        physical memory.

    Physical Addressing:
        The virtual address space is mapped into a physical address space that is 22 bits wide. 
        This means that the architecture can address up to (2^{22}) bytes of physical memory, which is approximately 4MB. 
        When considering device space, it effectively extends to 23 bits, allowing for additional addressing capabilities.

    Page Table:
        Each process has a dedicated page table that consists of 64 entries, with each entry being 16 bits. 
        This page table is crucial for translating virtual addresses to physical addresses, enabling the operating system to 
        manage memory efficiently. 
        The page table is located in dedicated memory, and each process has a base pointer to its own page table.

    Memory-Mapped I/O:
        The architecture employs memory-mapped I/O, meaning that certain memory addresses are reserved for I/O devices. 
        The top 128 bytes of memory are specifically allocated for device control blocks, 
        allowing the CPU to interact with hardware devices as if they were part of the memory space.

    Interrupts and DMA:
        The architecture supports external interrupts and Direct Memory Access (DMA). 
        This means that hardware devices can signal the CPU to interrupt its current operations, allowing for responsive 
        handling of events. 
        DMA allows devices to transfer data directly to and from memory without CPU intervention, improving performance.

    Endianness:
        The architecture uses big-endian format for data storage, meaning that the most significant byte of a word is stored 
        at the lowest memory address. 
        This affects how multi-byte data types are read from and written to memory.

    Addressing Modes:
        The architecture supports a variety of addressing modes, including register indirect, frame local, global, immediate, 
        push, and pop. 
        These modes provide flexibility in how operands are accessed and manipulated, allowing for more complex data structures 
        and operations.

    Atomic Instructions:
        The architecture includes atomic instructions such as "compare and branch" and "test and branch." 
        These instructions are executed as a single, indivisible operation, which is essential for maintaining 
        data integrity in multi-threaded or interrupt-driven environments.

    Microcode:
        A significant amount of microcode is utilized in the architecture, with five 512x8-bit Programmable Read-Only Memories (PROMs) 
        dedicated to storing microcode. 
        Microcode is a layer of instructions that translates higher-level machine instructions into sequences of operations that the 
        hardware can execute, 
        allowing for more complex instruction sets and functionalities.
</pre>
<b>Processor Commands</b>
<pre>
Here are several processor commands, their binary notation, and examples of their construction and application:

    Load Command:
    Syntax: ld.8/16 <dest>, [<source>]
    Binary Notation:
    The command might be structured as follows:
    [OP: 4 bits][Dest: 3 bits][Mode: 3 bits][Immediate/Data: 8/16 bits]
    
    Example:

    Command: ld.8 A, #u16(DP)
    This command loads an 8-bit value from the address specified by the Data Pointer (DP) into register A.
    Example Binary: 0010 001 010 00000001
    (Where 0010 is the opcode for load, 001 represents register A, and the rest is the immediate value.)

    Subtraction Command:

    Syntax: sub.8/16 A, [Operand]
    Binary Notation:
    The structure can be:
    [OP: 4 bits][Dest Reg: 3 bits][Mode: 3 bits][Immediate/Data: 8/16 bits]

    Example:

    Command: sub.16 A, #i16_exti8
    This command subtracts a 16-bit sign-extended immediate value from register A.
    Example Binary: 0100 001 011 00000010

    Branch Command:

    Syntax: br.[condition] d16
    Binary Notation:
    Format may look like: [OP: 4 bits][Cond: 4 bits][Address: 8 bits]

    Example:

    Command: br.eq #d16
    This instructs the processor to branch to the specified 16-bit address if the zero flag is set.
    Example Binary: 0110 0001 10101010

    System Call Command:

    Syntax: syscall u8
    Binary Notation:
    Structure: [OP: 4 bits][Reserved: 2 bits][Syscall Number: 8 bits]

    Example:

    Command: syscall #sys_num8
    This performs a system call using the specified 8-bit system call number.
    Example Binary: 1000 0001 00011010

    Write Code Page Table Entry Command:

    Syntax: wcpte A, (B)
    Binary Notation:
    Typical format: [OP: 4 bits][Source Reg: 3 bits][Destination Reg: 3 bits][Extra Flags/Offset: 6 bits]

    Example:

    Command: wcpte A, (B)
    This writes a code page table entry for the address in register B.
    Example Binary: 1010 001 010 001101
       
    </pre>
<b>Conclusion</b><br><br>

The Magic Architecture is characterized by its one-address design, efficient memory management through paging, and support for various
operations and commands. The architecture's use of microcode and atomic instructions enhances its capability to handle complex tasks 
while maintaining data integrity. The examples of processor commands illustrate how instructions are structured and executed within this 
architecture.
  
<pre>
Here’s a detailed explanation of the additional 20 facts regarding the "Magic Architecture," 
focusing on the microcode and its implications for the architecture's design and functionality:
  
1. Extensive Use of Microcode

The architecture employs microcode extensively, which means that many higher-level instructions are 
implemented as sequences of lower-level micro-operations. This allows for more complex instructions 
to be broken down into simpler steps that the hardware can execute.
  
2. Non-Orthogonal Opcode Encoding

The architecture uses a non-orthogonal opcode encoding scheme with 8-bit opcodes. This means that 
not all combinations of opcodes and operands are valid or meaningful, leading to a reliance on 
microcode to handle the variations and complexities of instruction execution.
  
3. Dedicated Microcode Region

There is a specific area in memory designated for microcode, where instructions are further divided
into multiple micro-operations. This separation allows for efficient execution and management of 
complex instructions.
  
4. Microcode Instructions for Memory Operations

Microcode instructions include specific operations for reading from or writing to different parts 
of memory registers. For example, instructions like READLO and WRITEHI indicate operations that 
target the lower or higher parts of a register, respectively.
  
5. Annotated Micro-Operations

Each micro-operation is annotated with specific operations that may apply to registers, such as 
INC_TO_Z (increment to zero) or DEC_TO_Z (decrement to zero). This level of detail allows for 
precise control over register states during execution.
  
6. Documented Opcodes with Hexadecimal Addresses

Certain opcodes are documented with hexadecimal addresses (e.g., 0x1E0 to 0x1FF), indicating that 
there are multiple implementations of microinstructions for different opcodes. This allows for 
flexibility in how instructions are executed based on the context.
  
7. Variants of Multi-Word Processing

Commands are labeled with designations like "Mop16," "Mop16a," or "Mop16Carry," which indicate 
different variants of multi-word processing operations or operations that specifically affect 
the carry flag in arithmetic operations.
  
8. Special Microcode Entries for Error Handling

The microcode includes special entries such as "UNUSABLE" and "Unreachable" to manage error 
conditions or invalid states. This helps ensure that the system can gracefully handle unexpected 
situations.
  
9. Control Flow Emphasis

Microcode emphasizes control flow, with each instruction concluding with a NEXT directive 
(e.g., NEXT(FALLTHRU) or NEXT(PCtoMAR)). This defines how control is transferred to the next 
instruction, ensuring proper sequencing.
  
10. Distinction Between Data Movement and Control Operations

The microcode clearly differentiates between data movement operations (e.g., transferring data 
from memory to the accumulator) and control operations (e.g., branching to a different instruction). 
This distinction is crucial for maintaining the integrity of program execution.
  
11. Combined Memory Access and Arithmetic Logic

Several operations combine memory access with arithmetic logic, as seen in commands that invoke 
Arithmetic Logic Unit (ALU) functions (e.g., ALU(OP_IR13, WORD, NO_CARRY)). This allows for 
efficient execution of complex operations.
  
12. Partitioned Use of Registers

The architecture features a clear partitioning of registers, including R_A (the primary accumulator), 
R_B, and R_C. R_C is often used for branching or condition tests, which helps streamline control 
flow in programs.
  
13. Page Table Design and Addressing Modes

The design of the page table and the addressing modes reflects a balance between hardware simplicity 
and the requirements of compiler output. This ensures that the architecture can efficiently support 
a variety of programming languages.
  
14. Trade-off in Design for Efficiency

While the original one-address design was straightforward, later additions of additional registers 
(like B and C) improve efficiency for hand-compiled code and non-optimizing C code generation. 
This trade-off enhances performance without overly complicating the architecture.
  
15. Microcode Scheduling

Microcode schedules indicate that even simple operations may be split across several micro-steps, 
with each step carefully sequenced. This allows for precise control over the execution timing of 
operations.
16. Specialized Commands for Atomic Operations

The use of microcode enables specialized commands for atomic operations, such as "compare and branch" 
and "test and branch." These commands ensure that operations are executed in a way that maintains data 
integrity and correct sequencing.
  
17. Big-Endian Bit and Byte Ordering

The architecture strictly adheres to big-endian ordering for both bits and bytes. This design choice 
is not only a technical specification but also a philosophical statement, as it reflects a preference 
for a certain way of organizing data in memory.
  
18. Rich Instruction Set

The architecture supports a rich instruction set that allows for a variety of operations, including 
complex data manipulations and control flow instructions. This richness is facilitated by the microcode 
structure.
  
19. Flexibility in Instruction Execution

The reliance on microcode allows for flexibility in how instructions are executed, enabling the architecture 
to adapt to different programming paradigms and optimize performance for specific tasks.
  
20. Emphasis on Compiler Optimization

The design considerations reflect an emphasis on optimizing the output of compilers, ensuring that the 
architecture can efficiently execute code generated by high-level programming languages.

These points collectively illustrate the complexity and thoughtfulness behind the Magic Architecture's design, 
emphasizing its reliance on microcode, the careful structuring of operations, and the balance between simplicity 
and functionality.
  
</pre>
