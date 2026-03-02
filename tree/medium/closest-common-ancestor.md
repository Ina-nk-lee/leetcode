## Closest Common Ancester

- Difficulty: Easy
- [Link](https://neetcode.io/problems/lowest-common-ancestor-in-binary-search-tree/history)

---

### Summary

- Given a binary search tree `root` and its subtrees `p` and `q`, find the lowest ancestrr tree node of `p` and `q`.

---

### Ideas

- Since it is a binary search tree, we can find `p` and `q` with time complexity of `O(h)`.
- `p` and `q` are both on the left or the right of `root`, or not.

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
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        curr = root
        while curr:
            if p.val < curr.val and q.val < curr.val:
                curr = curr.left
            elif p.val > curr.val and q.val > curr.val:
                curr = curr.right
            else:
                return curr
```

- There are 3 cases for `p` and `q`.
 1. They are on the left, which means we need to go further down the tree.
 2. They are on the right, which means we need to go further down the tree.
 3. They split (or one equals the current node), which makes `curr` the closest ancestor.

---

### Thoughts

- For the **iterative solution**, time complexity is **O(h)**, and space complexity is **O(1)**, because it iterates maximum `h` times.
- **Categorizing possible cases** is necessary to solve technical problems efficiently.
- In a **BST**, **comparing values directly** tells us which direction to move, which simplifies the logic significantly.
- **Dividinig a problem into well-defined** cases can make reasoning much clearer and more structured.