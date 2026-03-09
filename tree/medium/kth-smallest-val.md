## k-th Smallest Node in Binary Search Tree
- Difficulty: medium
- [Link](https://neetcode.io/problems/kth-smallest-integer-in-bst/)

---

### Summary
- Given the `root` of a BST, find the `k`th smallest value.

---

### Ideas
- Inorder traversals is helpful in this case since it visits nodes in ascending order of their values.

---

### Solution (DFS)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        ct = 0
        res = 0
        def helper(node):
            nonlocal ct, res
            if not node:
                return
            helper(node.left)
            ct += 1
            if ct == k:
                res = node.val
                return
            helper(node.right)
        helper(root)
        return res
```
- `ct` counts how many nodes have been visited in inorder traversal.
- `helper` traverses `root` inorder, increasing `ct` by `1` every node.
- Once it finds the `k`th smallest node, it saves its value to `res` and return immediately.
---


### Thoughts

- The time complexity is **`O(n)`** in the worst case, whereas the space complexity is **`O(h)`** where `h` is the height of the tree (that can be big as `n`) because of recursion stack.
- The key idea is that inorder traversal of a BST visits nodes in sorted order.
- Even though the traversal is **recursive**, the answer is determined **by the visitation order**, not by comparing subtree sizes.
- **Utilizing `nonlocal` variables** that need to be **updated across recursive calls** can be useful in recursive solutions.