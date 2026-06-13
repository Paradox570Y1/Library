![[Pasted image 20250718200226.png]]

[[ICMP]]

# What is runtime complexity?

![[Pasted image 20250718204204.png]]
- Time taken by algorithm depends on various factors like where i am running, when i am running and what other processes are running in CPU. So it depends on all that factors not just time complexity. 

![[Pasted image 20250718214939.png]]

![[Pasted image 20250813172558.png]]

![[Pasted image 20250718215028.png]]
- Cow algorithm: Copy on write  turns on dirty bit while writing data so that only that memory location changes replicated on ram as well. Otherwise you have to copy all elements from cache to ram.
![[Pasted image 20250718215116.png]]

![[Pasted image 20250718214436.png]]

![[Pasted image 20250718214630.png]]


# Conclusion
- Runtime Complexity of Selection Sort is N² for worst case , best case and average case.
![[Pasted image 20250718220403.png|300]]
- 1st Priority: Best time complexity is very important as for example if google search takes 4sec , instead of 3sec then many users will start using faster browser.
	- Quick sort uses even less instruction than Merge Sort.
- 2nd Priority: Space can indirectly affects runtime. 
	- So like for pc's you can use merge sort but in case of smart watch with constraint of space you might not be able to run merge sort as it will take more space which might not be available so instead use selection sort , so that it at least do the job.
- 3rd Priority: Is it cache friendly or not. Like is it randomly asking for memory location or asking for neighboring elements.
	- As merge sort is swapping elements at distant position it's ok for cache but for bubble sort is more cache friendly as it only do neighbor access even better than selection sort.
- 4th Priority: Is it [[stable sort]] or not.
	- Selection sort is not stable.

If not stable it can interchange name and sir name especially when name or sir name is same and swap still happens.
![[Pasted image 20250718220123.png|300]]

![[Pasted image 20250718220946.png|400]]
If a element is before b , then during sorting process it should remain that way , like  merge sort is stable but quick sort is not .
- 5th Priority: Number of swaps taken.
	- Selection sort has less no. of swaps , merge sort will do more and so do bubble sort will which will do unnecessary swaps.


- C uses quick sort blindly but Java runs some checks and select what algorithm will sort it faster in sort library.


# Max Heap
- Not good for finding kth largest value  with maxHeap , as we can only be sure of the largest value whereas 2nd largest could be at i index or i+1 index (not sure) .
	- Especially if we have to get all n elements, then TC-> O(2nlog n). Whereas merge Sort takes  TC-> O(nlog n) only.
- While inserting element it is added at end of heap , then it has to swim at max log n times to reach at correct position.
- While deleting element, largest element is swapped with last element, then size of array is decreased by 1. After that the top element in heap tries to sink to its correct place which will take log n.


# Selection Sort

- To get only first k largest elements then Selection Sort takes TC-> O(n\*k) which is good as long as k << n .
	- It is not stable sort.

>To record time include **<sys/time.h>** 
>![[Pasted image 20250813175715.png]]
>Then you can use `timeval` data type - this gives you current time from 1 Jan 1970 in seconds and microseconds. 1 Jan 1970 is called as called [[Unix epoch]].
>Store this calculated value in long long as it could be very large
>![[Pasted image 20250813181031.png]]

![[Pasted image 20250813181316.png]]

- To use `time(NULL)` include `<time.h>` lib.
![[Pasted image 20250813183003.png]]
# SSL

