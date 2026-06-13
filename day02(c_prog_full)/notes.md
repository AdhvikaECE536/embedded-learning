# Note

These are the programs i am going to practice on, given when prompted for me to revise and strenghten my base in C programming. 

---

Create your workspace now:
```bash
mkdir -p ~/c-bootcamp && cd ~/c-bootcamp
```

---

# LEVEL 0: Absolute Basics (Skip if Confident)
*Compile every program with:* `gcc -Wall -Wextra -g file.c -o file && ./file`

## 1. Hello World
```c
#include <stdio.h>
int main(void) {
    printf("Hello, Systems Lab\n");
    return 0;
}
```

## 2. Calculator (Switch + Functions)
```c
#include <stdio.h>

int calc(int a, int b, char op) {
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return b ? a / b : 0;
        default: return 0;
    }
}

int main(void) {
    int a, b; char op;
    scanf("%d %c %d", &a, &op, &b);
    printf("%d %c %d = %d\n", a, op, b, calc(a, b, op));
    return 0;
}
```

---

# LEVEL 1: Arrays & Control Flow (Revision)

## 3. Reverse Array
```c
#include <stdio.h>
int main(void) {
    int arr[5], i;
    for (i = 0; i < 5; i++) scanf("%d", &arr[i]);
    for (i = 4; i >= 0; i--) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

## 4. Find Max/Min
```c
#include <stdio.h>
int main(void) {
    int arr[] = {3, 1, 4, 1, 5, 9, 2, 6};
    int n = sizeof(arr)/sizeof(arr[0]);
    int max = arr[0], min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }
    printf("Max: %d, Min: %d\n", max, min);
    return 0;
}
```

## 5. Bubble Sort
```c
#include <stdio.h>
void bubble_sort(int *arr, int n) {
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (arr[j] > arr[j+1]) {
                int t = arr[j]; arr[j] = arr[j+1]; arr[j+1] = t;
            }
}
int main(void) {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    bubble_sort(arr, n);
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

## 6. Binary Search
```c
#include <stdio.h>
int bsearch(int *arr, int l, int r, int x) {
    while (l <= r) {
        int m = l + (r - l) / 2;
        if (arr[m] == x) return m;
        if (arr[m] < x) l = m + 1;
        else r = m - 1;
    }
    return -1;
}
int main(void) {
    int arr[] = {2, 3, 4, 10, 40};
    int x = 10;
    int r = bsearch(arr, 0, 4, x);
    printf("Found at index: %d\n", r);
    return 0;
}
```

---

# LEVEL 2: Pointers (The Non-Negotiable)
**Theory:** A pointer is just a variable holding a memory address. `&` gets the address. `*` dereferences it. Everything in systems (OS, embedded, MIPS) is about addresses.

## 7. Swap by Reference (The Classic)
```c
#include <stdio.h>
void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}
int main(void) {
    int x = 5, y = 10;
    swap(&x, &y);
    printf("x=%d, y=%d\n", x, y);
    return 0;
}
```

## 8. Pointer Arithmetic
```c
#include <stdio.h>
int main(void) {
    int arr[] = {10, 20, 30, 40, 50};
    int *p = arr;
    printf("%d\n", *p);      // 10
    printf("%d\n", *(p+1));  // 20
    printf("%d\n", *(p+4));  // 50
    // Same as:
    printf("%d\n", p[4]);    // 50
    return 0;
}
```

## 9. Array of Pointers
```c
#include <stdio.h>
int main(void) {
    int a = 10, b = 20, c = 30;
    int *ptrs[3] = {&a, &b, &c};
    for (int i = 0; i < 3; i++)
        printf("%d ", *ptrs[i]);
    printf("\n");
    return 0;
}
```

## 10. Pointer to Pointer (Double Pointer)
```c
#include <stdio.h>
#include <stdlib.h>

void allocate(int **pp, int val) {
    *pp = malloc(sizeof(int));
    **pp = val;
}

int main(void) {
    int *p = NULL;
    allocate(&p, 42);
    printf("%d\n", *p);
    free(p);
    return 0;
}
```
**Why:** `&p` is address of the pointer. `pp` stores that address. `*pp` is the pointer itself. `**pp` is the integer.

## 11. Const Pointers vs Pointer to Const
```c
#include <stdio.h>
int main(void) {
    int a = 10, b = 20;
    
    const int *p1 = &a;   // Pointer to constant: cannot change *p1
    // *p1 = 20; // ERROR
    p1 = &b;               // OK: can change where p1 points
    
    int *const p2 = &a;    // Constant pointer: cannot change p2
    *p2 = 20;              // OK
    // p2 = &b; // ERROR
    
    const int *const p3 = &a; // Both constant
    return 0;
}
```

## 12. Generic Swap with void* and memcpy
```c
#include <stdio.h>
#include <string.h>

void generic_swap(void *a, void *b, size_t size) {
    unsigned char temp[size];
    memcpy(temp, a, size);
    memcpy(a, b, size);
    memcpy(b, temp, size);
}

int main(void) {
    int x = 5, y = 10;
    generic_swap(&x, &y, sizeof(int));
    printf("x=%d, y=%d\n", x, y);
    
    double a = 1.1, b = 2.2;
    generic_swap(&a, &b, sizeof(double));
    printf("a=%.1f, b=%.1f\n", a, b);
    return 0;
}
```

---

# LEVEL 3: Memory Management (The OS Connection)
**Theory:** Stack = automatic, limited, fast. Heap = manual, large, slow. `malloc` asks the OS for heap memory. `free` returns it. Forget `free` = memory leak.

## 13. malloc, calloc, realloc basics
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n = 5;
    
    // malloc: uninitialized
    int *arr1 = malloc(n * sizeof(int));
    if (!arr1) return 1; // always check!
    
    // calloc: zero-initialized
    int *arr2 = calloc(n, sizeof(int));
    
    // Use arr1
    for (int i = 0; i < n; i++) arr1[i] = i + 1;
    
    // realloc: resize
    arr1 = realloc(arr1, 10 * sizeof(int));
    if (!arr1) return 1;
    
    free(arr1);
    free(arr2);
    return 0;
}
```

## 14. 2D Array with malloc (Array of Pointers)
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int rows = 3, cols = 4;
    
    // Array of pointers
    int **arr = malloc(rows * sizeof(int*));
    for (int i = 0; i < rows; i++)
        arr[i] = malloc(cols * sizeof(int));
    
    // Fill
    for (int i = 0; i < rows; i++)
        for (int j = 0; j < cols; j++)
            arr[i][j] = i * 10 + j;
    
    // Free (reverse order)
    for (int i = 0; i < rows; i++) free(arr[i]);
    free(arr);
    return 0;
}
```

