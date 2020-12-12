#### 1.两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两 个整数，并返回他们的数组下标。  

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。  

 

#### 示例:

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```


#### 解释

```
迭代数组，检测target-nums[i]是否在HashMap中，如果在直接返回{target - nums[i], i}
否则将nums[i]及其下标放入HashMap中  
时间复杂度:O(N)   空间复杂度:O(N)
```

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target - nums[i]), i};
            } else {
                map.put(nums[i], i);
            }
        }
        return new int[]{-1, -1};
    }
}
```