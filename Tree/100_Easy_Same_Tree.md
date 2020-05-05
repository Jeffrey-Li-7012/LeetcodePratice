## 100 Same Tree -- Easy

### Description

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.



### Examples

```pseudocode
Example 1:

Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true

Example 2:

Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false

Example 3:

Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```



### Solutions

#### Approach 1 - Recursion(Python版)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        # 如果p和q均为None/Null, 则视为相同，返回True
        if p is None and q is None:
            return True
        
		# 如果q和q其中一个为None/Null,则不同，返回False
        if p is None or q is None:
            return False

        # 基于前两步的判断之后，如果p和q存储的val不同，则不同，返回False
        if p.val != q.val:
            return False

        # 完成前面的判断后，说明现在p和q均不为空且值相等，应该在p，q的左右子树上进行递归调用（注意，逻辑连接词应该用and）
        return self.isSameTree(p.right,q.right) and self.isSameTree(p.left,q.left)
    
        
```

#### **Complexity Analysis**

- Time complexity : $O(N)$ , where N is a number of nodes in the tree, since one visits each node exactly once.
- Space complexity: $O(log(N))$  in the best case of completely balanced and $O(N)$ in the worst case of completely unbalanced tree, to keep a recursion stack.



#### Approach 2 - Iteration(Python版)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        # 单独检测两个node是否符合要求的函数
        def check(q,p):
            if p is None and q is None:
                return True
            if p is None or q is None:
                return False
            if p.val != q.val:
                return False
            
            return True
        
        # 一个用来存储待检测node pair的队列
        queue = [(p,q)]
        while queue:
            node1,node2 = queue.pop(0)
            # 调用check函数对取出来的node pair进行检测，如果不满足要求直接返回False
            if not check(node1,node2):
                return False
            # 如果当前取出来的node pair符合要求，且不为None，则把他们的对应左右child node分别形成node pair加入到队列中
            if node1:
                queue.append((node1.left,node2.left))
                queue.append((node1.right,node2.right))
                
        # 到整个queue都pop为空位置也没有return False，则这两个tree一定是same的
        return True
            
        
```

