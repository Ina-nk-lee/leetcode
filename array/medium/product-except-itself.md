## Product of array values except for itself

- Difficulty: Medium
- [Link](https://neetcode.io/problems/products-of-array-discluding-self/question)

---

### Summary

- Given an array of integers `nums`, return an array that contains the product of all elements except `nums[i]` for each `i`.
---

### Ideas

- It's unavoidable to check all the elements in `nums`.
- The most intuitive solution is to use the division operation, but the usual constraint is to avoid devision.

---

### Solution 1 (`O(n^2)`)

```python  
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = []
        for i in range(len(nums)):
            product = 1
            for j in range(len(nums)):
                if i != j:
                    product *= nums[j]
            result.append(product)
        
        return result

```
- Calculates the product of all the other numbers for each number in `nums`.

### Solution 2 (`O(n)`)

```python  
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = []
        product = 1
        zero_count = 0

        for num in nums:
            if num != 0:
                product *= num 
            else:
                zero_count += 1

        for num in nums:
            if zero_count == 0:
                result.append(product // num)
            elif zero_count == 1:
                if num == 0:
                    result.append(product)
                else:
                    result.append(0)
            else: 
                result.append(0)

        return result
```
- The first loop calculates the product of all the non-zero values in `nums`.
- `zero_count` stores the number of zeros in `nums` to handle the edge case where there are zeros in `nums`.
- The second loop divides `product` by the current number if there is no zero in `nums`.
- If there is one zero and the current number is the zero, add `product`. If not, add `0` to it.
- If there are multiple zeros, every product except self includes at lest one zero, so all the outputs in `result` must be 0.

### Solution 3 (`O(n)`)

```python  
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        left = [1] * n
        right = [1] * n
        result = [0] * n

        for i in range(1, n):
            left[i] = left[i - 1] * nums[i - 1]
        for i in range(n - 2, -1, -1):
            right[i] = right[i + 1] * nums[i + 1]
        for i in range(n):
            result[i] = left[i] * right[i]

        return result     

```
- `left` stores products of `0` th to `i - 1`th values from left to right, and `right` stores products of `n - 1`th to `0`th values from right to left.
- `result` has the product of `left[i]` and `right[i]`, which have a product of all the left values except for itself and a product of all the right values except for itself respectively.


### Thoughts

- For the **solution 1**, the time complexity is **`O(n^2)`** because we need to iterate `nums` for each number in `nums`. The space complexity is **`O(n)`**.
- For the **solution 2**, the time complexity is **`O(n)`** to traverse `nums`. The space complexity is also **`O(n)`** to create an array of size `n`.
- For the **solution 3**, the time complexity is **`O(n)`**, and the space complexity is also **`O(n)`** to create arrays of size `n`.
- However, it can be optimized to `O(1)` extra space(excluding the output array) by reusing `left` and `right` for `result`.