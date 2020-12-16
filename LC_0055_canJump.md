#### 55. 跳跃游戏
给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

#### 示例 1:

```
输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
```

#### 解释
```
dp[i]表示第i个元素最远可以跳到的地方
如果i - dp[i - 1] > 0说明不能跳到i处，直接结束
dp[i]等于当前位置+当前位置元素值和dp[i - 1]的最大值
时间复杂度:O(N)     空间复杂度:O(N)
```

```Java
class Solution {
    public boolean canJump(int[] nums) {
        if (nums.length == 0) return true; 
        int[] dp = new int[nums.length];
        if (nums[0] == 0 && nums.length == 1) return true;
        if (nums[0] == 0) return false;
        dp[0] = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (i - dp[i - 1] > 0) return false;
            dp[i] = Math.max(i + nums[i], dp[i-1]);
        }
        return true;
    }
}
```

#### 解释

```
K表示当前可以跳到的最远处，如果i > k则说明不能跳到i处，直接返回
时间复杂度:O(1)     空间复杂度:O(1)
```

```Java
class Solution {
    public boolean canJump(int[] nums) {
        int k = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > k) return false;
            k = Math.max(k, nums[i] + i);
        }
        return true;
    }
}
```