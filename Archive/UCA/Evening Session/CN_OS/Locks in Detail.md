# ⭐ **1. WHY DO WE NEED LOCKS?**

Because **multiple threads** accessing shared data may cause:

- race conditions
- inconsistent state
- lost updates
- corrupted objects

Locks ensure **only one thread** changes shared data at a time (or coordinated access).

[[Scenario discussing above problems]]

# Types of Locks

A. **Implicit Locks** (Built-in Locks)
Used with `synchronized`.
- `synchronized method`
- `synchronized block`
- object monitor locks

### Properties:

- Reentrant
- Block-based
- Cannot check lock state
- Cannot timeout
- Cannot interrupt waiting thread
- Auto-release when block ends

B. **Explicit Locks** (java.util.concurrent.locks)
Used with classes like:

- `ReentrantLock`
- `ReentrantReadWriteLock`
- `StampedLock`

These offer **more power and flexibility**.

---
[Art of Multiprogramming.pdf](file:///D:/a%20SEM%205/CN_OS/Art%20of%20Multiprogramming.pdf)

>**Interleaved** means **mixed together in an alternating or zig-zag pattern**.
### Moore's law
Moore's Law, first posited by Gordon E. Moore in 1965, observes that the number of transistors on microchips doubles roughly every two years while costs decrease. Not a fundamental law of science, this observation has nonetheless been a guiding principle in the semiconductor industry for nearly six decades. It predicts that as transistors become smaller, computing technology will continually advance, becoming faster, more energy-efficient, and more cost-effective over time. Today, Moore's insight remains a critical benchmark for technological progress, influencing everything from smartphones to data centers.

#### Multicores
This book focuses on how to program multiprocessors that communicate via a shared memory. Such systems are often called shared-memory multiprocessors or, more recently, multicores.

#### Challenge in Multiprocessor programming
Multiprocessor programming is challenging because modern computer systems are inherently asynchronous: activities can be halted or delayed without warning by interrupts, preemption, cache misses, failures, and other events. These delays are inherently unpredictable, and can vary enormously in scale: a cache miss might delay a processor for fewer than ten instructions, a page fault for a few million instructions, and operating system preemption for hundreds of millions of instructions.

### Maurice Herlihy and Nir Shavit study Approach
We approach multiprocessor programming from two complementary directions: principles and practice.
- In the principles part of this book, we focus on computability: figuring out what can be computed in an asynchronous concurrent environment. We use an idealized model of computation in which multiple concurrent threads manipulate a set of shared objects. The sequence of the thread operations on the objects is called the concurrent program or concurrent algorithm. This model is essentially the model presented by the Java, C#, or C++ thread packages.
- we view the acquisition of a basic understanding of concurrent shared-memory computability as a necessary step.
- The chapters dealing with principles take the reader through a quick tour of asynchronous computability, attempting to expose various computability issues, and how they are addressed through the use of hardware and software mechanisms.


#### 1.1 Shared Objects and Synchronization