## 15. Memory Leak Demo + Valgrind
```c
#include <stdlib.h>
int main(void) {
    int *p = malloc(100 * sizeof(int));
    p[0] = 42;
    // Oops! forgot free(p);
    return 0;
}
```
**Run with:** `gcc leak.c -o leak && valgrind ./leak`  
**Install valgrind:** `sudo apt install valgrind`

## 16. Custom Memory Allocator (Fixed Block)
```c
#include <stdio.h>
#include <stddef.h>

#define BLOCK_SIZE 1024
#define NUM_BLOCKS 10

static char heap[BLOCK_SIZE * NUM_BLOCKS];
static int used[NUM_BLOCKS] = {0};

void *my_alloc(size_t size) {
    if (size > BLOCK_SIZE) return NULL;
    for (int i = 0; i < NUM_BLOCKS; i++) {
        if (!used[i]) {
            used[i] = 1;
            return heap + (i * BLOCK_SIZE);
        }
    }
    return NULL;
}

void my_free(void *ptr) {
    if (!ptr) return;
    int idx = ((char*)ptr - heap) / BLOCK_SIZE;
    if (idx >= 0 && idx < NUM_BLOCKS) used[idx] = 0;
}

int main(void) {
    int *p1 = my_alloc(sizeof(int) * 100);
    int *p2 = my_alloc(sizeof(int) * 50);
    printf("Allocated at %p and %p\n", (void*)p1, (void*)p2);
    my_free(p1);
    my_free(p2);
    return 0;
}
```
**Why:** This is how real embedded allocators work. No `malloc` in FreeRTOS sometimes.

## 17. Stack vs Heap Address Inspection
```c
#include <stdio.h>
#include <stdlib.h>

int global_var = 10; // Data segment

void foo(void) {
    int local = 20;           // Stack
    int *heap = malloc(4);     // Heap
    static int s = 30;         // Data segment
    
    printf("global:  %p\n", (void*)&global_var);
    printf("local:   %p\n", (void*)&local);
    printf("heap:    %p\n", (void*)heap);
    printf("static:  %p\n", (void*)&s);
    printf("foo():   %p\n", (void*)&foo);
    free(heap);
}

int main(void) {
    foo();
    return 0;
}
```
**Observe:** Stack addresses are high and decrease. Heap addresses are low and increase.

