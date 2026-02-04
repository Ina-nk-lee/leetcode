## Most Frequent Elements in Array

- Difficulty: Medium
- [Link](https://neetcode.io/problems/top-k-elements-in-list/)

---

### Summary

- Given an array consists of integers and an integer `k`, find `k` most frequently appeared numbers within the array.

---

### Ideas

- We need to visit all the elements in `nums` to track frequencies.
- Hashmap can minimize the time complexity.

---

### Solution

```python  
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        d = defaultdict(int)
        for num in nums:
            d[num] += 1
        
        arr = sorted(d.items(), key = lambda item : item[1], reverse = True)
        result = []
        i = 0
        while i < k:
            result.append(arr[i][0])
            i += 1
        return result

```
- `d` is a dictionary with `num` as key and frequency as a value.
- `arr` is an array with `(key, frequency)` tuples, sorted by `frequency` in a descending order.
- The while loop adds up to `k`th frequently appeared numbers to `result`.
---

### Thoughts

- The time complexity is **`O(n log n)`**, not `O(n)`, because of the sorting step.
- The space complexity is **`O(n)`**, which accounts for the dictionary and sorted array.
- The use of **`defaultdict()`**, **`sorted()`** with a **lambda function**, and **tuple unpacking** is helpful for clean implementation.