#### 60. 排列序列
给出集合 [1,2,3,...,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

"123"
"132"
"213"
"231"
"312"
"321"
给定 n 和 k，返回第 k 个排列。

 

#### 示例 1：

```
输入：n = 3, k = 3
输出："213"
```

```Java
class Solution {
    int n2 = 0;
    List<Integer> list2 = new LinkedList();
    List<Integer> list = new LinkedList();
    boolean state;
    boolean[] vis = new boolean[10];

    public String getPermutation(int n, int k) {
        backtrack(n, k);
        String str = "";
        for (int i : list2) {
            str += String.valueOf(i);
        }
        return str;
    }

    public void backtrack(int n, int k) {
        if (list.size() == n) {
            n2++;
            if (n2 == k) {
                list2 = new LinkedList(list);
                state = true;
            }
            return;
        }

        for (int i = 1; i <= n && !state; i++) {
            if (vis[i]) {
                continue;
            }
            list.add(i);
            vis[i] = true;
            backtrack(n, k);
            vis[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```