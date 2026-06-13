## Phase 0: Open Your Terminal (30 seconds)
Press **`Ctrl + Alt + T`**.  
A black window opens. This is your home for the next 52 weeks.

---

## Phase 1: Terminal Survival Kit (10 minutes)

Type these **one by one**. Read the explanation after each.

```bash
whoami
```
*Shows your username. Know who you are.*

```bash
pwd
```
*Print Working Directory. Shows where you are right now. Likely `/home/yourname`.*

```bash
ls
```
*List. Shows files and folders in the current place.*

```bash
ls -la
```
*List with details. The `-l` is long format, `-a` shows hidden files (those starting with `.`).*

```bash
mkdir systems-lab
```
*Make Directory. Creates a folder named `systems-lab`.*

```bash
cd systems-lab
```
*Change Directory. Moves you inside `systems-lab`.*

```bash
pwd
```
*Now shows `/home/yourname/systems-lab`.*

```bash
mkdir week1
cd week1
pwd
```

**Create a file:**
```bash
touch hello.c
```
*Creates an empty file named `hello.c`.*

**Check it exists:**
```bash
ls
```

**View its contents (empty):**
```bash
cat hello.c
```
*Concatenate/print file contents.*

**Go up one folder:**
```bash
cd ..
```
*Two dots mean "parent folder".*

**Go back down:**
```bash
cd week1
```

**Other commands you will use daily:**
| Command | What it does | Example |
|---------|--------------|---------|
| `clear` | Clears terminal screen | `clear` |
| `history` | Shows past commands | `history` |
| `rm filename` | Delete file | `rm hello.c` |
| `rm -r foldername` | Delete folder and everything inside | `rm -r week1` |
| `cp file1 file2` | Copy file1 to file2 | `cp hello.c hello_backup.c` |
| `mv file1 file2` | Rename or move | `mv hello.c old/hello.c` |
| `man command` | Manual / help | `man gcc` |
| `sudo` | Do as superuser | `sudo apt update` |
| `exit` | Close terminal | `exit` |

> **Pro tip:** Press `Tab` to auto-complete file names. Press `Up arrow` to recall previous commands.

---

## Phase 2: Check Your Compiler (2 minutes)

```bash
gcc --version
```

If you see a version number (e.g., `gcc (Ubuntu 13.x.x)`), you are good.  
If you see "command not found", run:

```bash
sudo apt update
sudo apt install build-essential
```

Type your password when asked (it will not show on screen; this is normal).

---

## Phase 3: Your First C Program — `hello.c` (10 minutes)

You are inside `~/systems-lab/week1`.  
Open the file with a simple text editor:

```bash
nano hello.c
```

Type this exactly:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, Systems Lab!\n");
    return 0;
}
```

**Save and exit nano:**
- Press `Ctrl + O` (Write Out), then `Enter` to confirm.
- Press `Ctrl + X` to exit.

**Compile:**
```bash
gcc hello.c -o hello
```

*What happened:* `gcc` is the compiler. `hello.c` is your source. `-o hello` means "output an executable named `hello`".

**Run:**
```bash
./hello
```

*Output:*
```
Hello, Systems Lab!
```

> **Why `./`?** Linux does not run programs in the current folder unless you tell it exactly where they are. `./` means "right here".

---

## Phase 4: C Drill — Reverse Array (15 minutes)

This is your warm-up. It revises arrays, loops, and `scanf`.

Create file:
```bash
nano reverse_array.c
```

Type this:

```c
#include <stdio.h>

int main(void) {
    int arr[5];
    int i;

    printf("Enter 5 integers:\n");
    for (i = 0; i < 5; i++) {
        scanf("%d", &arr[i]);
    }

    printf("In reverse order:\n");
    for (i = 4; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```

Save (`Ctrl+O`, `Enter`, `Ctrl+X`).  
Compile and run:

```bash
gcc reverse_array.c -o reverse_array
./reverse_array
```

**Test it:**
```
Enter 5 integers:
10 20 30 40 50
In reverse order:
50 40 30 20 10
```

**If you get a segfault:** You probably forgot `&` in `scanf("%d", &arr[i]);`. The `&` gives the address where `scanf` should write. Without it, it crashes.

---

## Phase 5: Sum of Digits (15 minutes)

This revises `while` loops and modulo arithmetic.

```bash
nano sum_digits.c
```

Type this:

```c
#include <stdio.h>

int main(void) {
    int n, sum = 0, remainder;

    printf("Enter an integer: ");
    scanf("%d", &n);

    while (n != 0) {
        remainder = n % 10;   /* get last digit */
        sum += remainder;       /* add to sum */
        n /= 10;                /* remove last digit */
    }

    printf("Sum of digits = %d\n", sum);
    return 0;
}
```

Save. Compile. Run.

```bash
gcc sum_digits.c -o sum_digits
./sum_digits
```

**Test:**
```
Enter an integer: 347
Sum of digits = 14
```

---

## Phase 6: Organize & Git Init (10 minutes)

**Check your folder:**
```bash
ls -la
```

You should see:
- `hello.c`, `hello` (the executable)
- `reverse_array.c`, `reverse_array`
- `sum_digits.c`, `sum_digits`

**Clean up:** Remove the executables (we keep only source code in Git; executables are rebuilt).

```bash
rm hello reverse_array sum_digits
ls
```
Now only `.c` files remain. Good.

**Initialize Git:**
```bash
cd ~/systems-lab
git init
```

**Tell Git who you are:**
```bash
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

**Add all files:**
```bash
git add .
```

**Commit:**
```bash
git commit -m "Week 1 Day 1: hello, reverse array, sum digits"
```

**Check status:**
```bash
git status
```
It should say `nothing to commit, working tree clean`.

---

## What You Should Have Now

A folder structure like this:
```
/home/yourname/systems-lab/
└── week1/
    ├── hello.c
    ├── reverse_array.c
    └── sum_digits.c

---

**Quick Reference Card — Pin This**

| Task | Command |
|------|---------|
| Open terminal | `Ctrl + Alt + T` |
| Where am I? | `pwd` |
| List files | `ls` or `ls -la` |
| Make folder | `mkdir name` |
| Enter folder | `cd name` |
| Go up | `cd ..` |
| Create file | `touch name.c` |
| Edit file | `nano name.c` |
| Save in nano | `Ctrl + O`, `Enter` |
| Exit nano | `Ctrl + X` |
| Compile C | `gcc file.c -o output` |
| Run program | `./output` |
| Delete file | `rm file` |
| Delete folder | `rm -r folder` |
| Get help | `man command` |
| Git commit | `git add . && git commit -m "msg"` |

