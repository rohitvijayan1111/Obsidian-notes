# MIN1,MIN2 tricck
Great question — this shows you’re thinking like a **DP expert**.  
The **min1 / min2 trick** is not random; it comes from a specific DP pattern.

Below is the **general rule** for when you _can_ and _cannot_ use it, with examples.

---

✅ **WHEN you can use the min1/min2 technique**

You can use this trick **whenever your DP transition is:**

```
dp[i][j] = cost[i][j] + min(dp[i+1][x])   over all x ≠ j
```

or more generally:

```
dp[i][j] = something(j) + best_value among all other states except j
```

This structure appears in problems where:

- You must choose one option out of **k choices** per step
    
- You are **not allowed to choose the same choice as the previous step**
    
- Transition requires computing  
    → **minimum over all other choices except j**
    

### ✔️ Then instead of scanning all k states each time,

you can store:

- the minimum (min1)
    
- the second minimum (min2)
    
- the index of the minimum (idx_min1)
    

---

## ⭐ Classic DP problems where min1/min2 works

### 1️⃣ Paint House II / Walls Coloring II

You used it already:

```
dp[i][j] = cost[i][j] + min(dp[i+1][x] for x != j)
```

---

### 2️⃣ K Colors, No Adjacent Same (Strings, Arrays)

Example:

Given array `nums`, choose color for each index with rule:

```
dp[i][color] = nums[i][color] + min(dp[i-1][c] for all c != color)
```

Same structure → min1/min2 applies.

---

### 3️⃣ Partitioning sequences where "same as last" is disallowed

If your recurrence is:

```
dp[i][state] = weight + min(dp[i-1][all other states])
```

(Where states are mutually exclusive choices).

Example: painting fence with multiple colors + constraints.

---

### 4️⃣ Choosing best station/option except the same one

For example:

```
dp[day][station] = cost + min(dp[day+1][other stations])
```

Very common in path DP, resource assignment DP.

---

## 🚫 **WHEN you CANNOT use this trick**

### ❌ Case 1: Transition does NOT use “min over all other states”

Examples:

```
dp[i][j] = dp[i-1][j] + dp[i-1][j-1]
dp[i][j] = max(...)
dp[i][j] = something not involving excluding j
```

The min1/min2 trick **ONLY applies for minimization problems** of a very specific type.

---

### ❌ Case 2: There is another constraint besides “x ≠ j”

For example:

```
dp[i][j] = cost + min(dp[i-1][x]) where x must satisfy multiple rules
```

If more than one rule filters x, then just excluding the minimum sometimes fails.

---

### ❌ Case 3: Transition depends on dp[i][j] in more complex ways

If the recurrence uses:

- dp[i][j-1]
    
- dp[i][j+1]
    
- dp[i][j] itself
    
- dp[i-1][j] only
    

Then you can't use min1/min2.

---

## 🧠 **General Rule You Can Memorize**

Use **min1/min2 optimization** _when all these are true_:

### ✔ DP state is:

`dp[i][choice]`  
and there are **k choices**.

### ✔ Transition is:

“pick the best DP from previous step, except the one with the same choice.”

### ✔ The only invalid transition is:

cannot transition from `j → j`.

### ✔ You want:

`min over all choices except j`  
and not something more complex.

### ✔ Cost structure is linear / additive per step.

Whenever you see this structure → **instantly use min1/min2**.

---

## 🎯 **Why it works mathematically**

For a row like:

```
[5, 7, 8, 13]
```

To compute `min(all except index j)`:

- If j is _not_ index of global min → answer = global min
    
- If j _is_ index of global min → answer = second global min
    

That is the entire trick.

You avoid scanning all `k` values each time.

---

## 🔥 Summary Table — When to Apply

|DP Pattern|min1/min2 works?|Reason|
|---|---|---|
|`dp[i][j] = cost + min(dp[i-1][x] for x != j)`|✔ Yes|Exact match|
|Choose a different category each step|✔ Yes|Only exclusion is “same category”|
|Multi-constraint transitions|❌ No|Need more filters|
|Local transitions (j-1, j+1 only)|❌ No|Not “min of all others”|
|Transitions using sum, not min|❌ No|Trick only applies to min/max|

---

## If you want

I can give you:

✅ A rule-of-thumb cheat sheet  
✅ 10 practice problems where the min1/min2 trick applies  
✅ How to identify the pattern in < 3 seconds  
Just say the word.
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



