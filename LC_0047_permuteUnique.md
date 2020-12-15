#### 47. 全排列 II
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。

 

#### 示例 1：

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

#### 解释

```
回溯法，和46题差不多，在剪枝时条件更改为:
if (vis[i] == true || i > 0 && nums[i] == nums[i - 1] && vis[i - 1] == false) continue;
nums[i] == nums[i - 1] && vis[i - 1]是为了跳过相同元素重复添加
```

```Java
class Solution {
    List<List<Integer>> list = new LinkedList<>();
    List<Integer> temp = new LinkedList<>();
    boolean[] vis;

    public List<List<Integer>> permuteUnique(int[] nums) {
        if (nums.length == 0)
            return list;
        Arrays.sort(nums);
        vis = new boolean[nums.length];
        backtrack(nums);
        return list;
    }

    public void backtrack(int[] nums) {
        if (temp.size() == nums.length) {
            list.add(new LinkedList<>(temp));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (vis[i] == true || i > 0 && nums[i] == nums[i - 1] && vis[i - 1] == false) continue;
            vis[i] = true;
            temp.add(nums[i]);
            backtrack(nums);
            temp.remove(temp.size() - 1);
            vis[i] = false;
        }
    }
}
```