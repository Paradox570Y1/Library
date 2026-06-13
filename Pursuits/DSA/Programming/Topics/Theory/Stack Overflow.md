A stack overflow happens when a program's call stack exceeds the space allocated for it. The call stack is a special type of data structure that stores information about active subroutines or functions in a program. Each time a function is called, a new stack frame is created and added to the call stack. When the function exits, its stack frame is removed.

Common causes of stack overflow include:

- **Infinite or excessively deep recursion:** If a recursive function calls itself indefinitely without a base case, or if the recursion depth is too deep, it can exhaust the stack space.
- **Large local variables:** Declaring large local arrays or data structures within functions can consume significant stack space.

When a stack overflow occurs, the program typically crashes or is terminated by the operating system.
```c
void recursiveFunction(){
    recursiveFunction();// Infinite recursion leads to a stack overflow
}
int main(){
    recursiveFunction();
    return 0;
}
```