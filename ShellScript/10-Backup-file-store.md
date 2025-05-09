## 📦 Periodic Backup Shell Script

This script allows you to take **periodic backups** of a specified source directory and stores the backup as a `.zip` file in the destination directory.

---

### ✅ What This Script Does

* Takes two input paths: source and destination
* Compresses the **entire source folder** into a `.zip` file
* Adds a **timestamp** to the backup filename for uniqueness
* Stores the backup in the destination folder

---

### 📂 Example Directory Structure

---
![image](https://github.com/user-attachments/assets/8e25aeb5-5c23-4b33-88ea-e0721d92cf55)

---

```bash
/home/ubuntu/scripts     # Source directory
/home/ubuntu/backup      # Destination directory (where .zip files will be saved)
```

---

### 🛠️ Script: `backup.sh`

```bash
#!/bin/bash

<<info
This shell will take periodical backups

Example:
./backup.sh <src> <des>
src /home/ubuntu/scripts
des /home/ubuntu/backup
info

src=$1
des=$2

timestamp=$(date '+%Y-%m-%d')

zip -r "$des/backups-$timestamp.zip" $src > /dev/null

echo "++++++++++++++++++++++++++Backup Completed ++++++++++++++++++++++++++++++"
```

---

### 🚀 How to Use

1. **Make the script executable**:

   ```bash
   chmod +x backup.sh
   ```

2. **Run the script** with source and destination paths:

   ```bash
   ./backup.sh /home/ubuntu/scripts /home/ubuntu/backup
   ```

---

### 📌 Output

The script will create a file like this in your destination folder:

```
/home/ubuntu/backup/backups-2025-05-09.zip
```

✅ You’ll see this message if everything goes well:

```
++++++++++++++++++++++++++Backup Completed ++++++++++++++++++++++++++++++
```

---

### ❗ Requirements

Make sure the `zip` command is installed:

```bash
sudo apt install zip -y
```


