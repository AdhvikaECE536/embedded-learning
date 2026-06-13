I have been using simple commands like

```bash
mkdir folder
gcc file.c -o file
./file
```

(and others all being same as what i will comtinue to use now)

but, apparently, there are better and safer ways to write


```bash
mkdir -p ~/c-bootcamp && cd ~/c-bootcamp
```

| Part | What | Why |
|---|---|---|
| `mkdir` | "make directory" — creates a folder | You need somewhere to store all your C files |
| `-p` | "no error if it already exists" | Safe to run again accidentally |
| `~/c-bootcamp` | folder name, in your home directory | Keeps your work organized |
| `&&` | then, only if success | Only moves in if folder was created |
| `cd ~/c-bootcamp` | move into that folder | So your files save there |

---


### **To Compile and run**

**Simple version**
```bash
gcc -Wall -Wextra -g program01.c -o program01 && ./program01
```

| Part | What | Why |
|---|---|---|
| `gcc` | the C compiler | Converts your code into a runnable program |
| `-Wall` | all warnings | Catches bugs like your missing `&` today |
| `-Wextra` | extra warnings | Catches even more subtle mistakes |
| `-g` | debug info | Needed if you use GDB later |
| `program01.c` | your input file | The code you wrote |
| `-o program01` | output name | Names the result `program01` instead of `a.out` |
| `&&` | then if success | Only runs if compile succeeded |
| `./program01` | run it | `.` means current folder |

**Strict version (for assignments/projects):**
```bash
gcc -Wall -Wextra -Werror -g -O0 -std=c11 file.c -o file
```
3 extra flags on top of the simple version:

| Extra Flag | What | Why |
|---|---|---|
| `-Werror` | warnings = errors | Won't compile if any warning exists — forces clean code |
| `-O0` | zero optimization | Compiler doesn't reorder your code, easier to debug |
| `-std=c11` | C11 standard | Tells gcc which version of C rules to follow |

---
