
## ⏰ Automating Backups with Cron (Linux)

This guide explains how to **automatically run your `backup.sh` script** using a cron job at regular intervals (daily, weekly, etc.).

---

### 📌 What is Cron?

Cron is a Linux utility that lets you **schedule tasks** (called *cron jobs*) to run automatically at specified times or intervals.

---

### 🛠️ Prerequisites

* Your script (`backup.sh`) is working and executable
* The `zip` package is installed
* You have a valid source and destination directory

---

### ✅ Step 1: Make the Script Executable

```bash
chmod +x /home/ubuntu/script/backup.sh
```

---

### ✅ Step 2: Open the Crontab Editor

Run:

```bash
crontab -e
```
---
![image](https://github.com/user-attachments/assets/380e25fb-6b25-497c-8036-09801017bff6)

---

> This opens your user’s cron configuration in the default text editor.

---

### ✅ Step 3: Add a Cron Job

Here’s a sample entry to run the backup script **every day at 2:00 AM**:

```cron
0 2 * * * /home/ubuntu/script/backup.sh /home/ubuntu/scripts /home/ubuntu/backup
```

### ⏱ Cron Timing Format

```
* * * * * command_to_run
| | | | |
| | | | +----- Day of the week (0 - 6) [Sunday = 0]
| | | +------- Month (1 - 12)
| | +--------- Day of the month (1 - 31)
| +----------- Hour (0 - 23)
+------------- Minute (0 - 59)
```

### 🕒 More Schedule Examples

| Time                | Cron Expression | Meaning                     |
| ------------------- | --------------- | --------------------------- |
| Every day @ 2 AM    | `0 2 * * *`     | Daily backup at 2 AM        |
| Every hour          | `0 * * * *`     | Runs every hour on the hour |
| Every Sunday @ 1 AM | `0 1 * * 0`     | Weekly backup every Sunday  |

---

### ✅ Step 4: Save and Exit

After adding the cron job, save and exit the editor.
Your backup script is now scheduled to run automatically!

---

### 🔍 Check if Cron is Running

Ensure the cron service is running:

```bash
sudo systemctl status cron
```

---

### 📁 Where Backups Will Be Stored

Backups will be stored in the destination folder you provide, e.g.:

```
/home/ubuntu/backup/backups-YYYY-MM-DD.zip
```
