## Remove Node From the End of the List

- Difficulty: Medium
- [Link](https://neetcode.io/problems/remove-node-from-end-of-linked-list/question?list=blind75)

---

### Summary
- Given a singly linked list `head`, remove the `n`th element from the end and return the head of the list.

---

### Ideas
- First, locating the `n`th element is necessary.
- Second, we need to reach the `n`th element while storing its previous node.
- Third, connect the previous node's `.next` to the target node's `.next`.

---

### Solution

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        l = 0
        curr = head
        while curr:
            curr = curr.next
            l += 1
        target = l - n
        curr = head
        prev = None
        i = 0
        while i < target:
            prev = curr
            curr = curr.next
            i += 1
        if prev == None:
            return curr.next
        prev.next = curr.next
        curr = None
        return head
```

- The first loop calculates the length of the linked list.
- The second loop finds the `target` node that needs to be removed.
- After finding it, it sets `prev.next` as `curr.next`, to bypass `curr`.
- If there's no `prev`, it returns `curr.next` directly.

---

### Thoughts

- The time complexity is **`O(n)`** where `n` is the number of nodes.
- The space complexity is **`O(1)`** as no additional space is used.
- **Storing nodes that need to be accessed** is a fundamental step in linked list manipulation.
- **Visualizing a linked list** can help manipulate it efficiently with less confusion.
- **Managing the first and the last pointers** of a linked list is crucial to avoid an infinite loop.
- The condition of a loop also needs to be set properly to avoid referring to a `None` object.
- Need to handle edge cases thoroughly in linked list problems.