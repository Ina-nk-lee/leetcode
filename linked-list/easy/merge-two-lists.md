## Merge Two Linked List

- Difficulty: Easy
- [Link](https://neetcode.io/problems/merge-two-sorted-linked-lists/)

---

### Summary

- Given two sorted singly linked lists `list1` and `list2`, merge them into one sorted list and return its head.

---

### Ideas

- Since both lists are sorted and singly linked, we must visit **every node** in order.
- To construct the merged list, we track the head of the new list, and compare `list1` and `list2` one node at a time.
- At each step, we attach the smaller node to the merged list.
- We can solve this using either iteration or recursion.

---

### Solution 1

```python

class Solution1:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        newhead = None
        curr = None

        if list1 == None:
            return list2
        if list2 == None:
            return list1

        if list1.val < list2.val:
            newhead = list1
            curr = newhead
            list1 = list1.next
        else:
            newhead = list2
            curr = newhead
            list2 = list2.next

        while list1 != None and list2 != None:
            if list1.val < list2.val:
                curr.next = list1
                list1 = list1.next
            else:
                curr.next = list2
                list2 = list2.next
            curr = curr.next
        
        if list1 == None and list2 != None:
            curr.next = list2
        if list1 != None and list2 == None:
            curr.next = list1

        return newhead
```

- If either list is empty, return the other.
- Initialize `newhead` to the smaller of the two starting nodes.
- Use a pointer `curr` to build the merged list.
- At the end, attach the remaining non-empty list.

### Solution 2

```python

class Solution2:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        if list1 == None:
            return list2
        if list2 == None:
            return list1
        if list1.val < list2.val:
            newhead1 = list1.next

            list1.next = self.mergeTwoLists(newhead1, list2)
            return list1
        else:
            newhead2 = list2.next

            list2.next = self.mergeTwoLists(newhead2, list1)
            return list2  
```

- `mergeTwoLists` is a recursive function to merge the two given list.
- The base case is when either list is empty — return the other.
- Whichever smaller value comes first, and then it calls `mergeTwoLists` to decide the next node.
- This builds the merged list from the front using head recursion.
- Finally, the function returns `list1` or `list2` depending on where the smallest value is.

---

### Thoughts

- I first solved the problem using **iteration**, which required more setup (handling head and tail).
- Later, I revisited the problem and wrote a **recursive solution**, which is more concise.
- This is a good example of how head recursion simplifies pointer logic in linked lists.
- Time complexity is **O(n + m)** and space complexity is **O(n + m)** due to recursive stack.
- Could have used a **dummy node** as a head of the merged list and returned `dummy.next` to make the code more concise.