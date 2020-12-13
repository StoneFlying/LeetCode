#### 17. 电话号码的字母组合
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。



#### 示例:

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

#### 解释

```
回溯，每次取电话号码的一位数字，从该数字对应的所有字母中取得一个，然后再从后一数字对应的字母中取得一个，直到得到一个完整的组合后进行回退，遍历剩下的字母排列.
```
时间复杂度:O($3^m$ + $4^n$) 空间复杂度:O(m + n)

```Java
class Solution {
    Map<Character, String> phoneMap = new HashMap<Character, String>() {{
        put('2', "abc");
        put('3', "def");
        put('4', "ghi");
        put('5', "jkl");
        put('6', "mno");
        put('7', "pqrs");
        put('8', "tuv");
        put('9', "wxyz");
    }};
    StringBuilder combinations = new StringBuilder();
    List<String> list = new LinkedList();
    
    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0)
            return list;
        backtrack(digits, 0);
        return list;
    }
    
    public void backtrack(String digits, int index) {
        if (combinations.length() == digits.length()) {
            list.add(combinations.toString());
            return;
        }

        String letters = phoneMap.get(digits.charAt(index));
        int len = letters.length();
        for (int i = 0; i < len; i++) {
            combinations.append(letters.charAt(i));
            backtrack(digits, index + 1);
            combinations.deleteCharAt(index);
        }
    }
}
```