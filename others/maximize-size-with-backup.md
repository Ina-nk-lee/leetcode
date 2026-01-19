```python
class Solution:
    def max_size_backup(self, sizes: List[int]) -> int:
        sorted_sizes = sorted(sizes)
        total = 0
        for i in range(len(sorted_sizes)):
            if i % 2 == 1:
                total = total + sorted_sizes[i]
        return total

```