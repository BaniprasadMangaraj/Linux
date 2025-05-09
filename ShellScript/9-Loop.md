
## 🧠 What is a Loop in Shell Scripting?

A **loop** is a control structure that allows you to run a block of code **multiple times**. This is useful when you want to repeat actions, like processing files, checking statuses, or printing messages.

---

## 🔁 Types of Loops in Shell

| Loop Type    | Description                                 |
| ------------ | ------------------------------------------- |
| `for` loop   | Repeats for a fixed set of values or range. |
| `while` loop | Runs while a condition is true.             |
| `until` loop | Runs until a condition becomes true.        |

---

## 📌 Example: `for` Loop to Print Numbers from 1 to 5

### 🔧 Script

```bash
#!/bin/bash

# Function to print numbers from 1 to 5
print-numbers() {
    for i in {1..5}   # Loop from 1 to 5
    do
        echo "Number: $i"
    done
    echo "========= Loop Completed ========="
}

# Call the function
print-numbers
```

---

### 💬 Example Output

```bash
$ ./print_numbers.sh
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
========= Loop Completed =========
```

---

## 🔍 Explanation of the Script

| Line                      | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| `#!/bin/bash`             | Declares that the script runs using the Bash shell.   |
| `print-numbers() { ... }` | Defines a function named `print-numbers`.             |
| `for i in {1..5}`         | Begins a `for` loop that iterates from 1 to 5.        |
| `do ... done`             | Marks the block of code to execute on each iteration. |
| `echo "Number: $i"`       | Prints the current value of `i`.                      |
| `print-numbers`           | Calls the function to execute the loop.               |

---

## 🚀 How to Run the Script

1. Save it to a file:

   ```bash
   nano print_numbers.sh
   ```

2. Make it executable:

   ```bash
   chmod +x print_numbers.sh
   ```

3. Run it:

   ```bash
   ./print_numbers.sh
   ```

---

## ✨ Bonus: Customize the Loop

You can easily change the range or logic:

```bash
for i in {10..15}; do
  echo "Current Value: $i"
done
```

Or use a C-style loop:

```bash
for ((i=1; i<=5; i++)); do
  echo "i = $i"
done
```

---

## 🧪 More Real-World Use Cases

* Loop over files in a directory:

  ```bash
  for file in *.txt; do
    echo "Found file: $file"
  done
  ```

* Loop over a list of names:

  ```bash
  for name in Alice Bob Charlie; do
    echo "Hello, $name"
  done
  ```


