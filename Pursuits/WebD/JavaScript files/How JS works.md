JavaScript is neither purely interpreted nor purely compiled.  
It is a JIT-compiled (hybrid execution) language.

**## TL;DR

- JavaScript was originally interpreted → the label stuck
- Modern JS engines compile aggressively using JIT
- It’s not purely interpreted anymore
- “Interpreted vs compiled” is now a **spectrum**, not a binary**
# How JavaScript actually runs (modern engines)

### Step-by-step:

1. **Parsing**
    - JS source code is parsed into an AST (Abstract Syntax Tree)
        
2. **Interpretation**
    - Bytecode is generated
    - Code starts running immediately (fast startup)
        
3. **JIT Compilation**
    - Frequently used (“hot”) code is compiled into **native machine code**
    - Optimized for speed
        
4. **De-optimization (if needed)**
    
    - Engine can fall back if assumptions break
This mix = **hybrid execution model**


## Why JS is NOT “compiled like C/C++”

- No ahead-of-time compilation by default
- No standalone machine-code executable
- Happens **at runtime**, not before execution

---

## Why JS is NOT “interpreted like old scripting languages”

- It does **not** execute source line-by-line forever
- JIT compilers make it much faster than pure interpreters

---

## Interview-safe answer ⭐

> **JavaScript is a JIT-compiled language. It uses interpretation for quick startup and just-in-time compilation for performance, which is why it is sometimes called a hybrid of interpreted and compiled languages.**

---

## One-liner to remember

> **JavaScript is interpreted _and_ compiled — just not ahead of time.**


## What “interpreted” originally meant

Traditionally, an **interpreted language**:

- Runs **line by line** (or statement by statement)
    
- Is **not compiled ahead of time** into machine code
    
- Is executed by another program (an _interpreter_)
    

Early JavaScript (mid-1990s, in browsers like **Netscape** Navigator**) fit this perfectly:

- JS code was read and executed directly by the browser
    
- No build step
    
- No executable output file
    

So it got labeled **interpreted**, and the label stuck.


## What actually happens today (the plot twist)

Modern JavaScript engines like:

- **V8** (Chrome, Node.js)
    
- **SpiderMonkey**
    
- **JavaScriptCore**
    

do **both interpretation _and_ compilation**.

Typical flow:

1. **Parse** JS into an AST (syntax tree)
    
2. **Interpret** it initially (fast startup)
    
3. **JIT-compile** hot code paths into machine code
    
4. **Optimize / de-optimize** dynamically at runtime
    

So modern JS is **JIT-compiled**, not “purely interpreted”.


## The most accurate description today

If we’re being precise:

> **JavaScript is a dynamically typed, JIT-compiled language with interpreted semantics.**