# [322. Coin Change](https://leetcode.com/problems/coin-change/)


```
class Solution:
        def coinChange(self, coins: List[int], amount: int) -> int:
            

            n = len(coins)
            dp = [[float("inf") for _ in range(n)] for _ in range(amount + 1)]
            for i in range(n):
                dp[0][i]=0
            for i in range(amount+1):
                if i % coins[0]==0:
                    dp[i][0]=i // coins[0]
            for i in range(1,amount+1):
                for ind in range(1,n):
                    take = float("inf")
                    if i-coins[ind] >= 0:
                        take = 1+dp[i-coins[ind]][ind]
                    
                    not_take = dp[i][ind - 1]
                    dp[i][ind]=min(take, not_take)
                    

            res =dp[amount][n-1]
            return -1 if res == float("inf") else res

    #--------------------------------------------------------------
    # def recursive(self, coins: List[int], amount: int) -> int:
    #     def dp[amount,ind):
    #         if(amount==0):
    #             return 0
    #         elif(ind==0):
    #             #IF THE AMOUNT IS ACHIEVABLE
    #             if(amount%coins[ind]==0):
    #                 return amount//coins[ind]
    #             else:
    #                 return float("inf")
    #         #Include the coins and dont move
    #         #include the coin and move
    #         #dont include the coin and move
    #         return min(dp[amount-coins[ind],ind),dp[amount-coins[ind],ind-1),dp[amount,ind-1))
    #     n=len(coins)
    #     res=dp[amount,n-1)
    #     return -1 if res==float("inf") else res 
    #-----------------------------------------------------------------
    #  def topdown(self, coins: List[int], amount: int) -> int:
    #     def dp[amount, ind):
    #         if amount == 0:
    #             return 0
    #         if ind == 0:
    #             if amount % coins[ind] == 0:
    #                 return amount // coins[ind]
    #             else:
    #                 return float("inf")
    #         if dp[amount][ind] != -1:
    #             return dp[amount][ind]
            
    #         take = float("inf")
    #         if amount - coins[ind] >= 0:
    #             take = dp[amount - coins[ind], ind)
            
    #         take2 = float("inf")
    #         if amount - coins[ind] >= 0:
    #             take2 = dp[amount - coins[ind], ind - 1)

    #         not_take = dp[amount, ind - 1)

    #         dp[amount][ind] = min(take, take2, not_take)
    #         return dp[amount][ind]

    #     n = len(coins)
    #     dp = [[-1 for _ in range(n)] for _ in range(amount + 1)]
    #     res = dp[amount, n - 1)
    #     return -1 if res == float("inf") else res
    #-----------------------------------------------------------------

```





# ree


# [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)


You're right — thanks for pointing that out! Here's the **complete and clean documentation** including all three main approaches:

1. **Recursion (Exponential)**
    
2. **Top-Down DP (Memoization)**
    
3. **Bottom-Up DP (Tabulation - 2D)**
    
4. **Space Optimized DP (1D)**
    

---

## 🪜 1. Recursive Solution (Brute Force)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        def helper(target, ind):
            if target == 0:
                return 1  # One way to make amount 0 (choose nothing)
            if ind == 0:
                return 1 if target % coins[0] == 0 else 0

            include = 0
            if target - coins[ind] >= 0:
                include = helper(target - coins[ind], ind)  # Stay on same index
            not_include = helper(target, ind - 1)  # Move to previous index

            return include + not_include

        n = len(coins)
        return helper(amount, n - 1)
```

### ❗ Time and Space Complexity:

- **Time:** `O(2^n)` in worst case due to overlapping subproblems.
    
- **Space:** `O(amount)` for recursion stack depth.
    

---

## 🧠 2. Top-Down DP (Memoization)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        n = len(coins)
        dp = [[-1 for _ in range(n)] for _ in range(amount + 1)]

        def helper(target, ind):
            if target == 0:
                return 1
            if ind == 0:
                return 1 if target % coins[0] == 0 else 0
            if dp[target][ind] != -1:
                return dp[target][ind]

            include = 0
            if target - coins[ind] >= 0:
                include = helper(target - coins[ind], ind)
            not_include = helper(target, ind - 1)

            dp[target][ind] = include + not_include
            return dp[target][ind]

        return helper(amount, n - 1)
```