---

# LEVEL 4: Strings (The Systems Way)
**Theory:** A C string is a `char` array ending with `'\0'`. Never trust user input length. Buffer overflows are the #1 security bug.

## 18. my_strlen
```c
#include <stdio.h>

size_t my_strlen(const char *s) {
    const char *p = s;
    while (*p) p++;
    return p - s;
}

int main(void) {
    printf("%zu\n", my_strlen("Hello"));
    return 0;
}
```

## 19. my_strcpy
```c
#include <stdio.h>

char *my_strcpy(char *dest, const char *src) {
    char *d = dest;
    while ((*d++ = *src++));
    return dest;
}

int main(void) {
    char dest[20];
    my_strcpy(dest, "Hello");
    printf("%s\n", dest);
    return 0;
}
```

## 20. my_strcat
```c
#include <stdio.h>

char *my_strcat(char *dest, const char *src) {
    char *d = dest;
    while (*d) d++;
    while ((*d++ = *src++));
    return dest;
}

int main(void) {
    char dest[20] = "Hello";
    my_strcat(dest, " World");
    printf("%s\n", dest);
    return 0;
}
```

## 21. my_strcmp
```c
#include <stdio.h>

int my_strcmp(const char *s1, const char *s2) {
    while (*s1 && (*s1 == *s2)) {
        s1++;
        s2++;
    }
    return *(unsigned char*)s1 - *(unsigned char*)s2;
}

int main(void) {
    printf("%d\n", my_strcmp("abc", "abd")); // negative
    printf("%d\n", my_strcmp("abc", "abc")); // 0
    return 0;
}
```

## 22. my_strstr (Find Substring)
```c
#include <stdio.h>

const char *my_strstr(const char *haystack, const char *needle) {
    if (!*needle) return haystack;
    for (; *haystack; haystack++) {
        const char *h = haystack, *n = needle;
        while (*h && *n && *h == *n) { h++; n++; }
        if (!*n) return haystack;
    }
    return NULL;
}

int main(void) {
    const char *found = my_strstr("Hello World", "World");
    printf("%s\n", found ? found : "Not found");
    return 0;
}
```

## 23. Reverse Words in a String
```c
#include <stdio.h>
#include <string.h>

void reverse(char *l, char *r) {
    while (l < r) {
        char t = *l; *l = *r; *r = t;
        l++; r--;
    }
}

void reverse_words(char *s) {
    char *word_start = s;
    char *temp = s;
    
    while (*temp) {
        if (*temp == ' ') {
            reverse(word_start, temp - 1);
            word_start = temp + 1;
        }
        temp++;
    }
    reverse(word_start, temp - 1);
    reverse(s, temp - 1);
}

int main(void) {
    char s[] = "Hello World Systems";
    reverse_words(s);
    printf("%s\n", s);
    return 0;
}
```

---

# LEVEL 5: Structures & Unions (Data Packing)

## 24. Basic Struct
```c
#include <stdio.h>

struct Student {
    int id;
    char name[50];
    float marks;
};

int main(void) {
    struct Student s = {1, "Alice", 85.5};
    printf("%d %s %.1f\n", s.id, s.name, s.marks);
    return 0;
}
```

## 25. Pointer to Struct (-> operator)
```c
#include <stdio.h>
#include <stdlib.h>

struct Student {
    int id;
    char name[50];
};

int main(void) {
    struct Student *s = malloc(sizeof(struct Student));
    s->id = 2; // same as (*s).id
    strcpy(s->name, "Bob");
    printf("%d %s\n", s->id, s->name);
    free(s);
    return 0;
}
```

## 26. Self-Referential Struct (Linked List Node)
```c
#include <stdio.h>

struct Node {
    int data;
    struct Node *next; // self-referential
};

int main(void) {
    struct Node n1 = {10, NULL};
    struct Node n2 = {20, NULL};
    n1.next = &n2;
    printf("%d -> %d\n", n1.data, n1.next->data);
    return 0;
}
```

## 27. Unions (Shared Memory)
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[4];
};

int main(void) {
    union Data d;
    d.i = 65;
    printf("int: %d, float: %f, char: %s\n", d.i, d.f, d.str);
    printf("Size of union: %zu\n", sizeof(d)); // 4 bytes (max member)
    return 0;
}
```

## 28. Bit Fields (Embedded Classic)
```c
#include <stdio.h>

