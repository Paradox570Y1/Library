
# FILE SYSTEMS (Computer Architecture / OS)

## 1. What is a File System?

A **file system** is a method and data structure used by an operating system to:

- **Store**
    
- **Organize**
    
- **Access**
    
- **Manage files and directories** on secondary storage (HDD, SSD, USB, etc.)
    

📌 **Without a file system** → data is just a continuous stream of bits with no meaning.

---

## 2. Why File Systems are Needed

A file system provides:

1. **File naming** (human-readable)
    
2. **Directory structure**
    
3. **Storage allocation**
    
4. **Metadata management**
    
5. **Access control & security**
    
6. **Reliability and recovery**
    

---

## 3. Basic File System Architecture (High-Level)

`User  ↓ Application  ↓ Operating System  ↓ File System  ↓ Disk Controller  ↓ Secondary Storage`

---

## 4. Key Concepts & Terminology (VERY IMPORTANT)

### 4.1 File

- A **logical collection of data**
    
- Identified by **name + path**
    

### 4.2 Directory

- A **special file** that stores:
    
    - file names
        
    - file metadata
        
    - pointers to file data blocks
        

---

### 4.3 Block / Cluster

- **Block**: smallest unit of storage managed by OS
    
- **Cluster**: group of blocks (used in FAT systems)
    

📌 Larger cluster → faster access but **wastes space**  
📌 Smaller cluster → less waste but slower access

---

### 4.4 Metadata

Information about a file:

- File name
    
- Size
    
- Type
    
- Permissions
    
- Timestamps
    
- Location on disk
    

---

## 5. File Allocation Methods (Exam Favorite)

### 5.1 Contiguous Allocation

- Files stored in **continuous blocks**
    
- ✅ Fast access
    
- ❌ Fragmentation
    

---

### 5.2 Linked Allocation

- Each block points to next block
    
- ✅ No fragmentation
    
- ❌ Slow random access
    

---

### 5.3 Indexed Allocation

- Separate **index block** stores pointers to all file blocks
    
- ✅ Fast random access
    
- ❌ Extra space for index
    

📌 **NTFS & ext4 use advanced indexed allocation**

---

## 6. File Access Methods

1. **Sequential Access**
    
    - Read/write in order
        
2. **Direct (Random) Access**
    
    - Jump directly to any block
        
3. **Indexed Access**
    
    - Uses index table
        

---

## 7. Types of File Systems (Overview)

|File System|Used In|
|---|---|
|FAT32|Older Windows, USB|
|NTFS|Windows|
|ext4|Linux|
|exFAT|Flash drives, SD cards|

---

# CORE FILE SYSTEMS (KEYWORDS)

---

## 8. FAT (File Allocation Table)

### 8.1 What is FAT?

**FAT** uses a **table** that keeps track of:

- which disk blocks belong to which file
    
- which blocks are free or used
    

### 8.2 How FAT Works

`File → Cluster 5 → Cluster 8 → Cluster 12 → EOF`

The FAT table stores:

`5 → 8 8 → 12 12 → End`

---

### 8.3 FAT Variants

|Type|Max File Size|
|---|---|
|FAT16|2 GB|
|FAT32|4 GB|

---

### 8.4 Advantages

- Simple
    
- Fast for small devices
    
- High compatibility
    

---

### 8.5 Disadvantages

- No security
    
- No journaling
    
- File size limit
    
- Fragmentation
    

📌 **Used in**: USB drives, memory cards

---

## 9. NTFS (New Technology File System)

### 9.1 What is NTFS?

NTFS is an **advanced, secure, journaling file system** developed by Microsoft.

---

### 9.2 Key Features

- **Journaling** (crash recovery)
    
- **File permissions (ACLs)**
    
- **Encryption (EFS)**
    
- **Compression**
    
- **Large file support**
    
- **Hard links & symbolic links**
    

---

### 9.3 NTFS Structure

- Uses **Master File Table (MFT)**
    
- Each file has an entry in MFT
    
- Small files may be stored **inside MFT itself**
    

---

### 9.4 Advantages

- Highly secure
    
- Reliable
    
- Supports very large files
    

---

### 9.5 Disadvantages

- Complex
    
- Slower on small flash devices
    
- Limited support on non-Windows OS
    

📌 **Used in**: Windows OS

---

## 10. ext4 (Fourth Extended File System)

### 10.1 What is ext4?

ext4 is the **default Linux file system**, designed for **high performance and reliability**.

---

### 10.2 Key Features

- **Journaling**
    
- **Extents** (store continuous blocks together)
    
