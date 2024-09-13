# The Big Picture of Linux Systems
- Linux is complex with many interacting components.
- Abstraction helps simplify understanding.
- Focus on the main components: Hardware, Kernel, and User Space.

---

# Understanding Abstraction
- Abstraction: Ignoring details to focus on core operations.
- Analogy: Operating a car vs. understanding how every part works.
- Helps in troubleshooting and system building.

---

# Levels of Abstraction in Linux
- Linux is divided into 3 layers:
  - Hardware
  - Kernel
  - User Space
- These layers communicate to manage the system.

---

# Hardware: The Foundation
- **Hardware**: Memory (RAM), CPU, disks, and network interfaces.
- Responsible for raw processing and data storage.
- Example: Memory stores programs and data.

---

# Kernel: The Core of Linux
- **Kernel**: The mediator between hardware and user processes.
- Resides in memory and manages hardware resources.
- Performs tasks like memory management and process scheduling.

---

# User Space: The Application Layer
- **User Processes**: Programs running in user space.
- User space is the environment for interacting with the system.
- Limited permissions to avoid crashes.

---

# Kernel Mode vs. User Mode
- **Kernel Mode**: Full access to CPU and memory.
- **User Mode**: Restricted access to prevent system-wide crashes.
- Processes in user mode can only access safe memory regions.

---

# Main Memory in Linux
- Main memory stores all active processes and kernel functions.
- Organized into bits (0s and 1s).
- Processes work by accessing and modifying bits.

---

# The Role of the Kernel in Memory Management
- Splits memory for different processes.
- Ensures processes stay in their memory boundaries.
- Uses **Virtual Memory** to extend physical memory limits.

---

# Process Management: Context Switching
- Many processes seem to run simultaneously, but only one uses the CPU at a time.
- **Context Switch**: Kernel saves process state and switches to another.
- Allows multitasking and efficient CPU usage.

---

# Time Slices in Process Management
- Processes use the CPU in small time slices.
- **Multitasking**: Illusion of many processes running at once.
- Kernel decides which process runs next based on priority.

---

# Memory Management with Virtual Memory
- **Memory Management Unit (MMU)**: Helps kernel manage memory.
- Each process acts like it has its own memory space.
- **Page Table**: Maps virtual memory to physical memory locations.

---

# Device Drivers in the Kernel
- Kernel controls hardware through **device drivers**.
- Device drivers provide a uniform interface to processes.
- Only the kernel can directly interact with hardware devices.

---

# System Calls: Communicating with the Kernel
- **System Calls**: How user processes communicate with the kernel.
- Examples: Opening files, reading data, running commands.
- Critical for process creation (`fork()`), execution (`exec()`).

---

# Fork and Exec: Process Creation
- **fork()**: Creates a copy of a process.
- **exec()**: Replaces the process with a new program.
- Example: Running a command like `ls` involves both fork and exec.

---

# The User Space Environment
- **User Space**: Memory allocated to running processes.
- Programs interact with the system in this environment.
- Divided into basic, utility, and application-level services.

---

# Components in User Space
- **Basic Services**: Perform core system tasks.
- **Utility Services**: Manage networking, logging, and other system functions.
- **Applications**: Programs like web browsers and text editors.

---

# Users in Linux
- Each process is run by a **user** identified by a User ID.
- **root user**: The superuser with full system access.
- Users help enforce boundaries and permissions on the system.

---

# Groups and Permissions
- **Groups**: Collections of users for shared access.
- Permissions define what users can access and modify.
- Root has unrestricted access, while other users are limited.

---

# Summary and Looking Ahead
- We've introduced the core components of a Linux system.
- Key areas: Hardware, Kernel, and User Space.
- Future lessons will cover storage, file systems, and more detailed kernel functions.
