1. To concatenate a value to string , convert it to string.
![[Pasted image 20241113114515.png|300]]

2. To set precision use
![[Pasted image 20241113114620.png]]
it is present in `#include<iomanip>`

3. Using this we can access member functions from class too.
![[Pasted image 20241113121210.png|300]]

4. you can create array to ease calculation like give below
![[Pasted image 20241113123607.png|300]]
![[Pasted image 20241113123625.png|400]]

5. ways to set precision 
 ![[Pasted image 20241113191101.png|400]]
6. Initializing size to a array using constructor
![[Pasted image 20241113225033.png|200]]
here "this->" is used to refer to LIMIT variable of this instance of class.


```cpp
using namespace std;
class A
{
    int id;
    static int count;
public:
    A() {
        count++;
        id = count;
        cout << "constructor for id " << id << endl;
    }
    ~A() {
        cout << "destructor for id " << id << endl;
    }
};
  
int A::count = 0;
  
int main() {
    A a[3];
    return 0;
}
```

OUTPUT
```
constructor for id 1
constructor for id 2
constructor for id 3
destructor for id 3
destructor for id 2
destructor for id 1
```

7. use this to catch string msg 
![[Pasted image 20241117204336.png]]
8. To represent two int 3 and 45 as 3.45
![[Pasted image 20241121101826.png]]

9. To take all inputs without knowing the limit
![[Pasted image 20241121125628.png]]

10. to take modulus of double and int
![[Pasted image 20241121171209.png]]

11. using ostream
![[Pasted image 20241121183032.png]]

![[Pasted image 20241121183455.png]]
11. In initializer list we can only initialize variables of the current class and not the inherited class.

![[Pasted image 20241121194036.png]]
