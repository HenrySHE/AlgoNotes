# AlgoNotes

> Algo笔记本, 用来记录一下平时刷LeetCode的

----

## 题目12：数字转换罗马数字
日期: 2020-7-15 [LeetCode #12](https://leetcode-cn.com/problems/integer-to-roman/submissions/)

> 题目描述: ![ss](img/12-1.jpg)

### 题解：（Python）


```python
class Solution:
    def intToRoman(self, num: int) -> str:
        digits = [(1000, "M"), (900, "CM"), (500, "D"), (400, "CD"), (100, "C"), (90, "XC"), 
              (50, "L"), (40, "XL"), (10, "X"), (9, "IX"), (5, "V"), (4, "IV"), (1, "I")]
        
        roman_digits = []
        for value,symbol in digits:
            if num == 0: break
            count, num = divmod(num, value)
            roman_digits.append(symbol * count)
        return "".join(roman_digits)

```

需要的函数: `divmod(被除数,除数)`, 返回的是(商,余数)。例如：`divmod(1024,1000)`的结果就是`(1,24)`.

### 题解：（Java）

```java
public class TestAlgo {

    private final int[] VALUES = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
    private final String[] SYMBOLS ={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};

    public String intToRoman(int num) {
        num += 1 ;
        StringBuilder sb = new StringBuilder();
        for (int i=0; i <VALUES.length; i++){
            if (num <= 0) {
                break;
            }
            while (VALUES[i] < num) {
                num = num - VALUES[i];
                sb.append(SYMBOLS[i]);
            }

        }
        return sb.toString();
    }

    public static void main(String[] args) {
        TestAlgo ta = new TestAlgo();
        System.out.println(ta.intToRoman(1000));

    }
}
```

运行结果:
![运行结果](img/12-2.jpg)


