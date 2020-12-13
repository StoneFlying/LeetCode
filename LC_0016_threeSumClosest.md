#### 16. 最接近的三数之和
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

 

#### 示例：

```
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
```

#### 解释

```
和三数之和差不多
时间复杂度:O(n*n)   空间复杂度:O(1)
```

```Java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int left, right, sum;
        Arrays.sort(nums);
        int ans = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < nums.length; i++) {
            left = i + 1;
            right = nums.length - 1;
            while (left < right) {
                sum = nums[i] + nums[left] + nums[right];

                if (Math.abs(sum - target) < Math.abs(ans - target)) {
                    ans = sum;
                }

                if (sum - target == 0) {
                    return target;
                } else if (sum > target) {
                    right--;
                } else {
                    left++;
                }
            }
        }
        return ans;
    }
}

```