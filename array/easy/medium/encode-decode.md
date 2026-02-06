## Encode/Decode String

- Difficulty: Medium
- [Link](https://neetcode.io/problems/string-encode-and-decode/question)

---

### Summary

- Given a list of strings, design two functions that encode a list of strings to a string and decode a string to a list of strings.

---

### Ideas

- We must visit **each string** in the array to encode it to a string.
- Need to track **size** of each string to decode accurately -- like `varchar` type.

---

### Solution 1

```python
class Solution:
    def encode(self, strs: List[str]) -> str:
        result = ""

        if not strs:
            return result
        
        for i in range(len(strs)):
            result += str(len(strs[i]))
            result += ","

        result += "@"

        for i in range(len(strs)):
            result += strs[i]
        
        return result

    def decode(self, s: str) -> List[str]:
        result, size = [], []
        i = 0
        
        if not s:
            return result

        while s[i] != "@":
            temp = ""
            while s[i] != ",":
                temp += s[i]
                i += 1
            size.append(int(temp))
            i += 1
        i += 1

        j = 0
        while j < len(size):
            k = 0
            temp = ""
            while k < size[j]:
                temp += (s[i])
                i += 1
                k += 1
            result.append(temp)
            j += 1

        return result
```
- `encode()` converts a list of strings into one single string.
- First, it reads the size of each string with a delimiter `,`.
- After reading all the sizes, `@` is placed to separate the sizes from strings.
- The strings are concatenated to `result`, which is a return value.

- `decode()` converts one single string into a list of strings.
- First, it reads the string sizes in `s` and store sthem in the `size` array.
- Second, strings are decoded from `s` into an individual string based on their size in `size`.

### Solution 2

```python
class Solution:
    def encode(self, strs: List[str]) -> str:
        result = ""

        if not strs:
            return result
        
        for s in strs:
            result += str(len(s))
            result += "@"
            result += s
        
        return result

    def decode(self, s: str) -> List[str]:
        result = []

        if not s:
            return result

        i = 0
        while i < len(s):
            temp = ""
            while s[i] != "@":
                temp += s[i]
                i += 1
            leng = int(temp)
            i += 1
            result.append(s[i : i + leng])
            i += leng
        
        return result
```
- `encode()` encodes each string in the array in a `length@string` format(length-prefix encoding).
- `decode()` decodes a single string, `s`, based on the encoding format.
- The size of a string is read first, and the string is read from `s` based on the size by slicing `s`.
---

### Thoughts

- **Length-prefix encoding** is useful because decoding does not depend on a “safe delimiter” inside the original strings.
- If we treat the total number of characters across all strings as `L`, the core encode/decode work is **O(L)** and the extra space is also **O(L)**.
- In Python, repeated `result += ...` string concatenation can be slower in the worst case; using a list of chunks + `''.join(chunks)` keeps it clean and closer to **O(L)**.
- Python lists don’t allow assignment to an index that is out of range.