## Sum of 3 Integers

- Difficulty: Medium
- [Link](https://neetcode.io/problems/three-integer-sum/question)

---

### Summary

- Given an array of integers `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` where the sum of them is `0`, and `i`, `j`, `k` are unique.
---

### Ideas

- It's unavoidable to check all the elements in `nums`.
- Probably need to sort `nums` in order to handle duplicate triplets.

---

### Solution 1 (`O(n^2)`)

```python
class Solution:  
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        d = defaultdict(int)
        for num in nums:
            d[num] += 1
        result = []
        n = sorted(nums)
        for i, v in enumerate(n):
            d[v] -= 1
            if i > 0 and n[i] == n[i - 1]:
                continue
            for j in range(i + 1, len(n)):
                d[n[j]] -= 1
                if j - 1 > i and n[j] == n[j - 1]:
                    continue
                total = -(v + n[j])
                if total in d and d[total] > 0:
                    result.append([v, n[j], total])  
            for j in range(i + 1, len(n)):
                d[n[j]] += 1
        return result
```
- `d` stores each number and its count in `nums` as a key-value pair in a dictionary.
- `n` is sorted `nums` for handling duplicate numbers efficiently.
- In the outer loop, `i` increments until its value, `nums[i]`, becomes a new number in `nums` to avoid duplicates.
- Once that's done, it decrements `nums[i]`'s count in `d`, since it means the number is taken,
- `j` also increments until it finds a new number unless `j` is next to `i`, because we allow two duplicate numbers in a triplet.
- For each `nums[j]`, we look up `d` to find a target, which is `-(nums[i] + nums[j])`, if there's remaining count.
- If if finds a target, it adds the triplet to `result`.
- After the `j` iteration, we restore the count that was decremented by `j` for a next iteration.

### Solution 2 (`O(n^2)`)

```python  
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        result = []
        for i in range(len(nums)):
            if nums[i] > 0:
                return result
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            l = i + 1
            r = len(nums) - 1
            while l < r:
                s = nums[i] + nums[l] + nums[r]
                if s < 0:
                    l += 1
                elif s > 0:
                    r -= 1
                else:
                    result.append([nums[i], nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while l < r and nums[l] == nums[l - 1]:
                        l += 1
        return result
```
- `nums` is sorted to start from the smallest number in the array.
- If `nums[i] > 0`, it means there is no triplet that can be formed, since `i < l < r`, which is also `nums[i] <= nums[l] < nums[r]`.
- `i` increments until its value, `nums[i]`, becomes a new number in `nums` to avoid duplicates.
- `l` and `r` starts from the right next index of `i`.
- If `s < 0`, it means we need a bigger value. So we increment `l` by one. (`r` can't be incremented because it started from the biggest value.)
- If `s > 0`, it means we need a smaller value. So we decrement `r` by one. (`l` can't be decremented because it started from the smallest value.)
- If `s == 0`, it adds the triplet to `result` and increase `l` by 1 and decrease `r` by one, because `i` is fixed in the inner loop, so `nums[l]` and `nums[r]` need to be new numbers to find a new triplet.
- `l` increases until it finds a new distinct value.



### Thoughts
- The key pattern is **sort + two pointers**. Sorting makes the sum change simple: if the sum is too small, move `l++`. If it's too big, move `r--`.
- Duplication usually matters in two places:
 - skip duplicates for `i` (outer loop)
 - after finding `s==0`, skip duplicates for `l` (or `r`) before continuing.
- For the **solution 1**, the time complexity is **`O(n^2)`** where `n` is the length of `nums` because there's an inner loop inside the outer loop. The space complexity is **`O(n)`** because of a hashmap and a sorted array.
- For the **solution 2**, the time complexity is **`O(n^2)`** because there's an inner loop inside the outer loop. The space complexity is **`O(1)`** because it uses the existing array, `nums`.
- Both solutions are `O(n^2)` in time, but solution 2 is the more intuitive approaach, so it's easier to implement wiout bugs.
- This problem was challenging to me because the index manipulation was very confusing to me.
