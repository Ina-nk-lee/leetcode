## Valid Palindrome

- Difficulty: Easy
- [Link](https://neetcode.io/problems/is-palindrome/question?list=neetcode150)

---

### Summary

- Given a string, return `True` if it is a palindrome, and `False` otherwise.

---

### Ideas

- First, it's necessary to **filter out non-alphanumeric characters and convert all characters to lowercase** as preprocessing. This takes O(n) time and O(n) space.
- Then, we need to **check the characters from both ends** to determine if it's a palindrome.
- This requires **iterating through the string from the left and right**, which takes O(n) time.

---

### Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        result = []
        for char in s:
            if char.isalnum():
                result.append(char)
        cleaned = ''.join(result).lower()

        i = 0
        j = len(cleaned) - 1

        while i <= j:
            if cleaned[i] != cleaned[j]:
                return False
            i += 1
            j -= 1
        return True
```

- `cleaned` stores the lowercase alphanumeric characters of the input string.
- The loop compares the leftmost and rightmost characters.
- If they match, it moves the pointers **inward**.
- If they don't match, the function returns `False`.
- If all characters match until the pointers meet, the function returns `True`.

---

### Thoughts

- I've solved this problem many times, but I often struggle with **handling two pointers correctly**.
- This time, I got everything right except for **lowercasing the string during preprocessing**.
- Two-pointer problems can be tricky due to the need to **track two positions at once**.
- This pattern is useful for **tracking differences** in an array.