### ✅ Time and Space Complexity:

- **Time:** `O(amount × n)` — due to memoization.
    
- **Space:** `O(amount × n)` for memo table + recursion stack.
    

---

## 📊 3. Bottom-Up DP (Tabulation — 2D)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        n = len(coins)
        dp = [[0 for _ in range(n)] for _ in range(amount + 1)]

        # Base case: one way to make amount 0 (by taking nothing)
        for i in range(n):
            dp[0][i] = 1

        # Fill column 0: only using first coin
        for i in range(1, amount + 1):
            dp[i][0] = 1 if i % coins[0] == 0 else 0

        for target in range(1, amount + 1):
            for ind in range(1, n):
                include = 0
                if target - coins[ind] >= 0:
                    include = dp[target - coins[ind]][ind]  # stay at same coin
                not_include = dp[target][ind - 1]  # move to previous coin
                dp[target][ind] = include + not_include

        return dp[amount][n - 1]
```

### ✅ Time and Space Complexity:

- **Time:** `O(amount × n)`
    
- **Space:** `O(amount × n)`
    

---

## 💡 4. Space Optimized DP (1D)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1  # Base case: one way to make 0

        for coin in coins:
            for target in range(coin, amount + 1):
                dp[target] += dp[target - coin]

        return dp[amount]
```

### 🧠 Why This Works:

- Process each coin fully before moving to the next.
    
- This ensures no repeated combinations in different order.
    
- `dp[target] += dp[target - coin]` accumulates ways using that coin.
    

### ✅ Time and Space Complexity:

- **Time:** `O(amount × n)`
    
- **Space:** `O(amount)`
    

---

## 📋 Summary Table

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursion (Brute)|Exponential|O(amount) stack|Inefficient, for learning only|
|Top-Down DP|O(amount × n)|O(amount × n)|Uses memoization to avoid recomputation|
|Bottom-Up DP|O(amount × n)|O(amount × n)|Clear table-filling approach|
|Space Optimized DP|O(amount × n)|**O(amount)**|Best in practice|

Let me know if you want a **visual diagram** or **dry run** of any version!



# [Knapsack with Duplicate Items](https://www.geeksforgeeks.org/problems/knapsack-with-duplicate-items4201/1)


Absolutely! Here's a **complete, cleanly documented, and unified implementation** of the **Unbounded Knapsack Problem** in Python, covering all major approaches:

---

# 🧰 Problem: **Unbounded Knapsack**

Given:

- `val[]`: list of item values
    
- `wt[]`: corresponding list of item weights
    
- `capacity`: maximum weight the knapsack can hold
    

Goal:  
Maximize the **total value** such that any number of each item can be included (unbounded use allowed).

---

# ✅ Solution Approaches

## 🧩 1. Recursive (Brute Force)

```python
class Solution:
    def knapSack(self, val, wt, capacity):
        def helper(amount, ind):
            if amount == 0:
                return 0
            if ind == 0:
                return (amount // wt[0]) * val[0]  # Take as many as possible

            # Option 1: include current item (if it fits)
            inc = 0
            if amount - wt[ind] >= 0:
                inc = val[ind] + helper(amount - wt[ind], ind)  # Stay on same index

            # Option 2: skip current item
            not_inc = helper(amount, ind - 1)

            return max(inc, not_inc)

        n = len(wt)
        return helper(capacity, n - 1)
```

### ⏱️ Time & Space Complexity

- **Time:** Exponential (due to overlapping subproblems)
    
- **Space:** `O(capacity)` recursion stack depth
    

---

## 🧠 2. Top-Down DP (Memoization)

```python
class Solution:
    def knapSack(self, val, wt, capacity):
        n = len(wt)
        dp = [[-1] * n for _ in range(capacity + 1)]

        def helper(amount, ind):
            if amount == 0:
                return 0
            if ind == 0:
                return (amount // wt[0]) * val[0]
            if dp[amount][ind] != -1:
                return dp[amount][ind]

            inc = 0
            if amount - wt[ind] >= 0:
                inc = val[ind] + helper(amount - wt[ind], ind)

            not_inc = helper(amount, ind - 1)

            dp[amount][ind] = max(inc, not_inc)
            return dp[amount][ind]

        return helper(capacity, n - 1)
```

### ⏱️ Time & Space Complexity

