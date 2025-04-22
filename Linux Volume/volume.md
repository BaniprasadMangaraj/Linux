

# 📘 Linux Volume Management with AWS EBS (Step-by-Step Guide)

This guide will walk you through:
- Understanding volumes in Linux
- Working with AWS Elastic Block Store (EBS)
- Using **Logical Volume Manager (LVM)** for flexible, dynamic storage on EC2

---

## 📖 1. Introduction

### 💡 What is a Volume?
A **volume** is storage that can be used by your operating system to store data, just like your local hard drive.

### 🖥️ In AWS:
- **EBS (Elastic Block Store)** provides block-level storage volumes for EC2 instances.
- You can attach EBS volumes to EC2 instances just like plugging a USB drive into your computer.

### 🧱 In Linux:
There are different levels of managing storage:
- **Physical Volume (PV)**: Actual disk devices (e.g., `/dev/xvdf`)
- **Volume Group (VG)**: A pool of one or more physical volumes
- **Logical Volume (LV)**: Virtual partitions created from a volume group

---



## 📌 Table of Contents
1. [Introduction](#introduction)
2. [Types of Volumes](#types-of-volumes)
3. [Mounting Volumes in Linux](#mounting-volumes-in-linux)
4. [Managing AWS EBS on EC2](#managing-aws-ebs-on-ec2)
5. [Logical Volume Manager (LVM)](#logical-volume-manager-lvm)
6. [Using LVM with EBS for Dynamic Storage](#using-lvm-with-ebs-for-dynamic-storage)

---

## 🧠 Introduction

In Linux, storage can be managed in different ways using:
- Physical Volumes (PV)
- Volume Groups (VG)
- Logical Volumes (LV)

In AWS, you can use **Elastic Block Store (EBS)** to attach persistent block storage to EC2 instances.

---

## 🔄 Types of Volumes

| Type             | Description |
|------------------|-------------|
| **Physical Volume (PV)** | Actual disk device (e.g., `/dev/xvdf`) |
| **Volume Group (VG)**    | Pool of storage from multiple PVs |
| **Logical Volume (LV)**  | Logical partition created from VG |

---

## 🔧 Mounting Volumes in Linux

```bash
# Check mounted volumes
df -h

# List block devices
lsblk
```

---

## ☁️ Managing AWS EBS on EC2

### Step 1: Create EC2 Instance
- Instance Name: `volume`
- Storage: 8 GB

### Step 2: Connect to the EC2 Instance

```bash
df -h     # Check usage
lsblk     # View attached block devices
```

### Step 3: Create and Attach Additional EBS Volumes
- Go to **EC2 > Elastic Block Store > Volumes**
- Create three volumes: `5GB`, `8GB`, and `10GB`
- Attach them to the instance using `/dev/sdf`, `/dev/sdg`, `/dev/sdh`

```bash
lsblk     # Verify attached volumes (e.g., xvdf, xvdg, xvdh)
```

---

## 🧱 Logical Volume Manager (LVM)

### Step 1: Create Physical Volumes

```bash
pvcreate /dev/xvdf /dev/xvdg /dev/xvdh
pvs        # Check physical volumes
```

### Step 2: Create a Volume Group

```bash
vgcreate tws-vg /dev/xvdf /dev/xvdg /dev/xvdh
vgs        # Check volume group
```

### Step 3: Create a Logical Volume

```bash
lvcreate -L 10G -n tws-lv tws-vg
lvs        # Check logical volume
pvdisplay  # View PV details
```

---

## 📁 Mounting the Logical Volume

```bash
# Create mount directory
mkdir /mnt/tws-lv-mount

# Format the logical volume
mkfs.ext4 /dev/tws-vg/tws-lv

# Mount the volume
mount /dev/tws-vg/tws-lv /mnt/tws-lv-mount

# Verify
df -h
```

---

## 💼 Mounting Non-LVM EBS Volume

```bash
# Create directory
mkdir /mnt/tws-disk-mount

# Format disk
mkfs -t ext4 /dev/xvdh

# Mount the volume
mount /dev/xvdh /mnt/tws-disk-mount
```

---

## ⚙️ Dynamic Storage Management with LVM

You can extend your logical volume on the fly:

```bash
# Extend logical volume by 5GB
lvextend -L +5G /dev/tws-vg/tws-lv

# Resize the filesystem (optional depending on FS type)
resize2fs /dev/tws-vg/tws-lv
```

