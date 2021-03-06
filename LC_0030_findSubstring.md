#### 30. 串联所有单词的子串
给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。

 

#### 示例 1：

```
    输入：
    s = "barfoothefoobarman",
    words = ["foo","bar"]
    输出：[0,9]
    解释：
    从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
    输出的顺序不重要, [9,0] 也是有效答案。
```


#### 解释1 哈希表

```
两个哈希表，一个存储words， 一个存储截取的字符串，最后判断两个哈希表是否相等
```
时间复杂度:$O(N^2)$

```Java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> ans = new LinkedList();
        if (s.length() == 0 || words.length == 0) return ans;
        Map<String, Integer> count = new HashMap();

        for (int i = 0; i < words.length; i++) {
            count.put(words[i], count.getOrDefault(words[i], 0) + 1);
        }

        int wordSize = words[0].length();
        int allLen = words.length * wordSize;

        for (int i = 0; i < s.length() - allLen + 1; i++) {
            Map<String, Integer> temp = new HashMap();
            for (int j = i; j < i + allLen; j += wordSize) {
                String word = s.substring(j, j + wordSize);
                temp.put(word, temp.getOrDefault(word, 0) + 1);
            }
            if (count.equals(temp)) ans.add(i);
        }

        return ans;
    }
}
```


#### 解释2  滑动窗口
