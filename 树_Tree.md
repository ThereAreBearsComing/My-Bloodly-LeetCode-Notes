# My-Bloodly-LeetCode-Notes
You Only Look Lots of Times

# Tree 树
树源于链表，是对链表升级后得到的结构。
<br>链表：一个数据域 + 一个指针域
<br> 树：一个数据域 + 多个指针域
<br>图则为：有环，但所有节点间有通路的数据结构。树是对图进行简化后得到。

#### 相关概念：
* 根节点：非空树处于最上层的那个唯一节点，其余节点都是他的子孙后代。
* 节点的度：节点具有的孩子节点个数。
* 叶子节点：度为0的节点。
* 父子节点：直接相连的一对节点。
* 兄弟节点：由同一个父节点生出的不同的节点互称为兄弟节点。
* 节点层次；由根节点开始记为一层，其子节点记为二层，孙子节点记为三层......
* 节点深度：节点所在的层次数。
* 树的深度/高度：树的最大层次数
* 节点高度：***以节点为根*** 的子树的深度/高度。
* 有序树：以兄弟节点为根的子树交换位置得到的新树视为与原来的树不同的树。
* 无序树：以兄弟节点为根的子树交换位置得到的新树视为与原来的树相同的树。

#### 二叉树：
定义：二叉树是一种每个节点都不大于`2`的树。其中，每个节点的子节点有左右之分且左右子节点所在的子树不可交换位置，即二叉树为一个有序树。
<br>种类：
* 满二叉树：所有的叶子节点都在最底层，且所有的非叶子节点度都为`2`的树。
<br> 记满二叉树**T**高度为`h`，节点总数和为`n`，则**n = 2<sup>h</sup> - 1**,第`k`层节点数总和为**n = 2<sup>k - 1</sup>**。
<br> 从`1`开始，对`T`从上到下，从左到右进行编号。如果编号`i`的节点有父节点，则其父节点编号为`[i/2]`，如果有左子节点，左子节点编号为`2i`，如果有右子节点，其编号为`2i+1`。


* 完全二叉树：记二叉树高度为`h`。从`1`开始，对二叉树从上到下，从左到右进行编号。对高度同为`h`的满二叉树做同样的编号处理。如果二叉树中所有节点的编号都能够与满二叉树同样位置的节点的编号相同，则此二叉树为一个完全二叉树。

<br>1. 完全二叉树的叶子节点只能存在于最下面的两层中，且最下层的叶子节点全部靠左紧密排列。
<br>2. 完全二叉树中父子节点的编号规律与满二叉树完全相同，且编号大于`[n/2]`的节点必为叶子节点。
<br>3. 如果`n`为奇数，则每个非叶子节点都有两个子节点；如果`n`为偶数，则第`n/2`个节点必为非叶子节点，且它只有左子节点而无右子节点，其余非叶子节点都有两个子节点。


* 二叉搜索树(BST)：二叉搜索树要么是空树，要么必须满足下面条件：

<br>1. 左子树所有节点的关键字均小于根节点的关键字。
<br>2. 右子树所有节点的关键字均大于根节点的关键字。
<br>3. 左右子树也均为二叉搜索树。
<br>*二叉树的经典应用场景就是存放有序数据，提升擦找效率。用同一个有序序列，可以构造出多个不同的BST。*

* 平衡二叉树(AVL)：如果二叉树每个节点的左右子树高度差不大于`1`，则这棵二叉树就是平衡二叉树。
<br>*平衡二叉树的经典应用场景就是与二叉树搜索树相结合，形成平衡二叉搜索树。在构建二叉搜索树的同时，借助调整策略，使每个节点左右子树高度差都不大于`1`，保证二叉搜索树中的每个节点的左右子树都规模相当，让整个树看起来更加“匀称”。*

#### 树的核心操作为查找/搜索/遍历：
* 遍历：按照某种规则“访问”树中的每个节点，保证每个节点都会被“访问”到且每个节点只会被”访问“一次。
* “访问”：程序与节点产生交互或在节点进行某种操作。
* “进入”：程序来到了某个节点，并未对该节点产生任何交互。
* 不同规则下对用一节点的“进入”可能会发生多次，但是“访问”只会有一次。

### 深度优先搜索DFS
二叉树的深度优先搜索，在“进入”节点时有一下约定俗成的要求：
* 必须以根节点为起点并“进入”
* 优先“进入”当前节点的左子节点，其次是“进入“当前节点的右子节点。
* 如果当前节点为空，或者左右节点都被“进入”过，则返回并在此“进入”父节点。
<br> <img width="1018" alt="23" src="https://user-images.githubusercontent.com/74708198/160955845-2c47f1a9-86af-44bd-941c-b85b65e32df6.png">

#### 对应代码

```Python
def dfs(TreeNode root):
    if not root: return #当前节点为空返回父节点
    #第一次进入当前节点
    dfs(root.left)      #优先进入左子节点
    #第二次进入当前节点
    dfs(root.right)     #其次进入右子节点
    #第三次进入当前节点
    return              #左右子节点全部进入过，返回父节点
```

