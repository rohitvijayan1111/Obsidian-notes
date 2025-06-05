
# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

## Recursion 

class Solution:
    def climbStairs(self, n: int) -> int:
        def helper(ind):
            if(ind==0):
                return 1
            f1=helper(ind-1)
            f2=0
            if(ind-2>=0):
                f2=helper(ind-2)
            return f1+f2
        return helper(n)

Time complexity : o(2^n)
Space complexity : o(n)

---
## Top down

class Solution:
    def climbStairs(self, n: int) -> int:
        memo = {}
        def helper(ind):
            if ind == 0 or ind == 1:
                return 1
            if ind in memo:
                return memo[ind]
            memo[ind] = helper(ind - 1) + helper(ind - 2)
            return memo[ind]
        return helper(n)

Time complexity : o(n)
Space complexity: o(n)

---
## Bottom down

class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 0 or n == 1:
            return 1
        dp = [0] * (n + 1)
        dp[0] = 1  # 1 way to stay at ground level
        dp[1] = 1  # 1 way to reach step 1
        for i in range(2, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]
        return dp[n]


### 🧮 Time and Space Complexity

- **Time Complexity** = **O(n)** → One pass through the loop.    
- **Space Complexity** = **O(n)** → For the `dp` array.
---

 Optimized Space Version (Only O(1) space):
Since only the last two values are needed at any point, you can reduce space usage:

python
Copy
Edit
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 0 or n == 1:
            return 1

        prev2 = 1  # dp[0]
        prev1 = 1  # dp[1]

        for i in range(2, n + 1):
            current = prev1 + prev2
            prev2 = prev1
            prev1 = current

        return prev1

# [Frog Jump(DP-3)](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-dp-3/)

✅ Correct Recursive Version (Exponential Time)
python
Copy
Edit
class Solution:
    def minCost(self, heights):
        def helper(ind):
            if ind == 0:
                return 0  # No cost to stand at first stair
            
            # Jump from (i-1)
            cost1 = helper(ind - 1) + abs(heights[ind] - heights[ind - 1])
            
            # Jump from (i-2) if possible
            cost2 = float('inf')
            if ind > 1:
                cost2 = helper(ind - 2) + abs(heights[ind] - heights[ind - 2])
            
            return min(cost1, cost2)

        n = len(heights)
        return helper(n - 1)
🧠 Time and Space Complexity
Time Complexity: O(2^n) → due to overlapping subproblems

Stack Space: O(n) → max recursion depth

🛠️ Memoization (to make it efficient)
python
Copy
Edit
class Solution:
    def minCost(self, heights):
        n = len(heights)
        dp = [-1] * n  # Initialize dp array with -1 to indicate uncomputed states

        def helper(ind):
            if ind == 0:
                return 0
            if dp[ind] != -1:
                return dp[ind]
            
            # Option 1: Jump from (ind - 1)
            cost1 = helper(ind - 1) + abs(heights[ind] - heights[ind - 1])
            
            # Option 2: Jump from (ind - 2) if valid
            cost2 = float('inf')
            if ind > 1:
                cost2 = helper(ind - 2) + abs(heights[ind] - heights[ind - 2])
            
            dp[ind] = min(cost1, cost2)
            return dp[ind]

        return helper(n - 1)

⚡ Bottom-Up Tabulation Version (Best for Interviews)
python
Copy
Edit
class Solution:
    def minCost(self, heights):
        n = len(heights)
        dp = [0] * n
        dp[0] = 0

        for i in range(1, n):
            jump_one = dp[i - 1] + abs(heights[i] - heights[i - 1])
            jump_two = dp[i - 2] + abs(heights[i] - heights[i - 2]) if i > 1 else float('inf')
            dp[i] = min(jump_one, jump_two)

        return dp[n - 1]




# [198. House Robber](https://leetcode.com/problems/house-robber/)

Here's a clear breakdown of the **four approaches** to the **House Robber problem**, including your provided **shifted index top-down** version, each with its **code, explanation, and time complexity**:

---

### ✅ 1. **Recursive (Plain Recursion – No Memoization)**

