## Merge Multiple Linked Lists

- Difficulty: Medium
- [Link](https://neetcode.io/problems/merge-k-sorted-linked-lists/question)

---

### Summary
- Given a list of sorted singly linked lists, return a sorted, merged list with all the linked lists.

---

### Ideas
- We could look at the head of each list and find a node with a minimum value, and update the head to `head.next`.
- Another way is to merge `i`th list with `i - 1`th list until `i < len(lists)`.

---

### Solution 1 (Merging two lists at a time)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:    
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        def mergeTwo(l: ListNode, r: ListNode) -> ListNode:
            dummy = ListNode(0)
            curr = dummy
            while l and r:
                if l.val < r.val:
                    curr.next = l
                    l = l.next
                else:
                    curr.next = r
                    r = r.next
                curr = curr.next
            if not l:
                curr.next = r
            elif not r:
                curr.next = l
            return dummy.next
        if len(lists) == 0:
            return None
        i = 1
        while i < len(lists):
            lists[i] = mergeTwo(lists[i], lists[i - 1])
            i += 1
        return lists[len(lists) - 1]
```

- `mergeTwo` merges given two sorted lists in an ascending order.
- `mergeKLists` merges `k` number of lists one by one using `mergeTwo`.

---

### Solution 2 (Merging multiple lists using heap)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:    
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        class Wrapper:
            def __init__(self, node):
                self.node = node
            def __lt__(self, other):
                return self.node.val < other.node.val
        if not lists:
            return None
        heap = []
        for l in lists:
            if l:
                heapq.heappush(heap, Wrapper(l))
        dummy = ListNode(0)
        curr = dummy
        while heap:
            popped = heapq.heappop(heap).node
            curr.next = popped
            curr = curr.next
            if popped.next:
                heapq.heappush(heap, Wrapper(popped.next))
        return dummy.next
```

- `Wrapper` wraps `ListNode` in order to make it usable in heap by overriding default `__lt__`.
- `mergeKLists` pushes all the heads of lists into `heap`.
- The while loop takes the minimum node from `heap` and add it to `curr`.
- If the minimum node has `.next`, it pushes it to `heap`.

---

### Thoughts

- The time complexity of solution 1 is **`O(n * k)`** where `n` is the total number of nodes in `lists` and `k` is the number of lists in `lists`, because a merged result is repeatedly merged up to `k - 1` times.
- The space complexity is **`O(1)`** as no additional space is used.
- The time complexity of solution 2 is **`O(n * logk)`** where `n` is the total number of nodes in `lists` and `k` is the number of lists, because it pushes and pops `n` nodes to heap, which take `logk` each time as there are always less than `k` nodes in heap.
- The space complexity is **`O(k)`** for heap.
- **Using dummy node** is essential to handle edge cases without writing excessive code.
- **Overriding default `__lt__`** is necessary to use heap for non-integer values.