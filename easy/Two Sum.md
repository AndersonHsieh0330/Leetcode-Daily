# 1. Two Sum

[link](https://leetcode.com/problems/two-sum/)

```
public int[] twoSum(int[] nums, int target) {
        // key is the wanted number
        // value is the index
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0 ; i < nums.length ; i++){
            if(map.containsKey(nums[i])){
                return new int[]{map.get(nums[i]), i};
            }else {
                map.put(target - nums[i], i);
            }
        }
        
        return null;
    }
```