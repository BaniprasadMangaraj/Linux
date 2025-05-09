

### 📄 `arguments-in-shell-script.md`

````markdown
# 📘 Understanding Arguments in Shell Scripting

In Bash shell scripting, **arguments** are **values passed to the script when it's run**. They allow users to provide dynamic input without editing the script.

---

## 🧾 What Are Arguments?

Arguments are values given **after the script name** in the terminal. Bash automatically assigns them to special variables:

| Variable | Meaning                              |
|----------|--------------------------------------|
| `$0`     | The script name                      |
| `$1`     | First argument                       |
| `$2`     | Second argument                      |
| `$#`     | Total number of arguments            |
| `$@`     | All arguments as separate strings    |
| `$*`     | All arguments as a single string     |

---

## 🧪 Example Script: `movie-arguments.sh`

```bash
#!/bin/bash

# Accessing arguments passed to the script

echo "Script name        : $0"
echo "Movie name         : $1"
echo "Hero name          : $2"
echo "Villain name       : $3"
echo "Total arguments    : $#"
echo "All arguments (\$@): $@"
````

---

## 🚀 How to Use the Script

1. **Create the script:**

   ```bash
   nano movie-arguments.sh
   ```

   Paste the content above and save.

2. **Make it executable:**

   ```bash
   chmod +x movie-arguments.sh
   ```

3. **Run it with arguments:**

   ```bash
   ./movie-arguments.sh Sholay Amitabh Gabbar
   ```

---

## ✅ Sample Output

```bash
Script name        : ./movie-arguments.sh
Movie name         : Sholay
Hero name          : Amitabh
Villain name       : Gabbar
Total arguments    : 3
All arguments ($@): Sholay Amitabh Gabbar
```

---

## 💡 Why Use Arguments?

Arguments make your script:

* **Dynamic** – no need to hardcode values.
* **Reusable** – same script works for multiple inputs.
* **Efficient** – can be used in automation and scheduled tasks.

