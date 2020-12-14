#### 41. 缺失的第一个正数
给你一个未排序的整数数组，请你找出其中没有出现的最小的正整数。

 

#### 示例 1:

```
输入: [1,2,0]
输出: 3
```

#### 解释

```
将所有值x置换到数组下标x-1处，然后遍历数组，查看对应数组下标x的值是否为x+1，不是的话返回x+1即可
```

```Java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            if (i + 1 == nums[i]) continue;
            while (nums[i] > 0 && nums[i] <= nums.length && nums[nums[i] - 1] != nums[i]) {
                int temp = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = temp;
            }
        }

        for (int j = 0; j < nums.length; j++) {
            if (nums[j] != j + 1) {
                return j + 1;
            }
        }

        return nums.length + 1;
    }
}
```