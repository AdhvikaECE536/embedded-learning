
## Week 1: C Revision & Linux Environment
*Goal: You can write C without segfaults. You are comfortable in the terminal.*

### Day 1 — Setup & The Basics
| Block | Task |
|-------|------|
| **C Drill** | Write a program that reads 5 integers into an array and prints them in reverse. |
| **Theory** | Install Ubuntu (or VM). Open terminal. Learn: `cd`, `ls`, `pwd`, `mkdir`, `rm`, `touch`, `man`. |
| **Practice** | Write `hello.c`. Compile with `gcc hello.c -o hello`. Run `./hello`. |
| **Deliverable** | A folder `~/systems-lab/week1/` with 3 C files: `hello.c`, `reverse_array.c`, `sum_digits.c`. |

### Day 2 — Functions, Arrays, Strings
| Block | Task |
|-------|------|
| **C Drill** | Write `int max_of_three(int a, int b, int c)` and call it from `main`. |
| **Theory** | K&R C Chapter 1 (functions, arrays). Watch: NPTEL C Programming Lec 1 (1.5× speed). |
| **Practice** | Write a program that takes a string from `stdin` and counts vowels, consonants, digits. Do **not** use `strlen` from library; write your own `my_strlen`. |
| **Deliverable** | `string_stats.c` that works with `scanf("%s", str)` (assume no spaces for now). |

### Day 3 — Pointers (The Rusty Part)
| Block | Task |
|-------|------|
| **C Drill** | Given `int a = 5; int *p = &a;`, write a program that prints `a`, `&a`, `p`, `*p`, `&p`. |
| **Theory** | K&R Chapter 5 (pointers). Focus: `&` and `*`, pointer arithmetic, `*(arr + i)` vs `arr[i]`. |
| **Practice** | Rewrite `reverse_array.c` from Day 1 using **only pointers** (no `[]` brackets). Then write `swap(int *a, int *b)` and swap two variables in `main`. |
| **Deliverable** | `pointer_reverse.c`, `swap.c`. |

### Day 4 — Structures & typedef
| Block | Task |
|-------|------|
| **C Drill** | Create a `struct Point { int x; int y; };`. Write a function `float distance(struct Point a, struct Point b)`. |
| **Theory** | K&R Chapter 6 (structures). |
| **Practice** | Build a `struct Student { int id; char name[50]; float marks[5]; };`. Write functions to: (1) input one student, (2) print one student, (3) calculate average marks. |
| **Deliverable** | `student_struct.c`. |

### Day 5 — File I/O
| Block | Task |
|-------|------|
| **C Drill** | Write a program that writes the first 10 squares into a file `squares.txt`. |
| **Theory** | `fopen`, `fprintf`, `fscanf`, `fclose`, `feof`. |
| **Practice** | Write a program that reads `students.txt` (CSV format: `id,name,mark1,mark2,mark3`) and prints the student with highest average. |
| **Deliverable** | `file_student.c` + `students.txt` (create dummy data). |

### Day 6 — Linux Tools: gcc, make, gdb
| Block | Task |
|-------|------|
| **C Drill** | Debug a program with a missing `&` in `scanf`. Fix it. |
| **Theory** | Learn `gcc` flags: `-Wall`, `-Wextra`, `-g`, `-O2`. Learn `make` basics. |
| **Practice** | Write a `Makefile` that compiles all your Week 1 files. Then debug `pointer_reverse.c` using GDB: set breakpoint at `swap`, print pointer values, step through. |
| **Commands** | `gdb ./pointer_reverse` → `break swap` → `run` → `print *a` → `step` → `continue`. |
| **Deliverable** | A working `Makefile` and a screenshot/txt of your GDB session. |

### Day 7 — Mini Project: Console Student DB
| Block | Task |
|-------|------|
| **C Drill** | None. Focus on project. |
| **Practice** | Combine Days 4–6: a menu-driven program: `1. Add Student`, `2. View All`, `3. Save to File`, `4. Load from File`, `5. Exit`. Use `malloc` to hold up to 100 students dynamically. |
| **Deliverable** | `student_db.c`. Run it. Add 3 students. Save. Exit. Re-run. Load. Verify data persists. |

**Week 1 Checkpoint:** You have a GitHub repo? Push this folder now. If not, create one next week.

---

## Week 2: Memory, Pointers-Deep, and First Taste of OS
*Goal: You own pointers. You understand `malloc`. You have seen `fork()`.*

