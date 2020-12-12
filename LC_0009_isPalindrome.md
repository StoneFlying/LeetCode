#### 9. 回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

#### 示例 1:

```
    输入: 121
    输出: true
```
### 解释
```
反转数字的一半即可，当数字长度为奇数时，需要通过 rev / 10 去掉中位数
```
```Java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || x % 10 == 0 && x != 0) return false;

        int rev = 0;
        while (x > rev) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }

        if (rev == x || rev / 10 == x) return true;
        return false;
    }
}
```