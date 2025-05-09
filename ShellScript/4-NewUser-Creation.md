### 📄 `create-user-script.md`

````markdown
# 👤 Bash Script: Create a New Linux User

This Bash script automates the process of creating a new user on a Linux system. It uses prompts to collect the username and password from the user and handles user creation securely and interactively.

---

## 🧾 Script Overview

```bash
#!/bin/bash

<<help
This script is used to:
- Prompt the user for a username and password
- Create a new Linux user with a home directory
- Set the user's password

Explanation of commands:
- <<help ... help: Multiline comment block
- read -p: Prompt user for input
- echo -e: Enables interpretation of backslash escapes (e.g., \n for newline)
help

echo "============ Creation of user started ============"

# Prompt for username
read -p "Enter the username: " username

# Prompt for password (note: visible while typing)
read -p "Enter the password: " password

# Create the user with a home directory
sudo useradd -m "$username"

# Set the user's password
echo -e "$password\n$password" | sudo passwd "$username"

echo "============ Creation of user completed =========="
````

---

## 🧠 Explanation of Key Concepts

| Command           | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| `read -p`         | Prompts user and reads input into a variable                                |
| `sudo useradd -m` | Creates a new user with a home directory                                    |
| `echo -e`         | Enables special characters like `\n` (newline) to format the password input |
| `passwd`          | Sets the password for the new user                                          |
| `<<help ... help` | Multiline comment block (not executed)                                      |

---

## ⚠️ Notes

* This script must be run with **sudo/root privileges**.
* Password is entered in plain text and visible—use with caution in secure environments.
* You can improve security by hiding password input using `read -s`, like this:

```bash
read -s -p "Enter the password (hidden): " password
echo
```

---

## 🛠️ How to Use

1. **Create the script:**

   ```bash
   nano create-user.sh
   ```

   Paste the script into the file and save.

2. **Make it executable:**

   ```bash
   chmod +x create-user.sh
   ```

3. **Run the script with sudo:**

   ```bash
   sudo ./create-user.sh
   ```

---

## ✅ Sample Output

```bash
============ Creation of user started ============
Enter the username: testuser
Enter the password: testpass
Changing password for user testuser.
passwd: all authentication tokens updated successfully.
============ Creation of user completed ==========
```
