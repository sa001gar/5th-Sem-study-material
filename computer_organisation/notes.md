# Computer System Architecture – Full Notes (Markdown)

> Major/DS Course (Core): COMP 5012 (Theory)- Computer Organization

***

## 0. Syllabus broken into subtopics

### [Unit 1 – Introduction (10 hours)](#unit-1--introduction)

   - [1.1 Evolution of Computers](#11-evolution-of-computers)
   - [1.2 Stored Program Concept](#12-stored-program-concept)
   - [1.3 Von‑Neumann Architecture](#13-vonneumann-architecture)
   - [1.4 Information Representation and Codes](#14-information-representation-and-codes)
   - [1.5 Building Blocks of Computers](#15-building-blocks-of-computers)

### [Unit 2 – Register Transfer and Microoperations (15 hours)](#unit-2--register-transfer-and-microoperations)

   - [2.1 Concept of Bus](#21-concept-of-bus)
   - [2.2 Data Movement Among Registers](#22-data-movement-among-registers)
   - [2.3 RTL: A Language for Conditional Data Transfer](#23-a-language-to-represent-conditional-data-transfer-rtl)
   - [2.4 Data Movement From/To Memory](#24-data-movement-fromto-memory)
   - [2.5 Arithmetic Operations with Register Transfer](#25-arithmetic-operations-with-register-transfer)
   - [2.6 Logical Operations with Register Transfer](#26-logical-operations-with-register-transfer)
   - [2.7 Timing in Register Transfer](#27-timing-in-register-transfer)

### [Unit 3 – CPU Architecture (15 hours)](#unit-3--cpu-architecture)

   - [3.1 Instruction Format](#31-instruction-format)
   - [3.2 Instruction Execution](#32-instruction-execution)
   - [3.3 Fetch and Execution Cycles](#33-fetch-and-execution-cycles)
   - [3.4 CPU Organization with Large Register Sets](#34-cpu-organization-with-large-register-sets)
   - [3.5 Stacks](#35-stacks)
   - [3.6 Handling of Interrupts](#36-handling-of-interrupts)
   - [3.7 Handling of Subroutines](#37-handling-of-subroutines)
   - [3.8 Instruction Pipelining – Stages](#38-instruction-pipelining--stages)
   - [3.9 Pipeline Hazards](#39-pipeline-hazards)
   - [3.10 Methods to Remove/Reduce Hazards](#310-methods-to-removereduce-hazards)

### [Unit 4 – Micro‑programmed Control Unit (5 hours)](#unit-4--microprogrammed-control-unit)

   - [4.1 Basic Organization of Micro‑programmed Controller](#41-basic-organization-of-microprogrammed-controller)
   - [4.2 Horizontal Microinstruction Format](#42-horizontal-vs-vertical-microinstruction-formats)
   - [4.3 Vertical Microinstruction Format](#43-address-sequencer)
   - 4.4 Address Sequencer

### [Unit 5 – I/O Organization (5 hours)](#unit-5--io-organization)

   - [5.1 Strobe‑based Communication](#51-strobebased-communication)
   - [5.2 Handshake‑based Communication](#52-handshakebased-communication)
   - [5.3 Vector Interrupt](#53-vector-interrupt)
   - [5.4 Priority Interrupt](#54-priority-interrupt)
   - [5.5 DMA‑based Transfer](#55-dmabased-transfer)

### [Unit 6 – Programming the Basic Computer (10 hours)](#unit-6--programming-the-basic-computer)

   - [6.1 Instruction Formats](#61-instruction-formats-basic-computer)
   - [6.2 Addressing Modes](#62-addressing-modes)
   - [6.3 Instruction Codes](#63-instruction-codes)
   - [6.4 Machine Language](#64-machine-language)
   - [6.5 Assembly Language](#65-assembly-language)
   - [6.6 Input‑Output Programming](#66-inputoutput-programming)

***

## Unit 1 – Introduction

### 1.1 Evolution of computers

Early computers were built with **vacuum tubes** and were huge, slow, and power‑hungry (first generation machines like ENIAC).  Programs were set using switches and plug‑boards; to change the program you had to change the wiring manually.

The invention of the **transistor** replaced vacuum tubes, making computers smaller, faster, more reliable, and less power‑hungry (second generation).  Then **integrated circuits (ICs)** combined many transistors on a single chip (third generation), followed by **VLSI/ULSI** with millions or billions of transistors per chip, giving rise to microprocessors and modern PCs and smartphones.

Simple generation chart:

| Generation | Main technology | Typical feature |
| :-- | :-- | :-- |
| 1st | Vacuum tubes | Room‑sized, high power, very low speed |
| 2nd | Transistors | Smaller, less heat, more reliable |
| 3rd | IC (SSI/MSI) | Minicomputers, better cost/performance |
| 4th | VLSI chips | Microprocessors, personal computers |
| 5th+ | Multi‑core, SoC | High parallelism, embedded \& mobile systems |

***

### 1.2 Stored program concept

**Definition:** Instructions and data are both stored in a common, read‑write memory, and the CPU fetches and executes instructions from this memory sequentially (unless a branch occurs).

Because the program is stored in memory as binary data, it can be modified by another program (e.g., a compiler or loader), which makes general‑purpose computing and high‑level languages possible. In practice, the CPU repeatedly performs a **fetch–decode–execute** cycle using the Program Counter (PC) to track the address of the next instruction in memory.

***

### 1.3 Von‑Neumann architecture

Von‑Neumann architecture is a direct implementation of the stored program concept, where **one memory** holds both instructions and data.

**Main components:**

- **CPU (Central Processing Unit)**
    - ALU (Arithmetic Logic Unit) – performs arithmetic/logic.
    - Control Unit – fetches/decodes instructions, generates control signals.
    - Registers – small, fast storage inside CPU (e.g., PC, IR, ACC).
- **Main Memory** – stores program + data.
- **Input devices** – keyboard, mouse, etc.
- **Output devices** – monitor, printer, etc.
- **Buses** – shared communication lines: address bus, data bus, control bus.

Diagram (simplified):

```text
            +--------------------+
            |        CPU         |
            | +-----+  +------+  |
Input ----> | |CU   |  | ALU  |  | ----> Output
Devices     | +-----+  +------+  |    Devices
            |  Registers (PC,IR) |
            +---------+----------+
                      |
              System Bus (Addr + Data + Control)
                      |
            +---------v----------+
            |     Main Memory    |
            | (Instr + Data)     |
            +--------------------+
```

**Von‑Neumann bottleneck:** Because instruction and data share the same memory and bus, the CPU cannot fetch an instruction and data from memory in parallel; this memory bandwidth limit is called the “Von‑Neumann bottleneck”.

***

### 1.4 Information representation and codes

Computers represent everything in **binary**, using 0s and 1s. A sequence of bits forms larger units: nibble (4 bits), byte (8 bits), word (e.g., 16/32/64 bits).

#### 1.4.1 Unsigned binary numbers

For an n‑bit unsigned binary number $b_{n-1}b_{n-2}...b_1b_0$, its value is:

$$
\sum_{i=0}^{n-1} b_i \times 2^i
$$

Example: $1011_2 = 1\times 2^3 + 0\times 2^2 + 1\times 2^1 + 1\times 2^0 = 8 + 2 + 1 = 11_{10}$.

#### 1.4.2 1’s and 2’s complement

**1’s complement:** invert all bits (0→1, 1→0).
**2’s complement:** 1’s complement + 1 in LSB.

Example (4 bits):

- $5_{10} = 0101_2$.
- 1’s complement = 1010.
- 2’s complement = 1010 + 0001 = 1011 (represents −5 in 4‑bit 2’s complement).

Subtraction using 2’s complement: $A - B = A + (\text{2’s complement of }B)$.

#### 1.4.3 Character codes

- **ASCII:** 7/8‑bit code; for example, ‘A’ = 65 decimal = 01000001 binary.
- **Unicode:** variable‑length encoding (e.g., UTF‑8) to represent characters from many languages worldwide.

#### 1.4.4 Decimal‑related codes

- **BCD (Binary Coded Decimal):** each decimal digit is encoded separately using 4 bits (0–9 => 0000–1001).
- **9’s / 10’s complement:** used in decimal arithmetic (similar to 1’s/2’s complement logic for decimal digits).

#### 1.4.5 Error‑detecting codes

**Parity bit:** one extra bit is added so that total number of 1’s in the code word is even (even parity) or odd (odd parity), helping to detect single‑bit errors in transmission or memory.

***

### 1.5 Building blocks of computers

Digital systems are built from **combinational** and **sequential** logic.

- **Combinational logic**: output depends only on current inputs.
    - Examples: adders, multiplexers (MUX), decoders, encoders.
- **Sequential logic**: output depends on current inputs and past history (stored in memory elements).
    - Examples: flip‑flops, registers, counters, finite state machines.

Common building blocks:

- **Logic gates:** AND, OR, NOT, NAND, NOR, XOR, XNOR.
- **Flip‑flops:** basic 1‑bit storage; types SR, JK, D, T.
- **Registers:** group of flip‑flops for multi‑bit storage (e.g., 8‑bit register).
- **Counters:** special sequential circuits for counting pulses.

Block diagram of data path (simplified):

```text
+--------+     +--------+     +--------+
| Reg A  |---->|  ALU   |---->| Reg C  |
+--------+     +--------+     +--------+
    ^              ^
    |              |
+--------+     Control Signals
| Reg B  |
+--------+
```

***

## Unit 2 – Register Transfer and Microoperations

### 2.1 Concept of bus

A **bus** is a group of shared lines (wires) used to transfer data, addresses, or control signals among multiple units. Internal CPU buses allow many registers to communicate without dedicated point‑to‑point wiring between every pair.

Types (within a system):

- **Data bus:** carries data values.
- **Address bus:** carries addresses (selects memory/I/O locations).
- **Control bus:** carries control signals (read/write, interrupt, clock, etc.).

Internal CPU bus diagram:

```text
        +------+   +------+   +------+
        | R1   |   | R2   |   | R3   |
        +--+---+   +--+---+   +--+---+
           |          |          |
        EnR1       EnR2       EnR3  (tri-state)
           \         |         /
            \        |        /
             +-------+-------+
                     |
                     v
                  INTERNAL
                     BUS
                     |
                  +--+--+
                  | ALU|
                  +----+
```

Only one register at a time is enabled to put its contents on the bus; others remain in high‑impedance state.

***

### 2.2 Data movement among registers

We describe register transfers using **Register Transfer Language (RTL)**.

- Simple transfer:
    - $R2 \leftarrow R1$: copy contents of R1 to R2 in one clock pulse.
- Conditional transfer with control signal $P$:
    - $P: R2 \leftarrow R1$: if $P = 1$ before the clock edge, R2 is loaded with R1 on that edge.

**Example:** Swap contents of A and B using temporary register T:

```text
T ← A
A ← B
B ← T
```

In RTL:

- $T \leftarrow A$
- $A \leftarrow B$
- $B \leftarrow T$

If the bus is available, each arrow can represent one clock cycle.

***

### 2.3 A language to represent conditional data transfer (RTL)

RTL is a compact language to describe what happens in one clock cycle:

- **Left side**: destination register.
- **Right side**: source register, bus, ALU output, or memory.
- **Condition** (optional) before colon: control signal or timing signal (e.g., $T_0, T_1$ for different clock cycles in the instruction cycle).

Example of sequence for instruction fetch:

- $T_0:\ MAR \leftarrow PC$
- $T_1:\ MDR \leftarrow M[MAR]$
- $T_2:\ IR \leftarrow MDR,\; PC \leftarrow PC + 1$

Here $T_0, T_1, T_2$ represent different time steps (clock cycles) for microoperations.

***

### 2.4 Data movement from/to memory

A CPU typically uses:

- **MAR (Memory Address Register)** – holds the memory address.
- **MDR (Memory Data Register)** – holds data to be written or data read from memory.

**Memory Read** (conceptual RTL):

1. $MAR \leftarrow R1$   (address to be accessed is in R1)
2. MDR ← Memory[MAR]      (memory places data at that address onto bus into MDR)
3. $R2 \leftarrow MDR$  (data moved to destination register)

**Memory Write**:

1. $MAR \leftarrow R1$   (address)
2. $MDR \leftarrow R2$   (data)
3. Memory[MAR] ← MDR      (write operation)

Diagram:

```text
CPU                    Memory
+---------+            +----------+
|  MAR    |<----Addr-->| Address  |
+---------+            +----------+
|  MDR    |<----Data-->| Data     |
+---------+            +----------+
```

***

### 2.5 Arithmetic operations with register transfer

Arithmetic microoperations perform arithmetic on register contents via the ALU.

Common arithmetic microoperations:

- **Addition:** $R3 \leftarrow R1 + R2$
- **Subtraction:** $R3 \leftarrow R1 - R2$ (usually via 2’s complement)
- **Increment:** $R1 \leftarrow R1 + 1$ (often used for PC)
- **Decrement:** $R1 \leftarrow R1 - 1$

ALU‑centric diagram:

```text
R1 ----->+          +-----> R3
         |  ALU     |
R2 ----->+ (+, -, etc)
```

**Example:** $R3 \leftarrow R1 + R2$

1. Bus selects R1 and R2 as ALU inputs.
2. ALU performs addition.
3. Result is placed on internal bus.
4. R3 load signal is activated at next clock edge.

2’s complement subtraction example $A - B$:

- Find 2’s complement of B.
- Add to A.
- Overflow bit (carry out) is ignored for signed arithmetic.

***

### 2.6 Logical operations with register transfer

Logic microoperations perform bitwise operations.

Examples:

- **AND:** $R3 \leftarrow R1 \land R2$
- **OR:** $R3 \leftarrow R1 \lor R2$
- **XOR:** $R3 \leftarrow R1 \oplus R2$
- **NOT:** $R1 \leftarrow \text{NOT }R1$

Example: if R1 = 1010, R2 = 1100:

- R3 = R1 AND R2 = 1000
- R4 = R1 OR R2 = 1110
- R5 = R1 XOR R2 = 0110

These operations are implemented by the ALU’s logic section.

***

### 2.7 Timing in register transfer

Most register transfers are synchronized to a **system clock**.

- On the active clock edge (rising or falling), registers with their **load enable** signal high will latch the data present at their input.
- Control signals must be stable before the clock edge to satisfy setup time requirements.

Conceptual timing diagram:

```text
Clock:   _|‾|_|‾|_|‾|_|‾|_
P (ctrl):___----___________
R2←R1:   ____[Transfer]____
```

If control signal P = 1 between two edges, the microoperation $R2 \leftarrow R1$ occurs on that edge. Multiple microoperations can execute in the same cycle if they do not conflict (e.g., writing to different registers from different sources).

***

## Unit 3 – CPU Architecture

### 3.1 Instruction format

An **instruction format** is the layout of bits in an instruction; it defines how opcode and operands are encoded.

Typical fields:

- **Opcode field** – specifies the operation (ADD, SUB, LOAD, etc.).
- **Addressing mode bits** – may indicate immediate, direct, indirect, etc.
- **Register fields** – identify registers (e.g., R1, R2).
- **Address/Immediate field** – holds memory address or immediate constant.

Example (simple R‑format):

```text
| opcode (6) | rs (5) | rt (5) | rd (5) | shamt (5) | funct (6) |
```

Example (load instruction) for single accumulator machine:

- LOAD A, X → $AC \leftarrow M[X]$ (AC = accumulator, X = address).

#### 3.1.1 Types of instruction formats (by number of addresses)

- **Three‑address:** `ADD R1, R2, R3` → $R1 \leftarrow R2 + R3$.
- **Two‑address:** `ADD R1, R2` → $R1 \leftarrow R1 + R2$.
- **One‑address:** `ADD X` → $AC \leftarrow AC + M[X]$ (AC implied).
- **Zero‑address:** operations done on stack top; e.g., `ADD` → TOS ← (TOS + next element) in stack machines.

***

### 3.2 Instruction execution

Instruction execution process:

1. **Fetch** – CPU fetches instruction from memory location pointed by PC into IR.
2. **Decode** – Control Unit decodes opcode, determines operation and addressing mode.
3. **Operand fetch** – If required, operands are fetched from registers/memory.
4. **Execute** – ALU or other unit performs operation.
5. **Write back** – Result stored in register/memory, flags updated.
6. **PC update** – PC gets next instruction address (PC+1 or branch target).

***

### 3.3 Fetch and execution cycles

The **instruction cycle** is often divided into smaller cycles: **Fetch cycle** and **Execute cycle** (plus optional memory/interrupt cycles).

**Fetch cycle RTL (example):**

1. $T_0:\ MAR \leftarrow PC$
2. $T_1:\ MDR \leftarrow M[MAR]$
3. $T_2:\ IR \leftarrow MDR,\; PC \leftarrow PC + 1$

**Execute cycle:** depends on the instruction. Example for LOAD R1, X:

1. $T_3:\ MAR \leftarrow X$
2. $T_4:\ MDR \leftarrow M[MAR]$
3. $T_5:\ R1 \leftarrow MDR$

Instruction cycle diagram (conceptual):

```text
[ Fetch ] -> [ Decode ] -> [ Execute ] -> [ Interrupt Check ] -> [Next Fetch...]
```

***

### 3.4 CPU organization with large register sets

Some architectures have a **large set of general‑purpose registers** to reduce memory access and speed up execution.

- Example: 32 general‑purpose registers (R0–R31).
- Registers can be used for holding frequently used variables, temporary values, and addresses, reducing the need to go to memory for operands.

**Register‑file based CPU** (conceptual):

```text
           +--------------------+
           |   Register File    |
           | R0 R1 R2 ... R31   |
           +----+---------+-----+
                |         |
              src1      src2
                \       /
                 \     /
                  +---+---+
                  |  ALU  |
                  +---+---+
                      |
                    result
                      |
                    +---+
                    | RF|
                    +---+
```

Using more registers makes two/three‑address instructions efficient (e.g. `ADD R1, R2, R3`) and allows better compiler optimization.

***

### 3.5 Stacks

A **stack** is a LIFO (Last‑In First‑Out) structure used in CPU for:

- Storing return addresses for subroutines.
- Saving CPU state during interrupts.
- Temporary storage (e.g., expression evaluation).

It uses a **Stack Pointer (SP)** register to point to the top of the stack.

Operations (simplified):

- **PUSH X:**
    - SP ← SP − 1
    - M[SP] ← X
- **POP X:**
    - X ← M[SP]
    - SP ← SP + 1

Diagram:

```text
Higher Address
      ^
      |
    [   ]  <- bottom
    [   ]
    [ D ]  <- top element (SP)
      |
Lower Address
```

In many architectures, stack grows **downwards** (towards lower addresses).

***

### 3.6 Handling of interrupts

An **interrupt** is an event that temporarily stops the normal execution of the program so that the CPU can execute an **Interrupt Service Routine (ISR)**.

Steps (simplified):

1. Device/condition raises an interrupt request.
2. CPU finishes current instruction (if mask allows) and acknowledges interrupt.
3. Current PC and possibly other registers are saved (often on stack).
4. CPU loads ISR address (from vector table or fixed address).
5. ISR executes; may read/write device, clear interrupt flag.
6. ISR restores previous CPU state and executes **RET**/IRET to return to the interrupted program.

**Vectored interrupt:** device provides an interrupt vector that directly points to ISR address.

**Priority interrupts:** when multiple requests occur, priority logic decides which one is served first (hardware priority encoders or software polling).

***

### 3.7 Handling of subroutines

A **subroutine** (function/procedure) is a reusable block of code that can be called from different points in the program.

- **CALL**:
    - Save return address (usually PC) on stack.
    - Jump to subroutine start address.
- **RET**:
    - Pop return address from stack.
    - Jump back to caller.

Subroutines support **code reuse** and make programs modular and easier to maintain.

#### Parameter passing methods in 8085‑style systems

1. **Using registers**: store parameters in registers before CALL; subroutine reads from those registers.
2. **Using memory**: store parameters at known memory locations; subroutine reads from those locations.
3. **Using “M” (memory pointer)**: use HL pair to point to a memory location; subroutine reads via M.
4. **Using stack**: PUSH values on stack before CALL; subroutine POPs them.

***

### 3.8 Instruction pipelining – stages

**Instruction pipelining** splits instruction execution into stages so multiple instructions are processed simultaneously in different stages.

Classic 5‑stage pipeline:

1. **IF (Instruction Fetch)** – fetch instruction from memory.
2. **ID (Instruction Decode / Register Fetch)** – decode opcode, read registers.
3. **EX (Execute)** – perform ALU operation or calculate address.
4. **MEM (Memory Access)** – read/write memory if needed.
5. **WB (Write Back)** – write result to register file.

Timeline diagram (conceptual):

```text
Cycle:   1    2    3    4    5    6
Instr1: IF   ID   EX   MEM  WB
Instr2:      IF   ID   EX   MEM  WB
Instr3:           IF   ID   EX   MEM  WB
...
```

Once pipeline is full, ideally one instruction completes every cycle, increasing throughput.

***

### 3.9 Pipeline hazards

**Hazards** are conditions that prevent the next instruction in the pipeline from executing in its designated clock cycle.

Types:

1. **Structural hazards** – hardware resource conflict (e.g., single memory for both instruction and data access simultaneously).
2. **Data hazards** – instruction depends on result of a previous instruction that has not yet completed.
    - RAW (Read After Write) – most common.
3. **Control hazards** – due to branch and jump instructions (PC may change, making fetched instructions invalid).

Example of data hazard (RAW):

```text
I1: ADD R1, R2, R3   ; R1 = R2 + R3
I2: SUB R4, R1, R5   ; R4 = R1 - R5  (needs result of I1)
```

I2 needs R1’s new value before its EX stage, but I1 may not have written it back yet.

***

### 3.10 Methods to remove/reduce hazards

Common techniques:

- **Stalling / bubbles:** insert NOP cycles until hazard clears (simple but reduces performance).
- **Forwarding / bypassing:** add extra paths from later pipeline stages (EX/MEM/WB) back to earlier stages (EX) so result is used as soon as computed rather than waiting for WB.
- **Separate instruction/data memories:** avoid structural hazards between IF and MEM stages (Harvard‑like organization).
- **Branch prediction:** guess branch outcome; start fetching along predicted path, later flush wrong‑path instructions if prediction was wrong.
- **Delayed branch:** compiler schedules useful instructions in delay slot after branch to reduce penalty.

***

## Unit 4 – Micro‑programmed Control Unit

### 4.1 Basic organization of micro‑programmed controller

In a **micro‑programmed control unit**, the control signals for each step (microoperation) are stored in a special **control memory** as **microinstructions**.

Block diagram:

```text
           +-------------------------+
           |     Control Memory      |
           |  (Microinstructions)    |
           +-----------+-------------+
                       |
                       v
            +---------------------+
            | Control Data Reg.   |--> Control signals to datapath
            +---------------------+
                       ^
                       |
            +----------+----------+
            |  Address Sequencer  |
            |  (next microaddr)   |
            +----------+----------+
                       ^
                       |
                    Micro-PC
```

- Each **machine instruction** (e.g., ADD R1, R2) corresponds to a **microprogram**, i.e., sequence of microinstructions stored in control memory.
- **Address sequencer** decides next microinstruction address (sequential, branch, or based on condition flags).

This design simplifies modification of control logic (change microprogram rather than rewiring hardware) but can be slower than hardwired control.

***

### 4.2 Horizontal vs vertical microinstruction formats

#### 4.2.1 Horizontal microinstructions

- **Wide** microinstruction word with many bits; each bit (or small group) directly controls one signal or microoperation.
- Allows many microoperations in parallel (high degree of parallelism).
- Requires **large control memory** due to wide word length.

Example layout (conceptual):

```text
| Next-addr (n bits) | J bits | Control bits (many lines, each for one op) |
```

#### 4.2.2 Vertical microinstructions

- More **compact** encoding: control field is encoded, not one bit per signal.
- Requires **decoding** logic to generate individual control signals.
- Fewer bits → smaller control memory, but parallelism is limited and extra decode delay is introduced.

Layout example:

```text
| Next-addr | J | ALU-code | Src-reg | Dest-reg | Misc |
```

Here, ALU‑code, Src‑reg, Dest‑reg fields are encoded values; decoder circuits translate them into actual control lines.

***

### 4.3 Address sequencer

The **address sequencer** (micro‑PC logic) chooses the address of the next microinstruction.

Sources for next address:

1. Increment current micro‑PC (next sequential microinstruction).
2. Use address field from microinstruction (microbranch).
3. Use an external mapping from instruction opcode to start address of its microprogram.

The sequencer may also test condition flags (zero, negative, carry, etc.) or external inputs to decide if it should branch or continue sequentially.

***

## Unit 5 – I/O Organization

### 5.1 Strobe‑based communication

In **strobe‑based I/O**, one side (source or destination) uses a single control line (strobe) to indicate that valid data are available or have been accepted.

Two common forms:

1. **Source‑initiated strobe:**
    - Source puts data on bus.
    - Source asserts strobe to tell destination “data valid now”.
2. **Destination‑initiated strobe:**
    - Destination asserts strobe to request data.
    - Source responds by placing data on bus.

Simple timing (source‑initiated):

```text
Data:   ----[valid data]-------------
Strobe: ----____/‾‾‾‾\_______________
```

Advantage: simple; disadvantage: timing must be carefully controlled, and if other side is not ready at strobe time, data may be lost.

***

### 5.2 Handshake‑based communication

To make asynchronous communication more reliable, **handshake protocols** use two lines so both sides signal readiness.

Typical lines:

- `Data Ready` or `VALID` (from sender).
- `ACK` or `READY` (from receiver).

Example protocol (sender–receiver):

1. Sender puts data on bus.
2. Sender sets `VALID = 1`.
3. Receiver waits until `VALID = 1`, reads data, then sets `ACK = 1`.
4. Sender sees `ACK = 1`, clears `VALID`.
5. Receiver sees `VALID = 0`, clears `ACK`.

Timing (conceptual):

```text
Data:   ----[ data ]----------------------
VALID:  ____/‾‾‾‾‾‾‾‾\___________________
ACK:    ________/‾‾‾‾‾‾\________________
```

This allows each side to proceed at its own speed without tight timing requirements.

***

### 5.3 Vector interrupt

In a **vectored interrupt** system, each interrupt source is associated with a unique **vector** (address) of its ISR.

Approaches:

- Hardware provides a vector number, which is used as an index into a vector table holding ISR addresses.
- Or device directly outputs the starting address of ISR on the bus when interrupt is acknowledged.

Advantage: CPU can directly jump to correct ISR without extra polling, reducing latency.

***

### 5.4 Priority interrupt

When several interrupt requests occur simultaneously, **priority interrupt** logic decides which one to service first.

Techniques:

- **Daisy chaining:** devices connected in a chain; highest‑priority device is closest to CPU in chain.
- **Priority encoder:** hardware priority encoder selects highest‑priority active request.
- **Software polling:** CPU checks devices in a pre‑defined priority order in software.

Higher priority devices (e.g., disk, network) are serviced before lower priority ones (e.g., keyboard).

***

### 5.5 DMA‑based transfer

**Direct Memory Access (DMA)** allows data transfer between I/O devices and memory without continuous CPU involvement.

**DMA controller** has registers:

- Starting memory address.
- Transfer count (number of words/bytes).
- Control/status (read/write, channel enable, etc.).

Steps:

1. CPU initializes DMA controller (address, count, direction).
2. DMA requests bus control from CPU (bus request).
3. When CPU grants, DMA performs memory read/write cycles directly (device ↔ memory).
4. After transfer completes, DMA signals CPU via an interrupt.

Diagram:

```text
Device <--> DMA Controller <--> Memory
                     ^
                     |
                    CPU (initializes & later gets interrupt)
```

Advantage: high‑speed block transfer with minimal CPU overhead.

***

## Unit 6 – Programming the Basic Computer

### 6.1 Instruction formats (basic computer)

A **basic computer** model (like in many textbooks) has a small set of instruction formats that encode opcode and operands.

Typical categories (we already saw):

- Three‑address, two‑address, one‑address, zero‑address formats.

Example of one‑address format (accumulator machine):

```text
| opcode (bits) | address (bits) |
```

- ADD X → $AC \leftarrow AC + M[X]$.
- LOAD X → $AC \leftarrow M[X]$.
- STORE X → $M[X] \leftarrow AC$.

***

### 6.2 Addressing modes

**Addressing mode** describes how to interpret the address/operand field of an instruction.

Common addressing modes in your syllabus:

1. **Immediate addressing mode** – the operand is part of the instruction itself.
    - Example (8085‑style): `MVI A, 35H` → A ← 35H.
    - Advantage: fast, operand easily known; disadvantage: more instruction bytes.
2. **Register addressing mode** – operand is in a register.
    - Example: `MOV B, C` → B ← C.
    - Advantage: very fast, uses CPU registers; disadvantage: limited number of registers.
3. **Direct addressing mode** – instruction contains the memory address.
    - Example: `LDA 2000H` → A ← [2000H]; `STA 2000H` → [2000H] ← A.
    - Simple and clear but instruction length is large (3 bytes in 8085).
4. **Indirect addressing mode** – instruction specifies a register whose contents are the memory address.
    - Example: `STAX B` → [BC] ← A (stores A at memory location pointed by BC pair).
    - Useful for arrays, pointers, and loops.
5. **Implied (implicit) addressing mode** – operand is implied by the instruction.
    - Example: `STC` → set Carry flag; `CMC` → complement Carry flag.
    - No explicit operand field; simple one‑byte instructions.

Table summary:

| Mode | Where is operand? | Example |
| :-- | :-- | :-- |
| Immediate | In instruction itself | `MVI A, 35H` |
| Register | In a CPU register | `MOV B, C` |
| Direct | At given memory address | `LDA 2000H` |
| Indirect | At memory address in register | `STAX B` (via BC) |
| Implied | Fixed/implicit (e.g., flag) | `STC`, `CMC` |

***

### 6.3 Instruction codes

An **instruction code** is the actual binary representation stored in memory, containing opcode + operand/address fields.

Example mapping (imaginary):

| Mnemonic | Opcode (binary) | Meaning |
| :-- | :-- | :-- |
| LOAD A,X | 0001 | AC ← M[X] |
| ADD X | 0010 | AC ← AC + M[X] |
| STORE X | 0011 | M[X] ← AC |
| JMP X | 0100 | PC ← X |

Assembler converts mnemonics to these binary instruction codes.

***

### 6.4 Machine language

**Machine language** is the lowest‑level language consisting of binary instruction codes directly executed by the CPU.

- Difficult for humans to read/write.
- Tied to a specific architecture (ISA).
- Example (imaginary): `0010 0000 0010 0101` might mean ADD AC, [0x25].

***

### 6.5 Assembly language

**Assembly language** is a human‑readable representation of machine language using mnemonics and labels.

- Each instruction usually corresponds to one machine instruction.
- An **assembler** translates assembly code into machine code.

Example program (conceptual):

```asm
LOAD A, NUM1    ; AC ← M[NUM1]
ADD  NUM2       ; AC ← AC + M[NUM2]
STORE RESULT    ; M[RESULT] ← AC
HLT
NUM1: .WORD 5
NUM2: .WORD 7
RESULT: .WORD 0
```

Assembler converts labels `NUM1`, `NUM2`, `RESULT` into appropriate addresses.

***

### 6.6 Input‑output programming

CPU can control I/O devices using either **special I/O instructions** or **memory‑mapped I/O**.

Typical forms:

- **Programmed I/O (polling):**
    - CPU repeatedly checks device status register in a loop until device is ready; then reads/writes data.
- **Interrupt‑driven I/O:**
    - CPU does other work; device triggers interrupt when ready; ISR handles the actual data transfer.

Example (simple input–output using polling, pseudo assembly):

```asm
; Read character from input port and echo to output port
WAIT_IN: IN  STATUS_IN      ; read status of input device
         ANI 01H            ; check "data ready" bit
         JZ  WAIT_IN        ; if not ready, loop
         IN  DATA_IN        ; read input data into AC

WAIT_OUT: IN  STATUS_OUT    ; read status of output device
          ANI 01H           ; check "ready" bit
          JZ  WAIT_OUT
          OUT DATA_OUT      ; write AC to output
          HLT
```

Here `IN` and `OUT` are I/O instructions; the exact syntax will differ per architecture but idea is same: poll status then transfer data.
