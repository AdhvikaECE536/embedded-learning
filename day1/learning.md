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