<br> <img width="1031" alt="213" src="https://user-images.githubusercontent.com/74708198/160957844-3c174247-330a-4c78-ac1e-052f0f634e7f.png">

##### 前/先序遍历

<br> <img width="1044" alt="333" src="https://user-images.githubusercontent.com/74708198/160958157-a8f06f80-d205-4d70-a680-ea09d8f361c5.png">

##### 中先序遍历

<br> <img width="1037" alt="666" src="https://user-images.githubusercontent.com/74708198/160958629-bae01cb9-2c2e-47b0-a49b-ad632d4dab7c.png">

##### 后先序遍历

<br> <img width="1031" alt="888" src="https://user-images.githubusercontent.com/74708198/160958742-1ad68c02-b6b9-49d0-963d-ff7629bf9e00.png">

### 广度优先搜索BFS

<br> <img width="1005" alt="8" src="https://user-images.githubusercontent.com/74708198/160959197-18581c10-50d9-4909-86b2-8f4df9ebda0e.png">

#### 对应代码

```Python
def dfs(self,root: Optional[TreeNode]):
    q = [] #队列
    q.append(root) #队列初始化
    while len(q) and q[0]:
        cur = q.pop(0)
        print(cur.val) #访问
        if root.left:
            q.append(root.left)
        if root.right:
            q.append(root.right)
    return
```

```Python
def dfs(self,root: Optional[TreeNode]):
    q = [] #队列
    q.append(root) #队列初始化
    while len(q) and q[0]:    #while内，for循环外负责控制层级别的操作
        size = len(q)         #记录当前层中的节点总数
        for i in range(size): #for循环内部负责控制同一层内节点级别操作
            cur = q.pop(0)
            print(cur.val)    #访问
            if root.left:
                q.append(root.left)
            if root.right:
                q.append(root.right)
    return
```
## 104.双二叉树最大深度

给定一个二叉树，找出其最大深度。
<br> 二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
<br> **说明:** 叶子节点是指没有子节点的节点。

#### 示例：
给定二叉树 [3,9,20,null,null,15,7]，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度`3`。

链接：https://leetcode-cn.com/problems/maximum-depth-of-binary-tree

### 深度优先DSF
#### 前序遍历
```Python
class Solution:
    def dfs(self, root: Optional[TreeNode], temp: int, ans: int):
        if not root:   #如果root节点不是空,证明树有东西，不是空树
            self.ans = max(self.ans, temp) #如果temp更大，更新ans
            return #什么值也不返回，就只是让if条件在此终结 = return None
        temp += 1 
        self.dfs(root.left, temp, self.ans)   #左节点探索，有左节点则可以一直更新temp
        self.dfs(root.right, temp, self.ans)  #右节点探索，有右节点则可以一直更新temp
        return 

    def maxDepth(self, root: TreeNode) -> int:
        self.ans = 0
        temp = 0   #定义一个temp来储存深度
        self.dfs(root, temp, self.ans)
        return self.ans 
```
#### 后序遍历
```Python
class Solution:
    def dfs(self, root: Optional[TreeNode]):
        if not root:  
            return 0
        left  = self.dfs(root.left)  #左子树高度
        right = self.dfs(root.right) #右子树高度
        ans   = max(left, right) + 1 #加一个根节点
        return ans

    def maxDepth(self, root: TreeNode) -> int:
        ans = self.dfs(root)
        return ans
```

### 广度优先BSF
```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root: return 0
        q = [] #队列
        q.append(root) #队列初始化
        arr = 0
        while q:    #while内，for循环外负责控制层级别的操作
            size = len(q)         #记录当前层中的节点总数
            for i in range(size): #for循环内部负责控制同一层内节点级别操作
                node = q.pop(0)   #定义指针，从root节点开始
                if node.left:
                  q.append(node.left)
                if node.right:
                  q.append(node.right)
            arr += 1              #每次迭代完，记录层数
        return arr
```

## 111. 二叉树的最小深度

给定一个二叉树，找出其最小深度。
<br>最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
<br>**说明**：叶子节点是指没有子节点的节点。

#### 示例 1：
```
    3
   / \
  9  20
    /  \
   15   7
```
输入：root = [3,9,20,null,null,15,7]
<br>输出：2

#### 示例 2：
输入：root = [2,null,3,null,4,null,5,null,6]
<br>输出：5

链接：https://leetcode-cn.com/problems/minimum-depth-of-binary-tree

```Python
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if not root:  
            return 0
        if not root.left and not root.right:
            return 1
        
        min_depth = 10**5
        if root.left:
            min_depth = min(self.minDepth(root.left), min_depth) #在这里更新完,min_depth就已经是左子树的深度了
        if root.right:
            min_depth = min(self.minDepth(root.right), min_depth) #除非又子树更浅，不然不更新
        
        return min_depth + 1
```

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
* 时间复杂度：***O(n)***
* 空间复杂度：***O(n)***

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
* 时间复杂度：***O(n)***
* 空间复杂度：***O(n)***

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

* 时间复杂度：***O(n)***
* 空间复杂度：***O(h)***,`h`是树的高度

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

