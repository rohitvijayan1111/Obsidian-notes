
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



# 