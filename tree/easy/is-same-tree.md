## Is Same Tree

- Difficulty: Easy
- [Link](https://neetcode.io/problems/same-binary-tree/)

---

### Summary

- Given two binary trees `p`, `q`, check if they are structurally identical and have the same node values.

---

### Ideas

- We must visit **each node** in both trees to check both structure and values.
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
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if p == None and q == None:
            return True
        if p == None or q == None:
            return False
        return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```
- `isSameTree` is a recursive function to compare `p` and `q`.
- If only one of the trees is empty it returns `false`.
- If not, it compares the value of the roots and their children by passing them to `isSameTree`.

### Solution 2

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        queue = deque([(p, q)])

        while queue:
            p_curr, q_curr = queue.popleft()

            if not p_curr and not q_curr:
                continue
            if not p_curr or not q_curr:
                return False
            if p_curr.val != q_curr.val:
                return False
            queue.append((p_curr.left, q_curr.left))
            queue.append((p_curr.right, q_curr.right))
        
        return True
```
- Starting from the root of `p` and `q`, it compares their values.
- Nodes are added to the queue in BFS order (level by level, from left to right).
- If only one of the trees is `null`, it returns `false`.
- Finally, it returns `true` if it escapes the loop.
---

### Thoughts

- while **Recursion** is more straightforward and intuitive for tree problems, **iterative solution** with a queue is also efficient.
- For the **recursive solution**, time complexity is **O(n)**. Space complexity is **O(h)**, where h is the height of the tree (O(n) in the worst case).
- For the **iterative solution**, time complexity is **O(n)**, and space complexity is **O(n)**, because the queue may store up to **n/2 nodes** at the bottom level in a **complete binary tree**.
- Using a **tuple-based queue** helps keep the code clean and makes the node-pair comparisons explicit.
- Also, an **empty queue** (`while queue:` ends) is different from a queue **containing `None` values** in Python, which must be explicitly checked in traversal logic.
- In Python, `None` is an object without any value.