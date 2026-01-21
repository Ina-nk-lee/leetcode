## Cycle Detection in Linked List

- Difficulty: Easy
- [Link](https://neetcode.io/problems/linked-list-cycle-detection/)

---

### Summary

- Given a singly linked list `head`, return `true` if there's a cycle in it. If not, return `false`.

---

### Ideas

- Since the list is singly linked, we must visit **every node** to detect a cycle.
- We can utilize **two pointers** -- one that moves one step at a time, the other that moves two steps at a time (Floyd's Cycle Detection Algorithm).
- If they eventually meet, it shows that there is a cycle in the list.

---

### Solution

```python

class Solution1:
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        curr1 = head
        curr2 = head
        while curr2 != None and curr2.next != None:
            curr1 = curr1.next
            curr2 = curr2.next.next
            if curr1 == curr2:
                return True
        return False
```
- Loop until `curr1` meets `curr2` or `curr2`, `curr2.next` reaches `null`.
- At the end, return `false`, since it means there's no cycle.
---

### Thoughts

- I first thought of using brute force with a **set** to track visited values.
- However, setting the **edge case** and the **loop condition** could be tricky.
- Using **slow/fast pointers** is a good example of how to detect **a cycle or a repetition**.
- Time complexity is **O(n)** and space complexity is **O(1)**.