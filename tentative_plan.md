Here is your **complete 52-week, day-by-day roadmap**. Every day tells you exactly what to type, what to read, and what to build. No decisions. No guesswork.

---

## THE RULES

| Rule | What It Means |
|------|---------------|
| **1-hour day** | 15 min theory → 45 min code |
| **2-hour day** | 20 min theory → 70 min code → 10 min Git |
| **Light day** (exam week) | 15 min review → 15 min flashcards → stop |
| **Never miss 2 days** | If you skip Monday, you MUST do Tuesday |
| **C is a tool, not a subject** | You learn C syntax only when a system breaks without it |

---

## PHASE 0: FOUNDATION CAMP (Weeks 1–4)
*Goal: You can write C without segfaults. You are comfortable in Linux. You have seen a CPU built from gates.*

---

### WEEK 1: Linux + C Warm-Up

#### Day 1 (1 hr) — Terminal + First Program
**Read:** This conversation (the Day 1 I already gave you).  
**Type:**
```bash
cd ~
mkdir -p systems-lab/week1
cd systems-lab/week1
nano hello.c
```
**Code to type:**
```c
#include <stdio.h>
int main(void) {
    printf("Hello, Systems Lab\n");
    return 0;
}
```
**Commands:**
```bash
gcc hello.c -o hello && ./hello
git init
git add hello.c
git commit -m "Day 1: hello world"
```
**StackOverflow search:** "gcc compile c program linux"

---

#### Day 2 (1 hr) — Arrays + Functions
**Read:** K&R C, Chapter 1 (skip if bored, just reference).  
**Type:** `nano reverse_array.c`
```c
#include <stdio.h>
int main(void) {
    int arr[5], i;
    printf("Enter 5 ints: ");
    for (i = 0; i < 5; i++) scanf("%d", &arr[i]);
    printf("Reverse: ");
    for (i = 4; i >= 0; i--) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```
**Build:** `gcc reverse_array.c -o rev && ./rev`  
**Git:** `git add . && git commit -m "Day 2: reverse array"`

---

#### Day 3 (1 hr) — Pointers (The Scary Part)
**Read:** K&R Chapter 5.1–5.3 (just 3 pages). Focus on `&` and `*`.  
**Type:** `nano pointer_demo.c`
```c
#include <stdio.h>
int main(void) {
    int a = 10;
    int *p = &a;
    printf("a=%d, &a=%p, p=%p, *p=%d\n", a, (void*)&a, (void*)p, *p);
    
    int arr[] = {10, 20, 30};
    int *ptr = arr;
    printf("arr[0]=%d, *ptr=%d, *(ptr+1)=%d\n", arr[0], *ptr, *(ptr+1));
    return 0;
}
```
**Build and run.**  
**Key insight:** `*(ptr + 1)` moves 4 bytes (size of int). This is pointer arithmetic.

---

#### Day 4 (1.5 hr) — Swap by Pointer + Mini Shell Start
**Read:** K&R 5.2 (swap by reference).  
**Type:** `nano swap.c`
```c
#include <stdio.h>
void swap(int *a, int *b) {
    int t = *a; *a = *b; *b = t;
}
int main(void) {
    int x = 5, y = 10;
    swap(&x, &y);
    printf("x=%d, y=%d\n", x, y);
    return 0;
}
```
**Then:** `nano launcher.c` (the process launcher from previous message).  
**Build both.**  
**Git commit.**

---

#### Day 5 (1.5 hr) — Fork Deep Dive
**Read:** `man fork` (type this in terminal). Read first 20 lines.  
**Type:** `nano fork_chain.c`
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void) {
    printf("Parent PID: %d\n", getpid());
    pid_t p1 = fork();
    if (p1 == 0) {
        printf("Child 1 PID: %d, Parent: %d\n", getpid(), getppid());
        pid_t p2 = fork();
        if (p2 == 0) {
            printf("Grandchild PID: %d, Parent: %d\n", getpid(), getppid());
        }
    }
    while (wait(NULL) > 0); // wait for all children
    return 0;
}
```
**Run 3 times.** Notice PIDs change. Draw the tree on paper.

---

#### Day 6 (2 hr) — Pipe: Parent Talks to Child
**Read:** `man 2 pipe` (first 30 lines).  
**Type:** `nano pipe_demo.c`
```c
#include <stdio.h>
#include <unistd.h>
#include <string.h>

int main(void) {
    int fd[2];
    pipe(fd);
    pid_t pid = fork();
    if (pid == 0) {
        close(fd[1]);
        char buf[20];
        read(fd[0], buf, sizeof(buf));
        printf("Child got: %s\n", buf);
        close(fd[0]);
    } else {
        close(fd[0]);
        write(fd[1], "Hello child", 12);
        close(fd[1]);
    }
    return 0;
}
```
**This is IPC.** This is your OS course. The C was just syntax.

---

#### Day 7 (1 hr) — Catch-up / Git / Rest
**Commands:**
```bash
cd ~/systems-lab
git log --oneline
git status
```
**If behind:** Finish any incomplete code.  
**If ahead:** Read about `execvp` on StackOverflow: "how does execvp work in c"

---

### WEEK 2: Memory + Data Structures

#### Day 8 (1 hr) — Malloc Basics
**Read:** K&R 7.8 (storage management, 2 pages).  
**Type:** `nano malloc_demo.c`
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n = 5;
    int *arr = malloc(n * sizeof(int));
    if (!arr) { printf("Failed\n"); return 1; }
    
    for (int i = 0; i < n; i++) arr[i] = i * 10;
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    
    free(arr); // NEVER FORGET
    return 0;
}
```
**StackOverflow search:** "when to use malloc vs array in c"

