# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# 字符串 String

#### 常见字符串问题：
* 字符串匹配问题
* 子串相关问题
* 前缀/后缀相关问题
* 回文串相关问题
* 子序列相关问题

字符串的比较,`"abc"`与`"acc"`进行比较，因为b比c在字母中靠前，所以可以认为`b < c`，所以得出`"abc" < "acc"`，也可以说`"str1" < "str2"`。

### 字符串比较操作：
#### 如果等长则：
* 从两个字符串的第0个位置开始，一次比较对应位置上的字符串编码大小。
* if   `str1 [i]` ==`str2 [i]`： `i` += `1`
* elif `str1 [i]` < `str2 [i]`： `str1` < `str2`
* else: `str1` > `str2`
#### 如果不等长则：
* "abcde" > "abc"
* "abc" < "abcde"
* "abcd" == "abcd" 

##  680. 验证回文字符串 Ⅱ
给定一个非空字符串`s`，最多删除一个字符。判断是否能成为回文字符串。

#### 示例 1:
<br>输入: s = "aba"
<br>输出: true

#### 示例 2:
<br>输入: s = "abca"
<br>输出: true
<br>解释: 你可以删除c字符。

#### 示例 3:
<br>输入: s = "abc"
<br>输出: false

链接：https://leetcode-cn.com/problems/valid-palindrome-ii


```Python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        def checkPalindrome(low,high): #定义判断函数,用于后边调用
            i, j = low, high           #
            while i < j:               #当两指针相遇停止遍历
                if s[i] != s[j]:       #如果不等，直接返回False
                    return False
                else:                  #否则继续遍历
                    i += 1
                    j -= 1
            return True

        low, high = 0, len(s) - 1
        while low < high:
            if s[low] == s[high]:
                low  += 1
                high -= 1
            else: #这里调用函数然后，用+-1来跳过一个元素，从而等于判断删除一个字符是否回文
                return checkPalindrome(low+1,high) or checkPalindrome(low,high-1)
        return True
```

#### 复杂度分析

* 时间复杂度：***O(n)***，其中`n`是字符串的长度。判断整个字符串是否是回文字符串的时间复杂度是***O(n)***，遇到不同字符时，判断两个子串是否是回文字符串的时间复杂度也都是***O(n)***。
* 空间复杂度：***O(1)***。只需要维护有限的常量空间。

链接：https://leetcode-cn.com/problems/valid-palindrome-ii/solution/yan-zheng-hui-wen-zi-fu-chuan-ii-by-leetcode-solut/
