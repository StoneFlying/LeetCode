#### 15. 三数之和
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

#### 示例：

```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### 解释

```
固定一个位置，然后用两个指针分别指向该位置后的两端，计算三个位置的值的和，如果大于0，则右指针向左移动，如果小于0，则左指针向右移动！
注意去重：
    如果当前固定位置值和下一位置值相等，则下一位置应直接跳过
    三数和相等时:
        跳过右指针前边相等的值
        跳过左指针后边相等的值
```

```Java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new LinkedList();
        Arrays.sort(nums);

        int left, right, sum;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                return ans;
            }
            if (i != 0 && nums[i] == nums[i - 1]) continue;
            left = i + 1;
            right = nums.length - 1;
            while (left < right) {
                sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    ans.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left+1]) left++;
                    while (left < right && nums[right] == nums[right-1]) right--;
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return ans;
    }
}
```