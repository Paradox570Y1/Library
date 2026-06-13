### Reasons for choosing 31:

1. **Prime number advantage**
    
    - 31 is a prime number, which reduces the chances of hash collisions.
        
    - Using a prime ensures that permutations of characters produce more uniformly distributed hash values.
        
2. **Efficient computation**
    
    - Multiplying by 31 can be optimized by the compiler:
        
        `31 * hash = (hash << 5) - hash`
        
        (shift left by 5 = multiply by 32, then subtract `hash`).
        
    - This makes it very fast.
        
3. **Balance between collision rate and performance**
    
    - Small primes like 2, 3, 5… lead to more collisions.
        
    - Large primes increase overflow and performance cost.
        
    - 31 strikes a good balance: small enough for fast computation, large enough to reduce collisions.
        
4. **Historical and empirical reasons**
    
    - Early experiments in Java showed that 31 gave a very good distribution of hash codes across different strings.
        
    - It became the standard choice and is still used in `String.hashCode()`.