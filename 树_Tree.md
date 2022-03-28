# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# Tree

## 938. 二叉搜索树的范围和 | Range Sum of BST 

给定二叉搜索树的根结点`root`，返回值位于范围`[low, high]`之间的所有结点的值的和。

#### 示例1：
输入：root = [10,5,15,3,7,null,18], low = 7, high = 15
<br> 输出：32
#### 示例 2：
输入：root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
<br> 输出：23

链接：https://leetcode-cn.com/problems/range-sum-of-bst

#### 暴力解法
```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
        arr = []
        def DFS(node):   #右遍历二叉树，递归。方法源于94题
            if node:
                DFS(node.left)
                arr.append(node.val)
                DFS(node.right)
        DFS(root)         
        #arr = list(arr) #右历遍完将列表中的值替换为0，这样求和剪支一个效果
        for i in range(len(arr)):
          if low  > arr[i] or high  < arr[i] :
                arr[i] = 0          
        return sum(arr)
```
竟然比其他两个快一些，但是能解，用零替换不满足元素后，求和。

#### 递归
基本思路
这又是众多「二叉搜索树遍历」题目中的一道。
<br>__二叉搜索树的中序遍历是有序的。__
<br>只要对其进行「中序遍历」即可得到有序列表，在遍历过程中判断节点值是否符合要求，对于符合要求的节点值进行累加即可。
<br>二叉搜索树的「中序遍历」有「迭代」和「递归」两种形式。__由于给定了值范围__`[low,high]`，__因此可以在遍历过程中做一些剪枝操作，但并不影响时空复杂度__。

链接：https://leetcode-cn.com/problems/range-sum-of-bst/solution/gong-shui-san-xie-yi-ti-shuang-jie-di-gu-q2fo/

```Python
class Solution:
    def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
        self.cur = 0
        def dfs(node):
            if node.left:
                dfs(node.left)
            if node.val > high:
                return
            if node.val >= low:
                self.cur += node.val
            if node.right:
                dfs(node.right)
        dfs(root)
        return self.cur
```
#### 复杂度分析
* 时间复杂度：*O(n)*
* 空间复杂度：*O(n)*

#### 迭代
迭代其实就是使用「栈」来模拟递归过程，也属于树的遍历中的常见实现形式。
<br>__一般简单的面试中如果问到树的遍历，面试官都__`不会`__对__`「递归」`__解法感到满意，因此掌握__`「迭代/非递归」`__写法同样重要。__

链接：https://leetcode-cn.com/problems/range-sum-of-bst/solution/gong-shui-san-xie-yi-ti-shuang-jie-di-gu-q2fo/

```Python
class Solution:
    def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
        cur = 0
        stack = []
        while root or stack:
            if root:
                stack.append(root)
                root = root.left
            else:
                t = stack.pop(-1)
                if low <= t.val <= high:
                    cur += t.val
                root = t.right
        return cur
```
#### 复杂度分析
* 时间复杂度：*O(n)*
* 空间复杂度：*O(n)*

## 94. 二叉树的中序遍历

给定一个二叉树的根节点`root`，返回它的`中序`遍历。

#### 示例1：
输入：root = [1,null,2,3]
输出：[1,3,2]
#### 示例2:
输入：root = []
输出：[]
#### 示例3:
输入：root = [1]
输出：[1]

###### 进阶: 递归算法很简单，你可以通过迭代算法完成吗？
链接：https://leetcode-cn.com/problems/binary-tree-inorder-traversal

#### 基础：
* 前序遍历：打印 - 左 - 右，先访问根节点，然后访问左节点，最后右节点；
* 中序遍历：左 - 打印 - 右，先访问左节点，然后访问根节点，最后右节点；
* 后序遍历：左 - 右 - 打印，先访问左节点，然后访问右节点，最后根节点；

### 递归实现
题目要求的是中序遍历，那就按照`左-打印-右`这种顺序遍历树就可以了，递归函数实现
* 终止条件：当前节点为空时
* 函数内：递归的调用左节点，打印当前节点，再递归调用右节点

* 时间复杂度：*O(n)*
* 空间复杂度：*O(h)*,`h`是树的高度

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        arr = []
        def DFS(node):
            if node:
                DFS(node.left)
                arr.append(node.val)
                DFS(node.right)
        DFS(root)
        return arr
```