- **Time:** `O(n × capacity)`
    
- **Space:** `O(n × capacity)` for memo table + recursion stack
    

---

## 📊 3. Bottom-Up DP (Tabulation — 2D)

```python
class Solution:
    def knapSack(self, val, wt, capacity):
        n = len(wt)
        dp = [[0 for _ in range(n)] for _ in range(capacity + 1)]

        # Fill base cases
        for w in range(capacity + 1):
            dp[w][0] = (w // wt[0]) * val[0]

        for amount in range(1, capacity + 1):
            for ind in range(1, n):
                inc = 0
                if amount - wt[ind] >= 0:
                    inc = val[ind] + dp[amount - wt[ind]][ind]
                not_inc = dp[amount][ind - 1]
                dp[amount][ind] = max(inc, not_inc)

        return dp[capacity][n - 1]
```

### ⏱️ Time & Space Complexity

- **Time:** `O(n × capacity)`
    
- **Space:** `O(n × capacity)`
    

---

## 💾 4. Bottom-Up DP (Space Optimized — 1D)

```python
class Solution:
    def knapSack(self, val, wt, capacity):
        n = len(wt)
        dp = [0] * (capacity + 1)

        for i in range(n):
            for w in range(wt[i], capacity + 1):
                dp[w] = max(dp[w], val[i] + dp[w - wt[i]])

        return dp[capacity]
```

### ⏱️ Time & Space Complexity

- **Time:** `O(n × capacity)`
    
- **Space:** `O(capacity)` — space-optimized
    

---

## 📝 Example

```python
val = [6, 1, 7, 7]
wt = [1, 3, 4, 5]
capacity = 8

Solution().knapSack(val, wt, capacity)  # Output: 48
```

**Why 48?**  
You can take item 0 (value 6, weight 1) eight times → `6 × 8 = 48`.

---

## 📋 Summary of Approaches

|Approach|Time Complexity|Space Complexity|Remarks|
|---|---|---|---|
|Recursive|Exponential|O(capacity)|Brute force, slow|
|Top-Down (Memoization)|O(n × capacity)|O(n × capacity)|Caches overlapping subproblems|
|Bottom-Up (2D)|O(n × capacity)|O(n × capacity)|Classic tabulation|
|Bottom-Up (1D)|O(n × capacity)|**O(capacity)**|Best for performance|

---

Let me know if you'd like a **dry-run**, **diagram**, or if you want to implement the **bounded knapsack** version as well!


# [Rod Cutting Problem](https://www.geeksforgeeks.org/problems/rod-cutting0840/1)

Here's a clean, well-documented version of your solution to the **Rod Cutting Problem**, including **recursion**, **2D bottom-up DP**, and **1D space-optimized DP**, with **time and space complexity analysis**.

---

## 🎯 Problem: Rod Cutting

Given:

- A rod of length `n`
    
- An array `price[]`, where `price[i]` is the price of a rod of length `i+1`
    

**Goal**: Cut the rod into pieces (possibly reusing the same size) to maximize the total price.

---

## ✅ Full Python Implementation with All Approaches

```python
# User function Template for python3

class Solution:
    def cutRod(self, price):
        n = len(price)

        ###########################
        # 1️⃣ Recursive Approach (Exponential)
        ###########################
        # def helper(length, ind):
        #     if length == 0:
        #         return 0
        #     elif ind == 0:
        #         return length * price[0]  # only 1-length pieces
        #     
        #     cut = 0
        #     if length - (ind + 1) >= 0:
        #         cut = price[ind] + helper(length - (ind + 1), ind)  # cut and stay
        #     nocut = helper(length, ind - 1)  # move to smaller size
        #     return max(cut, nocut)
        # 
        # return helper(n, n - 1)

        ###########################
        # 2️⃣ Bottom-Up DP (Tabulation with 2D array)
        ###########################
        # dp = [[0 for _ in range(n)] for _ in range(n + 1)]
        # for length in range(n + 1):
        #     dp[length][0] = length * price[0]  # only using 1-length pieces
        # 
        # for length in range(1, n + 1):
        #     for ind in range(1, n):
        #         cut = 0
        #         if length - (ind + 1) >= 0:
        #             cut = price[ind] + dp[length - (ind + 1)][ind]
        #         nocut = dp[length][ind - 1]
        #         dp[length][ind] = max(cut, nocut)
        # 
        # return dp[n][n - 1]

        ###########################
        # 3️⃣ Space Optimized Bottom-Up DP (1D array)
        ###########################
        dp = [0 for _ in range(n + 1)]

        for i, p in enumerate(price):
            length_of_cut = i + 1
            for l in range(length_of_cut, n + 1):
                dp[l] = max(dp[l], p + dp[l - length_of_cut])

        return dp[n]
```

