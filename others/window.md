```python
class Solution:
    def minimize(self, window, timestamps: List[int]) -> int:
        left = 0
        right = 0
        mx = 0

        while right < len(timestamps):
            if timestamps[right] - timestamps[left] < window:
                if right - left > mx:
                    mx = right - left + 1
                right += 1
            else:
                left += 1

        return mx
```