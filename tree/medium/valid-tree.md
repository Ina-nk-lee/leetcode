## Valid Binary Search Tree
- Difficulty: medium
- [Link](https://neetcode.io/problems/valid-binary-search-tree/question)

---

### Summary
- Given a binary tree `root`, return `true` is `root` is a valid BST, otherwise return `false`.

---

### Ideas
- We can validate the BST by keeping a validd range`(mn, mx)` for each node.
- This can be done with recursion(DFS) or iteration(BFS).

---

### Solution 1 (DFS)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def validCheck(root: Optional[TreeNode], mn: int, mx: int) -> bool:
            if root:
                if not mn < root.val < mx:
                    return False
                else:
                    return validCheck(root.left, mn, root.val) and validCheck(root.right, root.val, mx)
            return True
        return validCheck(root, float("-inf"), float("inf")) 
```

- `validCheck` checks if the given node is valid with a given range.
- If the node `root` is valid, it checks if its subtrees are valid.
- For the left tree, the minimum value remains the same as its parent, while the maximum value becomes `root.val`.
- For the right tree, the maximum value remains the same as its parent, while the minimum value becomes `root.val`.
- `isValidBST` starts with the range -- `-inf` and `inf`.

---

### Solution 2 (BFS)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        q = deque()
        q.append((root, float("-inf"), float("inf")))
        while q:
            popped, mn, mx = q.popleft()
            if popped: 
                if not mn < popped.val < mx:
                    return False
                q.append((popped.left, mn, popped.val))
                q.append((popped.right, popped.val, mx))
        return True
```
- Starting from the range between `-inf` and `inf`, `isValidBST` checks the validity of each node.
- `q` has all the nodes in each level and their minimum and maximum values.
- For each node in a current level, it checks the validity of the node, `popped`.
- If it's valid, it adds its children to `q`.
- If it's not, it returns `false`.
- It returns `true` if it finishes the iteration without any invlid node.
---

### Thoughts
- The time complexity is **`O(n)`** for both solutions where `n` is the number of nodes in `root` since it level traverses all the nodes.
- The space complexity of solution 1 is **`O(n)`** because of the stack used for recursion.
- For solution 2, the space complexity is **`O(m)`** where `m` is the largest number of nodes on one level.
- While recursion(DFS) might be more intuitive, iteration(BFS) is more efficient in terms of space complexity.
- Using a tuple for data structures could be useful.
- The key idea is that each node must satisfy **not only its parent's condition**, but **also the full valid range passed down from its ancestors**.