```python
class Solution:
    def minimize(self, nums: List[int]) -> List[int]:
        best = []
        for i in range(max(nums) + 1):
            best[i] = i
        exist = set(nums)

        for i in range(max(nums) + 1):
            if i not in exist:
                continue
            step = i
            while step <= max(nums):
                if best[step] > num:
                    best[step] = num
                step = step + step

        total = 0
        for val in nums:
            total = total + best[val] 

        return total
```