## Invert Binary Tree

- Difficulty: Easy
- [Link](https://neetcode.io/problems/invert-a-binary-tree)

---

### Summary

- Given a binary tree `root`, return its inverted tree.

---

### Ideas

- We must visit **each node** in the tree to invert it and return **its mirrored version**.
- **Recursion** helps us invert the left and right subtrees before attaching them.
- **Queue** also can be used.

---

### Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution1:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root == None:
            return None
        else:
            temp = root.left
            root.left = self.invertTree(root.right)
            root.right = self.invertTree(temp)
            return root
```
- `invertTree` is a recursive function to invert `root`.
- If `root` is empty, it returns `null`.
- If not, it inverts its children by passing them to `invertTree`.

```python
from collections import deque

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution2:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root == None:
            return None
        else:
            queue = deque([root])
            
            while queue:
                curr = queue.popleft()
                temp = curr.left
                curr.left = curr.right
                curr.right = temp
                if curr.left != None:
                    queue.append(curr.left)
                if curr.right != None:
                    queue.append(curr.right)
            return root
```
- If `root` is empty, it returns `null`.
- Starting from `root`, it inverts its children.
- Nodes are added to the queue in BFS order (level by level, from left to right).
- Finally, it returns inverted `root` after flipping the entire tree.
---

### Thoughts

- **Recursion** is especially helpful for tree problems like this, though an **iterative solution** with a queue is also efficient.
- For the **recursive solution**, time complexity is **O(n)**. Space complexity is **O(h)**, where h is the height of the tree (O(n) in the worst case).
- For the **iterative solution**, time complexity is **O(n)**, and space complexity is **O(n)**, because the queue may store up to **n/2 nodes** at the bottom level in a **complete binary tree**. 