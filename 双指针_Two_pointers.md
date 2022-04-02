# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# 双指针 Two pointers



## 141. 环形链表

给你一个链表的头节点`head`，判断链表中是否有环。
<br>如果链表中有某个节点，可以通过连续跟踪`next`指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数`pos`来表示链表尾连接到链表中的位置（索引从`0`开始）。注意：`pos`不作为参数进行传递 。仅仅是为了标识链表的实际情况。
<br>如果链表中存在环 ，则返回`true`。 否则，返回`false`。

#### 示例 1：
输入：head = [3,2,0,-4], pos = 1
<br>输出：true
<br>解释：链表中有一个环，其尾部连接到第二个节点。

#### 示例 2：
输入：head = [1,2], pos = 0
<br>输出：true
<br>解释：链表中有一个环，其尾部连接到第一个节点。

#### 示例 3：
输入：head = [1], pos = -1
<br>输出：false
<br>解释：链表中没有环。

链接：https://leetcode-cn.com/problems/linked-list-cycle

#### 快慢指针
思考🤔一下，让快指针在head.next而慢指针在head,快指针将在飞循环处遥遥领先，但一旦进入循环，因为步伐不同，快指针总会和慢指针相遇，只是时间问题。
```Python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head or not head.next:
            return False
        
        slow = head
        fast = head.next

        while slow != fast:
            if not fast or not fast.next: #not这里指fast和fase.next为假值是None,''时执行下边的return
                return False
            slow = slow.next
            fast = fast.next.next       
        return True
```
***别再把 if not 记反了***