- **Delayed allocation**
    
- **Large file & volume support**
    
- **Backward compatible with ext3/ext2**
    

---

### 10.3 What are Extents?

Instead of storing every block address:

`Start Block + Length`

Example:

`Block 500 → 200 blocks`

✅ Faster access  
✅ Less fragmentation

---

### 10.4 Advantages

- Very fast
    
- Reliable
    
- Efficient for large files
    

---

### 10.5 Disadvantages

- Limited Windows support
    
- No built-in encryption like NTFS
    

📌 **Used in**: Linux OS

---

## 11. exFAT (Extended File Allocation Table)

### 11.1 What is exFAT?

exFAT is an improved version of FAT designed for **flash storage**.

---

### 11.2 Key Features

- Supports **large files (>4GB)**
    
- Optimized for **USB & SD cards**
    
- Lightweight (no journaling)
    

---

### 11.3 Advantages

- Cross-platform (Windows, macOS, Linux)
    
- Best for flash memory
    
- No file size limit like FAT32
    

---

### 11.4 Disadvantages

- No journaling
    
- Less secure
    
- Not ideal for OS drives
    

📌 **Used in**: SD cards, USB drives, cameras

---

## 12. Comparison Table (VERY EXAM-USEFUL)

|Feature|FAT32|NTFS|ext4|exFAT|
|---|---|---|---|---|
|Journaling|❌|✅|✅|❌|
|Security|❌|✅|Limited|❌|
|Max File Size|4GB|Very Large|Very Large|Very Large|
|OS Use|Old Windows|Windows|Linux|Flash devices|
|Performance|Low|High|Very High|Medium|

---

## 13. Journaling (1-Line Definition)

**Journaling** keeps a log of changes before committing them, enabling **fast recovery after crashes**.

---

## 14. One-Line Exam Definitions (REVISION GOLD)

- **File system**: A structure for storing and managing files on storage devices.
    
- **FAT**: Table-based file allocation system.
    
- **NTFS**: Secure, journaling file system by Microsoft.
    
- **ext4**: High-performance Linux file system using extents.
    
- **exFAT**: Flash-optimized FAT system supporting large files.
    

---

## 15. How to Write in Exam (TIP)

Start with:

1. Definition
    
2. Architecture
    
3. Features
    
4. Advantages
    
5. Disadvantages
    
6. Use cases
    
7. Comparison
    

---

If you want next:

- **Numericals / MCQs on file systems**
    
- **Short notes (2–3 mark answers)**
    
- **Diagrams you can draw in exams**
    
- **Crash 10-minute revision sheet**
    




# FILE OPERATIONS: `open`, `read`, `write`, `close`

## 1. What are File Operations?

**File operations** are system-level actions provided by the OS to allow programs to **access and manipulate files safely and efficiently**.

📌 Implemented using **system calls**, not normal functions.

---

## 2. Why OS Controls File Operations

Because OS must ensure:

- **Security**
    
- **Data consistency**
    
- **Concurrent access control**
    
- **Efficient disk usage**
    

---

## 3. File Operation Lifecycle (BIG PICTURE)

`open → read / write → close`

A file **must be opened before** it can be read or written.

---

## 4. `open` Operation

### 4.1 Definition

`open` establishes a **connection between a process and a file**, making it available for read/write operations.

---

### 4.2 What Happens Internally (VERY IMPORTANT)

When a process calls `open()`:

1. OS checks if file exists
    
2. Checks **permissions**
    
3. Loads file metadata into memory
    
4. Creates an entry in:
    
    - System-wide open file table
        
    - Per-process open file table
        
5. Returns a **file descriptor (FD)**
    

📌 **File Descriptor**: A small integer used to identify the open file.

---

### 4.3 Open Modes

|Mode|Meaning|
|---|---|
|Read (`r`)|Read only|
|Write (`w`)|Write only|
|Read-Write (`rw`)|Both|
|Append (`a`)|Write at end|
|Create|Create if not exists|

---

### 4.4 Key Points

- Same file can be opened by **multiple processes**
    
- Each process gets its **own file descriptor**
    

---

## 5. `read` Operation

### 5.1 Definition

`read` copies data **from file (disk) → memory (buffer)**.

---

### 5.2 How `read` Works Internally

1. OS checks file descriptor validity
    
2. Checks read permission
    
3. Finds current **file offset**
    
4. Copies requested bytes to buffer
    
5. Updates file offset
    

`Disk → Kernel Buffer → User Buffer`

---

### 5.3 File Offset (IMPORTANT)

- Offset = current position in file
    
