
# 🎬 Bash Script: Taking User Input Using `read`

This script demonstrates how to take **interactive input from the user** using the `read` command in a Bash script. It uses the `-p` option to **prompt** the user directly.

---

## 📜 Script Content (`user-input.sh`)

```bash
#!/bin/bash

# A simple script to take user input for a movie name

# Prompt the user to enter the movie name
read -p "Movie ka name kya hai: " fullname

# Output the user-provided movie name
echo "Movie ka name: $fullname"
````

---

## 🧠 Explanation

### 🔹 `read`

The `read` command is used to **take input from the user** during script execution.

### 🔹 `-p "prompt message"`

The `-p` option allows you to display a **prompt message** on the same line before accepting input.

### 🔹 `fullname`

This is a **variable** where the input will be stored.

---

## 🧪 How It Works

1. When you run the script:

   ```bash
   ./user-input.sh
   ```

2. It displays:

   ```
   Movie ka name kya hai:
   ```

3. You type:

   ```
   Sholay
   ```

4. It then prints:

   ```
   Movie ka name: Sholay
   ```

---

## 🛠️ Steps to Use

1. **Create the script:**

   ```bash
   nano user-input.sh
   ```

   Paste the script content and save it.

2. **Give execute permission:**

   ```bash
   chmod +x user-input.sh
   ```

3. **Run the script:**

   ```bash
   ./user-input.sh
   ```

---

## ✅ Output Example

```bash
Movie ka name kya hai: Sholay
Movie ka name: Sholay

