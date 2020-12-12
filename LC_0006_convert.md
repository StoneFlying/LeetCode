#### Z 字形变换

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
```
    L   C   I   R
    E T O E S I I G
    E   D   H   N
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：

```
string convert(string s, int numRows);
```

#### 示例 1:

```
    输入: s = "LEETCODEISHIRING", numRows = 3
    输出: "LCIRETOESIIGEDHN"
```

#### 解释
```
从左到右访问字符串，把字符放到合适的行中去，在开始行和末尾行时需要转向
```

```Java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) return s;

        boolean goingDown = false;
        List<StringBuilder> list = new LinkedList();
        for (int i = 0; i < Math.min(numRows, s.length()); i++) {
            list.add(new StringBuilder());
        }
        int curRow = 0;

        for (int i = 0; i < s.length(); i++) {
            list.get(curRow).append(s.charAt(i));
            if (curRow == 0 || curRow == numRows - 1) {
                goingDown = !goingDown;
            }
            curRow += goingDown ? 1 : -1;
            
        }

        StringBuilder ret = new StringBuilder();
        for (StringBuilder row : list) ret.append(row);
        return ret.toString();
    }
}
```