- Automatically moves forward after read
    

📌 Allows **sequential access**

---

### 5.4 Types of Read

- **Sequential read**
    
- **Random read** (using seek)
    

---

## 6. `write` Operation

### 6.1 Definition

`write` copies data **from memory (buffer) → file (disk)**.

---

### 6.2 How `write` Works Internally

1. Validates file descriptor
    
2. Checks write permission
    
3. Writes data at current offset
    
4. Updates offset
    
5. Updates file size (if needed)
    

`User Buffer → Kernel Buffer → Disk`

---

### 6.3 Write Modes

- **Overwrite**
    
- **Append**
    
- **Random write**
    

---

### 6.4 Buffered vs Direct Write

- **Buffered write**: data cached in memory (faster)
    
- **Direct write**: data written immediately to disk
    

📌 Journaling file systems use buffering heavily.

---

## 7. `close` Operation

### 7.1 Definition

`close` terminates the connection between process and file.

---

### 7.2 What Happens on `close()`

1. Flushes buffers to disk
    
2. Updates metadata
    
3. Removes file descriptor entry
    
4. Decreases open count
    

📌 File is released only when **open count = 0**

---

### 7.3 Why Close is Important

- Prevents data loss
    
- Frees system resources
    
- Avoids file corruption
    

---

## 8. Open File Tables (EXAM FAVORITE)

### 8.1 System-Wide Open File Table

- Maintained by OS
    
- Stores:
    
    - File location
        
    - Access mode
        
    - Open count
        
    - File offset
        

---

### 8.2 Per-Process Open File Table

- Maintained per process
    
- Maps:
    
    `File Descriptor → System Table Entry`
    

---

## 9. Concurrency & File Operations

### Problem

Two processes writing to same file → **data inconsistency**

### Solutions

- File locks
    
- Append-only mode
    
- Atomic write operations
    

---

## 10. Error Conditions (Quick Points)

|Operation|Possible Errors|
|---|---|
|open|file not found, permission denied|
|read|invalid FD, EOF|
|write|disk full, permission denied|
|close|invalid FD|

---

## 11. One-Line Exam Definitions (GOLD)

- **open**: Establishes access to a file and returns a file descriptor.
    
- **read**: Transfers data from file to memory.
    
- **write**: Transfers data from memory to file.
    
- **close**: Releases file resources and flushes buffers.
    

---

## 12. Comparison Table (Crisp)

|Operation|Purpose|Affects Offset|Disk Access|
|---|---|---|---|
|open|Access setup|❌|❌|
|read|Fetch data|✅|✅|
|write|Store data|✅|✅|
|close|Release file|❌|✅ (flush)|

---

## 13. Diagram You Can Draw in Exam

`Process   | File Descriptor   | Open File Table   | Disk Blocks`

---

## 14. Typical Exam Question Traps

- ❌ `read` without `open` → invalid
    
- ❌ Forgetting offset update
    
- ❌ Thinking `close` deletes file (it doesn’t)
    

---

## 15. 30-Second Revision Mnemonic

**O → R/W → C**

> Open it → Use it → Close it

---

If you want next:

- **seek() / lseek() explained**
    
- **Buffered vs unbuffered I/O**
    
- **File locking**
    
- **UNIX system calls vs library calls**
    
- **MCQs + numericals**
    



---

# I/O MANAGEMENT, DEVICE DRIVERS, BLOCKING & NON-BLOCKING I/O

---

## 1. I/O Management (Big Picture)

### 1.1 What is I/O Management?

**I/O Management** is the responsibility of the OS to **control, coordinate, and optimize input/output operations** between:

- CPU
    
- Memory
    
- I/O devices
    

📌 Goal: **Efficient, safe, device-independent I/O**

---

### 1.2 Why I/O Management is Needed

- Devices are **slow** compared to CPU
    
- Different devices have **different interfaces**
    
- Multiple processes may request I/O simultaneously
    

---

### 1.3 I/O Management Responsibilities

1. Device abstraction
    
2. Scheduling I/O requests
    
3. Buffering & caching
    
4. Error handling
    
5. Protection & access control
    

---

### 1.4 I/O Software Stack (EXAM DIAGRAM)

`User Process    ↓ I/O System Calls    ↓ Device-Independent I/O Software    ↓ Device Driver    ↓ Hardware Controller    ↓ I/O Device`

---

## 2. Device Drivers

### 2.1 What is a Device Driver?

A **device driver** is a **software program** that acts as an **interface between the OS and hardware device**.

📌 OS talks to drivers, drivers talk to hardware.

---