struct Flags {
    unsigned int is_alive : 1;
    unsigned int type : 3;     // 0-7
    unsigned int priority : 4; // 0-15
};

int main(void) {
    struct Flags f = {1, 5, 10};
    printf("Size: %zu bytes\n", sizeof(f));
    printf("alive=%d, type=%d, priority=%d\n", f.is_alive, f.type, f.priority);
    return 0;
}
```

## 29. Packed Struct (For Network Protocols / Registers)
```c
#include <stdio.h>

struct __attribute__((packed)) Packet {
    char header;
    int data;
    char footer;
};

int main(void) {
    printf("Packed size: %zu\n", sizeof(struct Packet)); // 6 instead of 12
    return 0;
}
```
**Why:** Hardware registers and network packets have no padding.

---

# LEVEL 6: File I/O (Binary & Text)

## 30. Text File Write/Read
```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("data.txt", "w");
    if (!fp) return 1;
    fprintf(fp, "ID,Name,Marks\n");
    fprintf(fp, "1,Alice,85\n");
    fclose(fp);
    
    fp = fopen("data.txt", "r");
    char line[100];
    while (fgets(line, sizeof(line), fp))
        printf("%s", line);
    fclose(fp);
    return 0;
}
```

## 31. Binary File Write/Read
```c
#include <stdio.h>

struct Student {
    int id;
    float marks;
};

int main(void) {
    struct Student s1 = {1, 85.5};
    FILE *fp = fopen("students.bin", "wb");
    fwrite(&s1, sizeof(s1), 1, fp);
    fclose(fp);
    
    struct Student s2;
    fp = fopen("students.bin", "rb");
    fread(&s2, sizeof(s2), 1, fp);
    printf("%d %.1f\n", s2.id, s2.marks);
    fclose(fp);
    return 0;
}
```

## 32. Hex Dump of a File
```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("students.bin", "rb");
    if (!fp) return 1;
    
    unsigned char buf[16];
    size_t n;
    int offset = 0;
    
    while ((n = fread(buf, 1, sizeof(buf), fp)) > 0) {
        printf("%08x: ", offset);
        for (size_t i = 0; i < n; i++)
            printf("%02x ", buf[i]);
        printf("\n");
        offset += n;
    }
    fclose(fp);
    return 0;
}
```

## 33. CSV Parser
```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char line[] = "1,Alice,85.5";
    char *token = strtok(line, ",");
    while (token) {
        printf("%s\n", token);
        token = strtok(NULL, ",");
    }
    return 0;
}
```

---

# LEVEL 7: Function Pointers & Callbacks (The Advanced Gateway)
**Theory:** A function pointer stores the address of a function. It allows you to pass behavior as data. This is how `qsort`, signal handlers, and state machines work.

## 34. Basic Function Pointer
```c
#include <stdio.h>

int add(int a, int b) { return a + b; }
int mul(int a, int b) { return a * b; }

int main(void) {
    int (*op)(int, int); // Declare function pointer
    op = add;
    printf("%d\n", op(2, 3)); // 5
    op = mul;
    printf("%d\n", op(2, 3)); // 6
    return 0;
}
```

## 35. Function Pointer Array (Jump Table)
```c
#include <stdio.h>

void op_add(void) { printf("Adding\n"); }
void op_sub(void) { printf("Subtracting\n"); }
void op_mul(void) { printf("Multiplying\n"); }

int main(void) {
    void (*ops[])(void) = {op_add, op_sub, op_mul};
    int choice;
    printf("Enter 0-2: ");
    scanf("%d", &choice);
    if (choice >= 0 && choice <= 2) ops[choice]();
    return 0;
}
```

## 36. Callback with qsort
```c
#include <stdio.h>
#include <stdlib.h>

