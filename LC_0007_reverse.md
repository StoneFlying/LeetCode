#### 7. 整数反转

#### 给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

#### 示例 1:

```
    输入: 123
    输出: 321
```

#### 解释
```
注意下溢出情况就好
```

```Java
class Solution {
    public int reverse(int x) {
        if (x > -10 && x < 10) return x;
        int rev = 0;

        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            // 检测溢出
            if (rev > Integer.MAX_VALUE / 10 || rev == Integer.MAX_VALUE && pop > 7) return 0;
            if (rev < Integer.MIN_VALUE / 10 || rev == Integer.MIN_VALUE && pop < -8) return 0;
            rev = rev * 10 + pop;
        }

        return rev;
    }
}
```