# 217. Contains Duplicate

[link](https://leetcode.com/problems/contains-duplicate/)

```
 public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0 ; i < nums.length ; i++){
            if (map.containsKey(nums[i])){
                return true;
            }
            
            map.put(nums[i], i);
        }
        
        return false;
    }
	
	
public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
            
        for(int i = 0; i < nums.length-1 ; i++) {
            if(nums[i] == nums[i+1]) {
                return true;
            }
        }
        
        return false;
    }
    
    
public boolean containsDuplicate(int[] nums) {
    Set<Integer> hashSet = new HashSet<Integer>();
            
    for(int i = 0; i < nums.length ; i++) {
        hashSet.add(nums[i]);
    }
        
    return hashSet.size() != nums.length;
}
```