int compare_asc(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int compare_desc(const void *a, const void *b) {
    return (*(int*)b - *(int*)a);
}

int main(void) {
    int arr[] = {3, 1, 4, 1, 5, 9};
    int n = 6;
    
    qsort(arr, n, sizeof(int), compare_asc);
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    
    qsort(arr, n, sizeof(int), compare_desc);
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

## 37. State Machine with Function Pointers
```c
#include <stdio.h>

typedef enum { STATE_IDLE, STATE_RUN, STATE_STOP, NUM_STATES } State;
typedef enum { EV_START, EV_STOP, EV_RESET, NUM_EVENTS } Event;

void on_idle(void) { printf("IDLE\n"); }
void on_run(void)  { printf("RUNNING\n"); }
void on_stop(void) { printf("STOPPED\n"); }

void (*state_table[NUM_STATES])(void) = {
    on_idle, on_run, on_stop
};

State transition[NUM_STATES][NUM_EVENTS] = {
    [STATE_IDLE] = { [EV_START] = STATE_RUN,  [EV_STOP] = STATE_IDLE, [EV_RESET] = STATE_IDLE },
    [STATE_RUN]  = { [EV_START] = STATE_RUN,  [EV_STOP] = STATE_STOP, [EV_RESET] = STATE_IDLE },
    [STATE_STOP] = { [EV_START] = STATE_RUN,  [EV_STOP] = STATE_STOP, [EV_RESET] = STATE_IDLE }
};

int main(void) {
    State current = STATE_IDLE;
    Event events[] = { EV_START, EV_STOP, EV_RESET, EV_START };
    
    for (int i = 0; i < 4; i++) {
        state_table[current]();
        current = transition[current][events[i]];
    }
    return 0;
}
```

---

# LEVEL 8: Bit Manipulation (Embedded & OS)

## 38. Set, Clear, Toggle, Check
```c
#include <stdio.h>

#define SET_BIT(x, n)    ((x) |= (1U << (n)))
#define CLEAR_BIT(x, n)  ((x) &= ~(1U << (n)))
#define TOGGLE_BIT(x, n) ((x) ^= (1U << (n)))
#define CHECK_BIT(x, n)  (((x) >> (n)) & 1U)

int main(void) {
    unsigned int reg = 0;
    SET_BIT(reg, 3);     // 0b1000 = 8
    printf("%u\n", reg);
    SET_BIT(reg, 0);     // 0b1001 = 9
    printf("%u\n", reg);
    CLEAR_BIT(reg, 0);   // 0b1000 = 8
    printf("%u\n", reg);
    TOGGLE_BIT(reg, 3);  // 0b0000 = 0
    printf("%u\n", reg);
    return 0;
}
```

## 39. Count Set Bits (Kernighan Algorithm)
```c
#include <stdio.h>

int count_bits(unsigned int n) {
    int count = 0;
    while (n) {
        n &= (n - 1); // Clears lowest set bit
        count++;
    }
    return count;
}

int main(void) {
    printf("%d\n", count_bits(0b101101)); // 4
    return 0;
}
```

## 40. Endianness Check
```c
#include <stdio.h>

int main(void) {
    unsigned int x = 1;
    char *c = (char*)&x;
    if (*c) printf("Little Endian\n");
    else    printf("Big Endian\n");
    return 0;
}
```

## 41. Swap without Temp (XOR)
```c
#include <stdio.h>

void xor_swap(int *a, int *b) {
    if (a == b) return; // critical!
    *a ^= *b;
    *b ^= *a;
    *a ^= *b;
}

int main(void) {
    int x = 5, y = 10;
    xor_swap(&x, &y);
    printf("%d %d\n", x, y);
    return 0;
}
```

## 42. Bit Masking for Hardware Registers
```c
#include <stdio.h>

// Simulate a hardware register
volatile unsigned int REG = 0x00;

#define REG_ENABLE  (1 << 0)
#define REG_MODE    (1 << 1)
#define REG_STATUS  (1 << 7)

int main(void) {
    REG |= REG_ENABLE;           // Turn on
    REG |= (REG_MODE);           // Set mode
    if (REG & REG_STATUS)        // Check status
        printf("Ready\n");
    printf("REG = 0x%02X\n", REG);
    return 0;
}
```

---

# LEVEL 9: Data Structures From Scratch (All with malloc/free)

## 43. Singly Linked List
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *next;
} Node;

Node* create_node(int data) {
    Node *n = malloc(sizeof(Node));
    n->data = data;
    n->next = NULL;
    return n;
}

void insert_head(Node **head, int data) {
    Node *n = create_node(data);
    n->next = *head;
    *head = n;
}

void delete_val(Node **head, int val) {
    Node *temp = *head, *prev = NULL;
    while (temp && temp->data != val) {
        prev = temp;
        temp = temp->next;
    }
    if (!temp) return;
    if (prev) prev->next = temp->next;
    else *head = temp->next;
    free(temp);
}

void print_list(Node *head) {
    while (head) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

void free_list(Node *head) {
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
    print_list(head);
    delete_val(&head, 2);
    print_list(head);
    free_list(head);
    return 0;
}
```

## 44. Doubly Linked List
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct DNode {
    int data;
    struct DNode *prev, *next;
} DNode;

DNode* create(int data) {
    DNode *n = malloc(sizeof(DNode));
    n->data = data; n->prev = n->next = NULL;
    return n;
}

void insert_head(DNode **head, int data) {
    DNode *n = create(data);
    if (*head) {
        n->next = *head;
        (*head)->prev = n;
    }
    *head = n;
}

void free_all(DNode *head) {
    while (head) {
        DNode *t = head;
        head = head->next;
        free(t);
    }
}

int main(void) {
    DNode *head = NULL;
    insert_head(&head, 10);
    insert_head(&head, 20);
    printf("%d <-> %d\n", head->data, head->next->data);
    free_all(head);
    return 0;
}
```

## 45. Circular Buffer (Ring Buffer) — Embedded Classic
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct {
    int *buffer;
    int head;
    int tail;
    int max;
    int count;
} cbuf_t;

cbuf_t* cbuf_init(int size) {
    cbuf_t *c = malloc(sizeof(cbuf_t));
    c->buffer = malloc(size * sizeof(int));
    c->max = size; c->head = c->tail = c->count = 0;
    return c;
}

bool cbuf_push(cbuf_t *c, int data) {
    if (c->count == c->max) return false;
    c->buffer[c->head] = data;
    c->head = (c->head + 1) % c->max;
    c->count++;
    return true;
}

bool cbuf_pop(cbuf_t *c, int *data) {
    if (c->count == 0) return false;
    *data = c->buffer[c->tail];
    c->tail = (c->tail + 1) % c->max;
    c->count--;
    return true;
}

void cbuf_free(cbuf_t *c) {
    free(c->buffer); free(c);
}

int main(void) {
    cbuf_t *cb = cbuf_init(4);
    int val;
    cbuf_push(cb, 10); cbuf_push(cb, 20);
    cbuf_push(cb, 30); cbuf_push(cb, 40);
    cbuf_push(cb, 50); // fails, full
    while (cbuf_pop(cb, &val)) printf("%d ", val);
    printf("\n");
    cbuf_free(cb);
    return 0;
}
```

## 46. Stack (Linked List Based)
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct Node {
    int data;
    struct Node *next;
} Stack;

void push(Stack **s, int data) {
    Stack *n = malloc(sizeof(Stack));
    n->data = data; n->next = *s; *s = n;
}

bool pop(Stack **s, int *data) {
    if (!*s) return false;
    Stack *t = *s;
    *data = t->data;
    *s = t->next;
    free(t);
    return true;
}

int main(void) {
    Stack *s = NULL;
    push(&s, 10); push(&s, 20); push(&s, 30);
    int v;
    while (pop(&s, &v)) printf("%d ", v);
    printf("\n");
    return 0;
}
```

## 47. Queue (Array Based with Front/Rear)
```c
#include <stdio.h>
#include <stdbool.h>

#define MAX 5
typedef struct { int data[MAX]; int front, rear, count; } Queue;

void init(Queue *q) { q->front = 0; q->rear = -1; q->count = 0; }

bool enqueue(Queue *q, int val) {
    if (q->count == MAX) return false;
    q->rear = (q->rear + 1) % MAX;
    q->data[q->rear] = val;
    q->count++;
    return true;
}

bool dequeue(Queue *q, int *val) {
    if (q->count == 0) return false;
    *val = q->data[q->front];
    q->front = (q->front + 1) % MAX;
    q->count--;
    return true;
}

int main(void) {
    Queue q; init(&q);
    enqueue(&q, 1); enqueue(&q, 2); enqueue(&q, 3);
    int v;
    while (dequeue(&q, &v)) printf("%d ", v);
    printf("\n");
    return 0;
}
```

## 48. Binary Search Tree
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int key;
    struct Node *left, *right;
} Node;

Node* insert(Node *root, int key) {
    if (!root) {
        Node *n = malloc(sizeof(Node));
        n->key = key; n->left = n->right = NULL;
        return n;
    }
    if (key < root->key) root->left = insert(root->left, key);
    else root->right = insert(root->right, key);
    return root;
}

void inorder(Node *root) {
    if (root) {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

void free_tree(Node *root) {
    if (root) {
        free_tree(root->left);
        free_tree(root->right);
        free(root);
    }
}

int main(void) {
    Node *root = NULL;
    root = insert(root, 50);
    insert(root, 30); insert(root, 70); insert(root, 20); insert(root, 40);
    inorder(root); printf("\n");
    free_tree(root);
    return 0;
}
```

## 49. Hash Table (Chaining)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 10

typedef struct Entry {
    char key[20];
    int value;
    struct Entry *next;
} Entry;

Entry *table[TABLE_SIZE] = {NULL};

unsigned int hash(const char *key) {
    unsigned int h = 0;
    for (int i = 0; key[i]; i++) h = h * 31 + key[i];
    return h % TABLE_SIZE;
}

void insert(const char *key, int value) {
    unsigned int h = hash(key);
    Entry *e = table[h];
    while (e) {
        if (strcmp(e->key, key) == 0) { e->value = value; return; }
        e = e->next;
    }
    e = malloc(sizeof(Entry));
    strcpy(e->key, key); e->value = value;
    e->next = table[h]; table[h] = e;
}

int* search(const char *key) {
    unsigned int h = hash(key);
    Entry *e = table[h];
    while (e) {
        if (strcmp(e->key, key) == 0) return &e->value;
        e = e->next;
    }
    return NULL;
}

int main(void) {
    insert("apple", 100); insert("banana", 200);
    int *v = search("apple");
    if (v) printf("apple = %d\n", *v);
    return 0;
}
```

---

# LEVEL 10: Systems Programming (Linux)

## 50. fork() and wait()
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void) {
    pid_t pid = fork();
    if (pid < 0) return 1;
    if (pid == 0) {
        printf("Child: PID=%d, Parent=%d\n", getpid(), getppid());
    } else {
        wait(NULL);
        printf("Parent: Child PID=%d\n", pid);
    }
    return 0;
}
```

## 51. Orphan and Zombie Demo
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(void) {
    pid_t pid = fork();
    if (pid == 0) {
        sleep(2);
        printf("Child: Parent now = %d (should be init/systemd)\n", getppid());
    } else {
        printf("Parent exiting before child\n");
        exit(0); // Child becomes orphan
    }
    return 0;
}
```

## 52. pipe() — Parent to Child Communication
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
        printf("Child received: %s\n", buf);
        close(fd[0]);
    } else {
        close(fd[0]);
        write(fd[1], "Hello child", 12);
        close(fd[1]);
    }
    return 0;
}
```

## 53. dup2() and Redirection
```c
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main(void) {
    int fd = open("output.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
    dup2(fd, STDOUT_FILENO); // Redirect stdout to file
    close(fd);
    printf("This goes to output.txt, not terminal!\n");
    return 0;
}
```

## 54. Mini Shell (fork + exec + wait)
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
        cmd[strcspn(cmd, "\n")] = 0; // remove newline
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

## 55. Shared Memory (shm)
```c
#include <stdio.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main(void) {
    int shmid = shmget(IPC_PRIVATE, 1024, IPC_CREAT | 0666);
    char *str = (char*) shmat(shmid, NULL, 0);
    strcpy(str, "Hello from shared memory");
    printf("Writer: %s\n", str);
    shmdt(str);
    // In another program, attach to same shmid to read
    return 0;
}
```

## 56. Signals (SIGALRM)
```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void handler(int sig) {
    printf("Alarm! Signal %d received\n", sig);
}

