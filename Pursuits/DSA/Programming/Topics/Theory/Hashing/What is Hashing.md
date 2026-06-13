-  Pre-storing and Fetching.
- Initially we will create another array which we will call hash array, all the values will be assigned 0. We call this hash array or frequency array.
- Now we will do pre calculation.
  ![[Pasted image 20240704110638.png|450]]
> __IMPORTANT: 
> The maximum size of array that you can declare *inside main* :
> 	  For integers => int arr\[10⁶]
> 	  For bool       => bool arr\[10⁷]
> The maximum size of array that you can declare *Globally* :
>       For integers => int arr\[10⁷]
> 	  For bool       => bool arr\[10⁸]
> If we declare of bigger size then it will result in segfault.__