---

## 🧠 Time & Space Complexity

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|**Recursive**|O(2ⁿ)|O(n) (stack)|Very inefficient for large `n`|
|**2D DP (Tabulation)**|O(n²)|O(n²)|Fills a table of size (n+1)×n|
|**1D DP (Optimized)**|**O(n²)**|**O(n)**|Best approach for this problem|

---

## 🔍 Example

```python
price = [3, 5, 8, 9, 10, 17, 17, 20]
Solution().cutRod(price)  # Output: 24
```

Explanation:

- Best cuts for rod of length 8: two cuts of length 2 (price 5) and two cuts of length 2 → total = 4×5 = 20
    
- But better is: 6 + 2 → 17 + 5 = 22
    
- Or: 2 + 2 + 2 + 2 → 4×5 = 20
    
- **Best**: 2×1 + 6 → 2×3 + 17 = **23**
    
- **Best overall**: 2×1 + 6 = 3 + 3 + 17 = **23**, or some other combo reaching **24** depending on values
    

---

## ✅ Final Recommendation

Use the **1D DP approach** for production or competitive programming:

- It retains the time efficiency of tabulation
    
- Saves space from `O(n²)` to `O(n)`
    
- Easy to implement and extend
    

Let me know if you'd like to also **return the cuts used**, or print all combinations that yield the max value!



# [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

We have shifted index

Here's a **well-documented version** of your `longestCommonSubsequence` implementation that includes:

1. **Brute-force recursion**
    
2. **Top-down memoization (recursive with caching)**
    
3. **Bottom-up tabulation**
    
4. **Bottom-up with space optimization**
    

Each version includes:

- Clear inline comments
    
- Time and space complexity analysis
    

---

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        """
        Computes the length of the longest common subsequence (LCS) between two strings.

        Approaches covered:
        1. Brute-force recursion (commented)
        2. Top-down DP (memoization)
        3. Bottom-up DP (tabulation) [commented]
        4. Bottom-up DP with space optimization (active)

        Time Complexity:
            - All DP approaches: O(m * n), where m = len(text1), n = len(text2)
        
        Space Complexity:
            - Brute-force recursion: O(m + n) (call stack)
            - Memoization: O(m * n) for cache + O(m + n) for recursion stack
            - Tabulation: O(m * n)
            - Space-optimized DP: O(n)

        Returns:
            int: Length of the longest common subsequence
        """

        m = len(text1)
        n = len(text2)

        ### 1. Brute-force Recursion (Exponential time complexity) ###
        # def helper(a, b):
        #     if a == 0 or b == 0:
        #         return 0
        #     if text1[a - 1] == text2[b - 1]:
        #         return 1 + helper(a - 1, b - 1)
        #     else:
        #         return max(helper(a - 1, b), helper(a, b - 1))
        # return helper(m, n)

        ### 2. Top-down Memoization ###
        # Uncomment this block to use memoization approach

        # dp = [[-1 for _ in range(n + 1)] for _ in range(m + 1)]

        # def helper(a, b):
        #     if a == 0 or b == 0:
        #         return 0
        #     if dp[a][b] != -1:
        #         return dp[a][b]
        #     if text1[a - 1] == text2[b - 1]:
        #         dp[a][b] = 1 + helper(a - 1, b - 1)
        #     else:
        #         dp[a][b] = max(helper(a - 1, b), helper(a, b - 1))
        #     return dp[a][b]

        # return helper(m, n)

        ### 3. Bottom-up Tabulation (Full DP Table) ###
        # Uncomment this block for a non-recursive full DP version

        # dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
        # for a in range(1, m + 1):
        #     for b in range(1, n + 1):
        #         if text1[a - 1] == text2[b - 1]:
        #             dp[a][b] = 1 + dp[a - 1][b - 1]
        #         else:
        #             dp[a][b] = max(dp[a - 1][b], dp[a][b - 1])
        # return dp[m][n]

        ### 4. Bottom-up Tabulation with Space Optimization (Optimal version) ###
        prev = [0] * (n + 1)
        curr = [0] * (n + 1)

        for a in range(1, m + 1):
            for b in range(1, n + 1):
                if text1[a - 1] == text2[b - 1]:
                    curr[b] = 1 + prev[b - 1]
                else:
                    curr[b] = max(prev[b], curr[b - 1])
            prev, curr = curr, prev  # Swap arrays to reuse space

        return prev[n]
