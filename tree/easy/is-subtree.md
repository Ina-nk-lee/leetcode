## Is Subtree

- Difficulty: Easy
- [Link](https://neetcode.io/problems/subtree-of-a-binary-tree/)

---

### Summary

- Given two binary trees `root`, `subRoot`, check if `root` has a subtree that is the same structure and node values of `subRoot`.

---

### Ideas

- We must visit **each node** in both trees to check both structure and values.
- After checking the parent node, its `left` and `right` node also need to be checked to see if they're the **same** with `subRoot`.
- **Recursion** helps compare two trees and their subtrees.
- **Queue** also can be used.

---

### Solution 1

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:   
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        def isSameTree(p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
            if p == None and q == None:
                return True
            if p == None or q == None:
                return False
            if p.val == q.val:
                return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
            else:
                return False 

        if root == None and subRoot == None:
            return True
        if root == None or subRoot == None:
            return False
        if isSameTree(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
```
- It passes the root and its child nodes with `subRoot` to `isSameTree`.
- If one of them matches, it returns `True`.
- `isSameTree` is a recursive function to compare `p` and `q`.

### Solution 2

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:   
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:     
        def isSameTree(p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
            queue = deque([(p, q)])
            while queue:
                curr_p, curr_q = queue.popleft()
                if curr_p == None and curr_q == None:
                    continue
                if curr_p == None or curr_q == None:
                    return False
                if curr_p.val == curr_q.val:
                    queue.append((curr_p.left, curr_q.left))
                    queue.append((curr_p.right, curr_q.right))
                else:
                    return False
            return True
                

        queue = deque([root])
        while queue:
            curr = queue.popleft()
            if isSameTree(curr, subRoot):
                return True
            if curr:
                queue.append(curr.left)
                queue.append(curr.right)
        return False
```
- It passes the root and its child nodes with `subRoot` to `isSameTree`.
- If one of them matches, it returns `True`.
- `isSameTree` is a iterative function to compare `p` and `q` using queue.
---

### Thoughts

- while **Recursion** is more straightforward and intuitive for tree problems, **iterative solution** with a queue is also efficient.
- For the **recursive solution**, time complexity is **O(n * m)**, where `n` is the number of nodes in `root` and `m` is the number of nodes in `subRoot`. Space complexity is **O(h_root + h_subroot)**, where `h_root` is the height of `root` and `h_subroot` is that of `subRoot`.
- For the **iterative solution**, time complexity is **O(n * m)**, and space complexity is **O(n + m)**, due to the use of `deque` storing up to `n` nodes during traversal and `m` nodes during comparison.
- Using a **tuple-based queue** helps keep the code clean and makes the node-pair comparisons explicit.