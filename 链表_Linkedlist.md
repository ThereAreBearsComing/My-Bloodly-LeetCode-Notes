# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# 链表 Linkedlist
<img width="606" alt="2" src="https://user-images.githubusercontent.com/74708198/160557455-04a4d98e-eb23-4e47-b405-7150b2f7178a.png">

#### 指针负值操作
```Python
p = p.next
```
实际上`p`为指向当先节点的指针，`p.next`则为`p`的下一个指针，即当前节点指向下一个节点的指针，所以都为指针！

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

## 82.删除排序链表中的重复元素 II
给定一个已排序的链表的头`head`，删除原始链表中所有重复数字的节点，只留下不同的数字。返回 *已排序的链表*。

#### 示例 1：
输入：head = [1,2,3,3,4,4,5]
<br>输出：[1,2,5]

#### 示例 2：
<img width="407" alt="1" src="https://user-images.githubusercontent.com/74708198/160522523-db6c29ee-0156-440a-be07-356be611cd3f.png">
输入：head = [1,1,1,2,3]
<br>输出：[2,3]

链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii

**链表和树的问题，一般都可以有递归和迭代两种写法。**

### 方法一：一次遍历
这里说的一次遍历，是说一边遍历、**一边统计相邻节点的值是否相等，如果值相等就继续后移找到值不等的位置，然后删除值相等的这个区间。**
<br>其实思路很简单，跟递归方法中的`while`语句跳过所有值相等的节点的思路是一样的：如果`cur.val == cur.next.val` 说明两个相邻的节点值相等，所以继续后移，一直找到`cur.val != cur.next.val`，此时的`cur.next` 就是值不等的节点。

比如：`1 -> 2 -> 2 -> 2 -> 3，`我们用一个`pre`指向 1；当`cur`指向第一个`2`的时候，发现`cur.val == cur.next.val`，所以出现了值重复的节点啊，所以`cur`一直后移到最后一个`2`的时候，发现`cur.val != cur.next.val`，此时`cur.next = 3`，所以`pre.next = cur.next`，即让`1`的`next`节点是`3`就把中间的所有`2`都删除了。
代码中用到了一个常用的技**dummy节点，也叫做哑节点**。它在链表的迭代写法中非常常见，因为对于本题而言，我们可能会删除头结点`head`为了维护一个不变的头节点，所以我们添加了`dummy`让`dummy.next = head`这样即使`head`被删了，那么会操作`dummy.next`指向新的链表头部，所以最终返回的也是`dummy.next`。

```Python
class Solution(object):
    def deleteDuplicates(self, head):
        if not head or not head.next:
            return head
        dummy = ListNode(0)
        dummy.next = head
        pre = dummy
        cur = head
        while cur:
            # 跳过当前的重复节点，使得cur指向当前重复元素的最后一个位置
            while cur.next and cur.val == cur.next.val:
                cur = cur.next
            if pre.next == cur:
                 # pre和cur之间没有重复节点，pre后移
                pre = pre.next
            else:
                # pre->next指向cur的下一个位置（相当于跳过了当前的重复元素）
                # 但是pre不移动，仍然指向已经遍历的链表结尾
                pre.next = cur.next
            cur = cur.next
        return dummy.next
```
* 时间复杂度：***O(N)***，对链表每个节点遍历了一次；
* 空间复杂度：***O(1)***，只使用了常量的空间。

### 方法二：利用计数，两次遍历
这个做法忽略了链表有序这个性质，使用了两次遍历，第一次遍历统计每个节点的值出现的次数，第二次遍历的时候，如果发现`head.next`的`val`出现次数不是`1`次，则需要删除`head.next`。

```Python
class Solution:
    def deleteDuplicates(self, head):
        dummy = ListNode(0)
        dummy.next = head
        val_list = []
        while head:
            val_list.append(head.val)
            head = head.next
        counter = collections.Counter(val_list)
        head = dummy
        while head and head.next:
            if counter[head.next.val] != 1:
                head.next = head.next.next
            else:
                head = head.next
        return dummy.next
```
* 时间复杂度：***O(N)***，对链表遍历了两次；
* 空间复杂度：***O(N)***，需要一个字典保存每个节点值出现的次数。

### 方法三：递归
#### 1.1 递归函数定义
**递归最基本的是要明白递归函数的定义！** 我反复强调过这一点。
<br>递归函数直接使用题目给出的函数`deleteDuplicates(head)`，它的含义是 删除`head`作为开头的有序链表中，值出现重复的节点。

#### 1.2 递归终止条件
终止条件就是能想到的基本的、不用继续递归处理的case。
<br>如果`head`为空，那么肯定没有值出现重复的节点，直接返回`head`；
<br>如果`head.next`为空，那么说明链表中只有一个节点，也没有值出现重复的节点，也直接返回`head`。
#### 1.3 递归调用
什么时候需要递归呢？我们想一下这两种情况：
<br>如果`head.val != head.next.val`，说明头节点的值不等于下一个节点的值，所以当前的`head`节点必须保留；但是`head.next`节点要不要保留呢？我们还不知道，需要对`head.next`进行递归，即对`head.next`作为头节点的链表，去除值重复的节点。所以`head.next = self.deleteDuplicates(head.next)`.
<br>如果`head.val == head.next.val`，说明头节点的值等于下一个节点的值，所以当前的 head 节点必须删除，并且`head`之后所有与`head.val`相等的节点也都需要删除；删除到哪个节点为止呢？需要用`move`指针一直向后遍历寻找到与`head.val`不等的节点。此时`move`之前的节点都不保留了，因此返回`deleteDuplicates(move)`;
#### 1.4 返回结果
题目让我们返回删除了值重复的节点后剩余的链表，结合上面两种递归调用的情况。
<br>如果`head.val != head.next.val`，头结点需要保留，因此返回的是`head`；
<br>如果`head.val == head.next.val`，头结点需要删除，需要返回的是`deleteDuplicates(move)`;。

<br>作者：fuxuemingzhu
<br>链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/solution/fu-xue-ming-zhu-di-gui-die-dai-yi-pian-t-wy0h/
```Python
class Solution(object):
    def deleteDuplicates(self, head):
        if not head or not head.next:
            return head
        if head.val != head.next.val:  #头指针指向的值等于，头指针下一个指针指向的值。
            head.next = self.deleteDuplicates(head.next) # xx.next = ww意思应该是把xx作为ww的头节点，xx指针指向ww
        else:
            move = head.next # mm = xx.next 意思是mm作为指向头节点的指针换到头节点指向下一个节点的指针，也就是吧原始的头节点砍掉了。
            while move and head.val == move.val: #这里move理解为遍历指针？(暂时不怎么理解)
                move = move.next
            return self.deleteDuplicates(move)
        return head
```
**时间复杂度**：***O(N)***，每个节点访问了一次。
<br>**空间复杂度**：***O(N)***，递归调用的时候会用到了系统的栈。




