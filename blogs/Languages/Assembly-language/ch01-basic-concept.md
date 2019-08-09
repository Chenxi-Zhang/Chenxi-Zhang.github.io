# Basic Concepts

### High-level, Assembly, Machine language
* Machine language is a numeric language understood by a CPU. Assembly language consists of statements written with short mnemonics like `ADD`. Assembly has a one-to-one relationship with machine language.
* High-level languages such as Java and C++ has a one-to-many relationship with assembly and machine language. 
* Assembly language is not portable. It is designed to a specific processor. If it executes on a different architecture, its instruction may be translated by a program inside the processor known as microcode interpreter.

----
### Virtual machine concept
* Computer can execute programs written in machine language. Call it L0.
* Programmers have a difficult time writing programs in L0. A new language, L1, could be easy to use. 2 ways to write program in L1 and run it on computer:
    - Interpretation: As the L1 program is running, each of its instructions could be decoded and executed by a program written in language L0.
    - Translation: The entire L1 program could be converted into ana L0 program by an L0 program specifically designed for this purpose. 
* **Virtual machine**: not only languages, we can think in terms of a hypothetical computer, or virtual machine. The virtual machine VM1, can execute commands written in language L1. VM0 can execute L0 commands. Each VM can be constructed of either hardware or software. 

----
### Data representation
* Binary integers: **Bits** are numbered sequentially starting at zero on the right site and increasing toward the left. The bit on the left is called the **most significant bit**(MSB), and the bit on the right is the **least significant bit**(LSB). 
* Binary addition: Beginning with the lowest bit to highest bit. 
* Hexadecimal Integer: 0, 1, 2, ..., 9, A, B, ..., F
* Signed Integers: Two's-Complement is formed by inverting (complementing) its bits and adding 1.

----
### Boolean Operations
* NOT:¬ or ~ or '
* AND: ^ or . 
* OR: v or +