## Binary Tree Maximum Path Sum
- Difficulty: hard
- [Link](https://neetcode.io/problems/binary-tree-maximum-path-sum/question)

---

### Summary
- Given a non empty binary tree `root`, return the maximum path sum of any non-empty path.

---

### Ideas
- Rather than thinking about a whole tree, we need to reduce the problem to a smaller version -- a single node.
- We need a recursive function that returns the maximum path sum of a node that can be extended through or from the current node.
 - This can return a path from its left, or a path from its right, or a node itself.
 - However, it cannot return a path from both left and right children at the same time, because it is a closed path that cannot be extended from/through `node` to its parent.
- At the same time, we need to store a maximum value of the entire `root` in a nonlocal variable.

---

### Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        mx = float("-inf")
        def getMaxUsablePath(node):
            nonlocal mx
            if not node:
                return 0
            l = getMaxUsablePath(node.left)
            m = node.val
            r = getMaxUsablePath(node.right)
            if l + m + r > mx:
                mx = l + m + r
            return max(m, l + m, r + m, 0)
        getMaxUsablePath(root)
        return mx
```

- `getMaxUsablePath` returns a maximum path sum of `node` that can be extended beyond `node`.
- `mx` stores the maximum path sum found **anywhere in the tree**.
- If `node` is `None`, it returns `0`.
- If not, it gets maximum path sums of `node.left` and `node.right`.
- `mx` gets updated if `l + m + r` is bigger than its current value. 
- Because it needs to return a maximum path sum of `node` that **can be extended beyond `node`**, it returns the highest value among `m`, a max path sum from the left (`l + m`), a max path sum from the right(`r + m`), and `0` (because we don't want to return a negative value that decreases the path sum). 
 - `l + m + r` cannot be passed because the path cannot be extended beyond `node`.
- `maxPathSum` returns `mx`.

---

### Thoughts
- The time complexity is **`O(n)`** where `n` is the number of nodes in `root`.
- The space complexity is **`O(h)`** where `h` is the height of `root` because of the recursion stack.
- **Distinguishing `mx` and the return value of `getMaxUsablePath` that is passed to a parent node** is tricky.
- They serve different purposes, so separating them clearly is the key to solving the problem.
- A **path doesn't need to pass through the root**; it could be **anywhere** in the tree.
- Understanding the **definition of path** is necessary to solve the problem.