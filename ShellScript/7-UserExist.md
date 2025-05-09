### `check-user.sh`

This script prompts you to input a username and checks if that username exists on your system by searching through the `/etc/passwd` file, which contains details about all users.

```bash
#!/bin/bash

# Prompt user for input
read -p "Enter the username you wish to check: " username

# Count occurrences of the username in /etc/passwd
count=$(cat /etc/passwd | grep "$username" | wc -l)

# Check if the count is greater than 0 (user exists)
if [ "$count" -gt 0 ]; then
    echo "✅ User '$username' exists in the system."
else
    echo "❌ User '$username' does not exist in the system."
fi
````

---

## 🧠 Explanation of the Script

Here’s a breakdown of what each part of the script does:

1. **Prompting for the Username**

   * `read -p "Enter the username you wish to check: " username`:
     This line asks the user to input a username and stores it in the variable `username`.

2. **Searching for the User**

   * `count=$(cat /etc/passwd | grep "$username" | wc -l)`:

     * **`cat /etc/passwd`**: Displays the contents of the `/etc/passwd` file, which contains information about all users.
     * **`grep "$username"`**: Searches for the entered username in the `/etc/passwd` file.
     * **`wc -l`**: Counts how many lines match the search. If the username exists, it will return a number greater than 0.

3. **Checking if the User Exists**

   * `if [ "$count" -gt 0 ]; then`:
     If the count is greater than 0, the user exists.
   * `echo "✅ User '$username' exists in the system."`: Displays a success message.
   * `else`: If the count is 0, the user doesn't exist.
   * `echo "❌ User '$username' does not exist in the system."`: Displays a failure message.

4. **Ending the Conditional Statement**

   * `fi`: Ends the `if` block.

---

## ⚙️ How to Use

### Step 1: Create the Script File

1. Open your terminal and create a new script file using a text editor:

   ```bash
   nano check-user.sh
   ```

2. Paste the above script into the editor.

3. Save and exit (`CTRL + X`, then `Y` to confirm).

### Step 2: Make the Script Executable

Run the following command to make your script executable:

```bash
chmod +x check-user.sh
```

### Step 3: Run the Script

To run the script, type:

```bash
./check-user.sh
```

You will be prompted to enter a username. Enter the username you wish to check.

### Example Output

**When the user exists:**

```bash
Enter the username you wish to check: johndoe
✅ User 'johndoe' exists in the system.
```

**When the user doesn't exist:**

```bash
Enter the username you wish to check: unknownuser
❌ User 'unknownuser' does not exist in the system.
```

---

## ⚠️ Important Notes

* The `/etc/passwd` file contains information about all users on the system. This is why the script searches through it to find the given username.
* The **`grep`** command is used to search for the entered username.
* **`wc -l`** is used to count the number of lines returned by the `grep` command. If the username exists, the count will be greater than 0.

---

## 💡 Additional Tips

* **What is `grep`?**
  `grep` is a command-line utility used to search for a specific pattern (in this case, the username) in a file. If it finds the pattern, it returns the matching lines.

* **What is `wc -l`?**
  `wc` stands for **word count**. The `-l` flag counts the number of lines in the output, which helps us know how many times the username appears.

---