### Day 8 — Dynamic Memory
| Block | Task |
|-------|------|
| **C Drill** | Allocate an array of 10 integers using `malloc`. Fill it. Free it. |
| **Theory** | `malloc`, `calloc`, `realloc`, `free`. Memory leaks. |
| **Practice** | Rewrite your Student DB to use a **linked list** instead of a fixed array. Each node is `malloc`'d. |
| **Deliverable** | `student_list.c` with `insert_student()`, `print_all()`, `free_all()`. |

### Day 9 — Pointer-to-Pointer & Function Pointers
| Block | Task |
|-------|------|
| **C Drill** | Write a function `void scale(int *x, int factor)` that multiplies `*x` by `factor`. |
| **Theory** | `int **pp`, function pointers `void (*fp)(int)`. |
| **Practice** | Write a generic `foreach(int *arr, int n, void (*op)(int *))` that applies `op` to every element. Test with `increment` and `square` functions. |
| **Deliverable** | `generic_foreach.c`. |

### Day 10 — String Manipulation From Scratch
| Block | Task |
|-------|------|
| **C Drill** | Implement `void my_strcpy(char *dest, const char *src)`. |
| **Theory** | Pointer arithmetic on strings. `const` correctness. |
| **Practice** | Implement `my_strlen`, `my_strcpy`, `my_strcmp`, `my_strcat`. Do **not** use `<string.h>`. Write a test harness that compares your output against the standard library. |
| **Deliverable** | `my_string.c` + `my_string.h`. |

### Day 11 — The Linked List (Systems Interview Classic)
| Block | Task |
|-------|------|
| **C Drill** | Draw a linked list of 3 nodes on paper. Label pointers. |
| **Theory** | Singly linked list: insert at head, delete by value, reverse. |
| **Practice** | Implement all three operations. Then write a recursive `print_list` and recursive `free_list`. |
| **Deliverable** | `linked_list.c` with `insert_head`, `delete_val`, `reverse_iterative`, `reverse_recursive`. |

### Day 12 — Processes: fork, exec, wait
| Block | Task |
|-------|------|
| **C Drill** | None. New concept. |
| **Theory** | Silberschatz Ch 3 (Process Concept). `fork()`, `getpid()`, `getppid()`, `wait()`. |
| **Practice** | Write `fork_demo.c`: Parent forks. Child prints its PID and exits with code 5. Parent waits, captures exit status with `WEXITSTATUS`, prints it. |
| **Deliverable** | `fork_demo.c`. Run it. Verify output. |

### Day 13 — Git & GitHub
| Block | Task |
|-------|------|
| **C Drill** | None. |
| **Theory** | Git basics: `init`, `add`, `commit`, `push`, `log`. |
| **Practice** | Initialize a repo `systems-lab`. Commit all Week 1–2 code. Create a GitHub repo. Push. Write a `README.md` listing what each file does. |
| **Deliverable** | Your code is on GitHub. |

### Day 14 — Mini Project: A Tiny Shell
| Block | Task |
|-------|------|
| **Practice** | Write `microshell.c` that: (1) prints `> ` prompt, (2) reads command with `fgets`, (3) forks, (4) child does `execlp(command, command, NULL)`, (5) parent waits. Support `exit` to quit. |
| **Stretch** | If time permits, support one pipe: `cmd1 | cmd2` (use `pipe()` + `dup2()`). |
| **Deliverable** | `microshell.c`. Test with `./microshell` → `ls` → `date` → `exit`. |

**Week 2 Checkpoint:** You have pushed C code to GitHub. You have written a linked list from scratch. You have created a process.

---

## Week 3: Digital Logic (Logisim-Evolution)
*Goal: You think in gates. You rest from C syntax but keep the C drill alive.*

> **Install:** `logisim-evolution` (free, Java-based). Do not use the old dead Logisim.

### Day 15 — Gates & Boolean Algebra
| Block | Task |
|-------|------|
| **C Drill** | Write a function `int is_power_of_two(unsigned int n)` using bit manipulation. |
| **Theory** | Boolean algebra: AND, OR, NOT, NAND, NOR, XOR. De Morgan’s laws. |
| **Practice** | In Logisim: build a circuit with 2 switches → AND gate → LED. Then build OR, NOT, XOR. Then build AND, OR, NOT using **only NAND gates**. |
| **Deliverable** | `gates_nand_only.circ` file. |

