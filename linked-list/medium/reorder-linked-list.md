## Linked List Reordered

- Difficulty: Medium
- [Link](https://neetcode.io/problems/reorder-linked-list/question)

---

### Summary

- Given a singly linked list `head`, reorder it.
- For example, `[0, 1, 2, 3, 4, 5]` should be reordered to `[0, 5, 1, 4, 2 ,3]`.

---

### Ideas

- First, to reorder the list, we need to visit **every node** in it.
- Reversing the list could help, because the second half of the list is reversed in the reordered list.
- Basically, the reversed second half is merged into the first half, by alternating nodes.

---

### Solution

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        slow = head
        fast = head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        prev = None
        r = slow.next
        slow.next = None
        while r:
            temp = r.next
            r.next = prev
            prev = r
            r = temp
        l = head
        r = prev
        while r:
            temp_l = l.next
            temp_r = r.next
            l.next = r
            r.next = temp_l
            l = temp_l
            r = temp_r
```

- The first loop finds the half point of the given linked list, by placing `slow` there.
- After finding `slow`, the linked list is cut into half.
- The second loop reverses the second half of the list.
- The third loop merges the two lists by connecting the nodes in turn.
---

### Thoughts

- The time complexity is **`O(n)`** where `n` is the number of nodes.
- The space complexity is **`O(1)`** as no additional space is used.
- **Visualizing a linked list** can help manipulate it efficiently with less confusion.
- **Managing the first and the last pointers** of a linked list is crucial to avoid an infinite loop.
- The condition of a loop also needs to be set properly to avoid refering to a `None` object.