#### 🔁 Idea:

- At each step, choose whether to rob the current house and skip the previous one (`n-2`), or skip the current house (`n-1`).
    
- Repeats many subproblems (exponential time).
    

#### 💡 Code:

```python
def rob_recursive(nums):
    def helper(n):
        if n < 0:
            return 0
        return max(nums[n] + helper(n - 2), helper(n - 1))
    return helper(len(nums) - 1)
```

#### ⏱ Time Complexity:

**O(2^n)** – Exponential, because every call splits into two.

#### 🧠 Space Complexity:

**O(n)** (due to call stack depth)

---

### ✅ 2. **Top-Down (Memoization / Standard DP)**

#### 🔁 Idea:

- Same recursive logic, but store results in `dp[n]` to avoid recomputation.
    

#### 💡 Code:

```python
def rob_top_down(nums):
    dp = [-1] * len(nums)
    def helper(n):
        if n < 0:
            return 0
        if dp[n] != -1:
            return dp[n]
        dp[n] = max(nums[n] + helper(n - 2), helper(n - 1))
        return dp[n]
    return helper(len(nums) - 1)
```

#### ⏱ Time Complexity:

**O(n)** – Each index is computed once.

#### 🧠 Space Complexity:

**O(n)** – For memoization array + recursion stack.

---

### ✅ 3. **Shifted Index Top-Down (Your Version)**

#### 🔁 Idea:

- Shift the indices by +1 to avoid negative indexing.
    
- Use `n == 0` and `n == 1` as base cases, and work up to `n == len(nums)`.
    

#### 💡 Code (fixed version):

```python
class Solution:
    def rob(self, nums):
        dp = [-1] * (len(nums) + 1)
        def helper(n):
            if n == 0:
                return 0
            if n == 1:
                return nums[0]
            if dp[n] != -1:
                return dp[n]
            dp[n] = max(nums[n - 1] + helper(n - 2), helper(n - 1))
            return dp[n]
        return helper(len(nums))
```

#### ⏱ Time Complexity:

**O(n)** – Each `helper(n)` is computed once and memoized.

#### 🧠 Space Complexity:

**O(n)** – For `dp` array and recursion stack.

---

### ✅ 4. **Bottom-Up (Tabulation)**

#### 🔁 Idea:

- Iteratively build the solution from the base cases.
    
- Avoid recursion completely.
    

#### 💡 Code:

```python
class Solution:
    def rob(self, nums):
        n = len(nums)
        if n == 0:
            return 0
        dp = [0] * (n + 1)
        dp[1] = nums[0]
        for i in range(2, n + 1):
            dp[i] = max(nums[i - 1] + dp[i - 2], dp[i - 1])
        return dp[n]
```

#### ⏱ Time Complexity:

**O(n)** – Single pass over the array.

#### 🧠 Space Complexity:

**O(n)** – For `dp` array. Can be optimized to **O(1)** (space-optimized version).

---

### ✅ (Optional) 5. **Bottom-Up Space Optimized**

```python
class Solution:
    def rob(self, nums):
        prev2, prev1 = 0, 0
        for num in nums:
            curr = max(num + prev2, prev1)
            prev2, prev1 = prev1, curr
        return prev1
```

#### ⏱ Time: **O(n)**

#### 🧠 Space: **O(1)**

---

### 📊 Summary Table:

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursive (plain)|O(2^n)|O(n)|Inefficient due to repeated subproblems|
|Top-Down (memoized)|O(n)|O(n)|Efficient, avoids recomputation|
|Shifted Index Top-Down|O(n)|O(n)|Same as top-down, cleaner indexing|
|Bottom-Up (tabulation)|O(n)|O(n)|Iterative, no recursion|
|Bottom-Up (space-opt)|O(n)|O(1)|Most efficient in terms of space|

Let me know if you'd like visual illustrations or debugging steps for any of these.




# [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)


