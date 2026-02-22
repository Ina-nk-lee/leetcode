## Reverse Linked List

- Difficulty: Easy
- [Link](https://neetcode.io/problems/reverse-a-linked-list/question)

---

### Summary

- Given a singly linked list `head`, return the head of the reversed list.

---

### Ideas

- First, to flip the list, we need to visit **every node** in it.
- Since it is a singly linked list, the reversed list **starts from the end** of the original list goes to the very first node.
- Also, we can only reference the next node from the current one.
- Therefore, a simple **iteration** or a **tail recursion** doesn't work in this case.
- We need to utilize **head recursion** so that we can attach nodes while returning from the recursive calls.

---

### Solution 1 (Recursive)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None or head.next == None:
            return head
        else:
            new_head = self.reverseList(head.next)
            head.next.next = head
            head.next = None
            return new_head
```

- `reverseList` is a recursive function to reverse the given list, `head`.
- It goes all the way to the last value, which becomes the new head.
- `new_head` represents the head of the reversed list.
- After the recursive call returns, we attach the current node after its next node, which is the last value of the reversed list. (We must not use `new_head` because `new_head` is a reversed linked list itself, not the next node)
- And then, we remove `.next` of the current node to avoid cycles.
- Finally, the function returns `new_head`.
---

### Solution 2 (Iterative)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head
        while cur:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
        return prev
```

- It stores a previous node in `prev` to conect it to `cur`.
- `temp` stores the next value.
- It moves `prev` and `cur` to the next nodes.
- It iterates until `cur` reaches `lastnode.next`, therefore, it returns `prev`.

---

### Thoughts

- At first, I could only think of tail recursion and forgot that head recursion was an option.
- I also tried an iterative approach, but it did not work out immediately, which got me stuck.
- Looking back at a previous solution helped me recall this pattern.
- Head recursion is useful when we need to process nodes in reverse order, because the recursive calls reach the end first and work backward, and we manipulate it afterwards.
- Time complexity of the recursive solution is **`O(n)`** where `n` is the number of nodes in `nums`, and space complexity is **`O(n)`**.
- Time complexity of the iterative solution is **`O(n)`**, and space complexity is **`O(1)`**.