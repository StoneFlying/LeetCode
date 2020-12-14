#### 31. 下一个排列
实现获取 下一个排列 的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须 原地 修改，只允许使用额外常数空间。

 

#### 示例 1：

```
    输入：nums = [1,2,3]
    输出：[1,3,2]
```

#### 解释

```
三步：
例如:1, 2, 5, 4, 1
1.从尾部开始寻找逆序排序， A[i] > A[j]   最后i指到2   j指到5
2.在A[i]到A[end]间寻找最小的大于A[i]的那个数，并将两个值交互,这里最小的大于2的是4  交换后为:1, 4, 5, 2, 1;
3.将A[j: end]间的数进行反转    反转后为1, 4, 1, 2, 5
```

```Java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        int j = nums.length - 1;
        int k = nums.length - 1;

        // 从尾部开始寻找逆序排列 A[i] > A[j]
        while (i >= 0 && nums[i] >= nums[j]) {
            i--;
            j--;
        }

        // 将A[i] 与A[j: end]之间刚好大于A[i]的数交换
        if (i >= 0) {
            while (nums[k] <= nums[i]) {
                k--;
            }

            int temp = nums[i];
            nums[i] = nums[k];
            nums[k] = temp;
        }

        // 反转A[j: end]
        for (int l1 = j, l2 = nums.length - 1; l1 <= l2; l1++, l2--) {
            int temp = nums[l1];
            nums[l1] = nums[l2];
            nums[l2] = temp;
        }
    }
}
```