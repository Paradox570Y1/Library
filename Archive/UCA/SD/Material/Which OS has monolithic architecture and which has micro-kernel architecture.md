### 🔧 **OS Architecture Types**

|Architecture|Description|
|---|---|
|**Monolithic Kernel**|Entire OS (core services + drivers) runs in a single address space (kernel mode).|
|**Microkernel**|Only minimal core services (e.g., IPC, scheduling) run in kernel mode; everything else runs in user mode.|
|**Hybrid Kernel**|Mix of monolithic and microkernel – minimal kernel functions, but still large kernel size.|
|**Exokernel / Nanokernel**|Experimental or specialized OS architectures; rare in consumer environments.|

---

### ✅ **Popular OS and Their Kernel Architectures**

#### 🧱 **Monolithic Kernel OS**

| OS                                                  | Kernel Type | Notes                                                          |
| --------------------------------------------------- | ----------- | -------------------------------------------------------------- |
| **Linux** (all distros: Ubuntu, Fedora, Arch, etc.) | Monolithic  | Modular design allows dynamic loading/unloading of components. |
| **MS-DOS**                                          | Monolithic  | Very simple and limited functionality.                         |
| **FreeBSD / NetBSD / OpenBSD**                      | Monolithic  | Derived from BSD Unix.                                         |
| **Solaris** (early versions)                        | Monolithic  | Solaris later incorporated hybrid features.                    |

---

#### 🧩 **Microkernel OS**

|OS|Kernel Type|Notes|
|---|---|---|
|**Minix**|Microkernel|Educational OS designed by Andrew Tanenbaum.|
|**QNX**|Microkernel|Used in embedded systems (automotive, medical).|
|**L4** (family: seL4, Fiasco, L4Ka::Pistachio)|Microkernel|High-performance microkernels used in secure environments.|
|**GNU Hurd**|Microkernel (Mach)|Experimental OS from GNU project.|

---

#### 🔀 **Hybrid Kernel OS**

|OS|Kernel Type|Notes|
|---|---|---|
|**Windows NT** (XP, 7, 10, 11, etc.)|Hybrid|Microkernel-like structure but includes many services in kernel mode.|
|**macOS**|Hybrid|Based on XNU, a combination of Mach (microkernel) + BSD (monolithic elements).|
|**iOS / iPadOS / watchOS / tvOS**|Hybrid|Also based on Apple’s XNU kernel.|
|**Solaris 10+**|Hybrid|Added modular components and dynamic kernel features.|
|**Android**|Hybrid (Linux Kernel)|Based on monolithic Linux kernel, but modularized heavily.|

---

### 📦 **Lesser-Known or Niche OS Examples**

|OS|Kernel Type|Notes|
|---|---|---|
|**Haiku OS**|Hybrid|Inspired by BeOS, with a modular kernel.|
|**ReactOS**|Hybrid|Windows-compatible OS written from scratch.|
|**TempleOS**|Monolithic|Lightweight OS with religious theming.|
|**Redox OS**|Microkernel|Modern microkernel OS written in Rust.|
|**Genode OS Framework**|Microkernel-based|Built on L4 family microkernels.|
|**Fuchsia** (by Google)|Microkernel|Uses a custom microkernel called _Zircon_.|

---

### 🧠 Summary Table

|Architecture|Examples|
|---|---|
|**Monolithic**|Linux, FreeBSD, MS-DOS, Solaris (early), TempleOS|
|**Microkernel**|Minix, QNX, L4, seL4, GNU Hurd, Redox, Fuchsia|
|**Hybrid**|Windows NT (all versions), macOS, iOS, Android, ReactOS|
|**Exokernel**|MIT Exokernel (experimental, academic)|

![[Pasted image 20250723112551.png|400]]

# Monolithic architecture
![[Pasted image 20250723112857.png]]