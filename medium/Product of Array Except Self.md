# 238. Product of Array Except Self

[link](https://leetcode.com/problems/product-of-array-except-self/)


```
1   2   3   4
[]  []  []  []
    1   1   1
2       2   2
3   3       3
4   4   4    

left = 0;
right = 3;

-> need 2 containers, leftContainer and rightContainer
-> set all entries of container to 1

-> start with left to right
-> i = 0
do nothing

-> i = 1
container[1] = nums(1-1) * container[0]
1            = 1         * 1   

-> i = 2
container[2] = nums(2-1) * container[1]
2            = 2         * 1   

-> i = 3
container[3] = nums(2) * container[2]
6            = 3       * 2   


-> now from right to left
-> i = 3
do nothing

-> i = 2
container[2] = nums(2+1) * container[3]
4            = 4         * 1   

-> i = 1
container[1] = nums(1+1) * container[2]
12           = 3         * 4   

-> i = 1
container[0] = nums(0+1) * container[1]
24           = 2         * 12  


-> multiply each entry in the two container with each other
```



```
public int[] productExceptSelf(int[] nums) {
        int[] leftContainer = new int[nums.length];
        int[] rightContainer = new int[nums.length];
        for(int i = 0; i < nums.length ; i++) {
            leftContainer[i] = 1;
            rightContainer[i] = 1;
        }
        
        for(int i = 1 ; i < nums.length ; i++){
            leftContainer[i] = nums[i-1] * leftContainer[i-1];
        }
        
         for(int i = nums.length - 2 ; i >= 0 ; i--){
            rightContainer[i] = nums[i+1] * rightContainer[i+1];
        }
        
        for(int i = 0; i < nums.length ; i++){
            leftContainer[i] = leftContainer[i] * rightContainer[i];
        }
        
        
        return leftContainer;
    }
    
    
//NOTE: if statements in forloop actually slows it down a lot, this solution actually had 1ms faster than 100% submissions
```