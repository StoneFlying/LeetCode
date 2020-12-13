#### 20. 有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

#### 示例 1:

```
    输入: "()"
    输出: true
```

#### 解释

```
时间复杂度:O(N)     空间复杂度:O(L)
```

```Java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack();
        for (int i = 0; i < s.length(); i++) {
            Character c = s.charAt(i);
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else if (c == ')') {
                if (stack.size() < 1) return false;
                if (stack.pop() != '(')return false;
            } else if (c == '}') {
                if (stack.size() < 1) return false;
                if (stack.pop() != '{')return false;
            } else if (c == ']') {
                if (stack.size() < 1) return false;
                if (stack.pop() != '[')return false;
            }
        }
        if (stack.size() != 0) return false;
        return true;
    }
}
```