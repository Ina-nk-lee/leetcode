## Longest Repeating Character with Replacement
- Difficulty: Medium
- [Link](https://neetcode.io/problems/longest-repeating-substring-with-replacement/history)

---

### Summary
- Given an uppercase string `s` and an integer `k`, return the length of the longest substring that can be made of the same character after at most `k` replacements.
---

### Ideas
- It's unavoidable to check all the characters in `s`.
- Need to find a consecutive interval that meets the requirement while going from left to right.

---

### Solution (`O(n)`)

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        seen = set(s)
        mx = 0
        for c in seen:
            l = 0
            r = 0
            count = 0
            while r < len(s):
                if s[r] == c:
                    count += 1
                while r - l + 1 > k + count:
                    if s[l] == c:
                        count -= 1
                    l += 1
                mx = max(mx, r - l + 1)
                r += 1
        return mx
```
- For each fixed `c` in `seen`, it checks `s`.
 - If `s[r] == c`, it increments `count`, which counts how many `c` are inside the window.
 - While the window size(`r - l + 1`) is bigger than `k + count`, it increases `l` and shrinks the window from the left.
 - `mx` contains the biggest window size.

### Thoughts
- The time complexity of the solution is **`O(n * m)`** where `n` is the length of `s` and `m` is the number of unique characters in `s`. However, `m` is `26` at most.
- Additionally, each index enters and leaves the window at most once, so both pointers move at most `n` times for a fixed `c`.
- The space complexity is **`O(m)`** where `m` is the number of unique characters in `s`.
- Sliding window solution is useful for problems that require a consecutive interval under a given condition.