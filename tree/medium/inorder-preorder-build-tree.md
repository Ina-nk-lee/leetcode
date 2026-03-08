## Building Tree with Inorder and Preorder Traversals
- Difficulty: medium
- [Link](https://neetcode.io/problems/binary-tree-from-preorder-and-inorder-traversal/question)

---

### Summary
- Given the inorder and preorder traversals, build a binary tree and return its root.

---

### Ideas
- All values in the tree is **unique**.
- `inorder` and `preorder` are the same length.
- While inorder traversal helps distinguish left and right, a root node can be found in preorder traversal.

---

### Solution 1 (DFS with hashmap)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        in_map = {v: i for i, v in enumerate(inorder)}
        i = 0
        def dfs(l, r):
            if l > r:
                return None
            nonlocal in_map, i
            node = TreeNode(preorder[i])
            mid = in_map[preorder[i]]
            i += 1
            node.left = dfs(l, mid - 1)
            node.right = dfs(mid + 1, r)
            return node
        return dfs(0, len(preorder) - 1)
```
- `in_map` maps each value in `inorder` to its index.
- `dfs` builds a tree based on the range between `l` and `r` in `inorder`.
- It starts by taking root from `preorder`.
- To determine `root.left` and `root.right`, it divides `inorder` into two sides using `preorder[i]` as a boundary.
---

### Solution 2 (DFS)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        pre_i = 0
        in_i = 0
        def dfs(lim):
            nonlocal pre_i, in_i
            if pre_i >= len(preorder):
                return None
            if inorder[in_i] == lim:
                in_i += 1
                return None
            v = preorder[pre_i]
            pre_i += 1
            node = TreeNode(v)
            node.left = dfs(v)
            node.right = dfs(lim)
            return node
        return dfs(float("inf"))
```
- `dfs` builds a tree with a given `lim`, which works as a boundary in `inorder`.
- Following each value in `preorder`, it determines `root.left` and `root.right` with `inorder`.
- If `inorder[in_i]` reaches `lim`, it returns `None` and moves on to a next node in `inorder`.


### Thoughts

- For the **hashmap solution**, the time complexity is **`O(n)`** and the space complexity is **`O(n)`** because of hashmap and recursion.
- For the **non-hashmap solution**, the time complexity is also **`O(n)`** and the space complexity is **`O(n)`** because of recursion.
- **Utilizing `nonlocal` is essential** to manipulate variables inside and outside a recursive function.
- **Inorder traversal** goes left - root - right, whereas **preorder traversal** goes root - left - right.
- By combining both traversals, we can reconstruct the binary tree.
 - **Inorder traversal** determines `root.left` and `root.right`.
 - **Preorder traversal** tells us which node is the next `root` to build.