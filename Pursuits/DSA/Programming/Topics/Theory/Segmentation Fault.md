A segmentation fault (often abbreviated as "segfault") occurs when a program attempts to access a memory segment that is not allowed to access. This is typically due to errors in pointer use or memory management. Some common causes include:

- **Dereferencing a null or uninitialized pointer:** Trying to access memory using a pointer that has not been properly initialized or that has been set to null.
- **Buffer overflow:** Writing data beyond the allocated memory bounds of an array.
- **Accessing freed memory:** Using memory that has already been released back to the system (use-after-free).
- **Invalid pointer arithmetic:** Performing incorrect pointer arithmetic that leads to accessing out-of-bounds memory.

When a segmentation fault occurs, the operating system typically terminates the program to prevent further damage or corruption of memory.
```c
int main(){
int *ptr = NULL; // Dereferencing a null pointer causes a segmetation fault
*ptr = 42;
return 0;
}
```