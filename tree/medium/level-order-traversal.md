## Level Order Traversal
- Difficulty: medium
- [Link](https://neetcode.io/problems/level-order-traversal-of-binary-tree/question)

---

### Summary
- Given a binary tree `root`, return a level order traversal from left to right, using a nested list, where each sublist contains the value of nodes in each level.

---

### Ideas
- We can use a queue for a level order traversal easily, but grouping each level as a sublist might be tricky.

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
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        q = deque()
        q.append(root)
        res = []
        while q:
            size = len(q)
            level = []
            for _ in range(size): 
                curr = q.popleft()
                if curr:
                    level.append(curr.val)
                    q.append(curr.left)
                    q.append(curr.right)
            if level:
                res.append(level)
        return res
```

- `q` represents a queue.
- For each level, nodes currently in `q` are processed and their values are added to `level`.
- For each processed node, its children are added to `q`, which means all the nodes on the sublevel are added to `q`.
- After processing all the nodes on the level, it adds a sublist, `level`, to `res`.
- These steps are repeated until there's nothing left in `q`.

---

### Thoughts
- The time complexity is **`O(n)`** where `n` is the number of nodes in `root` since it level traverses all the nodes, and the space complexity is **`O(n)`** due to the queue and result list.
- A useful pattern for level-order traversal is to store the **queue size before processing a level**, so that **all nodes in the same level can be grouped together**.
- Using `size = len(q)` before the loop ensures that **only nodes from the current level are processed** in that iteration.