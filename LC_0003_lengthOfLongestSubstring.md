#### 3. 无重复字符的最长子串
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。


#### 示例 1:

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

#### 解释
滑动窗口，rk记录右指针, 循环变量i记录左指针，每次循环时删除左指针在set集合中对应的值，然后递增右指针直到和集合中对应元素重复或者到达字符串边界


```Java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0) return 0;

        Set<Character> set = new HashSet<Character>();
        int rk = -1;
        int n = s.length();
        int ans = 0;

        for (int i = 0; i < n; i++) {
            if (i != 0) {
                set.remove(s.charAt(i-1));
            }

            while (rk < n - 1 && !set.contains(s.charAt(rk+1))) {
                set.add(s.charAt(rk + 1));
                rk++;
            }

            ans = Math.max(ans, rk - i + 1);
        }
        
        return ans;
    }
}
```