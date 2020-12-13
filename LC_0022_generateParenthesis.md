#### 22. 括号生成
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

 

#### 示例：

```
输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]
```


#### 解释

```
深度优先搜索，记录左括号和右括号已使用个数，右括号使用个数大于左括号使用个数时不满足条件，直接返回
当右括号或者左括号大于n时，不满足条件直接返回
```

```Java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        if (n == 0) return list;
        dfs("", 0, 0, list, n);
        return list;
    }

    public void dfs(String str, int left, int right, List<String> list, int n) {
        if (left > n || right > n || left < right) {
            return;
        }

        if (left == n && right == n) {
            list.add(str);
            return;
        }

        dfs(str + '(', left + 1, right, list, n);
        dfs(str + ')', left, right + 1, list, n);
    }
}
```