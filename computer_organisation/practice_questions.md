# Practice Questions with Answers
> Major/DS Course (Core): COMP 5012 (Theory)- Computer Organization

## 0. Index

- [Unit 1 – Introduction](#unit-1--introduction)
- [Unit 2 – Register Transfer and Microoperations](#unit-2--register-transfer-and-microoperations)
- [Unit 3 – CPU Architecture](#unit-3--cpu-architecture)
- [Unit 4 – Micro‑programmed Control Unit](#unit-4--microprogrammed-control-unit)
- [Unit 5 – I/O Organization](#unit-5--io-organization)
- [Unit 6 – Programming the Basic Computer](#unit-6--programming-the-basic-computer)

***
## Unit 1 – Introduction

### 2‑mark questions

**Q1. What is the stored program concept?**

**Ans:** The stored program concept says that both program instructions and data are stored in a common read‑write memory, and the CPU fetches instructions sequentially from this memory to execute them.

***

**Q2. What is the Von‑Neumann bottleneck?**

**Ans:** In Von‑Neumann architecture, program and data share the same memory and bus, so instruction fetch and data access cannot happen simultaneously, limiting throughput. This limitation is called the Von‑Neumann bottleneck.

***

**Q3. Define 2’s complement of a binary number.**

**Ans:** The 2’s complement of a binary number is obtained by inverting all its bits (1’s complement) and then adding 1 to the least significant bit. It is widely used to represent signed integers and perform subtraction.

***

### 5‑mark questions

**Q4. Explain the difference between 1’s complement and 2’s complement representations with example.**

**Ans:**

- In 1’s complement, negative numbers are represented by inverting all bits of the positive number; there are two representations of zero (positive and negative zero).
- In 2’s complement, negative numbers are represented by taking the 1’s complement and adding 1; there is only one zero and arithmetic hardware is simpler.
- Example with 4 bits: $+5 = 0101$.
    - 1’s complement of 5: 1010 (represents −5 in 1’s complement).
    - 2’s complement of 5: 1011 (represents −5 in 2’s complement).

***

**Q5. Describe the main components of a Von‑Neumann computer with a neat block diagram.**

**Ans:**

- Components: CPU (Control Unit, ALU, internal registers), main memory, input devices, output devices, and system buses (address, data, control).
- CPU fetches instructions from main memory using PC, decodes them in Control Unit, performs operations in ALU, and exchanges data and control signals with memory and I/O over buses.
- A standard block diagram shows CPU connected to memory and I/O via a common bus structure.

***

### 10‑mark question

**Q6. Explain the evolution of computer hardware from first‑generation to modern microprocessor systems. Highlight changes in technology, size, speed, and reliability.**

**Ans (points to cover):**

- 1st generation: vacuum tubes, huge size, high power consumption, frequent failures; programming via machine code and wiring.
- 2nd generation: transistors replaced tubes – smaller, more reliable, less heat, faster; introduction of assembly and early high‑level languages.
- 3rd generation: SSI/MSI ICs on a chip, minicomputers, better performance and cost; operating systems become more common.
- 4th generation: VLSI chips and microprocessors, personal computers, workstations; large main memory and disks, GUIs.
- 5th and later: multi‑core CPUs, SoCs, embedded systems, smartphones; high parallelism, integration of CPU, GPU, memory controllers on a single chip.
- Throughout generations: increase in speed, capacity, reliability, and portability; fall in cost per computation.

***

## Unit 2 – Register Transfer and Microoperations

### 2‑mark questions

**Q7. What is a microoperation? Give one example.**

**Ans:** A microoperation is a basic operation performed on data stored in registers, such as transfer, arithmetic, logic, or shift, that is completed in one clock cycle. For example, $R2 \leftarrow R1$ copies the contents of register R1 into R2.

***

**Q8. Write RTL for conditional transfer of data from R1 to R2 under control signal P.**

**Ans:** The RTL notation is:
$P: R2 \leftarrow R1$
This means “if P = 1, then on the next clock edge, R2 is loaded with the contents of R1.”

***

### 5‑mark questions

**Q9. Explain with a diagram how an internal bus is used to transfer data among registers.**

**Ans:**

- In a bus‑based organization, each register output connects to a common **data bus** via tri‑state drivers or multiplexers; only one register is enabled at a time to place its data on the bus.
- A destination register has a load control signal; when enabled, it latches the bus value on the active clock edge.
- Diagram: several registers (R1, R2, R3, …) connected to a shared internal bus, which also connects to the ALU input; control lines EnR1, EnR2, etc. select which register drives the bus.

***

**Q10. Differentiate between arithmetic, logic, and shift microoperations with examples.**

**Ans:**

- **Arithmetic microoperations** perform arithmetic operations like add, subtract, increment, and decrement, e.g., $R3 \leftarrow R1 + R2$.
- **Logic microoperations** perform bitwise logical operations such as AND, OR, XOR, NOT, e.g., $R3 \leftarrow R1 \land R2$.
- **Shift microoperations** move bits left or right within a register, including logical, arithmetic, and rotate shifts, e.g., logical shift left: $R1 \leftarrow shl(R1)$.

***

### 10‑mark question

**Q11. Describe in detail Register Transfer Language (RTL). Explain bus transfer, memory read/write, and timing of register transfer operations using suitable examples and diagrams.**

**Ans (points to cover):**

- Define RTL as a symbolic notation to describe microoperations on registers, where left side is destination and right side is source/expression, optionally preceded by condition (e.g., $T_0: MAR \leftarrow PC$).
- Show **bus transfer**: how enabling one register to drive the bus and enabling another to load from the bus implements $R2 \leftarrow R1$; include a small bus diagram (registers + internal bus + control lines).
- Explain **memory read**:
    - $MAR \leftarrow R1$; `MDR ← M[MAR]`; $R2 \leftarrow MDR$.
- Explain **memory write**:
    - $MAR \leftarrow R1$; $MDR \leftarrow R2$; `M[MAR] ← MDR`.
- Discuss **timing**: synchronous operation with system clock; microoperations occur on clock edges when corresponding control signals are asserted; briefly sketch a timing chart showing clock, control signal, and resulting transfer.

***

## Unit 3 – CPU Architecture

### 2‑mark questions

**Q12. What is an instruction format?**

**Ans:** An instruction format is the structure or layout of bits in an instruction word, typically including fields for opcode, addressing mode, registers, and address or immediate data.

***

**Q13. What is an instruction cycle?**

**Ans:** An instruction cycle is the complete sequence of operations performed by the CPU to fetch, decode, and execute a single instruction, including operand access, result write‑back, and possible interrupt check.

***

### 5‑mark questions

**Q14. Explain the steps involved in the fetch cycle of a typical CPU.**

**Ans:**

- **Step 1:** PC contents are sent to MAR: $MAR \leftarrow PC$.
- **Step 2:** A memory read is initiated; instruction word at address MAR is placed into MDR (or instruction buffer).
- **Step 3:** Instruction is transferred from MDR to IR: $IR \leftarrow MDR$.
- **Step 4:** PC is incremented to point to the next instruction: $PC \leftarrow PC + 1$.
- After this, the decode and execute phases operate on the instruction in IR.

***

**Q15. Compare three‑address, two‑address, one‑address, and zero‑address instruction formats with examples.**

**Ans:**

- **Three‑address:** has three operand fields; e.g. `ADD R1, R2, R3` → $R1 \leftarrow R2 + R3$; flexible but instruction is long.
- **Two‑address:** has two operand fields; e.g. `ADD R1, R2` → $R1 \leftarrow R1 + R2$; saves bits but one source is overwritten.
- **One‑address:** uses accumulator plus one memory address; e.g. `ADD X` → $AC \leftarrow AC + M[X]$; shorter instructions but fewer registers.
- **Zero‑address:** stack‑organized; operands are implicitly on stack top; e.g. `ADD` pops two values, pushes result; no operand fields but requires stack machine.

***

### 10‑mark question

**Q16. Explain in detail the stages of instruction execution using an instruction cycle diagram. Show the microoperations for a memory‑reference instruction (e.g., LOAD R1, X).**

**Ans (points to cover):**

- Draw/describe instruction cycle diagram: fetch, decode, effective address calculation, execute, write‑back, interrupt check.
- Describe **fetch microoperations**:
    - $T_0: MAR \leftarrow PC$
    - $T_1: MDR \leftarrow M[MAR]$
    - $T_2: IR \leftarrow MDR,\; PC \leftarrow PC + 1$.
- **Decode stage:** opcode and addressing mode bits in IR are interpreted by control unit.
- **Effective address calculation** if required (e.g., for indirect/direct addressing).
- **Execute (LOAD R1, X)**:
    - $T_3: MAR \leftarrow X$ (direct) or MAR ← M[addr] (indirect).
    - $T_4: MDR \leftarrow M[MAR]$.
    - $T_5: R1 \leftarrow MDR$.
- Mention how condition codes/flags may be set and then CPU returns to fetch next instruction.

***

## Unit 4 – Micro‑programmed Control Unit

### 2‑mark questions

**Q17. What is a microprogram?**

**Ans:** A microprogram is a sequence of microinstructions stored in control memory, each microinstruction specifying control signals for datapath microoperations to implement one machine‑level instruction.

***

**Q18. Distinguish between horizontal and vertical microinstructions.**

**Ans:** Horizontal microinstructions are wide words with many control bits directly controlling multiple microoperations in parallel, while vertical microinstructions use compact encoded fields that must be decoded, resulting in narrower control words but less parallelism.

***

### 5‑mark questions

**Q19. Draw and explain the basic organization of a micro‑programmed control unit.**

**Ans:**

- Draw a block diagram showing: control memory (ROM/PLA) storing microinstructions, micro‑PC (address register), address sequencer, control data register (holding current microinstruction), and generation of control signals to datapath.
- Explain that on each microcycle:
    - Micro‑PC supplies address to control memory.
    - Microinstruction is read into control data register.
    - Control fields generate control lines for buses, ALU, registers, etc.
    - Address sequencer determines next micro‑address (sequential or branched based on microinstruction or flags).

***

**Q20. What is an address sequencer in a microprogrammed control unit? Explain its role.**

**Ans:**

- Address sequencer is the hardware that decides the **next microinstruction address** for the control memory.
- It can: increment the current micro‑PC for sequential execution, load a new address from a microinstruction field for micro‑branches, or load a starting address based on machine opcode.
- It may also test condition flags or external signals (e.g., carry, zero) to choose between different micro‑branch targets.

***

### 10‑mark question

**Q21. Compare horizontal and vertical microprogramming, and discuss the trade‑offs involved in control memory size and execution speed.**

**Ans (points to cover):**

- **Horizontal microprogramming:**
    - Very wide microinstruction word; each microoperation/control line has a dedicated bit.
    - Allows many microoperations to be issued in parallel → higher potential speed.
    - Requires large control memory (more bits per instruction) and more complex wiring.
- **Vertical microprogramming:**
    - Microinstruction has encoded fields for ALU operation, source/destination registers, etc.; requires decoders.
    - Narrower words → smaller control memory, easier to modify.
    - Less parallelism and extra decoding delay; may need multiple microinstructions for same effect.
- Trade‑off: design chooses between memory usage and performance; some systems use **mixed** (quasi‑horizontal) formats.

***

## Unit 5 – I/O Organization

### 2‑mark questions

**Q22. What is the main idea of handshake‑based I/O communication?**

**Ans:** Handshake‑based I/O uses two control lines (e.g., VALID and ACK) so that both sender and receiver can signal readiness, allowing asynchronous and reliable data transfer without fixed timing assumptions.

***

**Q23. What is DMA?**

**Ans:** Direct Memory Access (DMA) is a technique where a special controller transfers blocks of data directly between memory and I/O devices, temporarily taking over the system bus so the CPU is free from handling each individual word transfer.

***

### 5‑mark questions

**Q24. Distinguish between strobe‑based and handshake‑based data transfer.**

**Ans:**

- **Strobe‑based:** uses a single control line (strobe) from either source or destination to indicate that data is valid or requested; simple hardware, but if the other side is not ready at the strobe time, data may be lost or mis‑read.
- **Handshake‑based:** uses two lines (VALID and ACK/READY); sender asserts VALID when data is ready, receiver asserts ACK after reading; both can wait for each other, providing reliable synchronization across different speeds.

***

**Q25. Explain the working of a DMA controller with a neat block diagram.**

**Ans:**

- Draw DMA controller with registers: address register, word count, control/status, and lines to memory and I/O device.
- Steps:
    - CPU initializes DMA with starting address, transfer count, and direction (read/write).
    - DMA requests bus from CPU (BUS REQUEST); CPU acknowledges (BUS GRANT).
    - DMA performs memory read/write cycles directly with the device, decrementing count and incrementing address.
    - When transfer completes, DMA raises an interrupt to inform CPU.

***

### 10‑mark question

**Q26. What are vectored and priority interrupts? Explain with suitable diagrams and examples how a system can implement priority among multiple interrupting devices.**

**Ans (points to cover):**

- **Vectored interrupts:** each interrupt source has a distinct vector that points to its ISR address, implemented via a vector table or device‑supplied address.
- **Non‑vectored:** CPU always jumps to a fixed address and software must determine the source.
- **Priority interrupts:** hardware or software decides which interrupt is serviced first when multiple requests occur.
    - Hardware methods:
        - Daisy chain (closest device to CPU has highest priority).
        - Priority encoder: combinational logic encodes highest‑priority active request.
    - Software methods: CPU polls devices in priority order.
- Include small diagrams: daisy chain connection and priority encoder block; mention that high‑priority devices like disks or network may pre‑empt lower priority like keyboard.

***

## Unit 6 – Programming the Basic Computer

### 2‑mark questions

**Q27. What is machine language?**

**Ans:** Machine language is a set of binary instruction codes directly executed by the CPU; each instruction encodes an operation and its operands in the specific ISA format.

***

**Q28. What is immediate addressing mode? Give an example.**

**Ans:** In immediate addressing mode, the operand value itself is contained in the instruction, not at some memory address. Example (8085‑style): `MVI A, 35H` loads hexadecimal 35 directly into accumulator A.

***

### 5‑mark questions

**Q29. Explain different addressing modes used in a basic computer with suitable examples.**

**Ans:**

- **Immediate:** operand is in the instruction; e.g., `MVI A, 35H`.
- **Register:** operand in register; e.g., `MOV B, C`.
- **Direct:** address field gives memory address; e.g., `LDA 2000H`.
- **Indirect:** address field names a register that holds the effective memory address; e.g., `STAX B` stores A at address contained in BC pair.
- **Implied:** operand is implicit; e.g., `STC` sets Carry flag.
Explain where each is useful: immediate for constants, register for fast operations, direct for single known locations, indirect for arrays/pointers, implied for flags and accumulator operations.

***

**Q30. Differentiate between machine language and assembly language.**

**Ans:**

- Machine language:
    - Pure binary codes; directly executed by CPU.
    - Hard for humans to read/write and debug.
- Assembly language:
    - Uses symbolic mnemonics (ADD, MOV, JMP) and labels.
    - Easier to program and understand; requires an assembler to translate to machine code.
- Both are low‑level and architecture‑specific, but assembly is more user‑friendly.

***

### 10‑mark question

**Q31. For a simple accumulator‑based basic computer, write and explain an assembly program to add two numbers stored in memory locations NUM1 and NUM2 and store the result at SUM. Show the corresponding instruction formats and explain the addressing modes used.**

**Ans (points to cover):**

- Assume one‑address format: `opcode` + `address`.
- Sample program (pseudo‑assembly):

```asm
LOAD NUM1     ; AC ← M[NUM1]
ADD  NUM2     ; AC ← AC + M[NUM2]
STORE SUM     ; M[SUM] ← AC
HLT
NUM1: .WORD 05H
NUM2: .WORD 07H
SUM:  .WORD 00H
```

- Explain each step:
    - `LOAD NUM1`: direct addressing, loads AC with the value at memory label NUM1.
    - `ADD NUM2`: direct addressing, adds M[NUM2] to AC, result in AC.
    - `STORE SUM`: direct addressing, stores AC into M[SUM].
- Show generic one‑address instruction format and how opcode and address field are filled for each instruction.
- Mention that labels NUM1, NUM2, SUM are converted by assembler into actual addresses in the instruction fields.
