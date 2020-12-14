#### 39. 组合总和
给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 
#### 示例 1：

```
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
```
时间复杂度:O(可行解长度之和)    空间复杂度:O(target)
```Java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new LinkedList();
        List<Integer> list = new LinkedList();
        dfs(res, candidates, target, list, 0);
        return res;
    }

    public void dfs(List<List<Integer>> res, int[] candidates, int target, List<Integer> list, int start) {
        if (target < 0) return;
        if (target == 0) {
            res.add(new LinkedList<>(list));
            return;
        }

        for (int i = start; i < candidates.length; i++) {
            list.add(candidates[i]);
            dfs(res, candidates, target - candidates[i], list, i);
            list.remove(list.size()-1);
        }
    }
}
```