```

---

### ✅ Summary of All Approaches:

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Brute-force recursion|Exponential|O(m + n)|Highly inefficient, for learning only|
|Top-down with memoization|O(m * n)|O(m * n) + O(m + n)|Caches overlapping subproblems|
|Bottom-up tabulation|O(m * n)|O(m * n)|Iterative, avoids recursion stack|
|Space-optimized tabulation|O(m * n)|O(n)|Most optimal in both time and space|

---




# [ Print Longest Common Subsequence](https://www.naukri.com/code360/problems/print-longest-common-subsequence_8416383?leftPanelTabValue=PROBLEM)

```
def findLCS(n: int, m: int, s1: str, s2: str) -> str:
    # Write your code here
    n,m=m,n
    dp=[[0 for _ in range(n+1)] for _ in range(m+1)]
    for a in range(1,m+1):
        for b in range(1,n+1):
            if(s1[a-1]==s2[b-1]):
                dp[a][b]=1+dp[a-1][b-1]
            else:
                dp[a][b]=max(dp[a-1][b],dp[a][b-1])
                
	#WE ONLY INCLUDE WHEN THE STR MATCH,ELSE WE MOVE UP
	r=m
    c=n
    s=""
    while(r>0 and c>0 and dp[r][c]!=0):
        if(s1[r-1]==s2[c-1]):
            s=s1[r-1]+s
            r-=1
            c-=1
        else:
            if(dp[r][c]==dp[r-1][c]):
                r-=1
            else:
                c-=1
    return s
    
```



### [Cutting Binary String](https://www.geeksforgeeks.org/problems/cutting-binary-string1342/1)

```
from functools import lru_cache

class Solution:
    def cuts(self, s):
        # code here
        n=len(s)
        powerset5=set()
        stop=2**31
        no=1
        while(no<stop):
            powerset5.add(no)
            no*=5
        
        @lru_cache(None)
        def helper(start):
            if(start==n):
                return 0
            
            min_cuts=float("inf")
            for i in range(start+1,n+1):
                sub=s[start:i]
                if sub[0]=='0':
                    continue
                
                value=int(sub,2)
                if(value in powerset5):
                    next_cut=helper(i)
                    if(next_cut!=float("inf")):
                        min_cuts = min(min_cuts, next_cut + 1)

            return min_cuts
        
        result = helper(0)
        return result if result != float('inf') else -1
                
```


# [OPTIMAL GAME PROBLEM](https://www.geeksforgeeks.org/problems/optimal-strategy-for-a-game-1587115620/1)

```PYTHON
## 1) Key observation (intuition)

When it’s your turn on the subarray `i..j`, you have two choices:

- Pick `arr[i]` → then the opponent plays optimally on `i+1..j`.
    
- Pick `arr[j]` → then the opponent plays optimally on `i..j-1`.
    

Important: the opponent tries to **minimize** _your eventual_ total (because they maximize their own). That fact leads to a `min` inside our recurrence.

---

## 2) Define DP like Striver

Let `dp[i][j]` = **maximum value the current player** can collect from the subarray `i..j` (both players play optimally).

If you pick `i`:

- Opponent will then leave you the worse of two sub-subproblems:
    
    - If opponent picks `i+1` → you get `dp[i+2][j]`
        
    - If opponent picks `j` → you get `dp[i+1][j-1]`  
        So value when picking `i` is:
        

`take_i = arr[i] + min( dp[i+2][j], dp[i+1][j-1] )`

If you pick `j`:

`take_j = arr[j] + min( dp[i+1][j-1], dp[i][j-2] )`

Take the best of these:

`dp[i][j] = max( take_i, take_j )`

Base cases:

- `dp[i][i] = arr[i]` (only one coin)
    
- If indices go out of range for `dp[...]` treat them as `0` (conveniently handled in code).
    

Time: `O(n^2)`; Space: `O(n^2)`.

```