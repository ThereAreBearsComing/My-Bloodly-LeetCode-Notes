# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times


# 列表 List

## 26.删除有序数组中的重复项

给你一个`升序排列`的数组`nums`，请你`原地`删除重复出现的元素，使每个元素`只出现一次`，返回删除后数组的新长度。元素的`相对顺序`应该保持`一致`。
由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有`k`个元素，那么`nums`的前`k`个元素应该保存最终结果。

将最终结果插入`nums`的前`k`个位置后返回`k`。

不要使用额外的空间，你必须在`原地`修改输入`数组`并在使用`O(1)`额外空间的条件下完成。

#### 判题标准:

系统会用下面的代码来测试你的题解:
```C
int[] nums = [...]; // 输入数组
int[] expectedNums = [...]; // 长度正确的期望答案

int k = removeDuplicates(nums); // 调用

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

如果所有断言都通过，那么您的题解将被`通过`。

链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array

#### 代码
```Python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        #双指针方法
        j = 0 #初始化二号指针
        for i in range(len(nums)):  #历遍指针i指针扫描一遍，j动一格
            if nums[i] != nums[j]:  #如果nums[i]不等于nums[j]
                j += 1              #让j指针原地更新，指向右一格，用于更新
                nums[j]=nums[i]     #更新nums[j]
        return j + 1                #更新j，让其向右移一个格子，再进行i的新一次的历遍    
```
首先注意数组是有序的，那么重复的元素一定会相邻。

要求删除重复元素，实际上就是将不重复的元素移到数组的左侧。
一个指针`i`进行数组遍历，另外一个指针`j`指向有效数组的最后一个位置。

只有当`i`所指向的值和`j`不一致（不重复），才将`i`的值添加到`j`的下一位置。

#### 复杂度分析
* 时间复杂度：O(n)
* 空间复杂度：O(1)

## 27.移除元素
给你一个数组`nums`和一个值`val`，你需要`原地`移除所有数值等于`val`的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用`O(1)`额外空间并`原地`修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

#### 说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```C
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

链接：https://leetcode-cn.com/problems/remove-element

#### 示例 1：
输入：nums = [3,2,2,3], val = 3
<br> 输出：2, nums = [2,2]
<br> 解释：函数应该返回新的长度`2`, 并且`nums`中的前两个元素均为`2`。你不需要考虑数组中超出新长度后面的元素。
<br> 例如，函数返回的新长度为`2`，而`nums = [2,2,3,3]`或`nums = [2,2,0,0]`，也会被视作正确答案。

#### 示例 2：
输入：nums = [0,1,2,2,3,0,4,2], val = 2
<br> 输出：5, nums = [0,1,4,0,3]
<br> 解释：函数应该返回新的长度`5`, 并且`nums`中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。

### 解法一,暴力(本人第一次自己做出习题,巨慢）

```Python
class Solution:
    def removeElement(cls, nums: List[int], val: int) -> int:       
        for i in range(len(nums)):  #i遍历列表
            if nums[i] == val:      #如果发现nums[i]和val相等
                nums[i] = 'a'       #将nums换成一个字符(随便啥都行，别是val会出现的任何形式)
        while 'a' in nums:          #找到nums中所有 替换掉的字符，直接remove只会去掉一个
            nums.remove('a')        #移除换掉的字符, .remove是删除指定值, .pop删除指定索引
        return len(nums)            #需要return结果，即新数组长度，否则会有stdout
```

想法就是替换掉列表中的所有`val`,然后挨个删除。

### 解法二，双指针

```Python
class Solution:
    def removeElement(cls, nums: List[int], val: int) -> int:       
        j = 0
        for i in range(len(nums)):
            if nums[i] != val:   
                nums[j] = nums[i]
                j += 1            
        return j #返回j的索引，即为新列表的长度，因为整个了表都是j指针重新指出来的
```

想象一下`i`指针遍历列表，发现和`val`相等直接跳过，用`j`指针挨个储存不等于值，最后相当于用`j`指针创造出了一个新的列表。
其中不会包含等于`val`的数值，因为i指针已经跳过了所有等于`val`的值，而`j`指针只会接收到i指针没跳过的数值。

