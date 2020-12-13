#### 14. 最长公共前缀
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

#### 示例 1:

```
    入: ["flower","flow","flight"]
    输出: "fl"
```
#### 示例 2:

```
    输入: ["dog","racecar","car"]
    输出: ""
    解释: 输入不存在公共前缀。
```

#### 解释
```
依次遍历每个字符串，通过遍历的字符串更新最长公共前缀
时间复杂度:O(mn)    空间复杂度:O(1)
```

```Java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0 || strs[0].equals("")) return "";
        int index = 0;
        String prev = strs[0];
        int flag = 0;
        for (int i = 1; i < strs.length; i++) {
            for (int j = 0; j < Math.min(strs[i].length(), prev.length()); j++) {
                if (strs[i].charAt(j) != prev.charAt(j)) {
                    flag = 1;
                    prev = prev.substring(0, j);
                    break;
                }
            }
            if (flag ==0) prev = strs[i].length() > prev.length() ? prev : strs[i];
            if (prev == "") return "";
        }
        return prev;
    }
}
```