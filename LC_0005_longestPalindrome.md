#### 5. 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

#### 示例 1：
```
    输入: "babad"
    输出: "bab"
    注意: "aba" 也是一个有效答案
```

#### 解释
```
中心扩散法，遍历字符串，从每个字符处向两边扩散寻找最长回文串
```

```Java
class Solution {
    public String longestPalindrome(String s) {
        if (s.length() == 0) return "";
        int end = 0, start = 0;

        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i+1);
            int len = Math.max(len1, len2);
            if (len > end - start + 1) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    public int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            --left;
            ++right;
        }
        return right - left - 1;
    }
}
```
