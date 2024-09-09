# How to Create LVM Partition in Linux: A Step-by-Step Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Step 1: Identify New Attached Raw Disk](#step-1-identify-new-attached-raw-disk)
4. [Step 2: Create PV (Physical Volume)](#step-2-create-pv-physical-volume)
5. [Step 3: Create VG (Volume Group)](#step-3-create-vg-volume-group)
6. [Step 4: Create LV (Logical Volume)](#step-4-create-lv-logical-volume)
7. [Step 5: Format LVM Partition](#step-5-format-lvm-partition)

## Introduction

This guide demonstrates how to create an LVM partition step-by-step in Linux. LVM (Logical Volume Management) is the recommended method for managing disk or storage on Linux systems, especially for servers. The main advantage of LVM partitions is the ability to extend their size online without downtime.

For this demonstration, we'll use Ubuntu 22.04 with a 15GB disk attached.

## Prerequisites

- Raw disk attached to Linux system
- Local user with sudo rights
- Pre-installed lvm2 package

## Step 1: Identify New Attached Raw Disk

1. Open the terminal and run:
   ```
   $ sudo dmesg | grep -i sd
   ```
   Look for the new 15GB disk in the output.

2. Alternatively, use the fdisk command:
   ```
   $ sudo fdisk -l | grep -i /dev/sd
   ```

From the output, we can confirm that the new attached disk is '/dev/sdb'.

## Step 2: Create PV (Physical Volume)

1. Ensure lvm2 package is installed:
   ```
   $ sudo apt install lvm2     // On Ubuntu / Debian
   $ sudo dnf install lvm2    // on RHEL / CentOS
   ```

2. Create PV on disk /dev/sdb:
   ```
   $ sudo pvcreate /dev/sdb
   ```

3. Verify PV status:
   ```
   $ sudo pvs /dev/sdb
   ```
   or
   ```
   $ sudo pvdisplay /dev/sdb
   ```

## Step 3: Create VG (Volume Group)

1. Create a volume group named 'volgrp01':
   ```
   $ sudo vgcreate volgrp01 /dev/sdb
   ```

2. Verify VG status:
   ```
   $ sudo vgs volgrp01
   ```
   or
   ```
   $ sudo vgdisplay volgrp01
   ```

## Step 4: Create LV (Logical Volume)

1. Create an LV of size 14GB:
   ```
   $ sudo lvcreate -L 14G -n lv01 volgrp01
   ```

2. Validate LV status:
   ```
   $ sudo lvs /dev/volgrp01/lv01
   ```
   or
   ```
   $ sudo lvdisplay /dev/volgrp01/lv01
   ```

## Step 5: Format LVM Partition

1. Format the LVM partition (choose ext4 or xfs):
   ```
   $ sudo mkfs.ext4 /dev/volgrp01/lv01
   ```
   or
   ```
   $ sudo mkfs.xfs /dev/volgrp01/lv01
   ```

2. Create a mount point:
   ```
   $ sudo mkdir /mnt/data
   ```

3. Mount the partition:
   ```
   $ sudo mount /dev/volgrp01/lv01 /mnt/data/
   ```

4. Verify the mount:
   ```
   $ df -Th /mnt/data/
   ```

5. Test by creating a dummy file:
   ```
   $ cd /mnt/data/
   $ echo "testing lvm partition" | sudo tee dummy.txt
   $ cat dummy.txt
   $ sudo rm -f dummy.txt
   ```

6. For permanent mounting, add to fstab:
   ```
   $ echo '/dev/volgrp01/lv01  /mnt/data  ext4  defaults 0 0' | sudo tee -a /etc/fstab
   $ sudo mount -a
   ```

This completes the process of creating an LVM partition in Linux.
