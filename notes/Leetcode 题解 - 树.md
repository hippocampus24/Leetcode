<!-- GFM-TOC -->
* [递归](#递归)
    * [1. 树的高度](#1-树的高度)
    * [2. 平衡树](#2-平衡树)
    * [3. 两节点的最长路径](#3-两节点的最长路径)
    * [4. 翻转树](#4-翻转树)
    * [5. 归并两棵树](#5-归并两棵树)
    * [6. 判断路径和是否等于一个数](#6-判断路径和是否等于一个数)
    * [7. 统计路径和等于一个数的路径数量](#7-统计路径和等于一个数的路径数量)
    * [8. 子树](#8-子树)
    * [9. 树的对称](#9-树的对称)
    * [10. 最小路径](#10-最小路径)
    * [11. 统计左叶子节点的和](#11-统计左叶子节点的和)
    * [12. 相同节点值的最大路径长度](#12-相同节点值的最大路径长度)
    * [13. 间隔遍历](#13-间隔遍历)
    * [14. 找出二叉树中第二小的节点](#14-找出二叉树中第二小的节点)
* [层次遍历](#层次遍历)
    * [1. 一棵树每层节点的平均数](#1-一棵树每层节点的平均数)
    * [2. 得到左下角的节点](#2-得到左下角的节点)
* [前中后序遍历](#前中后序遍历)
    * [1. 非递归实现二叉树的前序遍历](#1-非递归实现二叉树的前序遍历)
    * [2. 非递归实现二叉树的后序遍历](#2-非递归实现二叉树的后序遍历)
    * [3. 非递归实现二叉树的中序遍历](#3-非递归实现二叉树的中序遍历)
* [BST](#bst)
    * [1. 修剪二叉查找树](#1-修剪二叉查找树)
    * [2. 寻找二叉查找树的第 k 个元素](#2-寻找二叉查找树的第-k-个元素)
    * [3. 把二叉查找树每个节点的值都加上比它大的节点的值](#3-把二叉查找树每个节点的值都加上比它大的节点的值)
    * [4. 二叉查找树的最近公共祖先](#4-二叉查找树的最近公共祖先)
    * [5. 二叉树的最近公共祖先](#5-二叉树的最近公共祖先)
    * [6. 从有序数组中构造二叉查找树](#6-从有序数组中构造二叉查找树)
    * [7. 根据有序链表构造平衡的二叉查找树](#7-根据有序链表构造平衡的二叉查找树)
    * [8. 在二叉查找树中寻找两个节点，使它们的和为一个给定值](#8-在二叉查找树中寻找两个节点，使它们的和为一个给定值)
    * [9. 在二叉查找树中查找两个节点之差的最小绝对值](#9-在二叉查找树中查找两个节点之差的最小绝对值)
    * [10. 寻找二叉查找树中出现次数最多的值](#10-寻找二叉查找树中出现次数最多的值)
* [Trie](#trie)
    * [1. 实现一个 Trie](#1-实现一个-trie)
    * [2. 实现一个 Trie，用来求前缀和](#2-实现一个-trie，用来求前缀和)
<!-- GFM-TOC -->


# 递归

一棵树要么是空树，要么有两个指针，每个指针指向一棵树。树是一种递归结构，很多树的问题可以使用递归来处理。

## 1. 树的高度

104\. Maximum Depth of Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/description/)

```python  
class Solution:
    def maxDepth(self, root:TreeNode) -> int:
        """
        :type root:TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        else:
            left_height = self.maxDepth(root.left)
            right_height = self.maxDepth(root.right)
            return max(left_height, right_height) + 1  
```

## 2. 平衡树

110\. Balanced Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/balanced-binary-tree/description/)

```html
    3
   / \
  9  20
    /  \
   15   7
```

平衡树左右子树高度差都小于等于 1

```python  
class Solution:
    def isBalanced(self, root:TreeNode) -> bool:
        if not root: return True
        return abs(self.depth(root.left) - self.depth(root.right)) <= 1 and \
            self.isBalanced(root.left) and self.isBalanced(root.right)
    
    def depth(self, root):
        if not root:return 0
        return max(self.depth(root.left),self.depth(root.right)) + 1  
```

## 3. 两节点的最长路径

543\. Diameter of Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/diameter-of-binary-tree/description/)

```html
Input:

         1
        / \
       2  3
      / \
     4   5

Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].
```

```python  
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        self.ans = 1 
        def depth(root):
            if not root:return 0
            L = depth(root.left)
            R = depth(root.right)
            self.ans = max(self.ans, L + R + 1)
            return max(L,R) + 1
        depth(root)
        return self.ans - 1  
```

## 4. 翻转树

226\. Invert Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/invert-binary-tree/description/)

讲解：[Youtube](https://www.youtube.com/watch?v=_Bx_IeZrEKg)

```python    
class Solution:
    def invertTree(self,root:TreeNode) -> TreeNode:
        if root is not None:
            root.left,root.right = self.invertTree(root.right),self.invertTree(root.left)
        return root
```

## 5. 归并两棵树

617\. Merge Two Binary Trees (Easy)

[力扣](https://leetcode-cn.com/problems/merge-two-binary-trees/description/)

```html
Input:
       Tree 1                     Tree 2
          1                         2
         / \                       / \
        3   2                     1   3
       /                           \   \
      5                             4   7

Output:
         3
        / \
       4   5
      / \   \
     5   4   7
```

```python   
class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if not (t1 and t2):
            return t1 if t1 else t2
        t1.val += t2.val
        t1.left = self.mergeTrees(t1.left, t2.left)
        t1.right = self.mergeTrees(t1.right,t2.right)
        return t1
```

## 6. 判断路径和是否等于一个数

Leetcdoe : 112. Path Sum (Easy)

[力扣](https://leetcode-cn.com/problems/path-sum/description/)

```html
Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

路径和定义为从 root 到 leaf 的所有节点的和。

```python
class Solution:
    def hasPathSum(self,root:TreeNode, sum:int) -> bool:
        if not root: return False
        if not root.left and not root.right:
            return root.val == sum
        
        sum -= root.val
        return self.hasPathSum(root.left, sum) or self.hasPathSum(root.right, sum)
```

## 7. 统计路径和等于一个数的路径数量

437\. Path Sum III (Easy)

[力扣](https://leetcode-cn.com/problems/path-sum-iii/description/)

```html
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

路径不一定以 root 开头，也不一定以 leaf 结尾，但是必须连续。

```python  
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        def dfs(root, sumlist):
            if root is None: return 0
            sumlist = [num + root.val for num in sumlist] + [root.val]
            return sumlist.count(sum) + dfs(root.left, sumlist) + dfs(root.right, sumlist)
        return dfs(root,[])
```

## 8. 子树

572\. Subtree of Another Tree (Easy)

[力扣](https://leetcode-cn.com/problems/subtree-of-another-tree/description/)

```html
Given tree s:
     3
    / \
   4   5
  / \
 1   2

Given tree t:
   4
  / \
 1   2

Return true, because t has the same structure and node values with a subtree of s.

Given tree s:

     3
    / \
   4   5
  / \
 1   2
    /
   0

Given tree t:
   4
  / \
 1   2

Return false.
```

```python  
class Solution(object):
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        if not s and not t:
            return True
        if not s or not t:
            return False
        return self.isSameTree(s, t) or self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
        
    def isSameTree(self, s, t):
        if not s and not t:
            return True
        if not s or not t:
            return False
        return s.val == t.val and self.isSameTree(s.left, t.left) and self.isSameTree(s.right, t.right)
```

## 9. 树的对称

101\. Symmetric Tree (Easy)

[力扣](https://leetcode-cn.com/problems/symmetric-tree/description/)

```html
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

```python  
class Solution:
    def isSymmetric(self,root:TreeNode) -> bool:
        bli = []
        fli = []
        if root == None:
            return True
        if root and root.left == None and root.right == None:
            return True
        
        if root and root.left and root.right:
            self.pre_order(root.left,bli)
            self.post_order(root.right,fli)
            fli.reverse()
            if bli == fli:
                return True
            else:
                return False
    def pre_order(self,root,li):
        if root:
            li.append(root.val)
            self.pre_order(root.left,li)
            self.pre_order(root.right,li)
        elif root == None:
            li.append(None)
    
    def post_order(self,root,li):
        if root:
            self.post_order(root.left,li)
            self.post_order(root.right,li)
            li.append(root.val)
        elif root == None:
            li.append(None)
```

## 10. 最小路径

111\. Minimum Depth of Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/description/)

树的根节点到叶子节点的最小路径长度

```python  
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if not root:return 0
        def recursion(root1):
            if not root1:return float("inf")
            if not root1.left and not root1.right: return 1
            return min(recursion(root1.left),recursion(root1.right)) + 1
        return recursion(root)
```

## 11. 统计左叶子节点的和

404\. Sum of Left Leaves (Easy)

[力扣](https://leetcode-cn.com/problems/sum-of-left-leaves/description/)

```html
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

```python   
class Solution:
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
  
###方法一：前序遍历迭代解法
        if not root:return 0
        temp=root
        stack=[temp]
        res=0
        while stack:
            node=stack.pop()
            if node:
                if node.left and not node.left.left and not node.left.right:
                    res+=node.left.val
                stack.append(node.left)
                stack.append(node.right)
        return res

###方法二：前序遍历递归解法：
        self.res=0
        def helper(root):
            if not root:return 0
            if root.left and not root.left.left and not root.left.right:
                self.res+=root.left.val
            helper(root.left)
            helper(root.right)
        temp=root
        helper(temp)
        return self.res
```

## 12. 相同节点值的最大路径长度

687\. Longest Univalue Path (Easy)

[力扣](https://leetcode-cn.com/problems/longest-univalue-path/)

```html
             1
            / \
           4   5
          / \   \
         4   4   5

Output : 2
```

```python
```

## 13. 间隔遍历

337\. House Robber III (Medium)

[力扣](https://leetcode-cn.com/problems/house-robber-iii/description/)

```html
     3
    / \
   2   3
    \   \
     3   1
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

```python
```

## 14. 找出二叉树中第二小的节点

671\. Second Minimum Node In a Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/description/)

```html
Input:
   2
  / \
 2   5
    / \
    5  7

Output: 5
```

一个节点要么具有 0 个或 2 个子节点，如果有子节点，那么根节点是最小的节点。

```python  

```

# 层次遍历

使用 BFS 进行层次遍历。不需要使用两个队列来分别存储当前层的节点和下一层的节点，因为在开始遍历一层的节点时，当前队列中的节点数就是当前层的节点数，只要控制遍历这么多节点数，就能保证这次遍历的都是当前层的节点。

## 1. 一棵树每层节点的平均数

637\. Average of Levels in Binary Tree (Easy)

[力扣](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/description/)

```python. 
class Solution:
    def averageOfLevels(self, root: TreeNode) -> List[float]:
        if not root:return[]
        temp=root
        queue=[root]
        res=[]
        
        while queue:
            temp=[]
            for _ in range(len(queue)):
                node=queue.pop(0)
                if node:
                    temp.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
            l=len(temp)
            if l>0:
                aver=sum(temp)/l
                res.append(aver)
        return res
```

## 2. 得到左下角的节点

513\. Find Bottom Left Tree Value (Easy)

[力扣](https://leetcode-cn.com/problems/find-bottom-left-tree-value/description/)

```html
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

```python  
class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        if not root:
            return -1
        queue = collections.deque()
        queue.append(root)
        while queue:
            cur = queue.popleft()
            if cur.right:
                queue.append(cur.right)
            if cur.left:
                queue.append(cur.left)
        return cur.val
```

# 前中后序遍历

```html
    1
   / \
  2   3
 / \   \
4   5   6
```

- 层次遍历顺序：[1 2 3 4 5 6]
- 前序遍历顺序：[1 2 4 5 3 6]
- 中序遍历顺序：[4 2 5 1 3 6]
- 后序遍历顺序：[4 5 2 6 3 1]

层次遍历使用 BFS 实现，利用的就是 BFS 一层一层遍历的特性；而前序、中序、后序遍历利用了 DFS 实现。

前序、中序、后序遍只是在对节点访问的顺序有一点不同，其它都相同。

① 前序

```python  
```

② 中序

```python  
```

③ 后序

```python  
```

## 1. 非递归实现二叉树的前序遍历

144\. Binary Tree Preorder Traversal (Medium)

[力扣](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/description/)

```python   

```

## 2. 非递归实现二叉树的后序遍历

145\. Binary Tree Postorder Traversal (Medium)

[力扣](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/description/)

前序遍历为 root -> left -> right，后序遍历为 left -> right -> root。可以修改前序遍历成为 root -> right -> left，那么这个顺序就和后序遍历正好相反。

```python  
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []

        stack, output = [root, ], []
        while stack:
            root = stack.pop()
            output.append(root.val)
            if root.left is not None:
                stack.append(root.left)
            if root.right is not None:
                stack.append(root.right)
                
        return output[::-1]
```

## 3. 非递归实现二叉树的中序遍历

94\. Binary Tree Inorder Traversal (Medium)

[力扣](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/description/)

```python  
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        WHITE, GRAY = 0, 1
        res = []
        stack = [(WHITE, root)]
        while stack:
            color, node = stack.pop()
            if node is None: continue
            if color == WHITE:
                stack.append((WHITE, node.right))
                stack.append((GRAY, node))
                stack.append((WHITE, node.left))
            else:
                res.append(node.val)
        return res
```

# BST

二叉查找树（BST）：根节点大于等于左子树所有节点，小于等于右子树所有节点。

二叉查找树中序遍历有序。

## 1. 修剪二叉查找树

669\. Trim a Binary Search Tree (Easy)

[力扣](https://leetcode-cn.com/problems/trim-a-binary-search-tree/description/)

```html
Input:

    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3

Output:

      3
     /
   2
  /
 1
```

题目描述：只保留值在 L \~ R 之间的节点

```python  
class Solution:
    def trimBST(self, root: TreeNode, L: int, R: int) -> TreeNode:
        def trim(node):
            if not node:
                return None
            elif node.val > R:
                return trim(node.left)
            elif node.val < L:
                return trim(node.right)
            else:
                node.left = trim(node.left)
                node.right = trim(node.right)
                return node
        return trim(root)
```

## 2. 寻找二叉查找树的第 k 个元素

230\. Kth Smallest Element in a BST (Medium)

[力扣](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/description/)

```python  
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        def inorder(r):
            return inorder(r.left) + [r.val] + inorder(r.right) if r else []
        return inorder(root)[k - 1]
```

## 3. 把二叉查找树每个节点的值都加上比它大的节点的值

Convert BST to Greater Tree (Easy)

[力扣](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/description/)

```html
Input: The root of a Binary Search Tree like this:

              5
            /   \
           2     13

Output: The root of a Greater Tree like this:

             18
            /   \
          20     13
```

先遍历右子树。

```python  
class Solution(object):
    def __init__(self):
        self.total = 0

    def convertBST(self, root):
        if root is not None:
            self.convertBST(root.right)
            self.total += root.val
            root.val = self.total
            self.convertBST(root.left)
        return root

```

## 4. 二叉查找树的最近公共祖先

235\. Lowest Common Ancestor of a Binary Search Tree (Easy)

[力扣](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

```html
        _______6______
      /                \
  ___2__             ___8__
 /      \           /      \
0        4         7        9
        /  \
       3   5

For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```
解说:[youtube](https://www.youtube.com/watch?v=B48MMwTlRuA)
```python  
class Solution:    
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if p.val < root.val and q.val < root.val:
            return self.lowestCommonAncestor(root.left, p ,q)
        elif p.val > root.val and q.val > root.val:
            return self.lowestCommonAncestor(root.right, p ,q)
        else:
            return root
```

## 5. 二叉树的最近公共祖先

236\. Lowest Common Ancestor of a Binary Tree (Medium) 

[力扣](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

```html
       _______3______
      /              \
  ___5__           ___1__
 /      \         /      \
6        2       0        8
        /  \
       7    4

For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

```python  
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root or root == p or root == q: return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if not left: return right
        if not right: return left
        return root
```

## 6. 从有序数组中构造二叉查找树

108\. Convert Sorted Array to Binary Search Tree (Easy)

[力扣](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/description/)'

解说:[youtube](https://www.youtube.com/watch?v=SS5Td7iz_0k)

```python  
class Solution:
    def sortedArrayToBST(self, nums:List[int]) -> TreeNode:
        def make_tree(start_index,end_index):
            if start_index > end_index:
                return None
            mid_index = (start_index + end_index)//2
            this_tree_root = TreeNode(nums[mid_index])

            this_tree_root.left = make_tree(start_index,mid_index-1)
            this_tree_root.right = make_tree(mid_index+1,end_index)

            return this_tree_root
        return make_tree(0,len(nums)-1)
```

## 7. 根据有序链表构造平衡的二叉查找树

109\. Convert Sorted List to Binary Search Tree (Medium)

[力扣](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/description/)

```html
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

```python  
class Solution:
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        def findmid(head, tail):
            slow = head
            fast = head
            while fast != tail and fast.next!= tail :
                slow = slow.next
                fast = fast.next.next
            return slow
        
        def helper(head, tail):
            if  head == tail: return 
            node = findmid(head, tail)
            root = TreeNode(node.val)
            root.left = helper(head, node)
            root.right = helper(node.next, tail)
            return root
            
        return helper(head, None)
```

## 8. 在二叉查找树中寻找两个节点，使它们的和为一个给定值

653\. Two Sum IV - Input is a BST (Easy)

[力扣](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/description/)

```html
Input:

    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

Output: True
```

```python 
class Solution:
    def findTarget(self, root: TreeNode, k: int) -> bool:
        def searchTree(root):
            if not root:return []
            return searchTree(root.left)+[root.val]+searchTree(root.right)
        
        arr=searchTree(root)
        l,r=0,len(arr)-1
        while l<r:
            s=arr[l]+arr[r]
            if s==k:return True
            elif s>k:r-=1
            else:l+=1
        return False
```

## 9. 在二叉查找树中查找两个节点之差的最小绝对值

530\. Minimum Absolute Difference in BST (Easy)

[力扣](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/description/)

```html
Input:

   1
    \
     3
    /
   2

Output:

1
```

利用二叉查找树的中序遍历为有序的性质，计算中序遍历中临近的两个节点之差的绝对值，取最小值。

```python  
```

## 10. 寻找二叉查找树中出现次数最多的值

501\. Find Mode in Binary Search Tree (Easy)

[力扣](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/description/)

```html
   1
    \
     2
    /
   2

return [2].
```

答案可能不止一个，也就是有多个值出现的次数一样多。

```python  
```

# Trie

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/5c638d59-d4ae-4ba4-ad44-80bdc30f38dd.jpg"/> </div><br>

Trie，又称前缀树或字典树，用于判断字符串是否存在或者是否具有某种字符串前缀。

## 1. 实现一个 Trie

208\. Implement Trie (Prefix Tree) (Medium)

[力扣](https://leetcode-cn.com/problems/implement-trie-prefix-tree/description/)

```python  
```

## 2. 实现一个 Trie，用来求前缀和

677\. Map Sum Pairs (Medium)

[力扣](https://leetcode-cn.com/problems/map-sum-pairs/description/)

```html
Input: insert("apple", 3), Output: Null
Input: sum("ap"), Output: 3
Input: insert("app", 2), Output: Null
Input: sum("ap"), Output: 5
```

```python  
```