### Day 16 — Adders
| Block | Task |
|-------|------|
| **C Drill** | Write a program that adds two binary strings (as `char[]`) and prints the sum binary string. |
| **Theory** | Half adder (2 inputs, 2 outputs), Full adder (3 inputs, 2 outputs). |
| **Practice** | Build a half-adder in Logisim. Build a full-adder in Logisim. Then build a **4-bit ripple-carry adder** by chaining 4 full adders. Test all 16+16 combinations (or spot-check key ones). |
| **Deliverable** | `adder_4bit.circ`. |

### Day 17 — Multiplexers & Demultiplexers
| Block | Task |
|-------|------|
| **C Drill** | Write a function `int select(int a, int b, int sel)` that returns `b` if `sel==1`, else `a`. (This is a 2:1 MUX in C). |
| **Theory** | MUX: many inputs, one output, select lines. DEMUX: one input, many outputs. |
| **Practice** | Build a 2:1 MUX (1 select line, 2 data inputs). Build a 4:1 MUX (2 select lines). Build a 1:2 DEMUX. |
| **Deliverable** | `mux_demux.circ`. |

### Day 18 — Decoder & Encoder
| Block | Task |
|-------|------|
| **C Drill** | Write a program that takes an integer 0–7 and prints which bit is high (like a 3-to-8 decoder). |
| **Theory** | 2-to-4 decoder, 4-to-2 encoder, priority encoder. |
| **Practice** | Build a 2-to-4 decoder in Logisim. Build a 4-to-2 encoder. |
| **Deliverable** | `decoder_encoder.circ`. |

### Day 19 — Arithmetic Logic Unit (ALU)
| Block | Task |
|-------|------|
| **C Drill** | Write a simple ALU in C: `int alu(int a, int b, int op)` where `0=ADD, 1=SUB, 2=AND, 3=OR`. |
| **Theory** | ALU: arithmetic + logic unit. Select operation via control lines. |
| **Practice** | Build a **4-bit ALU** in Logisim. Inputs: two 4-bit numbers A and B. Control: 2-bit `op`. Output: 4-bit `Result`. Operations: ADD (use your ripple adder), AND, OR, NOT A. Add a `Zero` flag LED (lights up if result is 0). |
| **Deliverable** | `alu_4bit.circ`. |

### Day 20 — Review & C Connection
| Block | Task |
|-------|------|
| **C Drill** | Write a program that simulates a 1-bit full adder using boolean logic in C (no `+` operator for the bit; use `&`, `\|`, `^`). |
| **Practice** | Document your ALU: draw the block diagram on paper. Label every wire. Then write a C struct that represents the ALU state: `struct ALU { int a[4]; int b[4]; int op; int result[4]; int zero; };`. |
| **Deliverable** | A photo/scan of your ALU diagram + `alu_simulator.c`. |

### Day 21 — Rest / Catch-up
| Block | Task |
|-------|------|
| **Practice** | If behind, finish ALU. If ahead, build an 8-bit ALU by cascading two 4-bit ALUs. |
| **Deliverable** | Nothing new. Just polish. |

**Week 3 Checkpoint:** Can you build an ALU from gates? Can you explain the difference between a MUX and a DEMUX?

---

## Week 4: Sequential Logic & FSMs
*Goal: You understand clocks, memory, and state machines.*

### Day 22 — Flip-Flops
| Block | Task |
|-------|------|
| **C Drill** | Write a program that toggles a boolean flag every time you press Enter (simulating a T flip-flop). |
| **Theory** | SR latch, D flip-flop, JK flip-flop. Clock, edge-triggering. |
| **Practice** | In Logisim: build a D flip-flop using NAND gates and a clock. Add a D input and a Clock input. Verify Q updates only on clock edge. |
| **Deliverable** | `d_flipflop.circ`. |

### Day 23 — Registers & Counters
| Block | Task |
|-------|------|
| **C Drill** | Write a circular buffer (ring buffer) of size 8 in C. `enqueue` and `dequeue` with indices. |
| **Theory** | Shift register, binary counter, ripple counter. |
| **Practice** | Build a 4-bit register (4 D flip-flops with common clock). Build a 4-bit up-counter (increments every clock tick). Add a synchronous `Load` input to load a value. |
| **Deliverable** | `register_4bit.circ`, `counter_4bit.circ`. |

