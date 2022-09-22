# 53. Maximum Subarray

[link](https://leetcode.com/problems/maximum-subarray/)


```
preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

indexMap<num, index>
nodeMap<num, TreeNode>

// step through preorder array
index -> 0
nums[i] = 3 is always root

	3

index -> 1, nums[i] = 9
indexMap.get(9) = 0
num[0 + 1] = 3, meaning 9 must go on the left of 3


index -> 2, nums[i] = 20
hashmap.get(20) = 3
nums[3-1] = 15, meaning 20 must go on the right of 15
nums[3+1] = 7, meaning 20 must go on the left of 7

index -> 3, nums[i] = 15
hashmap.get(15) = 2
nums[2-1] = 3, meaning 15 must go on the right of 3
nums[2+1] = 20, meaning 15 must go on the left of 20

index -> 7, nums[i] = 7
hashmap.get(7) = 4
nums[4-1] = 20, meaning 7 must go on the right of 20

```


```
public int maxSubArray(int[] nums) {
        int sum = Integer.MIN_VALUE;
        int bestIncludingPrevious = 0;
        
        for( int i = 0 ; i < nums.length ; i++) {
            bestIncludingPrevious = Math.max(bestIncludingPrevious + nums[i], nums[i]);
            sum = Math.max(bestIncludingPrevious, sum);
        } 
        
        return sum;
    }
```