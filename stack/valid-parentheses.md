## Valid Parentheses

- Difficulty: Easy
- [Link](https://neetcode.io/problems/validate-parentheses/question)

---

### Summary

- Given a string `s` that includes `(, ), {, }, [, ]`, return `true` if and only if:
 1. Every bracket is closed by the same type of bracket.
 2. Parentheses open first and close later.
 3. Each closing bracket has a matching opening counterpart.

---

### Ideas

- First, we need to **iterate through the entire string** to check all brackets in the string. This takes O(n) time.
- Parentheses need to be firstly removed from where **an opening bracket and a closing bracket are placed consecuteively**. e.g. ()
 If any unmatched bracket remains in the stack after traversal, return `false`.

---

### Solution 1

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for char in s:
            if char == '(' or char == '{' or char == '[':
                stack.append(char)
            else:
                if len(stack) == 0:
                    return False
                if char == ')':
                    if stack[-1] == '(':
                        stack.pop()
                    else:
                        return False
                if char == '}':
                    if stack[-1] == '{':
                        stack.pop()
                    else:
                        return False
                if char == ']':
                    if stack[-1] == '[':
                        stack.pop()
                    else:
                        return False
        if len(stack) == 0:
            return True
        else:
            return False
```

- `stack` stores the opening brackets.
- For each closing bracket, we check if it matches the latest opening bracket.
- If it does, we pop from the stack.
- If not, we return `false`.
- If the stack is empty at the end, we return `true`.
- Space complexity: O(n)
- Time complexity: O(n)

### Solution 2

```python
class Solution:
    def isValid(self, s: str) -> bool:
        while '()' in s or '[]' in s or '{}' in s:
            s = s.replace('()', '')
            s = s.replace('{}', '')
            s = s.replace('[]', '')
        return s == ''
```

- This approach repeatedly removes matched bracket pairs from the innermost to outermost.
- If the final string is empty, it means all brackets were matched properly.
- Otherwise, it contains unmatched brackets and returns `False`.
- Space complexity: O(n)
- Time complexity: O(n^2) because `replace()` copies the entire string.
---

### Thoughts

- I've solved this problem several times, but it still took me a while because I forgot to **use a stack** in this context.
- I struggled especially with the idea of **removing the innermost brackets first**.
- Stack problems are tricky because they require **last-in-first-out (LIFO)** thinking.
- This pattern is useful whenever **reverse-order matching** is involved.