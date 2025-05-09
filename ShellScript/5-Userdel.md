### 📄 `explain-userdel-check.md`

````markdown
# 🧾 Bash Script: Delete User and Verify Deletion

This small script demonstrates how to delete a Linux user using `sudo userdel`, and then verifies whether the user was successfully removed by checking the `/etc/passwd` file.

---

## 📜 Script Snippet

```bash
sudo userdel $username
echo "Deletion of user completed"

cat /etc/passwd | grep $username | wc | awk '{print $1}'
````

---

## 🧠 Explanation Line by Line

### 🔸 `sudo userdel $username`

* `userdel` is a Linux command used to delete a user account.
* `$username` is a variable that holds the name of the user to be deleted.
* `sudo` is required because only superusers can delete user accounts.
* This **does not delete the user’s home directory** unless you use the `-r` option like `sudo userdel -r $username`.

---

### 🔸 `echo "Deletion of user completed"`

* Simply prints a confirmation message that the `userdel` command was executed.
* This **does not mean the user is deleted successfully** — it only confirms the command was issued.

---

### 🔸 `cat /etc/passwd | grep $username | wc | awk '{print $1}'`

This command chain checks whether the user still exists in the system:

#### 🔹 Breakdown:

1. `cat /etc/passwd`

   * Displays all the user accounts on the system. Each line corresponds to one user.

2. `grep $username`

   * Filters the lines from `/etc/passwd` that match the username.
   * If the user still exists, you'll see at least one line.

3. `wc`

   * `wc` stands for "word count".
   * Without an option, it returns 3 values: lines, words, and characters.

4. `awk '{print $1}'`

   * Extracts the **first field**, which is the **line count** from the previous result.

#### 🔹 What It Does:

* If the user **has been deleted**, the output will be `0`.
* If the user **still exists**, the output will be `1` or more.

---

## ✅ Example

Assume you want to delete a user named `testuser`.

```bash
username=testuser
sudo userdel $username
echo "Deletion of user completed"
cat /etc/passwd | grep $username | wc | awk '{print $1}'
```

**Output:**

```
Deletion of user completed
0
```

* `0` confirms the user `testuser` no longer exists in `/etc/passwd`.

---

````markdown
# 🗑️ Bash Script: Delete a Linux User

This script helps you safely delete a user from a Linux system using Bash. It prompts the user for a username, deletes the account, and optionally removes the user's home directory.

---

## 🧾 Script Content (`delete-user.sh`)

```bash
#!/bin/bash

<<help
This script:
- Prompts the admin for the username to delete
- Deletes the user account
- Optionally deletes the user's home directory

Commands:
- read -p: Prompts for input
- sudo userdel: Deletes a user
- sudo userdel -r: Deletes user and home directory
- <<help ... help: Multiline comment block
help

echo "============ User Deletion Script Started ============"

# Ask for the username to delete
read -p "Enter the username you want to delete: " username

# Confirm before deletion
read -p "Do you also want to delete the user's home directory? (yes/no): " delete_home

# Perform deletion
if [ "$delete_home" == "yes" ]; then
    sudo userdel -r "$username"
    echo "User '$username' and home directory deleted."
else
    sudo userdel "$username"
    echo "User '$username' deleted (home directory kept)."
fi

echo "============ User Deletion Script Completed ============"
````

---

## 🛠️ How to Use

1. **Create the script:**

   ```bash
   nano delete-user.sh
   ```

   Paste the script above and save it.

2. **Make the script executable:**

   ```bash
   chmod +x delete-user.sh
   ```

3. **Run the script with sudo privileges:**

   ```bash
   sudo ./delete-user.sh
   ```

---

## ✅ Sample Output

```bash
============ User Deletion Script Started ============
Enter the username you want to delete: testuser
Do you also want to delete the user's home directory? (yes/no): yes
User 'testuser' and home directory deleted.
============ User Deletion Script Completed ============
```

---

## ⚠️ Notes

* You **must run the script as root or with `sudo`**, or it won't be able to delete the user.
* If the user is logged in, deletion might fail unless the user is logged out.
* Use the `-r` option with `userdel` cautiously, as it **removes all files in the user's home directory**.


