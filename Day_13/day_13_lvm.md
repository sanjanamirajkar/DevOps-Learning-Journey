# Day 13 Linux Volume Management (LVM) CMD..

**What is LVM?**

LVM (Logical Volume Manager) allows flexible disk management in Linux.
Instead of fixed partitions, LVM lets you:

Resize volumes dynamically

- Combine multiple disks into one pool

- Extend storage without downtime (in most cases)

**LVM Structure:**

**PV (Physical Volume)**  Physical disk or loop device

**VG (Volume Group)** Pool of storage created from PV

**LV (Logical Volume)** Usable partition created from VG

### Step-by-Step Implementation

**Switch to Root**..
```
sudo -i
```
### Task 1: Check Current Storage
```
lsblk
pvs
vgs
lvs
df -h
```

Cmd Explain :

- lsblk shows block devices.

- pvs, vgs, lvs show nothing initially (fresh setup).

- df -h shows currently mounted filesystems.

**If No Spare Disk Create Virtual Disk**
```
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a
```
**Example loop device: /dev/loop0**

### Task 2: Create Physical Volume
```
pvcreate /dev/loop0
pvs
```

**CMD explain :**

- pvcreate initializes disk for LVM.

- pvs confirms PV creation.

### Task 3: Create Volume Group
```
vgcreate devops-vg /dev/loop0
vgs
```

**CMD explain :**

- VG is storage pool.

- Space of PV is now inside devops-vg.

### Task 4: Create Logical Volume
```
lvcreate -L 500M -n app-data devops-vg
lvs
```
**CMD explain :**

- Created 500MB logical volume.

- LV path: /dev/devops-vg/app-data

### Task 5: Format and Mount
```
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```
**CMD explain :**

- Formatting is required before mounting.

- Now usable like a normal partition.

### Task 6: Extend Logical Volume
```
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```
**CMD explain :**

- lvextend increases LV size.

- resize2fs resizes filesystem.

- Storage increased without deleting data.


## LVM Overview....

- Storage Structure: LVM works in three layers — Physical Volumes (PV) → Volume Groups (VG) → Logical Volumes (LV).

- Flexible Management: Unlike traditional partitions, LVM allows you to resize volumes dynamically.

- Creating PVs: Use pvcreate to convert raw disks or partitions into physical volumes.

- Volume Groups: Combine multiple PVs into a single VG to manage storage as one pool.

- Resizing Filesystem: After extending an LV, run resize2fs to use the added space.

- Mounting LVs: Format with mkfs.ext4 and mount to a directory for usage.

- Direct PV Mounting: Possible but not recommended — LVM abstraction is better.

---

### Output of Physical volume, Volume group and Logical volume created and mounted

<img width="1122" height="315" alt="Screenshot 2026-03-19 201026" src="https://github.com/user-attachments/assets/01fb5918-643e-4ecc-a7c4-d676e2f94369" />

<img width="1084" height="456" alt="Screenshot 2026-03-19 201105" src="https://github.com/user-attachments/assets/b8328641-89bb-4fad-8c60-df2e08be84de" />