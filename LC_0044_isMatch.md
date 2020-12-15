#### 44. 通配符匹配
给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。

'?' 可以匹配任何单个字符。
'*' 可以匹配任意字符串（包括空字符串）。
两个字符串完全匹配才算匹配成功。

说明:

s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。
#### 示例 1:

```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串
```

```
动态规划，dp[i][j]表示p的前i个字符是否和s的前j个字符匹配
状态转移方程:
    当p[i] == p[i - 1] || p[i - 1] == '?'时 dp[i][j] = dp[i-1][j-1]
    当p[i] == '*'时 dp[i][j] = dp[i][j-1](表示*号匹配当前位置字符) || dp[i-1][j](表示*号未匹配任何字符)
```

```Java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[p.length() + 1][s.length() + 1];
        dp[0][0] = true;
        for (int i = 1; i <= p.length(); i++) {
            if (p.charAt(i - 1) != '*') {
                break;
            } 
            dp[i][0] = true;
        }

        for (int i = 1; i <= p.length(); i++) {
            for (int j = 1; j <= s.length(); j++) {
                if (p.charAt(i - 1) == s.charAt(j - 1) || p.charAt(i - 1) == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p.charAt(i - 1) == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                }
            }
        }

        return dp[p.length()][s.length()];
    }
}

```