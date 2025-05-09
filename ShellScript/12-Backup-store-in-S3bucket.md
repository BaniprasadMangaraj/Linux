
## 🔧 Steps to Create an S3 Bucket and Set Up AWS CLI

### 1. **Create an AWS S3 Bucket**

1. Go to the **AWS S3 Console**:
   [S3 Console](https://s3.console.aws.amazon.com/s3/)

2. **Click on "Create bucket"**.

3. **Provide a unique name** for your bucket (e.g., `baniprasad-s3bucket`).

4. Choose the **Region** where you want to create the bucket.

5. Optionally, enable **versioning**, **encryption**, etc., based on your requirements.

6. Click on **Create**.

---

### 2. **Create an IAM User for Configuration**

1. Go to the **AWS IAM Console**:
   [IAM Console](https://console.aws.amazon.com/iam/)

2. Click on **Users** > **Add user**.

3. Enter the **username** (e.g., `backup-user`).

4. Choose **Programmatic access**.

5. **Set permissions**:

   * Select **Attach existing policies directly**.
   * Attach the **`AmazonS3FullAccess`** policy (to give access to S3).

6. Click on **Next: Tags**, then **Next: Review**, and finally **Create user**.

7. **Download or copy** the **Access Key ID** and **Secret Access Key**. You will need these for configuring the AWS CLI.

---

### 3. **Install AWS CLI v2 on Your Server**

1. Update the server:

   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

2. **Download AWS CLI v2**:

   ```bash
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   ```

3. **Unzip the downloaded file**:

   ```bash
   unzip awscliv2.zip
   ```

4. **Install AWS CLI**:

   ```bash
   sudo ./aws/install
   ```

5. **Verify AWS CLI installation**:

   ```bash
   aws --version
   ```

---

### 4. **Configure AWS CLI with IAM User Credentials**

1. **Configure AWS CLI** by running:

   ```bash
   aws configure
   ```

2. Enter the following details when prompted:

   * **AWS Access Key ID**: Paste the **Access Key** from the IAM user.
   * **AWS Secret Access Key**: Paste the **Secret Access Key** from the IAM user.
   * **Default region name**: Choose your region (e.g., `us-east-1`).
   * **Default output format**: Choose `json`.

---

### 5. **Sync Local Backup Folder to S3 Bucket**

1. To sync your local backup folder (`backup/`) to the S3 bucket (`baniprasad-s3bucket`), run:

   ```bash
   aws s3 sync backup/ s3://baniprasad-s3bucket
   ```

   This will upload the contents of the `backup/` folder to the `baniprasad-s3bucket`.

---

### 6. **Update Your Backup Script to Include AWS S3 Sync**

---
![image](https://github.com/user-attachments/assets/42a56a8f-9ff9-4dd1-a3fd-f9ac40747737)


---

Now, let’s modify your backup script to automatically sync the backup folder to your S3 bucket after the backup is created.

Edit your **`backup.sh`** script and add the following line to sync the backup to S3:

```bash
#!/bin/bash

<<info
This shell will take periodic backups and store them in an S3 bucket.

Usage:
./backup.sh <src> <des_s3_bucket>

Example:
./backup.sh /home/ubuntu/scripts s3://your-bucket-name/backup
info

# Assign input arguments
src=$1
des=$2

# Validate input
if [[ -z "$src" || -z "$des" ]]; then
  echo "❌ Error: Please provide both source and destination."
  echo "Usage: ./backup.sh <source_path> <destination_s3_path>"
  exit 1
fi

# Check if 'zip' is installed
if ! command -v zip &> /dev/null; then
  echo "❌ Error: 'zip' command not found. Please install it with 'sudo apt install zip'"
  exit 1
fi

# Generate timestamp
timestamp=$(date '+%Y-%m-%d_%H-%M-%S')

# Perform backup
backup_file="backups-$timestamp.zip"
zip -r "$backup_file" "$src" > /dev/null

# Upload to S3 bucket
aws s3 sync "$des" s3://baniprasad-s3bucket

# Clean up the local backup file
rm "$backup_file"

# Notify completion
echo "✅ Backup completed successfully and uploaded to S3: $des/$backup_file"
```

---

### 7. **Automate the Backup Script with Cron (Optional)**

To automate the backup script, you can schedule it to run periodically using cron:

1. Open the crontab editor:

   ```bash
   crontab -e
   ```

2. Add a cron job to run the backup script daily at 2 AM:

   ```bash
   0 2 * * * /home/ubuntu/script/backup.sh /home/ubuntu/scripts s3://baniprasad-s3bucket/backup
   ```

   This will run the backup script every day at **2:00 AM**.

---

---
![image](https://github.com/user-attachments/assets/95d9a3a1-1867-4d54-a599-d90f9981c03d)

---



##  File for Backup and S3 Integration**

````markdown
# Backup Script with S3 Integration

This script will take periodic backups of a specified directory and upload them to an Amazon S3 bucket.

## 🔧 Prerequisites

- **AWS CLI** installed and configured with IAM credentials.
- **An S3 bucket** to store the backups.
- **Access to your S3 bucket**.

## 📝 Steps to Use

### 1. Install the AWS CLI (if not installed)

```bash
sudo apt update
sudo apt install awscli -y
````

### 2. Configure AWS CLI

```bash
aws configure
```

Enter your **Access Key ID**, **Secret Access Key**, and **region** when prompted.

### 3. Make the script executable

```bash
chmod +x /home/ubuntu/script/backup.sh
```

### 4. Run the script

To run the backup script, use the following command:

```bash
./backup.sh /home/ubuntu/scripts s3://baniprasad-s3bucket/backup
```

### 5. Sync to S3

The backup will be synced to your S3 bucket (`s3://baniprasad-s3bucket/backup`).

### 6. Automate the script with Cron (optional)

To run this backup script periodically (e.g., every day at 2 AM), add it to your crontab:

```bash
crontab -e
```

Add the following line to schedule the backup:

```bash
0 2 * * * /home/ubuntu/script/backup.sh /home/ubuntu/scripts s3://baniprasad-s3bucket/backup
```

---
![image](https://github.com/user-attachments/assets/1ed0a9c4-97d2-4189-935d-47f9b9faafc9)

---

---

## ✅ Summary

* The script compresses the source directory into a `.zip` file.
* It uploads the backup to an S3 bucket with a timestamped filename.
* You can automate the process with **Cron** to back up periodically.

---

## 🔗 Helpful Links

* [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
* [Cron Expression Generator](https://crontab.guru/)

```

---

### ✅ Summary of Steps

1. Create an **S3 bucket**.
2. Create an **IAM user** and generate **Access Key and Secret Key**.
3. Install **AWS CLI** and configure it with your credentials.
4. Update the **backup script** to upload backups to the S3 bucket using `aws s3 sync`.
5. Optionally, automate the script using **cron**.
