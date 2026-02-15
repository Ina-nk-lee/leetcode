## Find Longest Substring Without Duplicates
- Difficulty: Medium
- [Link](https://neetcode.io/problems/longest-substring-without-duplicates/question)

---

### Summary
- Given a string `s`, find the longest substring without duplicates and return its length.
---

### Ideas
- It's unavoidable to check all the characters in `s`.
- Hashset could be useful because the order because the order is irrelevant.
- `O(n)` is achievable by using a sliding window with two pointers.

---

### Solution (`O(n)`)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l = 0
        r = 0
        seen = set()
        mx = 0
        while r < len(s):
            if s[r] not in seen:
                seen.add(s[r])
                if len(seen) > mx:
                    mx = len(seen)
                r += 1
            else:
                seen.remove(s[l])
                l += 1
        return mx
```
- If `s[r]` is not in `seen`, it adds the character to `seen` and increments `r`.
- If the updated `seen` is longer than `mx`, it updates `mx`.
- If `s[r]` is already in `seen`, it removes `s[l]` and moves `l` right, repeating as needed until the duplicate is gone.

### Thoughts
- The time complexity of the solution is **`O(n)`** where `n` is the length of `s` because each character is added/removed from `seen` at most once and both pointers move at most `n` times.
- The space complexity is **`O(n)`** for `seen`.
- In sliding window problems, need to carefully consider where the left pointer would go next.