### Day 24 — Finite State Machines (Theory)
| Block | Task |
|-------|------|
| **C Drill** | Write a C program that reads a string and detects if it contains the substring "1011" (simulate FSM logic with `if-else`). |
| **Theory** | Moore vs Mealy. State diagram, state table, state assignment. |
| **Practice** | Draw the state diagram for a **sequence detector** that detects `1011` in a serial bit stream. Draw the state table. |
| **Deliverable** | A clear hand-drawn state diagram + state table (photo it, save it). |

### Day 25 — FSM in Logisim (Moore)
| Block | Task |
|-------|------|
| **C Drill** | None. |
| **Theory** | Moore machine: output depends only on state. |
| **Practice** | Build the `1011` sequence detector as a Moore machine in Logisim. Use a register to hold state. Use a combinational circuit to compute next state. Output a LED that turns ON when `1011` is detected. Test with a manual clock and a sequence of bits. |
| **Deliverable** | `fsm_moore_1011.circ`. |

### Day 26 — C Recursion Revision (The Stack Connection)
| Block | Task |
|-------|------|
| **C Drill** | Write recursive factorial. Add `printf` at entry and exit to show call depth. |
| **Theory** | How function calls use the stack. Return address, local variables, parameters. |
| **Practice** | Write recursive `int fib(int n)`. Count how many times it calls itself. Then write a recursive function to reverse a linked list. |
| **Deliverable** | `recursion_stack.c` with factorial + fib + list reverse. |

### Day 27 — FSM in Logisim (Mealy) + C Comparison
| Block | Task |
|-------|------|
| **C Drill** | Write a Mealy-style parser in C: read chars one by one, set a flag immediately when "1011" is seen (no waiting for next state). |
| **Theory** | Mealy machine: output depends on state + input. |
| **Practice** | Build the same `1011` detector as a Mealy machine. Compare with Moore: fewer states? Faster output? Document differences. |
| **Deliverable** | `fsm_mealy_1011.circ` + a text file `moore_vs_mealy.txt` explaining differences. |

### Day 28 — Review & Integration
| Block | Task |
|-------|------|
| **Practice** | Build a **vending machine FSM** in Logisim: accepts 5 and 10 rupee coins. Dispenses when total ≥ 15. Returns change if overpaid. Use 2-bit inputs (00=nothing, 01=5, 10=10) and 2-bit outputs (00=none, 01=5change, 10=item, 11=item+5change). |
| **Deliverable** | `vending_machine.circ`. |

**Week 4 Checkpoint:** Can you draw a state diagram? Can you explain why a D flip-flop is edge-triggered? Can you write recursive C?

---

## Week 5: MIPS Assembly — The Bridge
*Goal: You see how C becomes hardware instructions. You write real assembly.*

> **Install:** MARS MIPS Simulator (Java `.jar`). Also install Java if not present.

### Day 29 — MIPS Intro & First Programs
| Block | Task |
|-------|------|
| **C Drill** | Write a C program that does `int a=5, b=7, c=a+b; printf("%d", c);`. You will translate this to MIPS today. |
| **Theory** | MIPS registers (`$zero`, `$t0-$t9`, `$s0-$s7`, `$a0-$a3`, `$v0-$v1`, `$sp`, `$ra`). R-format vs I-format. |
| **Practice** | In MARS: write `add_two.asm`. Load 5 into `$t0`, 7 into `$t1`, add into `$t2`, print using syscall. Run step-by-step. Watch registers. |
| **Deliverable** | `add_two.asm`, `add_array.asm` (add 5 numbers from a `.word` array). |

### Day 30 — Load/Store & Addressing
| Block | Task |
|-------|------|
| **C Drill** | Write a C program that iterates an array using pointer arithmetic: `*(arr + i)` instead of `arr[i]`. |
| **Theory** | `lw`, `sw`, `lb`, `sb`. Base + offset addressing. |
| **Practice** | Write `array_sum.asm`: define `.word 3, 1, 4, 1, 5, 9, 2, 6`. Compute sum in a loop. Use a pointer (`$t0` as base, increment by 4 each iteration). |
| **Deliverable** | `array_sum.asm`. |

### Day 31 — Branching & Loops
| Block | Task |
|-------|------|
| **C Drill** | Write `for`, `while`, and `do-while` loops in C for the same task (count 1 to 10). |
| **Theory** | `beq`, `bne`, `slt`, `slti`, `j`, `bgtz`, labels. |
| **Practice** | Write `find_max.asm`: find maximum in an array of 8 integers. Write `count_evens.asm`: count even numbers in an array. |
| **Deliverable** | `find_max.asm`, `count_evens.asm`. |

