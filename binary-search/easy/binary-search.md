## Binary Search

- Difficulty: Easy
- [Link](https://neetcode.io/problems/binary-search/question?list=neetcode150)

---

### Summary

- Given an array `nums` that is sorted in an ascending order with unique numbers, find `target` within it.
- Return the index of `target` if it exists. If not, return `-1`.
- The time complexity must be `O(logn)`.

---

### Ideas

- First, in order to follow the time complexity limit, **`O(logn)`**, we cannot iterate through the entire `nums`.
- Since `num` is already sorted, we can utilize **binary search** to find `target` and achieve `O(logn)` in time.
- Both iteration and recursion methods are available.

---

### Solution 1

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        def binary_search(low, mid, high, nums, target):
            if low > high:
                return -1
            if target == nums[mid]:
                return mid
            if target < nums[mid]:
                new_high = mid - 1
                return binary_search(low, low + ((new_high - low) // 2), new_high, nums, target)
            if target > nums[mid]:
                new_low = mid + 1
                return binary_search(new_low, new_low + ((high - new_low) // 2), high, nums, target)
        
        return binary_search(0, len(nums) // 2, len(nums) - 1, nums, target)
```

- `binary_search` is a recursive function to find `target`.
- It searches `target` by splitting the array into two intervals by `mid`.
- By passing `low` and `high` indices in `nums`, that indicate the current range to search, we can locate `target` recursively.
- If `low` exceeds `high`, it means `target` is not found. Return `-1`.
- If `nums[mid]` equals `target`, return the index.
- Otherwise, recurse into either left or right half depending on whether `target` is smaller or larger than `nums[mid]`.

### Solution 2

```python
class Solution:
        def search(self, nums: List[int], target: int) -> int:
            mid = len(nums) // 2
            low = 0
            high = len(nums) - 1
            while low < high:
                if target == nums[mid]:
                    return mid
                if target < nums[mid]:
                    high = mid - 1
                    mid = (high - low) // 2

                else:
                    low = mid + 1
                    mid = low + (high - low) // 2
            return -1

```

- This version performs the search **iteratively**.
- It narrows the search range using two pointers `low` and `high`.
- Each loop recalculates the midpoint and compares `nums[mid]` with `target`.
---

### Thoughts

- I remembered the **concept** from CPSC 221, but struggled with exact **index updates** (`low`, `mid`, `high`).
- Recursive and iterative approaches are both valid.
- **Binary Search** is useful anytime a sorted list and `O(logn)` constraint are involved.