## 15.三数之和
给你一个包含`n`个整数的数组`nums`，判断`nums`中是否存在三个元素`a，b，c`，使得`a + b + c = 0`？请你找出所有和为`0`且不重复的三元组。

注意：答案中不可以包含重复的三元组。

#### 示例 1： 
输入：nums = [-1,0,1,2,-1,-4]
<br> 输出：[[-1,-1,2],[-1,0,1]]

#### 示例 2：
输入：nums = []
<br> 输出：[]

#### 示例 3：
输入：nums = [0]
<br> 输出：[]

链接：https://leetcode-cn.com/problems/3sum

### 解题思路：排序 + 双指针
暴力法搜索为O(N<sup>3</sup>)时间复杂度，可通过双指针动态消去无效解来优化效率。
* 双指针法铺垫： 先将给定 nums 排序，复杂度为 O(NlogN)O(NlogN)。
* 双指针法思路： 固定`3`个指针中最左（最小）数字的指针`i`，双指针`j，k`分设在数组索引`(i, len(nums))(i,len(nums))`两端，通过双指针交替向中间移动，记录对于每个固定指针`i`的所有满足`nums[i] + nums[j] + nums[k] == 0`的`j,k`组合：
当`nums[k] > 0`时直接break跳出：因为`nums[j] >= nums[i] >= nums[k] > 0`，即`3`个数字都大于`0`，在此固定指针`i`之后不可能再找到结果了。
当`k`> 0且`nums[k] == nums[k - 1]`时即跳过此元素nums[k]：因为已经将`nums[k - 1]`的所有组合加入到结果中，本次双指针搜索只会得到重复组合。
`j，k`分设在数组索引`(i, len(nums))(i,len(nums))`两端，当`j < k`循环计算`s = nums[i] + nums[j] + nums[k]`，并按照以下规则执行双指针移动：
当`s < 0`时，`j += 1`并跳过所有重复的`nums[j]`；
当`s > 0`时，`k -= 1`并跳过所有重复的`nums[k]`；
当`s == 0`时，记录组合[i, j, k]至`res`，执行`j += 1`和`k -= 1`并跳过所有重复的`nums[j]`和`nums[k]`，防止记录到重复组合。

#### 代码

```Python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res, i = [], 0
        for i in range(len(nums) - 2):
            if nums[i] > 0 : break  #当nums[i]>0时候终止，因为nums[i]为最小值
            if i > 0 and nums[i] == nums[i-1]: continue # 跳过所有相同的nums[i]
            j , k = i + 1, len(nums) - 1 #定义剩下俩指针，除i外最左，一个在最右
            while j < k:                 #j必须小于k从而保持不重复
                    s = nums[i] + nums[j] + nums[k] #定义sum
                    if s < 0:   #小于0，要增加，所以让左侧指针向右，增加sum
                        j += 1
                        while j < k and nums[j] == nums[j-1]: j += 1 #跳过重复j
                    elif s > 0:  #大于0，要减少，所以让右侧指针向左，减小sum
                        k -= 1
                        while j < k and nums[k] == nums[k+1]: k -= 1 #跳过重复k
                    else:        #s=0时，储存结果
                        res.append([nums[i],nums[j],nums[k]])
                        j += 1  #依旧需要跳过重复j,k数值
                        k -= 1
                        while j < k and nums[j] == nums[j-1]: j += 1
                        while j < k and nums[k] == nums[k+1]: k -= 1
        return res
```

有人问马老师发生甚么事了，怎➡️么➡️说⬇️呢⬇️，犹豫不决先排序，步步逼近双指针。

#### 复杂度分析：
* 时间复杂度O(N<sup>2</sup>)：其中固定指针k循环复杂度O(N)，双指针`j,k`复杂度O(N)。
* 空间复杂度O(1)：指针使用常数大小的额外空间。

作者：jyd
链接：https://leetcode-cn.com/problems/3sum/solution/3sumpai-xu-shuang-zhi-zhen-yi-dong-by-jyd/