### Day 32 — Logical Ops & Bit Manipulation
| Block | Task |
|-------|------|
| **C Drill** | Write C functions: `is_even(int x)` using `x & 1`, `set_bit(int x, int n)`, `clear_bit(int x, int n)`. |
| **Theory** | `and`, `or`, `nor`, `xor`, `sll`, `srl`, `sra`. |
| **Practice** | Write `bit_ops.asm`: implement AND, OR, XOR, shift-left on two registers. Then write `parity.asm`: compute even parity of a 32-bit word. |
| **Deliverable** | `bit_ops.asm`, `parity.asm`. |

### Day 33 — C → MIPS Translation (Paper + MARS)
| Block | Task |
|-------|------|
| **C Drill** | Write a C function `int sum_of_squares(int n)` that returns `1² + 2² + ... + n²`. |
| **Theory** | Mapping C variables to registers. Mapping C loops to branch instructions. |
| **Practice** | On paper, translate your C function line-by-line to MIPS. Then type it into MARS. Run it for `n=5` (expected 55). Debug any mismatch. |
| **Deliverable** | Photo of your handwritten translation + `sum_of_squares.asm`. |

### Day 34 — System Calls & I/O
| Block | Task |
|-------|------|
| **C Drill** | Write a C program that reads an integer and a string, then prints both. |
| **Theory** | MIPS syscalls: 1 (print int), 4 (print string), 5 (read int), 8 (read string), 10 (exit). |
| **Practice** | Write `interactive.asm`: prompt user for 5 integers (one by one), store them in an array, print the array back, print the sum. |
| **Deliverable** | `interactive.asm`. |

### Day 35 — Mini Project: MIPS String Reversal
| Block | Task |
|-------|------|
| **Practice** | Write `reverse_string.asm`: read a string (max 20 chars), reverse it in place using a loop, print reversed string. Do not use a second array; swap characters from both ends. |
| **Deliverable** | `reverse_string.asm`. |

**Week 5 Checkpoint:** Can you write a loop in MIPS? Can you translate a simple C function to assembly by hand?

---

## Week 6: MIPS Procedures, Stack, and C Connection
*Goal: You understand how C function calls actually work at the machine level.*

### Day 36 — Procedures: `jal`, `jr`, `$ra`
| Block | Task |
|-------|------|
| **C Drill** | Write a C program with a function `int add(int x, int y)` called from `main`. Draw the stack frame on paper. |
| **Theory** | `jal` (jump and link), `jr $ra`. The `$ra` register. |
| **Practice** | Write `proc_add.asm`: `main` calls `add` with two immediates. `add` returns sum in `$v0`. `main` prints it. Trace `$ra` in MARS. |
| **Deliverable** | `proc_add.asm`. |

### Day 37 — Stack Frames & Saving Registers
| Block | Task |
|-------|------|
| **C Drill** | Write a C function that has 4 local variables and calls another function. |
| **Theory** | Stack pointer `$sp`. Saving `$ra`, `$s` registers. Stack frame layout. |
| **Practice** | Write `proc_nested.asm`: `main` calls `foo`, `foo` calls `bar`. `bar` returns a value. Ensure all `$ra` and `$s` registers are saved/restored properly. Use MARS to watch the stack segment (`0x7fff...`) grow and shrink. |
| **Deliverable** | `proc_nested.asm` + a text file `stack_trace.txt` showing `$sp` values at each call. |

### Day 38 — Recursive Factorial in MIPS
| Block | Task |
|-------|------|
| **C Drill** | Write recursive factorial in C. Add `printf("Enter n=%d\n", n)` at every call. |
| **Theory** | Recursion in assembly: base case, recursive case, saving `$ra` and argument registers on stack. |
| **Practice** | Write `fact.asm`: recursive factorial. Test with `n=0`, `n=1`, `n=5`, `n=7`. Watch `$sp` in MARS. Count how many words are pushed per call. |
| **Deliverable** | `fact.asm`. |

### Day 39 — Disassembly: C to MIPS (Compiler Explorer)
| Block | Task |
|-------|------|
| **C Drill** | Write a C program: `int square(int x) { return x*x; } int main() { return square(5); }` |
| **Theory** | How a compiler maps C to assembly. Optimizations (`-O0` vs `-O2`). |
| **Practice** | Go to **godbolt.org**. Select compiler `mips gcc`. Paste your C code. Compare compiler output with your hand-written `fact.asm` from Day 38. Notice: how does the compiler save registers? Does it use `$t` or `$s`? |
| **Deliverable** | Screenshot of Godbolt output + a text file `compiler_vs_manual.txt` listing 3 differences. |

