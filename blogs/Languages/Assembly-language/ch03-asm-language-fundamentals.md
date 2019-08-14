# Assembly Language Fundamentals

### Basic Elements
* Integer Constants: `[{+|-}] digits [radix]`. E.g. 26d, 42o, 1Ah, 0A3h.
* Integer Expressions: a mathematical expression involving integer values and arithmetic operators. It must evaluate to an integer, which can be stored in 32 bits (0 through FFFFFFFFh). the operators are:

| Operator | Name | Precedence Level|
| ---- | ---- | ---- |
| () | Parentheses | 1 |
| +, - | Unary plus, minus | 2 |
| *, / | Multiply, divide | 3 |
| MOD | Modulus | 3 |
| +, - | Add, subtract | 4 |
* Real Number Constants:
    - Decimal real: `[{+|-}]integer.[integer][E[{+|-}]integer]`. E.g. `2. +3.0 -44.2E+05 26.E5`
    - Encoded real: in hexadecimal, using the IEEE floating-point format. 
* Character Constants: 'A', "d"
* String Constants: 'Good morning', "1234".
* Reserved Words: 
    - Instruction mnemonics, such as MOV, ADD, and MUL
    - Register names
    - Directives, which tell MASM how to assemble programs
    - Attributes, which provide size and usage information for variables and operands. Examples are BYTE and WORD.
    - Operators
    - Predefined symbols, such as @data.
* Identifiers: 
    - 1 - 127 characters.
    - not case sensitive.
    - first character must be a letter, underscore, @, ?, or $.
    - not same as an assembler reserved word.
* Directives: a command embedded in the source code that is recognized and acted upon by the assembler. Directives can define variables, macros, and procedures. 
    - Define segment: The .DATA directive identifies the area of a program containing variables: `.data`. The .CODE directive identifies the area of a program containing executable instructions: `.code`. The .STACK directive identifies the area of a program holding the runtime stack, setting its size: `.stack 100h`. 
* Instructions: is a statement that becomes executable when a program is assembled. Instructions are translated by the assembler into machine language bytes, which are loaded and executed by the CPU at runtime. It contains 4 basic parts: Label (optional), Instruction mnemonic (required), Operand(s) (usually required), Comment (optional).
    - Basic syntax: `[label:] mnemonic [operands] [;comment]`
    - Label: an identifier that acts as a place marker for instructions and data. Data label is the location of a variable. `count DWORD 100`. It's possible to define multiple data items following a label. `array DWORD 1024, 2048`. Code label must end with a colon (:) character. It is used as target of jumping and looping instructions.
    - Instruction Mnemonic: `mov`: Move (assign) one value to another. `add`: Add two values. `sub`: Subtract one value from another. `mul`: Multiply two values. `jmp`: Jump to a new location. `call`: Call a procedure.
    - Operands: an instruction can have between 0 and 3 operands, each of which can be a register, memory operand, constant expression, or input-output port. A memory operand is specified by the **name of a variable** or by **one or more registers** containing the address of a variable. E.g. `96` is Constant. `2 + 4` is Constant expression. `eax` is a register. `count` is a memory.
        * `stc ; set Carry flag`
        * `inc eax ; add 1 to EAX` 
        * `mov count, ebx ; move EBX to count`
        * `imul eax, ebx, 5 ; EBX is multiplied by 5, and the product is stored in EAX`
    - Comments: all characters after `;` on the same line are ignored by the assembler. Or `COMMENT ! xxxxxxxxx !`. All characters between two `!` are ignored. Use `!` or other user-specified symbol.
* The NOP (No Operation) Instruction: Do nothing. Sometimes used by compilers and assemblers to align code to even-address boundaries. 

----
### Example: Adding and Subtracting Integer
```ASM
TITLE Add and Subtract  (AddSub.asm)
; This program adds and subtracts 32-bit integers.
INCLUDE Irvine32.inc
.code
main PROC
    
    mov     eax, 10000h     ; EAX = 10000h
    add     eax, 40000h     ; EAX = 50000h
    sub     eax, 20000h     ; EXA = 30000h
    call    DumpRegs        ; display registers
    
    exit
main ENDP
END main
```

----
### Assembling, Linking, and Running Programs
* The assemble-link-execute cycle:
    - Create a source file with codes. 
    - The assembler reads the source file and produces an object file (`*.o`).
    - The linker reads the object file and checks to see if the program contains any calls to procedures in a link library. The linker copies any required procedures from the link library, combines with the object file, and produces the executable file. 
    - The OS loader utility reads the executable file into memory and branches the CPU to the program's starting address, and the program begins to execute.

----
### Defining Data
* Intrinsic Data Types: DWORD holds a unsigned 32-bit integer logically. In fact, it could hold a signed 32-bit integer, a 32-bit single precision real, or a 32-bit pointer. 
* Data Definition Statement: `[name] directive initializer [, initializer] ...`. E.g. `count DWORD 12345`. 
    - name: identifier.
    - directive: BYTE, WORD, DWORD, REAL4, REAL8 ...
    - initializer: an integer constant or expression matching the size of the variable's type, such as BYTE or WORD. `?` wildcard indicates uninitialized data. 
    - Multi-initializer: see example. The `list` is located at offset 0000, so its value is 10. Next offset 0001 contains the value 20, and so on. 

```ASM
list BYTE 10, 20, 30, 40
     BYTE 50, 60, 70, 80
```
* Defining Strings: "" or ''. `gret BYTE "Good afternoon", 0`. Ends with 0, called a null-terminated string.  
* DUP Operator: `BYTE 20 DUP(0)` allocate 20 bytes, all equal to zero.
* Little Endian Order: x86 processors store and retrieve data from memory using *little endian order* (low to high). The least significant byte is stored at the first memory address. 
* Declaring Uninitialized Data: `.data?`

----
### Symbolic Constants
* Equal-Sign Directive: a symbol name with an integer expression. The syntax is `name = expression`. It's like a static constant. E.g. `Esc_key = 27`
* Calculating the sizes of arrays and strings: `$` operator (current location counter) returns the offset associated with the current program statement. Size is calculated by subtracting the offset of list from the current location counter:
```ASM
list BYTE 10, 20, 30, 40
ListSize = ($ - list)

list WORD 1000h, 2000h, 3000h, 4000h
ListSize = ($ - list) / 2
```
* EQU directive: associates a symbolic name with an integer or some arbitrary text. The syntax is `name EQU expression` or `name EQU <text>`. 
* TEXTEQU directive: creates what is known as a text macro. Syntax is `name TEXTEQU <text>` or `name TEXTEQU textmacro` or `name TEXTEQU %constExtr`.
