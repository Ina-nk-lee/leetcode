## Most Frequent Elements in Array

- Difficulty: Medium
- [Link](https://neetcode.io/problems/top-k-elements-in-list/)

---

### Summary

- Given an array consists of integers and an integer `k`, find `k` most frequently appeared numbers within the array.

---

### Ideas

- We could sort all the words alphabetically and group them using hashmap, but the time complexity of it is `O(mlogn)`, where `m` is the number of strings in `strs` and `n` is the length of the longest string in `strs`.
- Instead, we could use **frequency counting** to minimize the time complexity to **O(m * n)**.

---

### Solution

```python  
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = defaultdict(list)
        for s in strs:
            frq = [0] * 26
            for c in s:
                frq[ord(c) - ord('a')] += 1
            d[tuple(frq)].append(s)
        
        return list(d.values())

```
- `d` is a dictionary with `list` objects as values. `defaultdict(list)` automatically initialzes the value as an empty `list` if the key is not found.
- For each string in `strs`, it creates a frequency counting array, `frq` of size 26, where each index represents the count of each lowercase letter `a` to `z`.
- `ord(c) - ord('a')` computes the index for each character.
- `tuple(frq)` is used as a key in the dictionary, since lists cannot be used as dictionary keys.
- After processing all strings, `d.values()` contains all anagram groups.
- `List[]` is for type annotation in parameters; `list` is the actual list type used at runtime.
---

### Thoughts

- The time complexity is **`O(m * n)`** where `m` is the number of strings in `strs` and `n` is the maximum length of a string.
- The space complexity is **`O(m * n)`** as well since each string and its character frequencies are stored in memory.
- The use of **`defaultdict()`**, **`ord()`**, **`tuple()`**, **`list()`** makes the implementation concise and efficient.