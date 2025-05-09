```md
This script demonstrates the use of **user-defined variables** in a Bash shell script and prints them using the `echo` command. It also touches on **predefined (environment/special) variables** in Bash.

---

## 📦 Contents of `predefine-variable.sh`

```bash
#!/bin/bash

# User-defined variables
hero="ramesh"
villain="Vimal"

# Displaying values using echo
echo "Movie ka hero name : $hero"
echo "Movie ka villain name : $villain"
```

![Script Output Screenshot](https://github.com/user-attachments/assets/4e2944ba-43ae-406c-9718-188b5a629f1c)

---

## 🛠️ How to Use

1. **Create the file on your server:**

   ```bash
   nano predefine-variable.sh
   ```

   Paste the script above into the editor and save.

2. **Set execute permissions:**

   ```bash
   chmod 766 predefine-variable.sh
   ```

   > `766` means:
   >
   > * Owner can read/write/execute  
   > * Group and others can read/write

3. **Run the script:**

   ```bash
   ./predefine-variable.sh
   ```

---

## 📘 Bash Predefined (Special) Variables

Bash has many built-in variables. Here are some commonly used **predefined variables**:

| Variable      | Description                               | Example Output            |
| ------------- | ----------------------------------------- | ------------------------- |
| `$0`          | Script name                               | `./predefine-variable.sh` |
| `$1`, `$2`... | Positional parameters (arguments passed)  | `first`, `second`         |
| `$#`          | Number of arguments                       | `2`                       |
| `$@`          | All arguments                             | `arg1 arg2`               |
| `$$`          | Current script's process ID               | `14321`                   |
| `$?`          | Exit status of last command (0 = success) | `0`                       |
| `$_`          | Last argument of previous command         | `/home/user`              |

### Example (optional extension to your script):

```bash
#!/bin/bash

echo "Script name       : $0"
echo "Total arguments   : $#"
echo "First argument    : $1"
echo "All arguments     : $@"
echo "Process ID        : $$"
echo "Last command exit : $?"
```

Run it with arguments:

```bash
./predefine-variable.sh arg1 arg2
```
