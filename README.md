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

-----
## 题目1470：重新排列数组
日期: 2020-7-21 [LeetCode #1470](https://leetcode-cn.com/problems/shuffle-the-array/)

> 题目描述: 给你一个数组 nums ，数组中有 2n 个元素，按 [x1,x2,...,xn,y1,y2,...,yn] 的格式排列。

请你将数组按 [x1,y1,x2,y2,...,xn,yn] 格式重新排列，返回重排后的数组。


示例 1：

输入：nums = [2,5,1,3,4,7], n = 3
输出：[2,3,5,4,1,7] 
解释：由于 x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 ，所以答案为 [2,3,5,4,1,7]

### 题解：（Python）


```python
#思路: 很简单, 就是看中间len/2, 而且n都给了,直接遍历一遍,创建一个新的数组返回就可以
class Solution:
    def shuffle(self, nums: List[int], n: int) -> List[int]:
        returnList = []
        for i in range(n):
            returnList.append(nums[i])
            returnList.append(nums[i+n])
        return returnList
```


----

## 题目02/03：删除中间节点
日期: 2020-7-21 [LeetCode #0203](https://leetcode-cn.com/problems/delete-middle-node-lcci/)

> 题目描述: 实现一种算法，删除单向链表中间的某个节点（即不是第一个或最后一个节点），假定你只能访问该节点。


示例：

输入：单向链表a->b->c->d->e->f中的节点c
结果：不返回任何数据，但该链表变为a->b->d->e->f

### 题解：（Python）


```python
'''
思路: 很简单, 已经不用判断是否是末尾是否是开头了, 
    1. 先看这个linked_list的数据结构和可以调用的方法
    2. 然后替换掉当前的node值,变为他的下一个node的val(值被替换了)
    3. 最后把那个指针指向原来的node的下一个(就是node.next.next)
'''
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```

----
## 题目771：宝石与石头
日期: 2020-7-21 [LeetCode #771](https://leetcode-cn.com/problems/jewels-and-stones/)

> 题目描述: 给定字符串J 代表石头中宝石的类型，和字符串 S代表你拥有的石头。 S 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。J 中的字母不重复，J 和 S中的所有字符都是字母。字母区分大小写，因此"a"和"A"是不同类型的石头。

```python
class Solution:
    def numJewelsInStones(self, J: str, S: str) -> int:
        resultCount = 0
        '''
        for s in S:
            for j in J:
                if j == s:
                    resultCount += 1
        
        for s in S:
            if s in J:
                resultCount += 1
        '''
        sCount = int(len(S))
        for j in J:
            S = S.replace(j,'')
        sCount2 = int(len(S))
        return sCount-sCount2
```

----

## 题目154： 旋转数组的最小数字 // 寻找旋转排序数组中的最小值 II
日期: 2020-7-21 
- [[LeetCode #541](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)]
- [[LeetCode 剑指Offer #11](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)]

> 题目描述: 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

示例 1：

输入：[3,4,5,1,2]
输出：1
示例 2：

输入：[2,2,2,0,1]
输出：0

```python
'''
解题思路:
1. 最基础的办法, 遍历所有, 返回最小的(但是每个元素都要遍历一遍)
2. 二分法, 随着数组增大, 速度会明显增快, 找Pivot, 然后把中心点对比Low或者high, 看值的大小, 如果左边比右边大, 那么一截里面肯定存在那个最小数,然后一直找下去
'''

class Solution:
    def minArray(self, numbers: List[int]) -> int:
        low = 0
        high = len(numbers) - 1
        while low < high:
            pivot = low + (high-low)  // 2
            if numbers[pivot] < numbers[high]:
                high = pivot
            elif numbers[pivot] > numbers[high]:
                low = pivot + 1
            else:
                high -= 1
        return numbers[low]
```


----

## 题目1025：除数博弈
日期: 2020-7-24 [LeetCode #1025](https://leetcode-cn.com/problems/divisor-game/)

> 爱丽丝和鲍勃一起玩游戏，他们轮流行动。爱丽丝先手开局。
> 
> 最初，黑板上有一个数字 N 。在每个玩家的回合，玩家需要执行以下操作：
> 选出任一 x，满足 0 < x < N 且 N % x == 0 。
> 
> 用 N - x 替换黑板上的数字 N 。如果玩家无法执行这些操作，就会输掉游戏。
> 
> 只有在爱丽丝在游戏中取得胜利时才返回 True，否则返回 false。假设两个玩家都以最佳状态参与游戏。

 

示例 1：

输入：2
输出：true
解释：爱丽丝选择 1，鲍勃无法进行操作。
示例 2：

输入：3
输出：false
解释：爱丽丝选择 1，鲍勃也选择 1，然后爱丽丝无法进行操作。

### 题解：（Python）

> 解题思路: 这题很有意思，咋一看是要考虑是否是素数，看是否是奇数偶数。然后简单推算一下，发现，1的话，Alice没得选，A输；2的话，Bob没得选，A赢。 那么我们大胆猜测一下，只要A是奇数，那么她就输了，否则她就赢了。最后肯定要变成2，1的， 验证一下， 一直到5都是对的

```python
class Solution:
    def divisorGame(self, N: int) -> bool:
        return( N%2==0 )
```