_Problem Statement Link:_ [_House Robber_](https://www.codingninjas.com/codestudio/problems/house-robber_839733?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos)

A thief needs to rob money in a street. The houses in the street are arranged in a circular manner. Therefore the first and the last house are adjacent to each other. The security system in the street is such that if adjacent houses are robbed, the police will get notified.

Given an array of integers “Arr'' which represents money at each house, we need to return the maximum amount of money that the thief can rob without alerting the police.

**Examples**

![](https://lh5.googleusercontent.com/XG1_bncXs9qY3NldqFW-79mYZLwA84HZSsG58UaQR63ZatUYlRlUQ-0vFsCaEmPxBik4c9xftsYnzMZdtAlweBpvTZ0I3BBm9ZD_IVFkB-HAr7NuSTgf4jgzQsKV6qpgQyPu20zW)

**Pre-req:** [**Maximum Sum of non-adjacent elements**](https://takeuforward.org/data-structure/maximum-sum-of-non-adjacent-elements-dp-5/)

### **Solution :**

This question can be solved using the approach discussed in the [Maximum Sum of non-adjacent elements](https://takeuforward.org/data-structure/maximum-sum-of-non-adjacent-elements-dp-5/). Readers are highly advised to go through that article first and then read this. The rest of the article will refer to the previous article as Article DP5 and will relate to that approach. 

Now, we have a single test case. Three houses have money as shown.

![](https://lh5.googleusercontent.com/TQxjaokoYS4UBxXxGJlcSbVElkd46Mxc4w7tmg0I6-Tn8NKwa8HtaxZGDZkDAtd3oSIai0T2r8CJiu9d4foSWJbAaNmFNxG-divkVyFIrQA-5dVc85M0qSXDPcGkugjKsZvkwwIu)

- According to article DP5, the answer will be 4(2+2) as we are taking the maximum sum of non-adjacent elements.
- In this question, the first and last element are also adjacent(circular street), therefore the answer will be 3.

**Modification to Article DP5’s Approach**

We were finding the maximum sum of non-adjacent elements in the previous questions. For a circular street, the first and last house are adjacent, therefore one thing we know for sure is that the answer will not consider the first and last element simultaneously (as they are adjacent).

Now building on the article DP5, we can say that maybe the last element is not considered in the answer. In that case, we can consider the first element. Let’s call this answer ans1. Hence we have reduced our array(arr- last element), say arr1, and found ans1 on it by using the article DP5 approach.

![](https://lh3.googleusercontent.com/0mkwqypWCCVBzCR3p4y0kpIcfaOtXVj554Oppzazg3vz8R7BSgWstj6oIwKJtgmDVVZ7Ixn5I3q-KTAWMP3xWzQX88XoyrZBEZ7KcCH6T2IMGSserlmIDas4ZlI8OhMAe84kgL72)

Now, it can also happen that the final answer does consider the last element. If we consider the last element, we can’t consider the first element( again adjacent elements). We again use the same approach on our reduced array( arr - first element), say arr2. Let’s call the answer we get as ans2.

Now, the final answer can be either ans1 or ans2. As we have to return the maximum money robbed by the robber, we will return max(ans1, ans2) as our final answer.

![](https://lh6.googleusercontent.com/0x1VzdE2zZniwJr84vvkNsZWQSeNsKu385q_o-ySKc7rdFGdj-Qhc7I6XSif0vldfl9NIfqEd92e7mlYkDc6Z05dgtO0pZX7Qg30W09hU7qOHFuzvvv0Sh8KgphfR5IZ2mVdFJqf)

**Approach:**

The approach to solving this problem can be summarized as:

- Make two reduced arrays - arr1(arr-last element) and arr2(arr-first element).
- Find the maximum of non-adjacent elements as mentioned in article DP5 on arr1 and arr2 separately. Let’s call the answers we got ans1 and ans2 respectively.
- Return max(ans1, ans2) as our final answer.

**Code:**

C++JavaPython

```python
def solve(arr):
    n = len(arr)
    prev = arr[0]
    prev2 = 0

    for i in range(1, n):
        pick = arr[i]
        if i > 1:
            pick += prev2
        nonPick = 0 + prev

        cur_i = max(pick, nonPick)
        prev2 = prev
        prev = cur_i

    return prev
```