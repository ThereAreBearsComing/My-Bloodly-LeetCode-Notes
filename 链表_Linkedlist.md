# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# 链表 Linkedlist

## 21.合并两个有序链表

将两个升序链表合并为一个新的**升序**链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

#### 示例 1：
输入：l1 = [1,2,4], l2 = [1,3,4]
<br>输出：[1,1,2,3,4,4]

#### 示例 2：
输入：l1 = [], l2 = []
<br>输出：[]

#### 示例 3：
输入：l1 = [], l2 = [0]
<br>输出：[0]

链接：https://leetcode-cn.com/problems/merge-two-sorted-lists

### 递归
函数在运行时调用自己，这个函数就叫递归函数，调用的过程叫做递归。其特性为：
* 递归函数必须要有终止条件，否则会出错；
* 递归函数先不断调用自身，直到遇到终止条件后进行回溯，最终返回答案。

#### 本题思路：
终止条件：当两个链表都为空时，表示我们对链表已合并完成。
如何递归：我们判断`l1`和`l2`头结点哪个更小，然后较小结点的`next`指针指向**其余结点的合并结果。（调用递归）**

```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution: #merge v.合并,
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2  # 如果 l1==None
        if not l2: return l1  # 如果 l1==None
        if l1.val <= l2.val:  # 递归调用
            l1.next = self.mergeTwoLists(l1.next,l2) #把l1的第一个节点链上整个merge
            return l1 #返回去掉第一个Node的l1
        else:
            l2.next = self.mergeTwoLists(l1,l2.next) #把l2的第一个节点链上整个merge
            return l2 #返回去掉第一个Node的l2
```
#### 复杂度分析
给出一个递归算法，其时间复杂度*O(T)* 通常是递归调用的数量(记作*R*)和计算的时间复杂度的乘积（表示为*O(s)*）的乘积：*`O(T) = R * O(T)`*

#### 时间复杂度：*O(m+n)*
`m,n`为`l1`和`l2`的元素个数。递归函数每次去掉一个元素，直到两个链表都为空，因此需要调用*R = O(m + n)* 次。而在递归函数中我们只进行了`next`指针的赋值操作，复杂度为*O(1)* ，故递归的总时间复杂度为 *`O(T) = R * O(1) = O(m+n)`*。

#### 空间复杂度：*O(m+n)*
对于递归调用`self.mergeTwoLists()`当它遇到终止条件准备回溯时，已经递归调用了*O(m+n)* 次，使用了*O(m+n)* 个栈帧，故最后的空间复杂度为*O(m+n)*。

## 160.相交链表
给你两个单链表的头节点`headA`和`headB`，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回`null`。

<br>图示两个链表在节点 c1 开始相交：

<img width="426" alt="截屏2022-03-29 上午10 24 48" src="https://user-images.githubusercontent.com/74708198/160520189-77a0bb3d-9ac8-4db6-b26b-dc143443c89f.png">

<br>题目数据 **保证** 整个链式结构中不存在环。
<br>注意，函数返回结果后，链表必须 **保持其原始结构**。

#### 自定义评测：
**评测系统**的输入如下（你设计的程序**不适用**此输入）：
`intersectVal`- 相交的起始节点的值。如果不存在相交节点，这一值为`0`
`listA`- 第一个链表
`listB`- 第二个链表
`skipA`- 在`listA`中（从头节点开始）跳到交叉节点的节点数
`skipB`- 在`listB`中（从头节点开始）跳到交叉节点的节点数
评测系统将根据这些输入创建链式数据结构，并将两个头节点`headA`和`headB`传递给你的程序。如果程序能够正确返回相交节点，那么你的解决方案将被**视作正确答案**。
<br>链接：https://leetcode-cn.com/problems/intersection-of-two-linked-lists

### 你走过我来时的路(双指针)
pA走过的路径为A链+B链
<br>pB走过的路径为B链+A链
<br>pA和pB走过的长度都相同，都是A链和B链的长度之和，相当于将两条链从尾端对齐，如果相交，则会提前在相交点相遇，如果没有相交点，则会在最后相遇。(PA+C+PB+C = PB+C+PA+C)

```Python
pA:1->2->3->4->5->6->null->9->5->6->null
pB:9->5->6->null->1->2->3->4->5->6->null
```

```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        if headA == [] or headB == []:  #只要有一个空则为null
            return null   
        tmpA = headA    
        tmpB = headB  
        while tmpA != tmpB:  #当两指针指相同时，停止
            if tmpA:         #让A指针向后遍历，直到末尾换去到B链表
                tmpA = tmpA.next
            else:
                tmpA = headB
            if tmpB:         #让B指针向后遍历，直到末尾换去到A链表
                tmpB = tmpB.next
            else:
                tmpB = headA
        return tmpB          #returnA turnB 都可以
```




