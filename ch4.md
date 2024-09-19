# Disks and Filesystems

- **Overview**: This chapter dives into how to work with disks on a Linux system. 
  - Topics covered include partitioning disks, creating and maintaining filesystems, and working with swap space.

---

# Disk Devices in Linux

- **Device Names**: Disk devices typically have names like `/dev/sda` for the first disk.
  - Partitions are represented as `/dev/sda1`, `/dev/sdb3`, etc.
  - The kernel allows access to both entire disks and individual partitions simultaneously.
  
- **Partition Table**: Stores information on disk partitions.
  - Partitions are subdivisions of the disk.
  - Linux uses tools like `parted` and `fdisk` for managing partition tables.
  
- **Linux Logical Volume Manager (LVM)**: Adds flexibility to traditional disk management by pooling storage from multiple devices.

---

# Disk Partitioning

- **Partitioning Tools**:
  - **parted**: Text-based, supports MBR and GPT.
  - **gparted**: Graphical version of `parted`.
  - **fdisk**: Traditional partitioning tool for MBR and GPT, commonly used for creating and modifying partition tables.

- **Viewing Partition Tables**:
  - Use `parted -l` to display partition tables on your system.
  - Example:
    ```bash
    # parted -l
    Model: ATA Disk (scsi)
    Disk /dev/sda: 240GB
    Partition Table: msdos
    ```

- **MBR Basics**:
  - MBR supports up to four primary partitions; for more, use extended partitions.
  - Logical partitions exist within extended partitions.

---

# Creating and Modifying Partition Tables

- **Creating a New Partition Table**:
  - Example using `fdisk`:
    ```bash
    # fdisk /dev/sdd
    Command (m for help): n
    ```
  - You specify partition type, number, and size, and finalize the changes using the `w` command to write to the disk.

- **Modifying Partition Tables**:
  - Be cautious, as altering the partition table can destroy existing data.
  - Ensure no partitions on the disk are currently in use.

- **Partitioning SSDs**:
  - SSDs require proper partition alignment for performance.
  - Use tools like `fdisk` or `/sys/block` to check partition alignment.

---

# Filesystems

- **Overview**: Filesystems provide the structure to transform block devices into files and directories.
  - Different types of filesystems (ext4, Btrfs, FAT, XFS, etc.) are used for different purposes.

- **Common Filesystems**:
  - **ext4**: Default Linux filesystem, supports journaling and large files.
  - **Btrfs**: Newer, advanced filesystem with features like snapshots.
  - **FAT**: Used for compatibility with Windows and removable media.
  - **XFS**: High-performance filesystem for enterprise use.

---

# Creating and Mounting Filesystems

- **Creating Filesystems**:
  - Use `mkfs` to create a new filesystem.
  - Example for ext4:
    ```bash
    # mkfs -t ext4 /dev/sdf2
    ```

- **Mounting Filesystems**:
  - Attach a filesystem to the system with the `mount` command.
  - Example:
    ```bash
    # mount -t ext4 /dev/sdf2 /mnt/data
    ```
  - View currently mounted filesystems using `mount`.

- **Unmounting Filesystems**:
  - Detach a filesystem with the `umount` command:
    ```bash
    # umount /mnt/data
    ```

- **Mount Options**:
  - Common options include `ro` (read-only), `rw` (read-write), and `noexec` (disable execution).
  - Example:
    ```bash
    # mount -o ro /dev/sdf2 /mnt/data
    ```

---

# Managing Filesystems

- **Checking Filesystem Capacity**:
  - Use `df` to view filesystem usage.
  - Example:
    ```bash
    $ df -h
    Filesystem  Size  Used  Avail  Use%  Mounted on
    /dev/sda1   100G   20G   80G   20%   /
    ```

- **Disk Usage**:
  - Use `du` to see how much space is used by files and directories.
  - Example:
    ```bash
    $ du -sh /home/user
    ```

---

# Swap Space

- **Swap Overview**: Swap is disk space used to extend RAM.
  - You can use either a disk partition or a file as swap.

- **Creating Swap Space**:
  - **Using a Partition**:
    ```bash
    # mkswap /dev/sda5
    # swapon /dev/sda5
    ```
  - **Using a File**:
    ```bash
    # dd if=/dev/zero of=/swapfile bs=1M count=1024
    # mkswap /swapfile
    # swapon /swapfile
    ```

- **Monitoring Swap Usage**:
  - Check swap usage with the `free` command:
    ```bash
    $ free -h
    ```

---

# Logical Volume Manager (LVM)

- **Overview**: LVM allows flexible management of disk storage by pooling physical volumes into a volume group, and creating logical volumes from the pool.

- **Key LVM Operations**:
  - Add/remove physical volumes to/from a volume group.
  - Resize logical volumes without rebooting.
  - Example of viewing volume groups:
    ```bash
    $ vgs
    ```

- **Working with LVM**:
  - **Create a Physical Volume**:
    ```bash
    # pvcreate /dev/sda1
    ```
  - **Create a Volume Group**:
    ```bash
    # vgcreate my_vg /dev/sda1
    ```
  - **Create a Logical Volume**:
    ```bash
    # lvcreate -L 20G -n my_lv my_vg
    ```

- **Resizing Logical Volumes**:
  - Extend a logical volume:
    ```bash
    # lvextend -L +10G /dev/my_vg/my_lv
    ```

---

# Filesystem Check and Repair

- **Checking Filesystems**:
  - Use `fsck` to check and repair filesystems.
  - Example:
    ```bash
    # fsck /dev/sda1
    ```

- **Repairing Filesystems**:
  - The `fsck` tool can automatically fix common errors, but manual intervention may be required for serious issues.
  - Example of automatic repair:
    ```bash
    # fsck -y /dev/sda1
    ```