### Day 40 — Frame Pointer & Local Variables
| Block | Task |
|-------|------|
| **C Drill** | Write a C function with 2 local arrays of size 4. Print addresses of locals to see stack layout. |
| **Theory** | Frame pointer `$fp`. Accessing locals via negative offsets from `$fp`. |
| **Practice** | Write `fp_demo.asm`: a function that allocates 3 words on the stack for local variables, uses them, then restores `$sp`. Use `$fp` to access them. |
| **Deliverable** | `fp_demo.asm`. |

### Day 41 — String Operations in MIPS
| Block | Task |
|-------|------|
| **C Drill** | Revisit your `my_strlen` from Day 10. Imagine translating it to MIPS. |
| **Theory** | Byte addressing (`lb`, `sb`). Null terminator `0x00`. |
| **Practice** | Write `mips_strlen.asm`: takes address of string in `$a0`, returns length in `$v0`. Write `mips_strcpy.asm`: copy string from `$a0` to `$a1`. |
| **Deliverable** | `mips_strlen.asm`, `mips_strcpy.asm`. |

### Day 42 — Mini Project: Bubble Sort in MIPS + C Side-by-Side
| Block | Task |
|-------|------|
| **Practice** | Write `bubble_sort.c` (you know this). Then write `bubble_sort.asm` in MIPS. Both should sort an array of 10 integers. Add comments in the `.asm` file that map each block to the C line. |
| **Deliverable** | `bubble_sort.c` + `bubble_sort.asm` + `README.md` explaining the mapping. Push to GitHub. |

**Week 6 Checkpoint:** Can you explain what `jal` does? Can you trace a recursive function on the stack? Can you read compiler-generated assembly?

---

## The "C Revision Drill" Bank (10-Min Warm-Ups)

Do **one of these** before you open Logisim or MARS each day. They are designed to keep your C syntax sharp without consuming your main energy.

| # | Drill | Topic |
|---|-------|-------|
| 1 | Print reverse of an array | Loops, arrays |
| 2 | `max_of_three` function | Functions, conditionals |
| 3 | `swap` using pointers | Pointers |
| 4 | `my_strlen` | Pointer arithmetic |
| 5 | `struct Point` + distance | Structures |
| 6 | Read/write a text file | File I/O |
| 7 | `malloc` an array of 10 ints, fill, free | Dynamic memory |
| 8 | `foreach` with function pointer | Function pointers |
| 9 | Bitwise AND/OR/XOR on two integers | Bit manipulation |
| 10 | Detect if a number is power of two | Bit manipulation |
| 11 | Reverse a linked list iteratively | Linked lists |
| 12 | Count set bits in an integer | Bit manipulation |
| 13 | Implement a circular queue in an array | Arrays, pointers |
| 14 | Parse a simple CSV line | Strings, parsing |
| 15 | Simulate a 2:1 MUX in C | Logic → C mapping |

---

## Your Exact GitHub Repo Structure After Week 6

```
systems-lab/
├── week1-c-linux/
│   ├── hello.c
│   ├── reverse_array.c
│   ├── student_db.c
│   └── Makefile
├── week2-memory-os/
│   ├── linked_list.c
│   ├── generic_foreach.c
│   ├── my_string.c
│   ├── fork_demo.c
│   └── microshell.c
├── week3-digital-logic/
│   ├── gates_nand_only.circ
│   ├── alu_4bit.circ
│   └── alu_simulator.c
├── week4-sequential/
│   ├── d_flipflop.circ
│   ├── counter_4bit.circ
│   ├── fsm_moore_1011.circ
│   ├── vending_machine.circ
│   └── recursion_stack.c
├── week5-mips-intro/
│   ├── add_two.asm
│   ├── array_sum.asm
│   ├── find_max.asm
│   └── interactive.asm
└── week6-mips-procedures/
    ├── fact.asm
    ├── proc_nested.asm
    ├── bubble_sort.asm
    └── bubble_sort.c
```

If you want, I can give you the **exact code skeletons** for Day 1 (hello.c, reverse_array.c, sum_digits.c) so you spend zero time guessing file structure.