int main(void) {
    signal(SIGALRM, handler);
    alarm(2); // Send SIGALRM in 2 seconds
    printf("Waiting...\n");
    pause(); // Wait for signal
    return 0;
}
```

---

# LEVEL 11: Advanced C Concepts

## 57. const Correctness
```c
const int a = 10;           // a cannot change
int *p = &a;                // BAD: discards const
const int *p1 = &a;         // OK: p1 points to const int
int *const p2 = &a;         // BAD: a is const, cannot assign to *p2
const int *const p3 = &a;   // OK: p3 is const pointer to const int
```

## 58. volatile (Embedded/ISR)
```c
volatile int sensor_ready = 0;

// In ISR (interrupt handler):
void ISR(void) { sensor_ready = 1; }

// In main:
while (!sensor_ready); // Compiler will NOT optimize this away
```

## 59. Variable Arguments (printf clone)
```c
#include <stdio.h>
#include <stdarg.h>

void my_printf(const char *fmt, ...) {
    va_list args;
    va_start(args, fmt);
    while (*fmt) {
        if (*fmt == '%' && *(fmt+1) == 'd') {
            int i = va_arg(args, int);
            printf("%d", i);
            fmt += 2;
        } else {
            putchar(*fmt);
            fmt++;
        }
    }
    va_end(args);
}

