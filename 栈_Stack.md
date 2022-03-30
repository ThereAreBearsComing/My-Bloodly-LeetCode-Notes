# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# 栈 Stack


## 115.最小栈
设计一个支持`push`,`pop`,`top`操作，并能在常数时间内检索到最小元素的栈。

#### 实现 MinStack 类:

`MinStack()`初始化堆栈对象。
<br>`void push(int val)`将元素val推入堆栈。
<br>`void pop()`删除堆栈顶部的元素。
<br>`int top()`获取堆栈顶部的元素。
<br>`int getMin()`获取堆栈中的最小元素。
 

#### 示例 1:

#### 输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
<br>[[],[-2],[0],[-3],[],[],[],[]]

#### 输出：
[null,null,null,null,-3,null,0,-2]

#### 解释：
MinStack minStack = new MinStack();
<br>minStack.push(-2);
<br>minStack.push(0);
<br>minStack.push(-3);
<br>minStack.getMin();   --> 返回 -3.
<br>minStack.pop();
<br>minStack.top();      --> 返回 0.
<br>minStack.getMin();   --> 返回 -2.

链接：https://leetcode-cn.com/problems/min-stack

```Python
class MinStack:

    def __init__(self):
        self.stack = []      #初始化stack
        self.min_stack = []  #初始化minstack

    def push(self, val) -> None:
        self.stack.append(val)             #添加一个值在占栈顶
        if not self.min_stack or val <= self.min_stack[-1]: #判断是不是min栈栈顶或者min栈是不是空
            self.min_stack.append(val)     #如果小于或者min栈为空则添加

    def pop(self) -> None:
        if self.stack.pop() == self.min_stack[-1]: #判断删除的元素是否是最小元素，即是否等于min栈中的元素
            self.min_stack.pop()                   #如果是则删除一个min栈中的元素

    def top(self) -> int:
        return self.stack[-1]                      #取栈顶元素

    def getMin(self) -> int:
        return self.min_stack[-1]                  #取一个min栈的top元素


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
#### 复杂度分析：
* 时间复杂度***O(1)***：压栈，出栈，获取最小值的时间复杂度都为***O(1)***。
* 空间复杂度***O(N)***：包含**N**个元素辅助栈占用线性大小的额外空间。

链接：https://leetcode-cn.com/problems/min-stack/solution/min-stack-fu-zhu-stackfa-by-jin407891080/

