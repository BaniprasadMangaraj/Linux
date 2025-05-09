
````markdown
# 📦 Bash Script: Install a Single Package Using Argument

This script installs a single Linux package provided as a command-line argument. It uses `apt-get` to update the system and install the specified package.

---

## 🧾 Script Content (`install-one.sh`)

```bash
#!/bin/bash

<<info
This script installs a single package passed as an argument.
Usage:
    ./install-one.sh <package-name>

Example:
    ./install-one.sh curl
info

# Display the name of the package being installed
echo "📦 Installing package: $1"

# Update the system package index (hidden output)
sudo apt-get update > /dev/null

# Install the package
sudo apt-get install "$1" -y

# Confirm installation
echo "✅ Installation completed for: $1"
````

---

## 🧠 Explanation

| Line                              | Purpose                                               |
| --------------------------------- | ----------------------------------------------------- |
| `echo "Installing $1"`            | Shows the name of the package being installed         |
| `sudo apt-get update > /dev/null` | Updates the package list quietly (no terminal output) |
| `sudo apt-get install $1 -y`      | Installs the package passed as the first argument     |
| `-y`                              | Automatically confirms the installation prompt        |
| `echo "install completed"`        | Notifies user that the installation is done           |

---

## 💡 Why Use `/dev/null`?

### ❓ What is `/dev/null`?

* `/dev/null` is a **special file** in Linux/Unix systems often called a **"black hole"**.
* Anything written to `/dev/null` is **discarded immediately**, meaning it won’t be shown on the terminal or saved to a file.

### 🔍 Usage in the Script

* **`sudo apt-get update > /dev/null`**: The `apt-get update` command updates the system’s package list. By adding `> /dev/null`, we suppress the output (i.e., we don’t see the terminal scroll of update details).

* **Why Use `/dev/null`?**

  * **Prevent Clutter**: Running `apt-get update` typically generates a lot of terminal output. By redirecting this to `/dev/null`, we keep the terminal output clean and focus only on what’s important — the installation result.
  * **Silent Updates**: For automated scripts, you might not need to display update details. Sending the output to `/dev/null` avoids unnecessary noise.

### 🔒 Example of Using `/dev/null`:

If we didn't use `/dev/null`:

```bash
sudo apt-get update
```

The terminal will show update messages.

With `/dev/null`:

```bash
sudo apt-get update > /dev/null
```

The terminal stays clean.

---

## ⚙️ How to Use

1. **Create the script file:**

   ```bash
   nano install-one.sh
   ```

   Paste the above script and save.

2. **Make it executable:**

   ```bash
   chmod +x install-one.sh
   ```

3. **Run the script with a package name:**

   ```bash
   ./install-one.sh git
   ```

---

## ✅ Sample Output

```bash
📦 Installing package: git
✅ Installation completed for: git
```

---

## ⚠️ Notes

* You must run this script on Debian/Ubuntu systems where `apt-get` is available.
* The script will fail if:

  * No package name is given.
  * The package doesn't exist.
  * You're not running with `sudo` or root privileges.

---

## 🛡️ Bonus: Add Basic Error Check (Optional)

You can prevent empty input like this:

```bash
if [ -z "$1" ]; then
    echo "❌ Error: No package name provided."
    echo "Usage: ./install-one.sh <package-name>"
    exit 1
fi
```