int main(void) {
    my_printf("Value: %d, Next: %d\n", 42, 100);
    return 0;
}
```

## 60. offsetof and container_of (Linux Kernel Style)
```c
#include <stdio.h>
#include <stddef.h>

#define container_of(ptr, type, member) ({ \
    const typeof(((type *)0)->member) *__mptr = (ptr); \
    (type *)((char *)__mptr - offsetof(type, member)); })

struct Person {
    int age;
    char name[20];
    int id;
};

int main(void) {
    struct Person p = {25, "Alice", 101};
    int *id_ptr = &p.id;
    
    struct Person *pp = container_of(id_ptr, struct Person, id);
    printf("Name: %s, Age: %d\n", pp->name, pp->age);
    return 0;
}
```

## 61. Alignment and Padding
```c
#include <stdio.h>

struct Normal {
    char c;  // 1 byte
    int i;   // 4 bytes
    char d;  // 1 byte
}; // Size = 12 (padding added)

struct Packed {
    char c;
    int i;
    char d;
} __attribute__((packed)); // Size = 6

int main(void) {
    printf("Normal: %zu, Packed: %zu\n", sizeof(struct Normal), sizeof(struct Packed));
    printf("Offset of i: %zu\n", offsetof(struct Normal, i));
    return 0;
}
```

## 62. Static vs Extern
```c
// file1.c
static int hidden = 10; // Only visible in file1.c
int shared = 20;         // Visible everywhere (external linkage)

