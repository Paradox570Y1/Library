# Optimal
T.C. => O(log n)
```cpp
int func(int f,int num){
	    int ans=1;
	    while(f>0){
	        if(f%2==1){
	            ans*=num;f--;
	        }
	        else{
	            num*=num;f/=2;
	        }
	    }
	    return ans;
	}
```