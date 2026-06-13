Following are the five operators that we will be working with
![[Pasted image 20250123085933.png|250]]
- The numbers are denoting priority/precedence of the operators , higher the number more is the precedence.
- If any other operator is encountered then its priority will be -1.

**1. Infix Expression**
- It is the expression that we use heavily in C++ , Java or any programming language
- It is the most common expression that we use.
```d
	(p+q)*(m-n)
```
**2. Prefix Expression**
- It is used in a programming language extensively which is called `LISP`.
- It is also used in `Tree` data structure.
- Also Know as polish notation
```d 
	*+pq-mn
```
**3. Postfix Expression**
- These are used in stack based calculator
```d
	pq+mn-*
```