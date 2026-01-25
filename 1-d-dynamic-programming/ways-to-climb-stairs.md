## Distinctive ways to climb stairs

- Difficulty: Easy
- [Link](https://neetcode.io/problems/climbing-stairs/)

---

### Summary

- Given an integer `n`, return the number of distinct ways to climb `n` stairs by taking `1` or `2` steps at a time.

---

### Ideas

- We need to calculate the number of istinct ways to climb a staircase with steps between **`0` and `n`**.
- `climbStairs(n)` equals `climbStairs(n - 1) + climbStairs(n - 2)`, which is **Fibonacci sequence**.
- **Recursion** is the most intuitive way to solve the problem, but it calculates the **every possible combination** of all the numbers that is smaller than `n`, which eventually involves many repeatition.
- Thus, **Memoization** could make it much more efficient.

---

### Solution

```python  
class Solution:
    def climbStairs(self, n: int) -> int:
        def climbHelper(num: int, saved: dict) -> int:
            if num not in saved:
                saved[num] = climbHelper(num - 1, saved) + climbHelper(num - 2, saved)
            return saved[num]

        d = {}
        d[0] = 1
        d[1] = 1
        return climbHelper(n, d)
```
- `climbHelper()` helps track the number of possible calculations for `num` steps in `saved`.
- `climbStairs()` sets the dictionary -- `d` -- and base cases for the recursion and passes `n` and `d` to `climbHelper`.
---

### Thoughts

- while **Recursion** is more straightforward and intuitive for **Fibonacci sequence**, we need to make it more efficient by using **memoization**.
- For the **solution without memoization**, the time complexity is **O(2^n)** to calculate from scratch for every branch.
- For the **solution with memoization**, the time complexity is **O(n)** by saving the calculated values in the **dictionary**.
- The space complesity is **O(n)** because we need to use the **dictionary** that is big as `n`.
- **Memoization** is a very efficient solution for where we need to calculate **cumulative values**.