[Resource](https://www.geeksforgeeks.org/computer-networks/secure-socket-layer-ssl/)
- It is Secure Layer or Secure Socket Shell.(It's Internet Security Protocol)
- Communication is still HTTPS but data will go to SSL layer , do some encryption and decryption and then go to external terminal.
- If client sends data on server, then that server forwards the data to service provider server which later forward to website server. Now in this process their might be hacker who can do **Man in Middle Attack** and get copy of data , then he can use the data. To prevent this SSL comes in picture.


To Solve this issue of SSL , Symmetric key algo comes in picture
- Symmetric key algo is itself encrypted by the provider which has it's own public key.

![[Pasted image 20250725205914.png|300]]

# Bubble Sort
- It's inferior to selection sort in most cases.
- If data is mostly sorted then using intelligent Bubble Sort can be little better as if no swaps happens then it will break the loop early.



# Unix
- Though VM has it's own privileges but ultimately it's a program or process for Host machine .
- VM feature must be unable by Host , otherwise you will not be able to create a VM. Check BIOS If hypervisor is off  or on.
- The program executing in VM will use all the concepts of OS as well.

#Benifits
- I can have as many VM as required.
- I have configuration manager using which i can scale up or down the VM(instances) as per my need.
- All the risk can happen in VM like a hacker deleting files on VM or making the server busy. But our Host machine remains safe we relaunch a new instance.

- Suppose 100 user traffic is coming on your server than Kubernetes can launch 10 more docker containers to accommodate that in few milli seconds.

# Using Oracle VM

- To communicate with VM
	- You can create a mount point which is common area for VM and Host OS.
	- You can use some common app like Gmail to send data from Host and receive from Gmail in VM.
	- You can launch Apache server on VM and have  a shared port with Host to send and receive data.
- To stream line above process we can use  Vagrant which shares the folder of VM with your host machine.
	![[Pasted image 20250725215354.png|400]]
	
- You can download ubuntu image through bento repository
	![[Pasted image 20250725214744.png]]


# Insertion Sort
- It is like deck of cards.
- If the data is already sorted or nearly sorted, **insertion sort** is a preferred algorithm because it performs efficiently in such cases. This is because each element is compared only with its preceding elements, and as soon as the correct position is found (i.e., when the left element is not greater than the current one), no further comparisons or swaps are needed. This leads to a **best-case time complexity of O(n)** with **minimal shifting**.
- It only shifts elements **leftwards until a smaller one is found**, avoiding full-array traversal.
- Unlike other sorting algorithms, it **does not perform unnecessary operations** on already sorted data.
- Worst time complexity is O(N) 
![[Pasted image 20250801201210.png|400]]

- If n is small then in algorithms like King Sort then insertions sort is applied but  for larger value , merge or insertion sort is applied.
![[Pasted image 20250801202020.png|400]]

- Runtime: O(N) -> O(N²)
- No extra space required.
- Cache friendly
- It's stable sort
- Swaps: O(1) -> O(N²) swaps


# Recursion vs Iterative

![[Pasted image 20250801202914.png|400]]
- In both recursion and iterative no. of instructions sent to CPU is same so **Runtime Complexity is same** although recursion has less no. of lines of code.
- In recursion it is maintain extra data structure which is stack which is not the case with iterative approach.
	- So in recursion extra space might be required to maintain function stack.
	- So **recursion may use extra space**.
	- If interviewer asks about space complexity then it same for both recursion and iterative.
		- We don't consider recursion's function 
- Sometimes Iteratively very big or impossible code can be written in recursively in compact way.

- Steps to do recursion
	- Think how to break it into subproblems.
	- Exit condition
	- In subproblems try to keep the boundary of them to be mutually exclusive otherwise you might send more instructions to the compiler.(Your recursion should be working on different set of data otherwise it can give more than iteration time)
	![[Pasted image 20250801204518.png|300]]
- Binary search is good candidate to write a recursive code bcz
	![[Pasted image 20250801204926.png|400]]
```java
public static int binarySearchRecursive(int[] arr, int target, int low, int high) {
        if (low > high) {
            return -1; // Target not found
        }
        int mid = low + (high - low) / 2; // Prevents potential overflow

        if (arr[mid] == target) {
            return mid; // Target found
        } else if (target < arr[mid]) {
            return binarySearchRecursive(arr, target, low, mid - 1); // Search left half
        } else {
            return binarySearchRecursive(arr, target, mid + 1, high); // Search right half
        }
    }
}
```

### Analyzing Runtime complexity

![[Pasted image 20250801205821.png|300]]

![[Pasted image 20250801205931.png|300]]
- Since it is dividing length by 2 then TC => O(log₂ N) 

- Now for Fibonacci number
![[Pasted image 20250801211537.png|300]]

![[Pasted image 20250801211827.png|350]]


![[Pasted image 20250801210450.png|300]]

Analyzing cost for call
![[Pasted image 20250801212014.png|350]]

![[Pasted image 20250801212109.png|350]]

![[Pasted image 20250801212154.png|350]]


Q Tower of Hanoi
![[Pasted image 20250801214549.png|350]]

![[Pasted image 20250801214830.png|350]]

![[Pasted image 20250801215158.png]]


Q. What is the sum of even numbers in Fibonacci series



# Tower of Hanoi

```java

```

How many moves it takes 
![[Pasted image 20250815205149.png|400]]

# Merge Sort

![[Pasted image 20250815211357.png|400]]

![[Pasted image 20250815211643.png|400]]


![[Pasted image 20250815212157.png]]


![[Pasted image 20250815212616.png]]

- Literal swaps in merge sort is `0` but talking about movements while changing location is `n logn`.

![[Pasted image 20250815213521.png|400]]
![[Pasted image 20250815213536.png|400]]

# Inversion count
- How far an element is from getting sorted
![[Pasted image 20250815215609.png]]
- like there are 3 elements less then 4 which are placed after 4 , so 4 needs 3 moves to reach at its correct position.
- Similarly 3 is is misplaced by 2 positions and 2 is misplaced by 1



---
Discussion on puzzles
![[Pasted image 20250829202950.png]]

# Quick Sort

- It places the element at its correct position.
- It ensures that elements to the left of placed element is lesser than itself and elements after the placed element is greater than itself.

![[Pasted image 20250829204653.png]]


![[Pasted image 20250829205901.png|300]]'
![[Pasted image 20250829210552.png]]

So time complexity is n² when array is ordered whether reverse order or ascending one.
- In ascending order it will form skew tree.
- In descending order it will form zig-zag pattern.

To solve this problem instead of taking first or last element as pivot, take the middle element as pivot.
- Now the probability is less that the pivot taken is the smallest one.
- But still N² in case we always get smallest middle element.
![[Pasted image 20250829211533.png]]

![[Pasted image 20250829211812.png|300]]


- Caching better than merge sort but not as good as selection or bubble sort
- Swaps are kind of equal to merge sort.
	![[Pasted image 20250829211921.png|200]]

Kth Smallest Question Optimization
![[Pasted image 20250829212431.png]]

![[Pasted image 20250829212745.png]]


# Heap Sort

- Always gives O(n log n + n log n) time complexity.
	![[Pasted image 20250829214413.png]]
	- In case of ordered array one of function either sink() or swim() will take O(N) while other will take  O(N log N).
- Not a stable sort.
- Worst in Caching.
- Swaps are n log n
**Only use Heap sort if needed always n log n Time Complexity and there is little space in ram.
![[Pasted image 20250829220047.png|300]]


---

# Find if number is power of 2 or not
- [[Power of two]]

- Magician has deck of 52 cards and performing in front of an audience. One person at random from audience draws one card from the deck at random. Then shows that card to audience. Magician took that card, put it back in stack and shuffles it. Then that persons friend who was outside and not in the audience was called upon the stage. Then Magician draws four cards and present it to that friend. Then how can that friend find the same card which was shown to the audience.
![[Pasted image 20250905211448.png|300]]
-  You can flip the four cards to communicate the number of card as they are 13 and can be represented with 4 bits representing 4 cards.
- You can get which club the that card belongs to with orientation of first two cards which could be horizontal or vertical as their are 4 types of club.
- There are 100 cards and all cards are of square shape. One person will pick random card and keep it , then 2nd person will do the same and so does 3rd and 4th. Then Magician shuffles all those 4 cards. Then magician takes one card from 96 cards left and put that on top the 4 cards. Now this pile of 5 cards is handed to some other person from the audience.



# ! vs ~

! means does this thing exist or not.
- !(0) = 1
- !(anything except 0)  = 0

~ means flipping the bits

# Bitwise right shift and left shift

- What will be the result if we shift any negative number 31 times or divide it 31 times then what will be the result?
```txt
any -ve number will begin with 1 after that it could be any pattern of 0 and 1.
So on shifting 31 times this 1 at start will shift till end of the number.
While shifting , since number was negative 1 will be appended from the left.
Hence number will become 1111 1111 1111 1111 1111 1111 1111 1111 which is -1.
```
- So result will be `-1` always.


# Another approach to find which number is not in pair
- 
![[Pasted image 20250905221205.png]]




# Good Puzzle
- There is a prison. there are 10 prisoners and you are one of them, you have infinite black and white hats . in morning a random color hat is over their head. when prisoner are standing in straight line . so 1st person can see no one , next can see 1 , next can see 2 and so one. Prisoners can't hint each other. Then when 10th prisoner was asked about his hat color then he has to pick one , if wrong then die. Then it will be asked from 9th one. The idea is to save maximum number people by devising some strategy.

Solution:
- Take black hat as 1 and white hat as -1.
- Now person in question will multiply all colors he see in front of him.
- And he will say that color based on final result , then there is 50:50 chances that his color is same.
- Now Janitor moves to the next person , now next person knows what is the multiplication including him and he can do multiplication of all hats in front of him. Now he can deduce that including him multiply is lets say 1 and excluding him multiply is 1 again. then that mean his color is also 1. He will say it and will be alive. Rest will follow same





- What if there are 3 types of hat are there and rest problem is same.(black, white and red) now create a new strategy?
- What if there are any number of hat?
- What if there are any number of hat and any number of people?



Question: find lonely number while rest number form triplets and number could be anything in range upto n to 2 to the power 5.
![[Pasted image 20250912210301.png]]

in this question you add set bit for each position differently  while running the loop. Suppose at unit position you got some of set bit to be 4 then take %3 of it and if it is 0 then lonely number bit is 0 else %3 is 1 then lonely number bit is 1. Using this we can form the whole number.




![[Pasted image 20250912212407.png]]

![[Pasted image 20250912213719.png]]

![[Pasted image 20250912213702.png]]
![[Pasted image 20250912214709.png]]

![[Pasted image 20250912214313.png]]



What is base64?
- It is used to encrypt password, even images and video which is wrong.
- It is used for encoding and decoding.


![[Pasted image 20250912215501.png]]
- There could be any network component which during the process of transfer can't interpret symbols like Rupee because it is old technology. This can be seen when sometimes you receive weird text instead of correct one like triangle, circle etc. 
- Although receiving device can interpret the data but some networking device in between might not be able to do it. So this is the reason data is converted to base 64 format and then sent to receiver. Now receiver will convert these back to base 2 to get correct information.
- If some characters are not able to form pair then compensate with `=`


Implement base2 to base 64 encoding algorithm
![[Pasted image 20250912221119.png]]

![[Pasted image 20250912223039.png]]

- 4 - size%3 times equals lagaane hai


---
- `String Buffer` is used in thread safe environment which is the additional benefit of `String Buffer` over `String Builder`.
- Why String is mutable in java , this is bcz it uses the concept of String Pool where same string shares the same reference which saves space as well updating the string updates for all the pointers accessing it, so you don't have to update it every place.

- So basically in case of non thread safe data structures elements can be inserted in any order and there can also be case where some elements are lost reason being one thread override the insertion done by some other thread

- Do reader , writer problem.
- Learn about mutex , semaphores , locks , thread safe data structures.



There is a King who has 1000 barrels of wine. He is a drinker. After 1 week there is a party where he has to drink all bottles. Then there is a spy who wants to add poison in King's drink and one drop of that poison can instantly kill King. When he puts that poison in a barrel and got found out by guards and killed on the spot. If anyone drinks the poison now then that person will die after 7 days. Guards have the job to find which barrel has poison. Now guards are making use of prisoners who are at death row and there are only 10 prisoner. Since party is after a week. So, how to find that barrel of poison.

- Consider 10 bits representing 10 prisoners.
- Then mark all bottles from 0 to 1000.
- Then make people drink the bottle based on binary representation of that bottle's number.
- Then the people who die mark them one and marks rest of them 0 , then you will get bottle's number in this binary representation.


# Pointers
![[Pasted image 20250926210635.png]]

![[Pasted image 20250926211149.png]]
- J is just a number which is valid integer. Then size of pointer is going to be same as that of datatype  irrespective of it's content.
- When pointer moves, it moves by the bits of the data type stored.


![[Pasted image 20250926211844.png|200]]
![[Pasted image 20250926212401.png|300]]

- Python is an interpreted language and is not strictly type language. For example you can put any data type inside an array in python because it store array of pointers to the reference of data. So it basically makes a lookup.
[Python doc for object](https://docs.python.org/3/c-api/structures.html#c.PyObject)
- Pointer is basically hashcode of data.
- Using NumPy you can make use of data structure to improve the code efficiency.
![[Pasted image 20250926213504.png]]
![[Pasted image 20250926213606.png]]
- Here when iterating through array where index are stored as integer of 4 bytes then we add 1 to it to increment by 4 bytes again.
- In case of pointers we increment by size of type of data like here if we has a char array then it increments by 1 byte which is size of char.

![[Pasted image 20250926214141.png]]
- Simulate Memory Management in OS , you have to allocate memory for data of user and manage empty spaces using first fit or best fit.

##### Using Linked List
![[Pasted image 20250926214949.png|400]]



Problem
- There is a cap seller , cap merchant , he want to hire the smartest person to work in his shop. So, he conducted a test and he found 3 smartest person in that , now he has to find the smartest of the three. There is a box which has 3 white hat and 2 black hat . All three people knows that then they are blindfolded and put one cap on each and they are standing in triangle where they can see other two, not his own. Then asked to guess the color of the cap. Then one person guessed white, so what logic he gave to choose white?
Solution: All 3 were thinking and C saw that B is not telling the answer immediately that means the two caps that B saw must be white and since all 3 are intelligent person so they are good at knowing the probabilities of which cap they can have. That's why C deduce that he must have White cap because he can confirm that A has white but based on B thinking alot then C must not have black.
	![[Pasted image 20251003202024.png|300]]


# Function Pointers

![[Pasted image 20251003202444.png]]
- Accurate means two processes should not be allocated in the same memory block.

- Simulate Memory Management in OS , you have to allocate memory for data of user and manage empty spaces using first fit or best fit.
![[Pasted image 20251003203058.png]]
- If we use best fit then time complexity will always be O(N) but fragmentation will be less.
- If we use first fit then time complexity worst case is O(N) but fragmentation is more.
- We can perform defragmentation every time or can do it periodically after some time or do it when required.
- There is no perfect answer based on scenario every approach has pros and cons.
- In BST(Binary Search Tree) , cost of fragmentation is very high therefore we should use best fit where fragmentation is less.



- Function pointers in C are used for generics and not for callbacks like JS or Python.
	![[Pasted image 20251003205202.png|300]]
	![[Pasted image 20251003205302.png|300]]
	![[Pasted image 20251003205428.png|300]]
	![[Pasted image 20251003205734.png|300]]
- Write Generic sorting algos in C. You can use double * as well.

# Puzzle time

Q1
![[Pasted image 20251003210343.png]]

Q2
- There are 10 bags all having identical coins with 100 coins each. In 9 bags each coins weight is 10 gm and there is one bag which has 10.1 gm.
	![[Pasted image 20251003210539.png]]

Q3
- Variant of question 1, you have same condition but the defect in that one coin is unknown whether it is heavier or lighter.
	- Ternary Number concept to solve this problem
	![[Pasted image 20251010201254.png|200]]
	![[Pasted image 20251010201630.png|250]]
	![[Pasted image 20251010201639.png|250]]
	![[Pasted image 20251010201649.png|250]]
	![[Pasted image 20251010201830.png|300]]
	![[Pasted image 20251010202637.png|300]]




Generic code implementation
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

//works for any data type. do not change this method for any testing. As it is s generic method
void swap(void *a[], int i, int j)
{
    void *temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}
//works for any data type. do not change this method for any testing. As it is s generic method
void quick_sort(void *a[], int L, int R, int (*cmp)(void *, void *))
{
    if (L >= R)
        return;
    int p = L;
    int i = L + 1;
    for (; i <= R; i++)
    {
        if ((*cmp)(a[i], a[L]) < 0)
        {
            swap(a, i, ++p);
        }
    }
    swap(a, p, L);
    quick_sort(a, L, p - 1, cmp);
    quick_sort(a, p + 1, R, cmp);
}

struct student
{
    int id;
    char name[10];
};


int intCmp(void *x, void *y)
{
    int *i = (int *)(x);
    int *j = (int *)(y);
    if (*i == *j)
        return 0;
    if (*i > *j)
        return +1;
    return -1;
}

int floatCmp(void *x, void *y)
{
    float *i = (float *)(x);
    float *j = (float *)(y);
    if (*i == *j)
        return 0;
    if (*i > *j)
        return +1;
    return -1;
}
int studentIdCmp(void *x, void *y)
{
    struct student *i = (struct student *)(x);
    struct student *j = (struct student *)(y);
    if (i->id == j->id)
        return 0;
    if (i->id > j->id)
        return +1;
    return -1;
}

int studentNameCmp(void *x, void *y)
{
    struct student *i = (struct student *)(x);
    struct student *j = (struct student *)(y);
    return strcmp(i->name, j->name);
}



void test_float_sorting()
{
    printf("testing float sorting\n");
    float **b = (float **)(malloc(sizeof(float *) * 5));

    int i;

    for (i = 0; i < 5; i++)
    {
        printf("enter input:");
        float *num = (float *)(malloc(sizeof(float *)));
        scanf("%f", num);
        b[i] = num;
    }
    printf("unsorted data : ");
    for (int i = 0; i < 5; i++)
    {
        printf("%f->", *b[i]);
    }
    quick_sort((void **)b, 0, 4, (int (*)(void *, void *))floatCmp);
    printf("sorted data : ");
    printf("\n");
    for (int i = 0; i < 5; i++)
    {
        printf("%f->", *b[i]);
    }
    printf("\n");
}
void test_int_sorting()
{
    printf("testing int sorting\n");
    int **b = (int **)(malloc(sizeof(int *) * 5));

    int i;

    for (i = 0; i < 5; i++)
    {
        printf("enter input:");
        int *num = (int *)(malloc(sizeof(int *)));
        scanf("%d", num);
        b[i] = num;
    }
    printf("unsorted data : ");
    for (int i = 0; i < 5; i++)
    {
        printf("%d->", *b[i]);
    }
    quick_sort((void **)b, 0, 4, (int (*)(void *, void *))intCmp);
    printf("\n");
    printf("sorted data :");
    for (int i = 0; i < 5; i++)
    {
        printf("%d->", *b[i]);
    }
    printf("\n");
}
void test_student_sorting()
{
    printf("testing student sorting\n");
    struct student **b = (struct student **)(malloc(sizeof(struct student *) * 5));

    int i;

    for (i = 0; i < 5; i++)
    {
        struct student *s = (struct student *)(malloc(sizeof(struct student *)));
        printf("enter input (id):");
        scanf("%d", &s->id);
        printf("enter input (name):");
        scanf("%s", &s->name);

        b[i] = s;
    }
    printf("unsorted data : ");
    for (int i = 0; i < 5; i++)
    {
        printf("%d(%s)->", b[i]->id, b[i]->name);
    }
    quick_sort((void **)b, 0, 4, (int (*)(void *, void *))studentIdCmp);
    printf("\n");
    printf("sorted data by id :");
    for (int i = 0; i < 5; i++)
    {
        printf("%d(%s)->", b[i]->id, b[i]->name);
    }
    printf("\n");
    quick_sort((void **)b, 0, 4, (int (*)(void *, void *))studentNameCmp);
    printf("\n");
    printf("sorted data by name :");
    for (int i = 0; i < 5; i++)
    {
        printf("%d(%s)->", b[i]->id, b[i]->name);
    }
    printf("\n");
}
int main()
{
    test_int_sorting();
    test_float_sorting();
    test_student_sorting();
}
```



---
# Java
- Write once Run Anywhere.
- Due to Garbage Collector, memory management is not pain.
- Uses concept of OOPS, we can call it 99% Object Oriented as Java supports primitives like int which is not a child of object class.
- Robust with multi-threading language
- Strongly typed language.
- It supports double inheritance but not triple as every class in java by default extends Object class and it can extend one more class using extend keyword. Hence at max it can have two parents out of which one is default.
![[Pasted image 20251010205224.png|400]]

- Therefore following methods are by default with every class
![[Pasted image 20251010210538.png]]![[Pasted image 20251010210653.png]]

- What is stopping c from being platform independent language like java?
- Whit is Big Endian and Small Endian
	- normally OS are Big Endian.
	- Small Endian in UNIX which makes binary operation easy
	- There could be issues when you compile code in big endian machine but run it on small endian.
		![[Pasted image 20251010213339.png|250]]
	- Java is Big Endian in itself
		- `.class` compiled file is in Big Endian.
		- But it gets executed inside JVM and JVM is the process for the OS. If that code wants to use hardware or other resources then JVM perform the conversions from big endian to small endian in case of small endian machines.
		- JRE (Java Runtime Environment) provides the environment to run java code but it does not has compiler and hence used in production where compiling is not required.
		- JDK (Java Development Kit) has Runtime environment, compiler , even debugger.
		- Since window file names are not case sensitive and UNIX file names are case sensitive hence Java is made case sensitive to run in both environment without issue.


- JAVA's Magic number (Cafe babe)
	- Java is a type of Coffee so developer fixed the initial byte code to represent CAFE BABE
	![[Pasted image 20251010214511.png]]
	After conversion
	![[Pasted image 20251010214516.png]]

- Java also has JIT
	- It caches the machine code (byte code) once `.class` file runs.
	- So next time machine code can directly run by JIT.
- `Micronant` is another java `Kernal` which is not platform independent but is even faster than `SpringBoot`. But it doesn't have huge community support and hence not used much.


- class loader
- root loader
- jvm

![[Pasted image 20251010220006.png]]

[Link](https://www.geeksforgeeks.org/java/java-class-file/)

# Classloader
- A **ClassLoader** is a part of the **Java Runtime Environment (JRE)** responsible for **loading classes into memory** when a Java program runs.
- When you run a Java program, your code (in `.class` files) isn’t immediately part of memory. The **ClassLoader** loads these classes **dynamically** — only when needed — rather than all at once.
	![[Pasted image 20251017200848.png|300]] 
	- Three types of ClassLoader
		- Application
		- Extension
		- Root or bootstrap 
	- They follow delegation principle where they don't want to do the work themselves but delegate to their parents.
	![[Pasted image 20251017201442.png|300]]
	- If no location specifies then ClassLoader search in current directory (.)
	![[Pasted image 20251017201621.png|300]]
	- `rt.jar` typically in lib.
	- ClassLoader job is to search in this `rt.jar` file where all the classes are present.
![[Pasted image 20251017201927.png|450]]
![[Pasted image 20251017202152.png|200]]
- Object of class is created in Object pool.
- What happens if we put the same class file in x.jar and y.jar files both or even multiple jar files. When java ClassLoader will run, it will randomly pick class from any jar file which ever comes first. This is called "Java Class Hell". So this is very big problem in java which a developer should take care of.
- To prevent Jar Hell one should do versioning for jar files.
- That's why use Build Tools like Maven, Gradle and not build manually.
![[Pasted image 20251017202726.png|400]]
- If you are creating a class which uses some constant data then it's good to use static keyword to keep a single copy of data and since it is constant then it's good practice to make use of final keyword with that.

- If you are assigning int value to long data type then it gets implicitly type casted.

![[Pasted image 20251017203753.png]]
- In java even if parameter of function takes long and we pass an int argument then it still works but this will not work in C/C++.
	- This is because **Auto Widening** in JAVA.
	- Here JAVA tries to find the best bit in whole file if argument is int and it did not find function signature which has int parameter then it will try to find better fit if available like long etc.
- But you can't have two functions with same type of parameter
	![[Pasted image 20251017204111.png|300]]

- What if we have a class Integer as parameter of function and while calling the function with primitive int as parameter?
	- Then since JAVA didn't find the function taking int parameter then it will try to find the best fit using `Auto Boxing`.
- Similarly in case parameter of function is int and we pass Integer as argument then it also does `unboxing`.

# Variable Argument
- To pass dynamic number of arguments in a function.
![[Pasted image 20251017205224.png|300]]
- In case you only pass one argument but there are two functions variable argument and same data type
	![[Pasted image 20251017205749.png]]
	- The best fit would be `int i` one.

# Select Preferences
- What if we pass an int parameter while passing function.
![[Pasted image 20251017210807.png|400]]

Expected preference as per overhead and the right way is:
Variable int argument -> Integer Wrapper Class -> long

Actual preference
long -> Integer Wrapper Class -> Variable int argument


- The reason for this blunder is JAVA ensures Backward compatibility with previous versions of JAVA. Since long was used since version one and concept of wrapper class and variable int argument came later hence the preferences were decided according to that.
![[Pasted image 20251017210630.png|300]]

# Java History

![[Pasted image 20251017210909.png|300]]
- Auto-widening also existed in JDK 1.0
![[Pasted image 20251017210920.png|300]]
![[Pasted image 20251017211006.png|300]]
![[Pasted image 20251017211019.png|300]]
![[Pasted image 20251017211027.png|300]]
![[Pasted image 20251017211039.png|300]]

Since java is backward compatible hence it has to keep the wrong way of giving preference.

> When Sun Microsystems has downfall then Oracle bought JAVA as it's databases were using JAVA and they want future support of language.



# Inheritance

- Abstract Class 
	- It can not be initialized.
	- It can contain one or more abstract methods whose implementation does not exist along with methods whose implementation exists.
	- If a class extends abstract class then it has to define the the abstract functions of parent class.
	- We can create a child of class.
	![[Pasted image 20251017212529.png|300]]
- Interface
	- It contains all abstract methods.
	- It fakes multiple inheritance in java.
	- It prevents diamond problem as it's implementation does not exist earlier but defined later dynamically.

![[Pasted image 20251017213037.png|300]]

For `Maruti m2 = new Car();`
- First make ClassLoader.
	![[Pasted image 20251017213923.png|100]]
- Now using pointer we can say m2 is of type Maruti.
	![[Pasted image 20251017214028.png|200]]
- Now the object formed is of type Car and that object is getting assigned to m2 hence m2 is of type Maruti which is pointing to Object of Car.
	![[Pasted image 20251017214126.png|200]]
![[Pasted image 20251017214344.png|300]]
- Type of m2 defines the scope to which functions it can call.
- From m2 i can call f1, f2, f3. There is no problem in calling f1 and f2. But calling f3 can break the code and creates confusion for compiler as object of Car doesn't have f3 which is pointed by m2 reference and java doesn't allow confusion hence it doesn't work.



For `Car c2 = new Maruti()`
![[Pasted image 20251017214826.png|300]]
- Now it's sure that c2 can only call f1 and f2 . No confusion at all hence java allows.
- So type of c2 defines the scope to which functions it can call.
- We use type casting to give JAVA a disclaimer that in case if the code is broken down then it's not the fault of JAVA.
- 

# Java allows child class to change visibility
- But in only allows to increase the visibility from private to protected/public / protected to public.
	- Since increasing visibility means it is still accessible at the child but in case you do the opposite then their can be cases where child will set the visibility so low that it's not even visible to that child itself.
	- So it is done because at runtime this concept should not fail.
![[Pasted image 20251017215251.png|300]]


# Exception Handling

- At top level everything is object then their is throwable interface.
	![[Pasted image 20251024201004.png|300]]
	- Errors like : Out of Memory, Index out of bound and other JVM errors
		- We do not have any control if they occurs.
	![[Pasted image 20251024201206.png|300]]
	- Exception on other hand.
		- They can be handled or can halt the program execution.
		- It's upto you if you want to catch an exception or not.
		- Ex: `IOException`, `File Not Found`, Exception
		![[Pasted image 20251024201722.png|400]]
		![[Pasted image 20251024202046.png|400]]
		
		![[Pasted image 20251024202312.png|400]]
		- To handle above exception:
			First way is:
			![[Pasted image 20251024202423.png|400]]
			Second way is:
			Using try block and finally block.
			![[Pasted image 20251024202524.png|300]]
			![[Pasted image 20251024202742.png|300]]

# Unchecked Exception
- These exception are not mandatory to be handled , it's upto developer.
- So developer is not bound to handle these exception.

![[Pasted image 20251024203607.png|400]]
- We cannot use `FileNotFound` exception in place of `IOException` as all errors in this case can come under `IOException` but `FileNotFound` can not handle other file related exception.


# Finally
- Finally code is executed even if code catches an exception.
![[Pasted image 20251024204031.png|400]]

> In `UNIX` by default you cannot open more then 1024 files. This includes temp files, socket etc. as well.


# Try Resource
- It came after java 8.
![[Pasted image 20251024204650.png|300]]
- here it automatically closes file once scope gets finished.
- All the resources are handled by JAVA.
- Internally it might implement try and finally concept only


- Exceptions are handled sequentially.
	![[Pasted image 20251024205055.png|200]]


# Exception Visibility
- You can only decrease the Exception visibility from parent to child.
![[Pasted image 20251024210637.png|300]]
![[Pasted image 20251024210321.png|300]]
![[Pasted image 20251024210435.png|300]]
- So visibility can be handled in parts like here Car class handles `IOException` and Maruti class handles `FileNotFound` Exception.


# Interfaces
- Most used interfaces that we must know.
	- `Marker Interface`: They are empty interface with no body.
		- Even if they are implemented in a class then still they can be kept empty.
		- Examples are :
			- Serializable
			- Cloneable
			- Remote
				- RMI calls not used now days.
	- `Iterable` like Iterator.
		It forces you to implement iterate() method which has at least two functions `hasNext()` and `next()`.
		![[Pasted image 20251024214358.png|400]]
	- `Comparable` contains compareTo(other object) method.
		- It is part of the class.
		- Only one comparable can be written as it's implemented within class.
	- `Comparator` contains compare(obj1, obj2) method.
		- It can be internal and external but can be implemented outside of class.
		- We can write as many comparator as we want. So based on scenario we can pass different comparator object.
	- `Runnable`
		- Using Runnable we can extend a class as well along with implementing thread functionality.
		![[Pasted image 20251024213804.png|400]]


![[Pasted image 20251107201122.png|400]]

![[Pasted image 20251107201551.png|300]]

Linked List implementation with iterator.
- This is the standard way to add iterator  for any  collection.
![[Pasted image 20251107201831.png|300]]
![[Pasted image 20251107202046.png|300]]

```java
import java.util.Iterator;

public class MyLinkedList implements Iterable<Integer> {

  @Override
  public Iterator<Integer> iterator() {
    return new MyLinkedListIterator();
  }

  private class Node {
    public int data;
    public Node next;

    public Node(int k) {
      this.data = k;
      this.next = null;
    }
  }

  private Node head;

  public void insert(int k) {
    Node n = new Node(k);
    if (head == null) head = n;
    else {
      Node t = head;
      while (t.next != null) {
        t = t.next;
      }
      t.next = n;
    }
  }

  private class MyLinkedListIterator implements Iterator<Integer> {
    private Node t = head;

    @Override
    public boolean hasNext() {
      return t != null;
    }

    @Override
    public Integer next() {
      int val = t.data;  // get current data
      t = t.next;        // move to next node
      return val;        // return current data
    }
  }

  public static void main(String[] args) {
    MyLinkedList l = new MyLinkedList();
    l.insert(1);
    l.insert(2);
    l.insert(3);

    // Using enhanced for-loop (works with Iterable)
    for (int x : l) {
      System.out.println(x);
    }

    // Using iterator explicitly
    Iterator<Integer> ite = l.iterator();
    while (ite.hasNext()) {
      System.out.println(ite.next());
    }
  }
}

```


![[Pasted image 20251107204204.png|300]]
# Collection Interface

![[Pasted image 20251107211304.png|400]]

![[Pasted image 20251107213233.png|400]]

Q. Five pirates need to divide 100 Gold Coins. Pirates have a hierarchy, from Level 1 to level 5. The highest level pirate is the leader. The leader proposes a plan to distribute the gold and all the pirates vote on it (including the leader). If at least 50% of the pirates agree on the plan, the gold is split according to the proposal. If not, level-5 pirate is kicked from the ship, and the level-4 pirate now proposes a new plan. This process continues until a proposal is accepted. All pirates are extremely smart and extremely greedy. How does level-5 Pirate divide the treasure?


In generics of Set we can only pass classes like Integer and not primitives like int. 
![[Pasted image 20251107214540.png|300]]
- Time complexity is O(1) but **conditional** not necessary it's always O(1).
- It's efficiency depends on hashing technique implemented.
- It has two factors which are initiated on creation of hash set which is number of buckets and load factor.
	![[Pasted image 20251107215840.png|300]]

# Trees

- Self Balancing BST
	- Red Black Tree
	- AVL Tree
	- Comparison


- If anyone is trying to solve crud problem
	- one can use LL, stack, queue, priority queue, BST
	- The best data structure to use for CRUD is BST.
	- Only problem with BST is worst case could be O(N)
		- This happens when BST is right/left leaning tree.
			![[Pasted image 20251114191134.png|150]]
		- To solve this problem we will try to convert it to full Tree.
			![[Pasted image 20251114191220.png|200]]
			- But now issue is that converting to full tree requires very high cost. So, instead we will make some compromises while trying to improve tree structure for better time complexity.

# Red Black Tree
- Works on the concept of 2-3 Search Tree.
	- Means either we have 2 way three or at max 3 way tree
		![[Pasted image 20251114191509.png]]
		- If C is red then it is never counted as height.
		- Our goal is minimize reds in a path. At least minimize two consecutive reds.
			![[Pasted image 20251114191743.png|300]]
		- Structure remains that of a 2 way subtree
			![[Pasted image 20251114191833.png|100]]

- Rules
	- Every node is colored (red/black)
	- root is black
	- nulls are black (leaves)
	- New node is red
	- Red node will have both black children
	- Every path from root to leaf has equal no black node
- Red black tree height would be log N + k.

# Left Leaning Red Black Tree

- A right node is always black
- left is red and left grand child is red then left rotate
- both red then flip colour

![[Pasted image 20251114193027.png|300]]

![[Pasted image 20251114193408.png|300]]

1. Left rotate
![[Pasted image 20251114193704.png|300]]

![[Pasted image 20251114194146.png|400]]
![[Pasted image 20251114194501.png|300]]
- Runtime complexity is O(1).

2. Right rotate
![[Pasted image 20251114194741.png|300]]

![[Pasted image 20251114194832.png|300]]

![[Pasted image 20251114195314.png|300]]
- Runtime complexity is O(1).

3. Flip Color
![[Pasted image 20251114195500.png|300]]
- Runtime complexity is O(1).

- At max these operations will run log n times.
- At max 3 operations will happen at each node.
- So net Time complexity is O(3log n).
- Although it's kind of impossible that each node uses 3 operations.
![[Pasted image 20251114195931.png|200]]
![[Pasted image 20251114200112.png|200]]

##### Calculating height of tree

![[Pasted image 20251114200517.png]]

![[Pasted image 20251114201001.png|350]]

![[Pasted image 20251114201122.png|350]]

![[Pasted image 20251114201325.png|350]]

![[Pasted image 20251114201447.png|300]]

![[Pasted image 20251114202101.png|300]]

![[Pasted image 20251114202308.png|400]]
![[Pasted image 20251114202247.png|400]]

![[Pasted image 20251114202457.png|400]]



![[Pasted image 20251114205601.png|400]]
![[Pasted image 20251114205903.png|400]]

### Summary 
![[Pasted image 20251121201220.png]]

![[Pasted image 20251121201342.png]]


# Implement AVL
- AVL tree memory footprint is more than that of Red-Black Tree
- It ensures that height gap between left subtree and right subtree should be +1, -1 or 0.
![[Pasted image 20251121202942.png|400]]


Case 1: +2(Type 1) right rotate
Case 2: -2(Type 1)  left rotate
Case 3: +2 (Type 2) first left rotate then right rotate
Case 4: -2 (Type 2) first rotate right then left rotate
![[Pasted image 20251121203438.png|400]]
![[Pasted image 20251121203552.png|200]]



- Red black tree is not very strict as height gap can be 1 or 2 or 3 as well.
- Memory footprint of Red black is better.
- Number of rotations are more in AVL as it's a strict tree.
- Search cost is lesser in AVL due to the strictness.
- Insertion is littler slower in AVL to maintain it's strict gap of 1.

In Database in most cases uses Red Black tree as memory footprint and insertion is better. Searching a bit more like 2 or 3 level is not that much hit to time complexity.
![[Pasted image 20251121204318.png]]

![[Pasted image 20251121212659.png]]

![[Pasted image 20251121212438.png]]

![[Pasted image 20251121212433.png]]
![[Pasted image 20251121211923.png]]

# Tools necessary for development

Wireshark : listens all ports and prints the log .
- Let's see how TCP works
![[Pasted image 20251121214433.png]]
![[Pasted image 20251121214439.png]]

- 3 way handshake is needed in TCP to know size of buffer as well.

![[Pasted image 20251121215440.png]]

- Extra empty bits are added so that in future if they required new flags to server some purpose then they don't need to change the structure around the world.
![[Pasted image 20251121215451.png]]


- Urgent bit is need if you do TELNET or user cancels the further processing with Ctrl + C or kills the process.
- Push flag to directly send to application layer.


![[Pasted image 20251121220529.png]]

TTL determines how many max hops it can do to reach the destination in case it takes more than TTL then it will never reach.



![[Pasted image 20251122201128.png]]

ICMP and IGMP can ideally be said to be applied on transport layer but it is not a transport layer protocol as it does not add port number.
- They are like network protocols.
![[Pasted image 20251122202352.png]]

![[Pasted image 20251122203112.png]]
Trace Route
Ping
TCP / UDP
TCP Header



- Buffer is something which is faster than hard disk but it's not ram , it is using hard disk only.

![[Pasted image 20251122204127.png]]


![[Pasted image 20251122204237.png]]

In UNIX system if more than 1024 files are open then it crashes hence we should close the buffer after our work is done.

![[Pasted image 20251122204549.png|400]]


New way to do the same thing in shorter syntax

![[Pasted image 20251122204703.png|400]]

If i have to do same kind of sorting in a file hosted on AWS S3 bucket, let's say it has 10 GB of data to sort.
So the constraint is ram is less than size of ram.

Now creating list of string will exhaust the resources.

![[Pasted image 20251122205545.png]]

# External Sort

![[Pasted image 20251122210037.png|400]]
- Create chunks of data then sort them individually and then merge them.

- To merge take pointer to each chunk and sort them then take from sorted chunks take first line from the sorted chunks  and move to next line in that chunk then again sort all chunks pointers and repeat the process.
- This is similar to merging sorted array
- Instead of sorting again and again make use of minHeap.
- I need to know file size and from runtime get the free ram size.
	- In case ram size is greater than file size then we can proceed with normal sorting.
	- In case ram size is lesser than file size then use external sort.

- If number of files is greater than 1024 then throw exception as it can't be done even by External sort.

![[Pasted image 20251122210800.png]]


![[Pasted image 20251122211537.png]]

![[Pasted image 20251122211956.png]]
![[Pasted image 20251122212040.png]]

Or create a function like this to call in above code
![[Pasted image 20251122212127.png]]

![[Pasted image 20251122212725.png|400]]

![[Pasted image 20251122212703.png|400]]

![[Pasted image 20251122214259.png]]

>[Resource](https://piazza.com/class/mcpnle047cd61c/post/28)

# B+ Tree used in databases

![[Pasted image 20251122220741.png|300]]


# HashSet

![[Pasted image 20251128201346.png]]
K can become constant if implemented with very good hashing technique and hashing array has less collisions and array size dynamically changes as needed



Other techniques:
- Separate Chaining
- Open Addressing
	- linear probing
		![[Pasted image 20251128202649.png]]
		- In linear probing in case the hashcode we got is already occupied then we are adding k (here 1) to the remainder and again repeating the process until it reaches a spot it is not occupied.
		- Even in case of deletion operations it checks if memory location is marked as deleted then we again has to do linear probing.
		- Benefits:
			- easy to implement
			- cache friendly as it keeps neighbor data in cache
		- Cons:
			- Due to lot of Clustering it is not very optimized.
	- quadratic probing
		![[Pasted image 20251128204044.png]]
		- In this the k used is i square which reduces the clustering.
		- Benefits:
			- okay clustering
			- okay caching
		- Since the logical architecture is same as that of linear probing so there is not much improvement.
	- double addressing
		![[Pasted image 20251128204409.png]]
		- In this k is taken as 1 + key and modulo is done with a prime a number.


![[Pasted image 20251128205027.png|300]]
![[Pasted image 20251128205050.png|300]]

![[Pasted image 20251128205259.png|300]]

![[Pasted image 20251128205512.png|300]]
![[Pasted image 20251128205645.png|400]]
![[Pasted image 20251128205908.png|400]]
![[Pasted image 20251128210234.png|400]]

![[Pasted image 20251128210352.png]]

![[Pasted image 20251128210735.png]]

![[Pasted image 20251128210458.png]]
![[Pasted image 20251128210807.png]]
![[Pasted image 20251128210831.png]]
![[Pasted image 20251128210844.png]]
![[Pasted image 20251128211131.png]]

![[Pasted image 20251128211148.png]]


Before generic developer used Object class as every object drives from object
But this involve some more implementations for different data types but type casting error challenges happens and it's not robust and program can fail at runtime which java doesn't want. 
![[Pasted image 20251128214658.png]]

To solve this issue Generics came
- Any unoccupied keyword can be used.
- But Java developers made some naming convention although you can use any name but it makes cross development easy.
	![[Pasted image 20251128215112.png]]

- multiple interfaces are allowed
	![[Pasted image 20251128215257.png]]
-  in case using class has to be the first otherwise search could become class
- So either all has to be interface or one of them can be a class but it has to be a first one.
![[Pasted image 20251128221951.png]]

# Wild Card Generic

![[Pasted image 20251205200912.png|400]]


![[Pasted image 20251205200954.png|300]]

Even though Car is parent of Maruti but this doesn't implies that List of car is parent of list of Maruti.

- To solve this issue
	- Use Wild card generic
		![[Pasted image 20251205201226.png|300]]
		- Now list of car and list of Maruti both can be child of list.
		- Now we can either use extend or super
		![[Pasted image 20251205201410.png|400]]
		- You can pass any super class as well like Object.
		![[Pasted image 20251205201658.png|300]]
		- In super case we can add List of Integer, Number and object as well.
		- In extends case we cannot extend object.



# History of software development

### Stages of development in general
- Requirement is needed to build a product.
- Some architects will build HLD
- Then that HLD will be transformed LLD.
- Then developers will start building the product.
- Then testing of product will  happen.
- Finally the product will be deployed.

Now at every stage their is chance of failure.
- So faster we catch the issue in early stage that's best for the fast development.

# Software Development Life Cycle (SDLC)

![[Pasted image 20251205202431.png|300]]

### Waterfall Model
- This process takes 5-6 months.
- It was used 25 years old.
- This model's foundation is requirement document. It should be as perfect as possible otherwise if any issue is encountered later then it will be huge overhead to recover that defect.
- 
- There is no feedback mechanism which ensures that the product is aligned with the client's needs.
![[Pasted image 20251205202515.png|200]]

### V-Shaped Model
- This model added validation at each stage of waterfall model

![[Pasted image 20251205203128.png]]

### Prototype Model
- Then arrived prototype model which made things easier.
- So teams first build prototype then take feedbacks based on prototype before building the actual product.

![[Pasted image 20251205203240.png]]


# Spiral Model
- It is a theoretical model and not used much.
![[Pasted image 20251205203243.png|300]]


### Agile Model
- We will not build whole product.
- Instead we will build features in a sprint within 2-3 weeks
- So iteratively we will pick 2-3 features and build them in their sprint.
- Now every feature can be validated with customer and feedback can be gathered from the client and in case that feature is flagged wrong then only 2-3 weeks effort is wasted.
- In case of some defects in feature then they will be given 
- If a team is only able to complete 2 sprints out of 3 then manager can analyze if team is under staffed. Manager can also predict that how many months will be needed to build the product based on current staff.
- So forecasting became much easier with this model.
- Most companies keep 4 weeks sprint although it can vary between 2 to 4 week.
- Their is also 2-3 days which team can decide to fix bugs where they segregate if those bugs fixes really needed and will it affect our feature development.
- Tools like selenium are used to automate the testing, so scripts to test are written parallelly during development otherwise one has to test whole feature in
- Deployment should also be automated.
- For designing also their should be use of automation tools to design for effective use of agile model.
![[Pasted image 20251205203254.png]]


# CICD
- Jenkins is typically used in industry to define pipeline and is used to automate deployment, like if someone pushes code then it will be queued and after some time it will start build in after `sonarQube` has verified the static code based on the rules defined in it. This verification will be done automatically within few minutes.
- Jenkins can also change database , where in Jenkins pipeline their are scripts defined to do different stages of work of deployment automatically.
- Git is open source technology developed by GitHub. Bitbucket is also like GitHub and is a paid software which can run all commands of Git but provides better features for setting up pipelines.
- Jenkins can also run all commands on server as well with automated scripts to stop the server make changes start server do the verification and deploy build.
![[Pasted image 20251205204943.png]]



# Infrastructure setup tools
- Puppet setup the dependencies, infrastructure using Agent in each device like each system should have JDK 11 , has particular tools in all systems.
![[Pasted image 20251205205908.png|400]]


- It provides even more automation to setup the infrastructure.
- No agent is needed it uses SSH to setup infra in all systems.
- It's the latest and new companies are using ansible.
![[Pasted image 20251205210114.png|400]]


- CHEF the old tool to setup infra , hardly used anywhere
![[Pasted image 20251205210300.png|400]]



# Docker

Now what if developers are working on different machines like Windows , MacOS, Linux etc. where they have developed their code in their machine environment. Now challenge is to run that code in all kind of machines. Now we can't control the fact that all systems should be same. So what kind of environment we should deploy our code.
So this is the issue that happens during development. This is where Docker comes into picture.

Docker says that Docker containers should have Node.js version 10 installed , then make a directory and install all below mentioned package using npm run.
![[Pasted image 20251205211156.png|300]]

- It also signify which port to expose to the outer world like it could be used by server to listen
![[Pasted image 20251205211303.png]]

# Practical

![[Pasted image 20251205211608.png|400]]
![[Pasted image 20251205211812.png]]
- It takes some time unless cached if used earlier.
- Now Docker Image is created

![[Pasted image 20251205211917.png|400]]
- Here is the docker image with name `myapp`.
- After image is ready that can be moved anywhere on Docker repo as well.

![[Pasted image 20251205212217.png]]
- Now we can run the docker container and check using `ps` command to check running process.


![[Pasted image 20251205212351.png]]
- We can forward the traffic from one port to another port as well.
- To do that first we need to kill the process of running image and make the change
![[Pasted image 20251205212453.png]]

![[Pasted image 20251205212650.png]]
- Launching first server can take little time as image build might not be completed.
- After that launching more servers will be quick.

- We can check that using `Curl` command
![[Pasted image 20251205212813.png]]

- Docker basically do Container Orchestration.
- It can be deployed anywhere anytime quickly.
- Docker used to earn money by merchandise and training employees of a company to use Docker.

# Kubernetes
- It requires a container orchestrator like docker or rocket. Although rocket is not used now days.
- Usually building docker container developer uses centos, light weight Linux OS like alpine versions which just have basic functionality and not unnecessary Linux commands even commands like ping is not included. 
- Suppose different developers are building different features of a product now testers have developed scripts to test that where OS commands are also run which involves creating deleting files , now what if due to bug a tester sends a code which deletes root itself , now this will be devastating. So to prevent that every developer tester can easily run the feature in a copy of the product running in Docker container environment and run it their so even if that code damage that copy, the product remains safe. So the new running environment is a different machine itself withing the system in which original product files are there.
	![[Pasted image 20251206202101.png|300]]
- If in container application and database both is installed then data will be stored in `/etc/data` of that container.
- Now came another issue like when a product is being developed inside a container and that container got killed or destroyed then new container with same configuration as the killed one is launched from the initial state. This means even the local database were destroyed within the killed container and a new local database is created from initial state in the new container. Now this is the issue that data is lost so to prevent it is where databases like MongoDB comes in. Database will be mounted to the container.
	![[Pasted image 20251206202605.png|200]]
	- So using Volume (-v) mounting command we can directly map local database directory in docker container at `/etc/data` to the directory of host OS such as `C:/data`.
	- So if a container is deleted then in new container we just need to map it's local database directory to our host OS directory containing the database and the data persists.
	- Otherwise you can use cloud database instead of doing this Host OS directory mapping. But Cloud database is slower and hence during development often databases are mapped to host OS and kept local to provide faster reads and writes.

- Now another issue is lets say container has some of it's own databases and that databases need to be accessed is being used by all the containers. Then for synchronization their will be use of locks and that means database will be available to only one container application at a time. Now if a new user is created from one container than that might not be updated for other containers.
- So if one container wants to talk to another container then to do that we have to create a bridge or  a network to that.
	![[Pasted image 20251206204409.png|300]]
	- It will be local hence it will be fast.
	- Even cost will be less.
	- Private IP's and host name will be stored in that Bridge.
# Proxy vs Reverse Proxy

How Proxy is different from VPN
- In VPN when data packet arrives at the VPN then it adds another TCP and IP header in outer layer of packet and sends it to receiver where that packet is restored.
- Proxy is to hide the client as proxy server has mapping of where to deliver sender's request , now even google who monitors all requests, will think it is send by the proxy server not the original client that actually sends it.
- In server deployment we need reverse proxy as no one wants to expose all their machines over the internet. Another reason is to scale up or scale down machines their should be a API Gateway for the requests which will be routed to servers.
- Every load balancer is a reverse proxy.
![[Pasted image 20251206205409.png]]
-  Another possibility is that all request arrives at Load Balancer which routes it to some Application Gateway which will further route to the server.
	![[Pasted image 20251206205939.png|400]]

- Or we can just use Load Balancer directly sending traffic to server.
	![[Pasted image 20251206210112.png|450]]

Netflix created Eureka Server which was a discovery service and every application of Netflix is registered on that discovery service which has all the information of what servers are available , what are killed which can accommodate the request etc. So in case if you want that your application is not down even for 2 second then you can use discovery service which will provide the Load Balancer , API gateway with the necessary info about the servers. We also need to create a cluster of Discovery Service as if it got down then whole system will not work well. What it saves some time while processing the requests.


![[Pasted image 20251206211526.png]]

- Different algorithms to distribute traffic by load balancer in Nginx.
	- round_robin
	- least_connection
	- ip_hash

![[Pasted image 20251206212108.png]]


![[Pasted image 20251206212243.png]]

![[Pasted image 20251206212221.png]]


![[Pasted image 20251206213725.png]]

To run commands on container ssh from outside of container in host OS.
![[Pasted image 20251206213853.png]]
![[Pasted image 20251206213952.png]]

So we can read files from outside but to edit files you have to go inside of container
![[Pasted image 20251206214038.png]]

docker compose : It's docker's own orchestration tool which handle all containers and also connects all local containers running in local machine but it cannot connect docker containers on same network but on different machines.
Kubernetes : it is also used to connect all the docker containers but it can connect it over the network where docker containers are running on different machines over the network.
![[Pasted image 20251206214235.png]]


---
# Streams in Java
![[Pasted image 20251220201429.png]]

- Earlier java offered object oriented programming but later in JAVA 8 functional programming was also introduced which included stream as well.
- Stream has following characteristics
	- Copy of original input.
		- A stream works on a **separate view of data**, not directly on the original collection. So, the original list or set **remains unchanged** even after stream operations.
	- input is immutable.
		- Streams **cannot modify the source data**. They only read data and produce a **new result**, ensuring safety and no side effects.
	- on demand (Lazy execution)
		- Stream operations execute **only when a terminal operation is called**.  Until then, no processing happens, which saves time and resources.
	- It has multiple intermediate function and terminal function.
		- **Intermediate functions** (`filter`, `map`, `sorted`) build the processing pipeline.
		- **Terminal functions** (`collect`, `forEach`, `count`) trigger execution and produce the final result.
	- It's memory footprint is less.
		- Streams process data **one element at a time**, instead of storing intermediate results. This makes them **memory-efficient**, especially for large datasets.
	- It is closed at the end.
		- After a terminal operation, the stream is **automatically closed**. Once closed, it **cannot be reused**.
	- Supports chaining
		- Multiple stream operations can be **chained together in a single pipeline**. Each operation’s output becomes the input of the next, making code **clean and readable**.

![[Pasted image 20251220201940.png]]


```java
Stream<Integer> s = input.stream();
Stream<Integer> s1 = s.filter(n -> n % 2 == 0);
Stream<Integer> s2 = s1.map(n -> n * 2);
Stream<Integer> s3 = s2.sorted();
Stream<Integer> s4 = s3.distinct();
List<Integer> res = s4.collect(Collectors.toList());
```

Above steps can be done in one go as well
![[Pasted image 20251220202210.png|300]]


# Singleton

![[Pasted image 20251220203215.png|500]]
- Node JS is supporting multiple processes with event driven architecture.

![[Pasted image 20251220203303.png|500]]
- Java supports multi threading for multiple processes.
- Earlier Java has to create multiple objects of controller which means it has do a lot of work in just building the objects and also fill object pool for each request of the user.
- Later Java introduced to have a single object which is shared by multiple users and each user can execute their piece of code from the shared code.

![[Pasted image 20251220204203.png|320]]

##### How this shared class is provided
![[Pasted image 20251220204407.png|400]]
- Now here we are doing eager loading which means resources are always allocated even though this class is never used by any service. 
- To prevent it , lazy loading is introduced as follows

![[Pasted image 20251220204716.png|300]]
- Now the issue here is multithreading like if two threads calls `getInstance`() method at the same time then both will make different objects which is solved by synchronization as follows.

![[Pasted image 20251220204817.png|400]]
- Now this synchronization makes things slower forever like giving entry to one request at a time but we can improvise by making it synchronous only when requests were accumulated during the first time instance was null but after the first such batch of requests are processed later requests which don't find instance to be null will be executed at the same time

![[Pasted image 20251220205531.png|400]]


- Now still there is very slight possibility that multiple object still forms due to transition of object creation between ram and secondary memory, due to this microseconds of delay there can be process which reads the previous null state from the secondary memory. So to prevent this, we can use volatile so that threads pick objects directly from the ram. Now `Java runtime ka baap bhi iss class ke do objects nhi bnaa sakta`.


Normal Class
![[Pasted image 20251226201703.png|400]]

![[Pasted image 20251226203514.png|300]]

![[Pasted image 20251226204600.png]]

![[Pasted image 20251226203702.png|300]]


# Algorithm to find best way to add upto given number with minimum set of values. Basically Coin Change with infinite coins.

![[Pasted image 20251220212145.png]]


![[Pasted image 20251220212625.png|400]]

To make 7 with 3 elements the runtime complexity is 3⁷.


NP Complete

```
P: Easy to Solve in poly(x) and Check in poly(x) NP: Hard to Solve (not in poly(x)) and but Easy to check in poly(x) Eg. Sudoku It is theorized that if you can solve any one of NP Hard problem in polynomial time than it will imply that any other NP Hard problem can be translated into it and solved in polynomial time
```

![[Pasted image 20251226213004.png]]

![[Pasted image 20251226213008.png]]

![[Pasted image 20251226213015.png|300]]

![[Pasted image 20251226214459.png|300]]


[[Make Target string from dictionary]]


![[Pasted image 20260109202017.png]]



# Balanced Parenthesis
![[Pasted image 20260123202600.png|500]]


![[Pasted image 20260123202629.png|500]]

![[Pasted image 20260123203031.png|300]]

![[Pasted image 20260123203247.png|300]]

![[Pasted image 20260123204213.png|300]]

![[Pasted image 20260123204713.png]]

# Possible BST
![[Pasted image 20260123205304.png|400]]

![[Pasted image 20260123205307.png|400]]

Another way to solve these questions

### Catalan number
![[Pasted image 20260123205507.png|300]]
![[Pasted image 20260123205602.png|400]]
![[Pasted image 20260123205653.png|300]]

But to implement this we again need the loop which would take up the same time complexity as the dp approach if implemented normally.
![[Pasted image 20260123210018.png|300]]

![[Pasted image 20260123210220.png|300]]
We can convert this formula to this format to improve the time complexity of our code
![[Pasted image 20260123210336.png|300]]
Now we need just a loop to do the same task
![[Pasted image 20260123210518.png|300]]


![[Pasted image 20260123211026.png|300]]

Number of ways to make triangles inside n side polygon
![[Pasted image 20260123211854.png|400]]
![[Pasted image 20260123211931.png|500]]



### Find number of ways to reach e from s with crossing the diagonal

![[Pasted image 20260123212228.png]]

- In a way it is restricting movement of R , which is no. of R taken cannot be more than D.


### Another similar question to find number of ways to make mountains
![[Pasted image 20260123212544.png]]


# Dyck Path


Following are Catalan formula problems
[GFG](https://www.geeksforgeeks.org/dsa/catalan-coding-problems/)

# Asynchronous Communication

- Queue, Streams
- Similar to database if we want asynchronous communication across services then we can use a queue or stream in the middle which will allow us to achieve eventual consistency.
- Cache distributed
![[Pasted image 20260124203357.png]]

No SQL uses sharding then SQL uses partition tolerance

No SQL typically uses Cassandra and Mongo DB and how they are different.

- Cassandra is better for heavy write operation because it only need to update a column as it is a columnar database whereas Mongo DB is a document data base.
- Mongo DB is ok for both read and write.
- Cassandra can make immediate availability as well but yeah it does have to comprise on availability.
- So if i want more consistency then i will go with Cassandra otherwise if availability is my priority then go with MongoDB.

![[Pasted image 20260124203932.png|400]]


![[Pasted image 20260124205521.png|400]]
- Active MQ
- Rabbit MQ (used now days)
	- It's very fast , faster then any queue.
	- Following are it's attributes.
	![[Pasted image 20260124205733.png|300]]
- Kafka
	- It is a stream which might look like a queue.
	- Partition Consumer, Partition Key/io, Consumer group, Broker, Kafka cluster, zoo keeper, KRaft, Topic
	- Broker -> Topic ->Partitions
	- Replication factor in topics is typically 3.
		- Due to this Kafka is fault tolerant.
	![[Pasted image 20260124210455.png|300]]
	![[Pasted image 20260124212548.png]]
	- Broker ensures that their is at least one writer is available with help of configuration manager.
	- In Kafka one problem is during partition the actual order might not be maintained.
		![[Pasted image 20260124210941.png|250]]
	- If multiple Consumer group are reading from same topic
	- Kafka achieved parallelism through partition , partition key will remain sticky.
		- Partition key is often calculated by hashcode % mod.
		![[Pasted image 20260124211509.png|400]]
	![[Pasted image 20260124211831.png|400]]
	- Rebalancing - if one consumer goes down then another consumer will get access to the partition it was using. Kafka does it internally automatically.
		- Now how Kafka recognize which partition data is which , to achieve that it maintains an offset number for each partition.
		- Their is also retention period which Kafka maintains to free partition.
	- If partition gets down then if their is a partition copy then it will launch new partition from that.
	- Key serializer or de-serializer, value serializer or de-serializer
		- Auto acknowledgements, message sent automatically.
	- Inside a consumer group each consumer will get distinct data to achieve parallel processing while multiple consumer group get same data.
	- Transition Log Manager

![[Pasted image 20260127195933.png]]


In Kafka message header functions like header ID.


# Event Driven Architecture
- Saves the system from complete failure due to loose coupling of modules.
![[Pasted image 20260127200912.png|300]]

- In Event driven we can independently scale each micro service instead of having a single machine to process everything.
- Service based testing can be done.
- Distributed unique trace id should be implemented to trace in which service the issue has occurred. To search the trace one can use log stash , elastic search (no sql database which is very good to search for string) , grafana , kibana etc.
- Unlike monolithic where for introducing every small feature you have to create a new build of whole application , here we can create build of service independent of each other. Like Linux uses monolithic  architecture so any new feature introduction leads to a whole new build release.

# API Gateway

![[Pasted image 20260130201534.png|300]]
![[Pasted image 20260130202215.png|300]]
- DDOS attach is difficult to handle so to prevent that we make a payload from requests which can be used as a key.

![[Pasted image 20260130202828.png|300]]
LB - load balancer,  US - User micro Service
![[Pasted image 20260130203120.png|200]]

- We should not expose which is not required even the ping command which are very basic.
![[Pasted image 20260130203213.png|300]]



Fast but not distributed

![[Pasted image 20260130203555.png|300]]

- cache back - data can be stale in cache
- cache through - read operations are always going to cache but this can also result in overhead if we want to rollback the updates.

![[Pasted image 20260130203709.png|300]]
- Data will remain stale for few minutes let's stay 5 minutes after that updates will be reflected

# Discovery Service
- Netflix is one of the pioneer in building it
- Eureka server

![[Pasted image 20260130204407.png|300]]
![[Pasted image 20260130204540.png|300]]
Instead of Discovery service we can use nested Load Balancer.


![[Pasted image 20260130204953.png|300]]

![[Pasted image 20260130205111.png|200]]
- Which methods are idempotent. why it matters
- There are two scenarios when i get network not found error from my API call.

- For Client - Server call it is HTTP method.


# Circuit Breaker

![[Pasted image 20260131201646.png|300]]
- How will you implement circuit breaker in scenario you can't use any 3rd party api , what data structure you will use?
hashmap
![[Pasted image 20260131202022.png|400]]
- sliding window , atomic integer
- bucket4j 
![[Pasted image 20260131202522.png|300]]

![[Pasted image 20260131202848.png|300]]
- compensating transaction

# JIRA

![[Pasted image 20260206203208.png]]

[[Maven]]
[[Gradle]]
[[ORM]]
[[REST API]]

![[Pasted image 20260224195103.png]]

![[Pasted image 20260224194751.png]]

Cloud Database


