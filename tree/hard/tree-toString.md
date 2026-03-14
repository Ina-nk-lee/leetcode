## Binary Tree toString
- Difficulty: hard
- [Link](https://neetcode.io/problems/serialize-and-deserialize-binary-tree/question)

---

### Summary
- Implement functions to serialize a binary tree into string and deserialize the string back into a tree.

---

### Ideas
- Need to use a delimiter for tree values.
- Need a null marker as well so that missing children can be reconstructed correctly.
- Level order traversal is intuitive for both serialization and deserialization.

---

### Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Codec:
    # Encodes a tree to a single string.
    def serialize(self, root: Optional[TreeNode]) -> str:
        res = []
        q = deque()
        q.append(root)
        while q:
            curr = q.popleft()
            if curr:
                res.append(f"{curr.val}")
                q.append(curr.left)
                q.append(curr.right)
            else:
                res.append("n")            
            res.append(",")
        return "".join(res)

    # Decodes your encoded data to tree.
    def deserialize(self, data: str) -> Optional[TreeNode]:
        vals = data.split(",")
        if vals[0] == "n":
            return None
        root = TreeNode(int(vals[0]))
        q = deque([root])
        i = 1
        while q:
            node = q.popleft()
            if vals[i] != "n":
                node.left = TreeNode(int(vals[i]))
                q.append(node.left)
            i += 1
            if vals[i] != "n":
                node.right = TreeNode(int(vals[i]))
                q.append(node.right)
            i += 1
        return root
```

- `serialize` uses a queue, `q` to serialize `root` in the level order.
 - For each node in the tree, it adds the value to `res` and appends its left and right children to `q`.
 - If the node is `null`, it adds `n` to `res`.
 - After adding a value to `res`, it adds `,` to `res` as a delimiter.
- `deserialize` reads tree values in `data` by splitting it with `,`.
 - Using a queue, it adds nodes to `root` from `vals` in level order.
 - For each node, it adds `vals[i]` for `node.left` and `node.right`.
---

### Thoughts
- The time complexity is **`O(n)`** where `n` is the number of nodes in `root` for both functions.
- The space complexity is **`O(n)`** for both functions because the queue and the serialized values may store up to `O(n)` elements.
- Placing **delimiters** is essential for separating node values.
- **Null markers** are essential; without them, the original tree structure cannot be reconstructed uniquely.
- Using a **queue** properly for **level order traversal** is important.