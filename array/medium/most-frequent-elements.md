## Most Frequent Elements in Array

- Difficulty: Medium
- [Link](https://neetcode.io/problems/top-k-elements-in-list/)

---

### Summary

- Given an array of integers `nums` and an integer `k`, return the `k` most frequent elements.

---

### Ideas

- We need to visit all the elements in `nums` to track frequencies.
- Hashmap can minimize the time complexity.
- Heap is useful to track the biggest values.

---

### Solution 1 (`O(nlogn)`)

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

### Solution 2 (`O(n + klogn)`)

```python  
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        d = defaultdict(int)
        for num in nums:
            d[num] += 1
        
        pairs = []
        for key, val in d.items():
            pairs.append((-val, key))

        heapq.heapify(pairs)
        result = []
        for _ in range(k):
            result.append(heapq.heappop(pairs)[1])

        return result

```
- `d` is a dictionary with `num` as key and frequency as a value.
- `pairs` is a tuple array that has `(-value, key)` from `d`.
- `-value` is necessary to pop a number with the biggest frequency because heap only supports `min-heap`.
- After heapifying `pairs`, it pops `k` most frequently appeared values from it.

### Solution 3 (`O(n)`)

```python  
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        d = defaultdict(int)
        for num in nums:
            d[num] += 1        

        freq = [[] for _ in range(len(nums) + 1)]
        for key, val in d.items():
            freq[val].append(key)
        
        result = []
        for i in range(len(freq) - 1, 0, -1):
            for j in freq[i]:
                result.append(j)
                if len(result) == k:
                    return result

```
- `d` is a dictionary with `num` as key and frequency as a value.
- When a non-existing key in `d` is accessed, `defaultdict(int)` automatically creates the key with a default value of `0`.
- `freq` is a bucket sort array that has frequency as an index and an array of numbers appeared in `nums` as a value.
- `freq = [[] for _ in range(len(nums) + 1)]` initializes `freq` with `[]` as default values.
- `len(nums) + 1` ensures that the frequency can be big as the size of `nums`.
- `for i in range(len(freq) - 1, 0, -1)` iterates `freq` in a descending order from the biggest index.
- Once `result` has the `k` number of numbers, it's returned.

### Thoughts

- For the **solution 1**, the time complexity is **`O(n log n)`**, not `O(n)`, because of the sorting step(`O(nlogn)`), and the space complexity is **`O(n)`**, which accounts for the dictionary and sorted array.
- The use of **`defaultdict()`**, **`sorted()`** with a **lambda function**, and **tuple unpacking** is helpful for clean implementation.
- For the **solution 2**, the time complexity is **`O(n + klogn)`** to traverse `nums`, create a tuple array, heapify the array, and pop `k` number of values from the heap, and the space complexity is also **`O(n)`** to create arrays and a dictionary of size `n`.
- **Heap** lets you get **min/max** repeatedly in **`O(log n)`** per pop (after O(n) heapify).
- Need to get used with **array manipulation** syntax in Python.
- For the **solution 3**, the time complexity is **`O(n)`** because counting frequencies take `O(n)` and iterating over the bucket array also takes `O(n)` in the worst case, and the space complexity is also **`O(n)`** to create arrays of size `n`.
- **Bucket sort** is effective when the **range** of possible frequencies is **bounded**.
- Need to get used with **array manipulation** syntax in Python.