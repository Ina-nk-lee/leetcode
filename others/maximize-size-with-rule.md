```python
class Solution:
    def max_size(self, sizes: List[int], rules: List[List[int]]) -> int:
        sizes_copy = sizes.copy()
        total_a = 0
        for rule in rules:
            if sizes_copy[rule[0]] > sizes_copy[rule[1]]:
                total_a = total_a + sizes_copy[rule[0]]
                sizes_copy[rule[1]] = 0
            else:
                total_a = total_a + sizes_copy[rule[1]]
                sizes_copy[rule[0]] = 0
        
        sizes_copy.sort(reverse = True)
        for i in range(len(sizes_copy)):
            if i % 2 == 0:
                total_a = total_a + sizes_copy[i]

        return total_a
```