## Highest Profit from Stock

- Difficulty: Easy
- [Link](https://neetcode.io/problems/buy-and-sell-crypto/question)

---

### Summary

- Given an array of stock prices, find the best time to buy and sell to maximize profit.

---

### Ideas

- First, we need to **iterate through the entire array** to check all prices and find the best time to buy and sell. This takes O(n) time.
- We'll use an integer variable `gap` to store the **current maximum profit**, and two pointers (`i` and `j`) to track **the buying and selling days**.
- As we iterate, we compare each potential profit (`prices[j] - prices[i]`) to `gap` and update it if a higher profit is found.

---

### Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        gap = 0
        i = 0
        j = 0

        while i <= j and j < len(prices):
            if prices[j] - prices[i] > gap:
                gap = prices[j] - prices[i]
            else:
                if prices[j] < prices[i]:
                    i = j
            j += 1

        return gap
```

- `gap` stores the highest profit found so far.
- For each price at day `j`, we check if selling on day `j` after buying on day `i` yields a higher profit than `gap`.
- If it does, we update `gap`.
- If a lower price is found at day `j`, we move the buy pointer `i` to `j`, since it's better to buy at the lower price going forward.
- The loop continues until `j` reaches the end of the array.

---

### Thoughts

- I've solved this problem several times, but I often make mistakes when managing the two pointers.
- This time, I initially forgot to **reset `i` when a lower price was found**, which caused incorrect results.
- Two-pointer problems can be tricky because they require **coordinating two moving parts**.
- This pattern is useful when **tracking changes or differences** over a sequence of values.