// file2.c
extern int shared; // Declares shared from file1.c
// extern int hidden; // ERROR: hidden is static
```

---

# LEVEL 12: Algorithms (Recursion Practice)

## 63. Recursive Factorial + Fibonacci
```c
#include <stdio.h>

int fact(int n) { return n <= 1 ? 1 : n * fact(n-1); }
int fib(int n) { return n <= 1 ? n : fib(n-1) + fib(n-2); }

int main(void) {
    printf("fact(5)=%d, fib(7)=%d\n", fact(5), fib(7));
    return 0;
}
```

## 64. Merge Sort
```c
#include <stdio.h>
#include <stdlib.h>

void merge(int *arr, int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    int *L = malloc(n1 * sizeof(int));
    int *R = malloc(n2 * sizeof(int));
    for (int i = 0; i < n1; i++) L[i] = arr[l + i];
    for (int j = 0; j < n2; j++) R[j] = arr[m + 1 + j];
    
    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
    free(L); free(R);
}

void merge_sort(int *arr, int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        merge_sort(arr, l, m);
        merge_sort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

int main(void) {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = 6;
    merge_sort(arr, 0, n-1);
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Your 30-Day C Drill Schedule

| Day | Programs to Write |
|-----|-----------------|
| 1 | 1, 2, 3 |
| 2 | 4, 5, 6 |
| 3 | 7, 8, 9 |
| 4 | 10, 11, 12 |
| 5 | 13, 14 |
| 6 | 15, 16 |
| 7 | 17, 18 |
| 8 | 19, 20, 21 |
| 9 | 22, 23 |
| 10 | 24, 25, 26 |
| 11 | 27, 28, 29 |
| 12 | 30, 31, 32 |
| 13 | 33, 34 |
| 14 | 35, 36 |
| 15 | 37, 38 |
| 16 | 39, 40 |
| 17 | 41, 42 |
| 18 | 43 (Linked List) |
| 19 | 44 (Doubly Linked) |
| 20 | 45 (Circular Buffer) |
| 21 | 46 (Stack) |
| 22 | 47 (Queue) |
| 23 | 48 (BST) |
| 24 | 49 (Hash Table) |
| 25 | 50, 51 (fork) |
| 26 | 52, 53 (pipe, dup2) |
| 27 | 54 (Mini Shell) |
| 28 | 55, 56 (shm, signals) |
| 29 | 57, 58, 59, 60, 61 |
| 30 | 63, 64 (recursion, merge sort) |

---

## Compile Everything With This Strict Flag Set

```bash
gcc -Wall -Wextra -Werror -g -O0 -std=c11 file.c -o file
```

| Flag | Meaning |
|------|---------|
| `-Wall` | All warnings |
| `-Wextra` | Extra warnings |
| `-Werror` | Treat warnings as errors (forces clean code) |
| `-g` | Debug info for GDB |
| `-O0` | No optimization (easier to debug) |
| `-std=c11` | C11 standard |

---

## What to Do Right Now

```bash
cd ~/c-bootcamp
nano program01.c
# (paste program 1)
gcc -Wall -Wextra -g program01.c -o program01 && ./program01
```
