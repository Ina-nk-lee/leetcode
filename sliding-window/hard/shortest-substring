## Shortest Substring with Given Characters
- Difficulty: Hard
- [Link](https://neetcode.io/problems/minimum-window-with-characters/question?list=blind75)

---

### Summary
- Given two strings `s` and `t`, return the shortest substring from `s` that contains all the characters in `t` including duplicates.
---

### Ideas
- It's unavoidable to check all the characters in `s`.
- Need to find a shortest interval that meets the requirement while going from left to right.
- The right pointer of the window moves first to meet the condition and the left one follows to minimize the window size.

---

### Solution (`O(n)`)

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        count = defaultdict(int)
        for char in t:
            count[char] += 1

        l = 0
        r = 0
        have = 0
        mn_l = 0
        mn_r = 0
        mn = len(s)
        while r < len(s):
            if s[r] in count:
                count[s[r]] -= 1
                if count[s[r]] == 0:
                    have += 1
            if have == len(count):
                while s[l] not in count or count[s[l]] < 0:
                    if s[l] in count:
                        count[s[l]] += 1
                    l += 1
                if r - l + 1 <= mn:
                    mn_l = l
                    mn_r = r
                    mn = r - l + 1
            r += 1
        if not all(v <= 0 for v in count.values()):
            return ""
        else: 
            return s[mn_l:mn_r + 1]
```
- `count` contains the characters that `s` should have in its window.
- `r` goes to the right first to fulfill the condition to have the characters in `count`.
- It increments `have` every time the window has all the counts of a character.
- Once it has all the characters, `l` goes to the right to minimize the window size by removing extra characters.
- If the window size is smaller than `mn` after the minimization, it updates `mn`, `mn_l`, `mn_r`.
- After the loop, if the values in `count` is not positive values, it returns `""`.
- If not, it returns the smallest window size.


### Thoughts
- The time complexity of the solution is **`O(n + m)`** where `n` is the length of `s` and `m` is that of `t` because `l` and `r` check the elements of `s` once at most, and the characters of `t` are added to `count`.
- The space complexity is **`O(unique(m))`** because of `count`.
- By using `have` rather than going through the entire `count`, it can check the window requirement with a constant time. 