---

#### Day 9 (1.5 hr) — Linked List (The Core Structure)
**Read:** No book. Just type this carefully.  
**Type:** `nano linked_list.c`
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *next;
} Node;

Node* create(int data) {
    Node *n = malloc(sizeof(Node));
    n->data = data;
    n->next = NULL;
    return n;
}

void insert_head(Node **head, int data) {
    Node *n = create(data);
    n->next = *head;
    *head = n;
}

void print(Node *head) {
    while (head) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

void free_all(Node *head) {
    while (head) {
        Node *t = head;
        head = head->next;
        free(t);
    }
}

int main(void) {
    Node *head = NULL;
    insert_head(&head, 3);
    insert_head(&head, 2);
    insert_head(&head, 1);
    print(head);
    free_all(head);
    return 0;
}
```
**Build. Run. Modify:** Add `delete_val` function.  
**Git commit.**

---

#### Day 10 (1.5 hr) — Structs + Function Pointers
**Read:** K&R 6.1–6.3 (structures).  
**Type:** `nano task_struct.c`
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Task {
    int id;
    int priority;
    void (*run)(void); // FUNCTION POINTER
} Task;

void task_a(void) { printf("Running Task A\n"); }
void task_b(void) { printf("Running Task B\n"); }

int main(void) {
    Task t1 = {1, 10, task_a};
    Task t2 = {2, 5, task_b};
    
    Task *tasks[] = {&t1, &t2};
    for (int i = 0; i < 2; i++) {
        printf("Task %d (pri %d): ", tasks[i]->id, tasks[i]->priority);
        tasks[i]->run();
    }
    return 0;
}
```
**This is how RTOS tasks work.** You just built a mini scheduler.

---

#### Day 11 (1 hr) — Bit Manipulation
**Read:** None. Just memorize these.  
**Type:** `nano bits.c`
```c
#include <stdio.h>

#define SET_BIT(x, n)    ((x) |= (1U << (n)))
#define CLEAR_BIT(x, n)  ((x) &= ~(1U << (n)))
#define TOGGLE_BIT(x, n) ((x) ^= (1U << (n)))
#define CHECK_BIT(x, n)  (((x) >> (n)) & 1U)

int main(void) {
    unsigned int reg = 0;
    SET_BIT(reg, 3);    // 0b1000 = 8
    printf("After set bit 3: %u\n", reg);
    
    SET_BIT(reg, 0);    // 0b1001 = 9
    printf("After set bit 0: %u\n", reg);
    
    if (CHECK_BIT(reg, 3)) printf("Bit 3 is ON\n");
    
    CLEAR_BIT(reg, 0);
    printf("After clear bit 0: %u\n", reg);
    return 0;
}
```
**You will use this for FPGA registers and automotive ECUs.**

---

#### Day 12 (2 hr) — Circular Buffer (RTOS Classic)
**Type:** `nano circbuf.c` (from the 64-program list, program 45).  
**This is in your RTOS course.** FreeRTOS uses this for interrupt-safe queues.

---

#### Day 13 (1.5 hr) — Mini Shell with Pipe
**Read:** StackOverflow: "how to implement shell with pipe in c"  
**Type:** `nano microshell.c`
```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void) {
    char cmd[100];
    while (1) {
        printf("> ");
        fflush(stdout);
        if (!fgets(cmd, sizeof(cmd), stdin)) break;
        cmd[strcspn(cmd, "\n")] = 0;
        if (strcmp(cmd, "exit") == 0) break;
        
        pid_t pid = fork();
        if (pid == 0) {
            execlp(cmd, cmd, NULL);
            perror("exec failed");
            return 1;
        } else {
            wait(NULL);
        }
    }
    return 0;
}
```
**Test:** `ls`, `pwd`, `date`, `whoami`, `exit`

---

#### Day 14 (1 hr) — Week 2 Review + Git
**Commands:**
```bash
cd ~/systems-lab
git add .
git commit -m "Week 2: memory, linked list, bits, shell"
```
**Flashcard review:** `&`, `*`, `malloc`, `free`, `fork`, `pipe`, `struct`, function pointer syntax.

---

### WEEK 3: Digital Logic (The Fun Starts)

#### Day 15 (1.5 hr) — Install + First Circuit
**Install:**
```bash
sudo apt install logisim-evolution
```
**Open:** `logisim-evolution`  
**YouTube:** Search "logisim evolution tutorial 4 bit adder"  
**Build:** 1-bit half adder (2 switches → XOR gate → LED for sum, AND gate → LED for carry)

---

#### Day 16 (1.5 hr) — Full Adder + 4-Bit Ripple Adder
**Build:** Chain 2 half adders + 1 OR gate = full adder.  
**Then:** Chain 4 full adders = 4-bit adder.  
**Test:** 3+5=8, 7+8=15, 15+1=0 with carry out.

---

#### Day 17 (1 hr) — Multiplexers
**Build:** 2:1 MUX, 4:1 MUX in Logisim.  
**Theory:** A MUX is a hardware `if-else`.

---

#### Day 18 (1.5 hr) — ALU Design
**Build:** 4-bit ALU. Control: 2-bit `op`. Operations: ADD, AND, OR, NOT.  
**This is in your MIPS course.**

---

#### Day 19 (1 hr) — Flip-Flops
**Build:** D flip-flop using NAND gates + clock.  
**Watch:** Output changes only on clock edge.

---

#### Day 20 (1.5 hr) — Counter + Register
**Build:** 4-bit up-counter. Add `Load` input.  
**This is how a PC (program counter) works.**

---

#### Day 21 (1 hr) — FSM: Sequence Detector
**Build:** Detect `1011` in a serial stream. Moore machine.  
**YouTube:** "logisim sequence detector fsm"

---

### WEEK 4: Sequential Logic + FSMs

#### Day 22 (1.5 hr) — FSM: Vending Machine
**Build:** Accept 5 and 10. Dispense at 15. Return change.  
**States:** IDLE, GOT5, GOT10, GOT15, OVERPAID.

---

#### Day 23 (1 hr) — Review C: Recursion
**Type:** `nano fib.c`
```c
#include <stdio.h>
int fib(int n) { return n <= 1 ? n : fib(n-1) + fib(n-2); }
int main(void) {
    for (int i = 0; i < 10; i++) printf("%d ", fib(i));
    printf("\n");
    return 0;
}
```
**Trace:** Add `printf("fib(%d)\n", n)` to see the call tree.

---

#### Day 24 (1.5 hr) — C + Hardware Connection
**Type:** `nano alu_sim.c`
```c
#include <stdio.h>

#define OP_ADD 0
#define OP_AND 1
#define OP_OR  2
#define OP_NOT 3

unsigned int alu(unsigned int a, unsigned int b, int op) {
    switch (op) {
        case OP_ADD: return a + b;
        case OP_AND: return a & b;
        case OP_OR:  return a | b;
        case OP_NOT: return ~a;
        default: return 0;
    }
}

int main(void) {
    printf("3+5=%u\n", alu(3, 5, OP_ADD));
    printf("3&5=%u\n", alu(3, 5, OP_AND));
    return 0;
}
```
**This is your Logisim ALU in C.**

---

#### Day 25 (1 hr) — Stack Frames (GDB Practice)
**Type:** `nano stack_trace.c`
```c
#include <stdio.h>

void bar(int x) {
    int local = x * 2;
    printf("bar: local at %p\n", (void*)&local);
}

void foo(int x) {
    int local = x + 1;
    printf("foo: local at %p\n", (void*)&local);
    bar(local);
}

int main(void) {
    foo(5);
    return 0;
}
```
**Run:** `gcc -g stack_trace.c -o st && gdb ./st`  
**GDB commands:** `break bar`, `run`, `info frame`, `bt` (backtrace)

---

#### Day 26 (1.5 hr) — Memory Layout Visualization
**Type:** `nano memory_layout.c` (from program 17 in previous list).  
**Observe:** Stack addresses > Heap addresses > Data addresses.

---

#### Day 27 (1 hr) — Git + Document
**Commit everything.** Write `README.md` explaining your ALU and FSM.

---

#### Day 28 (1 hr) — Rest / Catch-up

---

## PHASE 1: OPERATING SYSTEMS (Weeks 5–14)

### WEEK 5: MIPS Assembly Intro

#### Day 29 (1.5 hr) — Install MARS + First Program
**Install:**
```bash
sudo apt install default-jre
# Download Mars4_5.jar from: https://courses.missouristate.edu/KenVollmar/mars/
java -jar Mars4_5.jar
```
**Type in MARS:**
```asm
# add_two.asm
.data
msg: .asciiz "Sum = "

.text
main:
    li $t0, 5
    li $t1, 7
    add $t2, $t0, $t1
    
    li $v0, 4
    la $a0, msg
    syscall
    
    li $v0, 1
    move $a0, $t2
    syscall
    
    li $v0, 10
    syscall
```
**Run step-by-step.** Watch registers.

---

#### Day 30 (1.5 hr) — Array Sum in MIPS
**Type:**
```asm
# array_sum.asm
.data
arr: .word 10, 20, 30, 40, 50
n:   .word 5

.text
main:
    la $t0, arr      # base address
    lw $t1, n        # count
    li $t2, 0        # sum
    li $t3, 0        # index
    
loop:
    beq $t3, $t1, done
    lw $t4, 0($t0)
    add $t2, $t2, $t4
    addi $t0, $t0, 4
    addi $t3, $t3, 1
    j loop
    
done:
    li $v0, 1
    move $a0, $t2
    syscall
    
    li $v0, 10
    syscall
```
**This is your C pointer arithmetic in hardware.**

---

#### Day 31 (1 hr) — Branching + Loops
**Type:** `find_max.asm` — find maximum in array of 8 integers.

---

#### Day 32 (1.5 hr) — Procedures: jal, jr
**Type:**
```asm
# proc_add.asm
.text
main:
    li $a0, 5
    li $a1, 7
    jal add_nums
    move $a0, $v0
    li $v0, 1
    syscall
    li $v0, 10
    syscall

add_nums:
    add $v0, $a0, $a1
    jr $ra
```
**Watch `$ra` in MARS.** It holds the return address.

---

#### Day 33 (1.5 hr) — Stack Frames in MIPS
**Type:** `fact.asm` — recursive factorial.  
**Trace `$sp` manually.** Draw stack on paper.

---

#### Day 34 (1 hr) — C to MIPS Translation
**In C:**
```c
int square(int x) { return x * x; }
int main() { return square(5); }
```
**Translate to MIPS by hand.** Then check with godbolt.org (select `mips gcc`).

---

#### Day 35 (1 hr) — String Operations
**Type:** `mips_strlen.asm` — count chars until `\0`.

---

### WEEK 6: MIPS Deep Dive

#### Day 36 (1.5 hr) — Bubble Sort in MIPS
**Type:** `bubble_sort.asm` — sort 10 integers.  
**Comment every line mapping to C.**

---

#### Day 37 (1.5 hr) — Single-Cycle Datapath in Logisim
**Build:** PC + Instruction Memory + Register File + ALU + Data Memory.  
**Connect for `addi` instruction.**

---

#### Day 38 (1 hr) — Control Unit
**Build:** ROM-based control unit for 4 instructions: `add`, `lw`, `sw`, `beq`.

---

#### Day 39 (1.5 hr) — Complete Single-Cycle CPU
**Connect everything.** Test with a simple program.

---

#### Day 40 (1 hr) — Document + Git

---

#### Day 41 (1 hr) — Review: C + MIPS Connection
**Type:** `nano mips_emulator.c` — a tiny C program that simulates `add`, `lw`, `sw`.

---

#### Day 42 (1.5 hr) — Mini Project: C + MIPS Side-by-Side
**Bubble sort in both.** Push to GitHub.

---

### WEEK 7: OS Intro + xv6 Boot

#### Day 43 (1.5 hr) — Clone and Boot xv6
```bash
cd ~
git clone https://github.com/mit-pdos/xv6-riscv.git
cd xv6-riscv
make qemu
```
**Explore:** `ls`, `cat README`, `echo hello`

---

#### Day 44 (1.5 hr) — xv6: Add a System Call
**Read:** `kernel/syscall.c`, `user/usys.pl`  
**Add:** `trace` system call that prints syscall number.

---

#### Day 45 (1 hr) — C Review: Function Pointers + qsort
**Type:** `nano qsort_demo.c` (from program 36).

---

#### Day 46 (1.5 hr) — xv6 Lab: Utilities
**Do:** `sleep`, `pingpong` (pipe between processes), `primes` (sieve of Eratosthenes using pipe)

---

#### Day 47 (1.5 hr) — xv6: Process Scheduling
**Read:** `kernel/proc.c` — `scheduler()` function.  
**Trace:** How does round-robin work?

---

#### Day 48 (1 hr) — C: Custom Memory Allocator
**Type:** `nano my_malloc.c` (from program 16).

---

#### Day 49 (1.5 hr) — xv6: Virtual Memory
**Read:** `kernel/vm.c` — `walk()` function.  
**Understand:** Page table walking.

---

### WEEK 8: CPU Scheduling

#### Day 50 (1.5 hr) — Scheduler Simulator in C
**Type:** `nano scheduler.c`
```c
#include <stdio.h>

typedef struct {
    int id, burst, arrival;
} Process;

void fcfs(Process *p, int n) {
    int time = 0;
    for (int i = 0; i < n; i++) {
        printf("P%d [%d-%d]\n", p[i].id, time, time + p[i].burst);
        time += p[i].burst;
    }
}

int main(void) {
    Process p[] = {{1, 10, 0}, {2, 5, 0}, {3, 8, 0}};
    fcfs(p, 3);
    return 0;
}
```
**Extend:** Add SJF, Round Robin.

---

#### Day 51 (1.5 hr) — Round Robin with Quantum
**Modify scheduler.** Add Gantt chart output.

---

#### Day 52 (1 hr) — C: Struct Alignment + Padding
**Type:** `nano alignment.c` (from program 61).

---

#### Day 53 (1.5 hr) — xv6: Modify Scheduler
**Change:** Time slice quantum in `kernel/proc.c`.

---

#### Day 54 (1.5 hr) — Priority Scheduling
**Add to simulator.** Compare starvation.

---

#### Day 55 (1 hr) — C: offsetof + container_of
**Type:** `nano container_of.c` (from program 60).  
**This is Linux kernel style.**

---

### WEEK 9: Process Synchronization

#### Day 56 (1.5 hr) — Semaphores in C
**Type:** `nano sem_demo.c`
```c
#include <stdio.h>
#include <semaphore.h>
#include <pthread.h>

sem_t sem;

void* worker(void* arg) {
    sem_wait(&sem);
    printf("Worker %ld in critical section\n", (long)arg);
    sleep(1);
    sem_post(&sem);
    return NULL;
}

int main(void) {
    sem_init(&sem, 0, 1);
    pthread_t t1, t2;
    pthread_create(&t1, NULL, worker, (void*)1);
    pthread_create(&t2, NULL, worker, (void*)2);
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    sem_destroy(&sem);
    return 0;
}
```
**Build:** `gcc sem_demo.c -o sem -pthread && ./sem`

---

#### Day 57 (1.5 hr) — Producer-Consumer
**Type:** Bounded buffer with mutex + 2 semaphores (empty, full).

---

#### Day 58 (1 hr) — C: volatile + sig_atomic_t
**Read:** StackOverflow "when to use volatile in c"  
**Type:** `nano volatile_demo.c`

---

#### Day 59 (1.5 hr) — Dining Philosophers
**Type:** Classic deadlock simulation. Fix with resource ordering.

---

#### Day 60 (1.5 hr) — xv6: Locks
**Read:** `kernel/spinlock.c`  
**Understand:** How xv6 implements spinlocks.

---

#### Day 61 (1 hr) — C: Atomic Operations
**Type:** `__sync_fetch_and_add`, `__sync_lock_test_and_set`.

---

### WEEK 10: Deadlocks

#### Day 62 (1.5 hr) — Banker's Algorithm
**Type:** `nano banker.c` — full implementation.

---

#### Day 63 (1.5 hr) — Deadlock Detection
**Type:** Resource allocation graph simulator.

---

#### Day 64 (1 hr) — C: setjmp/longjmp (Error Handling)
**Type:** `nano setjmp_demo.c`

---

#### Day 65 (1.5 hr) — xv6: File System
**Read:** `kernel/fs.c` — `bmap()`, `dirlookup()`.

---

#### Day 66 (1.5 hr) — xv6 Lab: File System
**Do:** Symbolic links or large files lab.

---

#### Day 67 (1 hr) — C: mmap
**Type:** `nano mmap_demo.c` — memory-map a file.

---

### WEEK 11: Memory Management

#### Day 68 (1.5 hr) — Paging Simulator
**Type:** `nano paging.c` — logical to physical with page table.

---

#### Day 69 (1.5 hr) — Page Replacement: FIFO, LRU
**Extend simulator.**

---

#### Day 70 (1 hr) — C: Memory-Mapped I/O Simulation
**Type:** `nano mmio.c` — read/write to fake hardware registers.

---

#### Day 71 (1.5 hr) — xv6: Page Tables
**Do:** `pgaccess` lab (detect page access bits).

---

#### Day 72 (1.5 hr) — Segmentation
**Add to simulator.**

---

#### Day 73 (1 hr) — C: Custom printf (varargs)
**Type:** `nano my_printf.c` (from program 59).

---

### WEEK 12: File Systems

#### Day 74 (1.5 hr) — FAT-like File System in C
**Type:** Create, delete, list files in a disk image.

---

#### Day 75 (1.5 hr) — Disk Scheduling
**Type:** FCFS, SSTF, SCAN, C-SCAN simulator.

---

#### Day 76 (1 hr) — C: Bitmaps
**Type:** `nano bitmap.c` — track free blocks.

---

#### Day 77 (1.5 hr) — xv6: Complete Labs
**Finish:** Any remaining xv6 labs.

---

#### Day 78 (1.5 hr) — OS Mini-Project: Custom Shell
**Features:** Pipes, redirection, background jobs.

---

#### Day 79 (1 hr) — Git + Document

---

### WEEK 13: OS Review + Buffer

#### Day 80–85 — Review weak areas. Redo any failed labs.

---

### WEEK 14: OS Capstone

#### Day 86–91 — **Project:** Extend xv6 with a new feature (your choice: priority scheduling, memory compression, etc.)

---

## PHASE 2: REAL-TIME SYSTEMS (Weeks 15–22)

### WEEK 15: Real-Time Foundations

#### Day 92 (1.5 hr) — Task Model + Python Simulator
**Read:** Liu Ch 1.  
**Type:** `nano rts_tasks.py` (yes, Python is fine for theory):
```python
tasks = [
    {"id": 1, "period": 10, "wcet": 3},
    {"id": 2, "period": 15, "wcet": 4},
]
```

---

#### Day 93 (1.5 hr) — RMS Scheduler in Python
**Implement:** Rate Monotonic. Check schedulability (`U <= n*(2^(1/n)-1)`).

---

#### Day 94 (1 hr) — C: Review for RTOS
**Redo:** Circular buffer, linked list, function pointers.

---

#### Day 95 (1.5 hr) — EDF + LLF in Python
**Implement:** Compare with RMS.

---

#### Day 96 (1.5 hr) — Response Time Analysis
**Type:** Calculate WCRT for task set.

---

#### Day 97 (1 hr) — C: Static vs Dynamic Allocation
**Type:** Compare `malloc` vs global array vs stack array performance.

---

### WEEK 16: FreeRTOS Setup

#### Day 98 (1.5 hr) — Install STM32CubeIDE + FreeRTOS
**Download:** STM32CubeIDE (free).  
**Create:** Project for STM32F446RE (or your board).

---

#### Day 99 (1.5 hr) — First FreeRTOS Task
**Code:** Blink LED in a task.

---

#### Day 100 (1 hr) — C: const correctness review
**Type:** `nano const_demo.c`

---

#### Day 101 (1.5 hr) — Multiple Tasks + Priorities
**Code:** 3 tasks, different priorities, print task name.

---

#### Day 102 (1.5 hr) — Queues
**Code:** Pass sensor data between tasks.

---

#### Day 103 (1 hr) — C: Alignment + packed structs
**Type:** `nano packed_demo.c`

---

### WEEK 17: FreeRTOS Synchronization

#### Day 104–109 — Semaphores, mutexes, priority inheritance, recursive mutexes.

---

### WEEK 18: FreeRTOS Interrupts + Timers

#### Day 110–115 — ISRs, software timers, tick hook.

---

### WEEK 19: RTOS Memory + I/O

#### Day 116–121 — Static allocation, heap management, UART driver.

---

### WEEK 20: RTOS Mini-Project

#### Day 122–127 — **Project:** Real-time data logger (ADC → queue → SD card → UART).

---

### WEEK 21: Automotive / CAN Bus Intro

#### Day 128 (1.5 hr) — CAN Protocol Study
**Read:** Navet Ch 3.  
**Buy:** Arduino + MCP2515 module (~₹800).

---

#### Day 129 (1.5 hr) — Send CAN Frame
**Code:** Arduino sends "Hello CAN" every second.

---

#### Day 130 (1 hr) — C: Bit timing calculation
**Type:** Calculate CAN baud rate registers.

---

#### Day 131 (1.5 hr) — Receive CAN Frame
**Code:** Second Arduino receives and prints.

---

#### Day 132 (1.5 hr) — OBD-II Reader
**Code:** ELM327 + Python reads engine RPM.

---

#### Day 133 (1 hr) — C: CRC calculation
**Type:** `nano crc.c` — CAN uses CRC for error detection.

---

### WEEK 22: Real-Time Capstone

#### Day 134–139 — **Project:** RTOS-based automotive node (CAN + sensor + actuator).

---

## PHASE 3: ADVANCED ARCHITECTURE (Weeks 23–34)

### WEEK 23: MIPS Pipeline Simulator in C

#### Day 140 (1.5 hr) — 5-Stage Simulator
**Type:** `nano pipeline.c` — fetch, decode, execute, mem, writeback.

---

#### Day 141 (1.5 hr) — Hazard Detection
**Add:** RAW, WAR, WAW detection.

---

#### Day 142 (1 hr) — C: Struct packing for pipeline registers
**Type:** `nano pipe_regs.c`

---

#### Day 143 (1.5 hr) — Forwarding Unit
**Add:** Bypass logic.

---

#### Day 144 (1.5 hr) — Stall + Flush
**Add:** Load-use hazard, branch misprediction flush.

---

#### Day 145 (1 hr) — C: Branch predictor (1-bit)
**Type:** `nano bpredict.c`

---

### WEEK 24: Cache Simulator

#### Day 146 (1.5 hr) — Direct-Mapped Cache
**Type:** `nano cache.c` — tag, index, offset.

---

#### Day 147 (1.5 hr) — Set-Associative
**Extend:** 2-way, 4-way, LRU.

---

#### Day 148 (1 hr) — C: Memory trace parser
**Type:** Parse SPEC-like traces.

---

#### Day 149 (1.5 hr) — Write Policies
**Add:** Write-through, write-back, write-allocate.

---

#### Day 150 (1.5 hr) — AMAT Calculation
**Type:** Plot miss rate vs cache size.

---

#### Day 151 (1 hr) — C: Prefetcher simulation
**Type:** Simple stride prefetcher.

---

### WEEK 25: OpenMP

#### Day 152 (1.5 hr) — Hello OpenMP
**Code:**
```c
#include <omp.h>
#include <stdio.h>
int main(void) {
    #pragma omp parallel
    printf("Hello from thread %d\n", omp_get_thread_num());
    return 0;
}
```
**Build:** `gcc -fopenmp hello_omp.c -o hello_omp && ./hello_omp`

---

#### Day 153 (1.5 hr) — Parallel For
**Code:** Parallel array sum, matrix-vector multiply.

---

#### Day 154 (1 hr) — C: False sharing demo
**Type:** Measure performance with/without padding.

---

#### Day 155 (1.5 hr) — Reduction + Critical
**Code:** Parallel dot product, find max.

---

#### Day 156 (1.5 hr) — Scheduling Clauses
**Test:** `static`, `dynamic`, `guided` with irregular workload.

---

#### Day 157 (1 hr) — C: Thread-local storage
**Type:** `__thread` keyword demo.

---

### WEEK 26: MPI

#### Day 158 (1.5 hr) — Hello MPI
```bash
sudo apt install mpich
mpicc hello_mpi.c -o hello_mpi
mpirun -np 4 ./hello_mpi
```

---

#### Day 159 (1.5 hr) — Point-to-Point
**Code:** Send/receive array.

---

#### Day 160 (1 hr) — C: Derived datatypes
**Type:** MPI struct for custom data.

---

#### Day 161 (1.5 hr) — Collectives
**Code:** Broadcast, reduce, scatter-gather.

---

#### Day 162 (1.5 hr) — Ring Communication
**Code:** Token passing around ring.

---

#### Day 163 (1 hr) — C: Non-blocking MPI
**Type:** `MPI_Isend`, `MPI_Irecv`.

---

### WEEK 27: Multi-Core + Cache Coherence

#### Day 164 (1.5 hr) — MESI Simulator
**Type:** `nano mesi.c` — 2 cores, snooping.

---

#### Day 165 (1.5 hr) — False Sharing Fix
**Code:** Pad structs to cache line size (64 bytes).

---

#### Day 166 (1 hr) — C: Memory barriers
**Type:** `__sync_synchronize()` demo.

---

#### Day 167 (1.5 hr) — Amdahl's Law Calculator
**Type:** Speedup vs parallelism.

---

#### Day 168 (1.5 hr) — Profiling with perf
**Commands:** `perf stat`, `perf record`, `perf report`.

---

#### Day 169 (1 hr) — C: Lock-free stack
**Type:** CAS-based push/pop.

---

### WEEK 28: GPU / CUDA (Optional)

#### Day 170–175 — If you have NVIDIA GPU: vector add, matrix multiply, memory coalescing.

---

### WEEK 29: Parallel Project

#### Day 176–181 — **Project:** Parallel N-body or 2D heat diffusion (MPI + OpenMP).

---

### WEEK 30: Architecture Review

#### Day 182–187 — Review simulators. Optimize cache/pipeline code.

---

## PHASE 4: FPGA (Weeks 31–40)

### WEEK 31: Verilog Basics

#### Day 188 (1.5 hr) — Install + First Module
**Install:** Vivado WebPACK (free, large download).  
**Or use:** Icarus Verilog + GTKWave (lighter):
```bash
sudo apt install iverilog gtkwave
```
**Type:** `nano half_adder.v`
```verilog
module half_adder(
    input a, b,
    output sum, carry
);
    assign sum = a ^ b;
    assign carry = a & b;
endmodule
```
**Testbench:** `nano half_adder_tb.v`
```verilog
`timescale 1ns/1ps
module tb;
    reg a, b;
    wire sum, carry;
    half_adder uut(a, b, sum, carry);
    initial begin
        $dumpfile("wave.vcd");
        $dumpvars(0, tb);
        a=0; b=0; #10;
        a=0; b=1; #10;
        a=1; b=0; #10;
        a=1; b=1; #10;
        $finish;
    end
endmodule
```
**Run:**
```bash
iverilog -o sim half_adder.v half_adder_tb.v
vvp sim
gtkwave wave.vcd
```

---

#### Day 189 (1.5 hr) — Full Adder + 4-Bit Adder

---

#### Day 190 (1 hr) — C: Verilog simulation in C (optional)
**Type:** Simple gate-level simulator in C.

---

#### Day 191 (1.5 hr) — MUX + Decoder in Verilog

---

#### Day 192 (1.5 hr) — Sequential: D-FF, Counter

---

#### Day 193 (1 hr) — C: Bitwise ops review (for FPGA registers)

---

### WEEK 32: Verilog Advanced

#### Day 194 (1.5 hr) — FSM in Verilog
**Type:** Sequence detector (the one from Logisim, now in Verilog).

---

#### Day 195 (1.5 hr) — UART Transmitter
**Type:** Send serial data. Test with GTKWave.

---

#### Day 196 (1 hr) — C: UART simulation in C
**Type:** Bit-bang UART in C for verification.

---

#### Day 197 (1.5 hr) — FIFO in Verilog
**Type:** Synchronous FIFO with empty/full flags.

---

#### Day 198 (1.5 hr) — Block RAM Inference
**Type:** Initialize memory, read/write.

---

#### Day 199 (1 hr) — C: Memory controller simulation

---

### WEEK 33: FPGA Flow

#### Day 200 (1.5 hr) — Vivado Project
**Create:** New project, add Verilog files, synthesize.

---

#### Day 201 (1.5 hr) — Constraints (XDC)
**Type:** Pin assignments, clock constraints.

---

#### Day 202 (1 hr) — C: XDC parser (optional)

---

#### Day 203 (1.5 hr) — Implementation + Bitstream
**Generate:** Bitstream, program FPGA (if you have board).

---

#### Day 204 (1.5 hr) — ILA (Integrated Logic Analyzer)
**Debug:** Capture internal signals.

---

#### Day 205 (1 hr) — C: Post-synthesis simulation

---

### WEEK 34: FPGA Embedded Design

#### Day 206 (1.5 hr) — AXI4-Lite Slave
**Type:** Simple register interface.

---

#### Day 207 (1.5 hr) — SPI Master
**Type:** Interface with external sensor.

---

#### Day 208 (1 hr) — C: SPI simulation in C

---

#### Day 209 (1.5 hr) — DSP: FIR Filter
**Type:** Multiply-accumulate with Block RAM + DSP slices.

---

#### Day 210 (1.5 hr) — HLS Intro
**Type:** Vivado HLS, C to hardware.

---

#### Day 211 (1 hr) — C: FIR filter in C (golden reference)

---

### WEEK 35: FPGA Project

#### Day 212–217 — **Project:** Digital oscilloscope on FPGA (ADC + buffer + display).

---

### WEEK 36: FPGA Review

#### Day 218–223 — Polish project. Document. GitHub.

---

## PHASE 5: INTEGRATION (Weeks 37–48)

### WEEK 37: ROS2 Intro

#### Day 224 (1.5 hr) — Install + Turtlesim
```bash
sudo apt install ros-humble-desktop
source /opt/ros/humble/setup.bash
ros2 run turtlesim turtlesim_node
```

---

#### Day 225 (1.5 hr) — Publisher/Subscriber in C++
**Type:** Custom topic, send sensor data.

---

#### Day 226 (1 hr) — C: ROS2 message structs
**Type:** C struct that maps to ROS message.

---

#### Day 227 (1.5 hr) — Launch Files

---

#### Day 228 (1.5 hr) — RViz + TF2

---

#### Day 229 (1 hr) — C: Coordinate transforms in C

---

### WEEK 38: Robotics Control

#### Day 230 (1.5 hr) — PID Controller in C
**Type:** Motor speed control.

---

#### Day 231 (1.5 hr) — Encoder Reading
**Type:** Quadrature decoder.

---

#### Day 232 (1 hr) — C: PID simulation in C
**Type:** Step response plot (text-based).

---

#### Day 233 (1.5 hr) — Sensor Fusion (Complementary Filter)
**Type:** IMU + encoder → position.

---

#### Day 234 (1.5 hr) — micro-ROS on ESP32
**Type:** ROS2 node on microcontroller.

---

#### Day 235 (1 hr) — C: Sensor calibration in C

---

### WEEK 39: Automotive Deep Dive

#### Day 236 (1.5 hr) — AUTOSAR Classic Study
**Read:** Free AUTOSAR docs. Draw layered architecture.

---

#### Day 237 (1.5 hr) — CAN Matrix Design
**Type:** Design message database for a car subsystem.

---

#### Day 238 (1 hr) — C: CAN frame parser in C
**Type:** Parse CAN ID, DLC, data bytes.

---

#### Day 239 (1.5 hr) — FlexRay Basics
**Read:** Navet Ch 4.

---

#### Day 240 (1.5 hr) — Ethernet for Automotive
**Study:** 100BASE-T1, SOME/IP.

---

#### Day 241 (1 hr) — C: SocketCAN in C
**Type:** Send/receive CAN frames on Linux.

---

### WEEK 40: Capstone Design

#### Day 242–247 — **Design:** Choose capstone. Draw architecture. Plan components.

---

### WEEK 41: Capstone Build (Core)

#### Day 248–253 — Implement hardest subsystem first.

---

### WEEK 42: Capstone Integration

#### Day 254–259 — Connect subsystems. Debug interfaces.

---

### WEEK 43: Capstone Test

#### Day 260–265 — Test all modes. Measure timing. Profile.

---

### WEEK 44: Capstone Polish

#### Day 266–271 — Code cleanup. Documentation. Demo video.

---

### WEEK 45: Portfolio + Resume

#### Day 272–277 — GitHub READMEs. LinkedIn updates. Resume projects section.

---

### WEEK 46: Interview Prep Start

#### Day 278–283 — DSA review. LeetCode easy/medium (1 per day).

---

### WEEK 47: System Design Basics

#### Day 284–289 — Read "Designing Data-Intensive Applications" (Martin Kleppmann) Ch 1–3.

---

### WEEK 48: Mock Interviews

#### Day 290–295 — Practice explaining your projects. Record yourself.

---

## PHASE 6: BUFFER + FINAL PUSH (Weeks 49–52)

### Weeks 49–52
- Catch up on anything delayed
- Deep dive into weak areas
- Final capstone polish
- Apply for internships/jobs

---

## YOUR START TONIGHT CHECKLIST

```bash
# 1. Open terminal
Ctrl + Alt + T

# 2. Create workspace
mkdir -p ~/systems-lab/week1
cd ~/systems-lab/week1

# 3. Write hello.c (from Day 1 above)

# 4. Compile and run
gcc hello.c -o hello && ./hello

# 5. Git init
git init
git add hello.c
git commit -m "Day 1: start of 52-week systems journey"

# 6. Create GitHub repo (go to github.com, create repo, follow push instructions)
```

**Total time: 45 minutes.**

---


## DAILY SEARCH TEMPLATES

When stuck, search exactly these:

| Problem | Search Query |
|---------|-------------|
| `fork()` confusion | "fork return value parent child c" |
| `malloc` crash | "malloc returns null c" |
| Pointer syntax | "c pointer to pointer example" |
| Segfault | "gdb backtrace segfault c" |
| MARS error | "mars mips syscall not recognized" |
| Logisim bug | "logisim evolution clock not ticking" |
| xv6 panic | "xv6 panic initcode not found" |
| FreeRTOS config | "freertos configtick_rate_hz" |
| Verilog syntax | "verilog non-blocking assignment" |
| Vivado error | "vivado constraint file xdc tutorial" |

---
