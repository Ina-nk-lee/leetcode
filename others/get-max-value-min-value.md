```python
class Solution:
    def get_max_min(self, reqs: int, nums: List[int]) -> int:
        max_val = max(nums)
        freq = [0] * (max_val + 1)

        for v in nums:
            freq[v] = freq[v] + 1

        total = 0
        cur_max = max_val
        min_val = min(nums)

        for i in range(reqs):
            while freq[cur_max] == 0 and cur_max > 0:
                cur_max -= 1
            
            if cur_max == 0:
                break

            total += cur_max

            freq[cur_max] -= 1
            if cur_max - 1 >= 0:
                freq[cur_max - 1] += 1

            while max_val >= min_val and freq[min_val] == 0:
                min_val += 1

            total += min_val
 
        return total
```
