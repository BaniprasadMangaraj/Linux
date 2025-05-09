
## 🧠 What is a Function in Shell Scripting?

A **function** in a shell script is a named block of code that you can execute whenever needed, without repeating the same logic.

---

## ✅ Benefits of Using Functions

* **Reusability**: Write once, use many times.
* **Readability**: Easier to understand and maintain.
* **Modularity**: Break complex tasks into smaller pieces.

---

# 📌 Example 1: Create a Linux User

### 🔧 Script

```bash
#!/bin/bash

# Function to create a new user
create-user() {
    read -p "Enter the username: " username   # Prompt the user for input
    sudo useradd -m "$username"               # Create the user with a home directory
    echo "=============== User '$username' created successfully ============================"
}

# Call the function
create-user
```

### 💬 Example Output

```
$ ./create_user.sh
Enter the username: john
=============== User 'john' created successfully ============================
```

---

# 📌 Example 2: Check Disk Usage and Warn if Above Limit

### 🔧 Script

```bash
#!/bin/bash

# Function to check disk usage
check-disk-usage() {
    threshold=80  # Set threshold percentage

    usage=$(df / | grep / | awk '{print $5}' | sed 's/%//g')  # Get root (/) partition usage

    echo "Current disk usage: $usage%"

    if [ "$usage" -gt "$threshold" ]; then
        echo "⚠️ Warning: Disk usage is above ${threshold}%!"
    else
        echo "✅ Disk usage is under control."
    fi
}

# Call the function
check-disk-usage
```

### 💬 Example Output

```
$ ./check_disk.sh
Current disk usage: 82%
⚠️ Warning: Disk usage is above 80%!
```

---

## 🚀 How to Run These Scripts

1. Save each script to a file:

   * `create_user.sh`
   * `check_disk.sh`

2. Make them executable:

   ```bash
   chmod +x create_user.sh check_disk.sh
   ```

3. Run them:

   ```bash
   ./create_user.sh
   ./check_disk.sh
   ```

---

## 📚 Summary

| Feature | Example 1             | Example 2                     |
| ------- | --------------------- | ----------------------------- |
| Purpose | Add a user            | Monitor disk space            |
| Input   | Username              | None (reads system data)      |
| Output  | User creation success | Disk usage warning or success |

---

## ✨ Tips

* Use `functions` when you repeat tasks like checking services, logging info, or validating inputs.
* Use `"$variable"` syntax to avoid bugs caused by spaces or special characters.
* Add error handling to make scripts production-ready.