### 2.2 Why Device Drivers are Needed

- Hardware devices differ widely
    
- OS cannot know device-specific details
    
- Enables **hardware independence**
    

---

### 2.3 Functions of a Device Driver

- Initialize device
    
- Translate OS requests into device commands
    
- Handle interrupts
    
- Perform error detection
    
- Transfer data between device and memory
    

---

### 2.4 Types of Device Drivers

|Type|Example|
|---|---|
|Character driver|Keyboard, mouse|
|Block driver|Hard disk, SSD|
|Network driver|Ethernet, Wi-Fi|

---

### 2.5 Device Driver Working (Step-by-Step)

1. Process issues I/O request
    
2. OS forwards request to driver
    
3. Driver programs device controller
    
4. Device performs I/O
    
5. Device sends interrupt
    
6. Driver informs OS
    
7. OS wakes waiting process
    

---

## 3. I/O Techniques (Context)

### 3.1 Programmed I/O

- CPU continuously polls device
    
- ❌ Wastes CPU time
    

---

### 3.2 Interrupt-Driven I/O

- Device interrupts CPU when ready
    
- ✅ Better CPU utilization
    

---

### 3.3 DMA (Direct Memory Access)

- Device transfers data directly to memory
    
- ✅ High performance
    
- Used for disks, network cards
    

---

## 4. Blocking I/O

### 4.1 Definition

In **blocking I/O**, the **calling process is suspended** until the I/O operation completes.

---

### 4.2 How Blocking I/O Works

1. Process issues I/O request
    
2. Process enters **waiting state**
    
3. OS schedules another process
    
4. I/O completes
    
5. Process resumes execution
    

`Request → WAIT → Data Ready → Resume`

---

### 4.3 Characteristics

- Simple to program
    
- Process cannot do other work
    
- Efficient for short I/O
    

---

### 4.4 Example

Reading from keyboard:

`scanf() waits until user enters input`

---

## 5. Non-Blocking I/O

### 5.1 Definition

In **non-blocking I/O**, the I/O call **returns immediately**, even if the operation is not completed.

---

### 5.2 How Non-Blocking I/O Works

1. Process issues I/O request
    
2. OS returns control immediately
    
3. Process continues execution
    
4. Process checks later for completion
    

`Request → Continue → Check → Use Data`

---

### 5.3 Characteristics

- No waiting
    
- Requires polling or event notification
    
- More complex to program
    

---

### 5.4 Example

Network socket programming:

`read() returns -1 if data not ready`

---

## 6. Blocking vs Non-Blocking I/O (VERY IMPORTANT)

|Feature|Blocking I/O|Non-Blocking I/O|
|---|---|---|
|Process state|Waiting|Running|
|CPU usage|Lower|Higher|
|Programming|Simple|Complex|
|Response time|Slower|Faster|
|Used in|Simple apps|High-performance systems|

---

## 7. Relation with I/O Management

|Component|Role|
|---|---|
|I/O Management|Overall coordination|
|Device Driver|Device-specific handling|
|Blocking I/O|Process waits|
|Non-Blocking I/O|Process continues|

---

## 8. Buffering in I/O (Key Concept)

### 8.1 What is Buffering?

Temporary storage of data in memory during I/O.

### 8.2 Purpose

- Handle speed mismatch
    
- Reduce device access
    
- Improve performance
    

---

## 9. Spooling (Exam Favorite)

### 9.1 Definition

**Spooling** stores I/O data on disk to allow:

- Concurrent CPU and I/O operations
    

### 9.2 Example

- Print spooling
    

---

## 10. Error Handling in I/O

- Device failure
    
- Timeout
    
- Partial transfer
    

Handled mainly by **device drivers**

---

## 11. One-Line Exam Definitions (GOLD)

- **I/O management**: OS function that controls and optimizes device input/output.
    
- **Device driver**: Software interface between OS and hardware.
    
- **Blocking I/O**: Process waits until I/O completes.
    
- **Non-blocking I/O**: Process continues execution during I/O.
    

---

## 12. Common Exam Traps

- ❌ Device driver ≠ hardware
    
- ❌ Blocking I/O ≠ slower always
    
- ❌ Non-blocking I/O ≠ asynchronous (they’re related but not identical)
    

---

## 13. 30-Second Revision Mnemonic

**I/O Path**

> Process → OS → Driver → Device → Interrupt → OS → Process

---

## 14. How to Write a 10-Mark Answer

1. Define I/O management
    
2. Draw I/O stack
    
3. Explain device drivers
    
4. Explain blocking & non-blocking
    
5. Add comparison table
    