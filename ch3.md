# Devices and Kernel Infrastructure in Linux

- **Overview**: A tour of the kernel's device infrastructure in a functioning Linux system.
- **Goals**:
  - Learn how the kernel presents devices.
  - Understand device files and sysfs.
  - Use `udev` to configure and interact with devices.

---

# Device Files

- **Device Nodes**: Files representing devices in Unix systems located in `/dev`.
  - Devices appear as files, allowing programs to interact with them like regular files.
- **Example**: `$ echo blah blah > /dev/null` sends output to a device (here `/dev/null`), and the kernel bypasses standard file operations.
- **Identifying Devices**: Use `ls -l /dev` to view device files and their permissions.
  - Example output:
    ```
    brw-rw----  1 root disk 8, 1 sda1
    crw-rw-rw-  1 root root 1, 3 null
    ```
  - The file type (`b` for block device, `c` for character device) and major/minor device numbers (e.g., `8, 1` for `sda1`) identify devices.

---

# Types of Device Files

- **Block Devices**: Access data in fixed chunks (e.g., hard drives like `/dev/sda`).
- **Character Devices**: Handle data streams (e.g., `/dev/null`, printers).
- **Pipe Devices**: Connect processes with I/O streams instead of a kernel driver.
- **Socket Devices**: Used for interprocess communication (e.g., Unix domain sockets).

---

# sysfs Device Path

- **Purpose**: Provides a uniform way to access hardware attributes.
  - Devices listed in `/sys/devices`, like `/sys/devices/pci0000:00/.../block/sda`.
- **Difference from `/dev`**: `/dev` is used for interaction with devices, while `/sys` provides detailed device information.
- **Example**: `$ cat /sys/block/sda/dev` shows the major and minor device numbers.

---

# udev: User-Space Device Management

- **Overview**: Manages device files in `/dev` dynamically, handles device events (like when a USB drive is inserted).
- **How it Works**: 
  1. Kernel detects a new device and sends a uevent.
  2. `udevd` processes the event and creates the corresponding device file in `/dev`.
- **Example Command**: `$ udevadm info --query=all --name=/dev/sda` to display information about `/dev/sda`.

---

# The `dd` Command

- **Purpose**: Read/write data from/to devices.
- **Basic Usage**: `$ dd if=/dev/zero of=new_file bs=1024 count=1`.
  - Reads from `/dev/zero` and writes one 1024-byte block to `new_file`.
- **Common Options**:
  - `if=`: Input file or device.
  - `of=`: Output file or device.
  - `bs=`: Block size for reading and writing.
  - `count=`: Number of blocks to copy.

---

# Device Naming Conventions

- **Hard Disks**: `/dev/sd*` (e.g., `/dev/sda` for the first disk, `/dev/sdb` for the second).
  - **Partitions**: `/dev/sda1`, `/dev/sda2`, etc.
- **Virtual Disks**: `/dev/xvd*`, `/dev/vd*` (for virtualized environments).
- **Non-Volatile Memory Devices**: `/dev/nvme*` for NVMe SSDs.
- **Device Mapper**: `/dev/dm-*`, `/dev/mapper/*` for logical volumes.
  
---

# Special Devices

- **CD/DVD Drives**: `/dev/sr*` (SCSI devices for optical drives).
- **Serial Ports**: `/dev/ttyS*`, `/dev/ttyUSB*`, `/dev/ttyACM*`.
- **Parallel Ports**: `/dev/lp*`, `/dev/parport*`.
- **Audio Devices**: `/dev/snd/*`, `/dev/dsp`, `/dev/audio` (ALSA and OSS sound systems).

---

# udev and devtmpfs

- **devtmpfs**: Simplified in-memory filesystem for managing device files.
  - Automatically created during boot.
  - udev sets permissions and links.
- **Example**: Links in `/dev/disk/by-id` point to block devices (e.g., `/dev/sda`).

---

# udevd Operation

1. **Kernel Sends uevent**: Notification about new devices.
2. **udevd Processes**: Loads uevent attributes, applies rules, and configures devices.
3. **Rules and Actions**: `/etc/udev/rules.d` defines how udevd handles devices.

---

# udevadm: udev Administration Tool

- **Monitor Device Events**: `$ udevadm monitor` shows real-time kernel and udev events when devices are added or removed.
- **Query Device Info**: `$ udevadm info --query=all --name=/dev/sda` shows details about the `/dev/sda` device.
  
---

# SCSI and USB Storage

- **SCSI**: Small Computer System Interface used for communication between devices (disks, USB drives).
- **USB Storage**: SCSI-over-USB communication for devices like flash drives.
- **Example**: `$ lsscsi` lists SCSI devices and their `/dev` paths.

---

# Multiple Access Methods for Devices

- **Block Devices**: Use drivers like `sd` for disks and `sr` for optical drives.
- **Generic Devices**: `sg` allows direct SCSI communication.
  - Example: Use `/dev/sg1` for optical drive writing tasks.

---

# Conclusion

- **Understanding Devices**: Linux presents devices as files, making it easy to interact with them using standard I/O operations.
- **udev and sysfs**: Play a crucial role in dynamically managing devices and providing detailed information about hardware.
- **Next Steps**: Dive deeper into disk management and storage in the next chapter.
