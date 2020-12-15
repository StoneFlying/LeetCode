#### 46. 全排列
给定一个 没有重复 数字的序列，返回其所有可能的全排列。

#### 示例:

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### 解释

```
回溯法，由于数组元素不重复，每添加一个元素时需要判断该元素是否重复存在，通过一个布尔数组标识nums中相应元素是否已经添加过即可
```

```Java
class Solution {
    List<List<Integer>> list = new LinkedList<>();
    List<Integer> temp = new LinkedList<>();
    boolean[] vis;

    public List<List<Integer>> permute(int[] nums) {
        if (nums.length == 0)
            return list;
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
            if (vis[i] == true) continue;
            vis[i] = true;
            temp.add(nums[i]);
            backtrack(nums);
            temp.remove(temp.size() - 1);
            vis[i] = false;
        }
    }
}
```