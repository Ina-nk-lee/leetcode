## Contains Duplicate

- Difficulty: Easy
- [Link](https://neetcode.io/problems/is-anagram?list=neetcode150)

---

### Summary

- With the two strings `s` and `t`, return `True` if they are anagrams of each other.
- Otherwise, return `False`.

---

### Ideas

- We need to **keep track of letters** to check how many times they appeared in both of the strings.
- This requires **iterating through both strings**, which takes O(n) time.
- We also need a **data structure** to efficiently store character counts.
- Since **letter order doesn't matter** in anagrams, a **hash map that maps characters to their counts** is suitable.
- Additionally, **lookup in a hash map takes O(1)** time on average.
- The hash map requires **O(n) space** in the worst case.

---

### Solution

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        saved = dict()

        for letter in s:
            if letter in saved:
                saved[letter] += 1
            else:
                saved[letter] = 1

        for letter in t:
            if letter in saved:
                saved[letter] -= 1
                if saved[letter] == 0:
                    del saved[letter]
            else:
                return False

        if len(saved) == 0:
            return True
        else:
            return False
```

- `saved` stores the letter-appearance pairs in `s`.
- For each character in `t`, the loop checks if it exists in `saved`.
- If it does, it subtracts 1 from the count and deletes the key if the count reaches 0.
- If any character in `t` doesn’t exist in `saved`, the function returns `False`.
- If no keys remain after iterating through `t`, the strings are anagrams and the function returns `True`.

---

### Thoughts

- This wasn't too challenging, but it helped me revisit Python’s **hash map usage**.
- I had to ensure proper deletion of keys once their count reached 0.
- Constant-time lookup in hash maps is very useful in scenarios involving counting.
- This pattern is likely to be helpful in other problems involving **frequency tracking**.
