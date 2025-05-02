- [ ] **Majority Element** [🔗](https://www.geeksforgeeks.org/problems/majority-element-1587115620/1)
    - [ ] What did I learn?
        - Used Boyer-Moore Majority Vote Algorithm to find majority element in O(n) time and O(1) space.
    - [ ] Where did I go wrong?
        - 
    - [ ] Notes
        - Boyer-Moore keeps a candidate and adjusts a counter; if counter drops to zero, candidate is updated.
        - After finding candidate, verify if it actually appears more than n/2 times.
    - [ ] Related Topics
        - Array
        - Greedy
        - Voting Algorithm
        -
-  **2145. Count the Hidden Sequences** [🔗](https://leetcode.com/problems/count-the-hidden-sequences/)
    
    -  Problem Summary (What is given and what is needed?)
	     #flashcards/leetcode/Arrays
        - You are given an array `differences` that represents the difference between consecutive elements of a hidden sequence. You are also given two integers `lower` and `upper`, which define the allowed inclusive range for each element of the hidden sequence. You need to return how many possible hidden sequences exist that satisfy the given differences and the value range. :: [Answer](obsidian://open?vault=Obsidian%20Vault&file=Leetcode%2FArray%2FRandom%20Problems)<!--SR:!2025-04-29,2,248-->

            
    -  My Initial Thoughts
        
        - I observed that the `differences` array was given, so I thought of creating the actual hidden array by keeping the first element as X and constructing the rest using the difference array.
            
        - Then I realized we could find the answer by calculating `r - l + 1` (where r is the highest valid starting point and l is the lowest).
            
        - `r = upper - max(prefix sums)`
            
        - `l = lower - min(prefix sums)`
            
        - If `l > r`, it means no valid sequences exist.
            
        - Otherwise, the number of sequences is `r - l + 1`.
            
    -  Mistakes Made
        
        - Instead of checking if `l > r`, I mistakenly checked whether both `l` and `r` were within the `lower` and `upper` bounds.
            
    -  Key Takeaways
        
        - It's better to focus on the minimum and maximum prefix sums to figure out the valid starting range, rather than checking each starting number individually.
            
        - Carefully think through what conditions actually invalidate a solution.
            
    -  Step-by-Step Approach
        
        - Initialize `mini` and `maxi` to 0.
            
        - Traverse the `differences` array to calculate running sums (prefix sums), and update `mini` and `maxi` with the minimum and maximum prefix sum values.
            
        - Calculate `r_bound = upper - maxi` and `l_bound = lower - mini`.
            
        - If `l_bound > r_bound`, return 0 (no valid sequences).
            
        - Otherwise, return `r_bound - l_bound + 1` as the count of possible sequences.
            
    -  Time Complexity Analysis
        
        - O(n), where n is the length of the `differences` array (single pass).
            
    -  Space Complexity Analysis
        
        - O(1), only a few extra variables used.
            
    -  Related Concepts and Topics
        
        - Prefix Sums
            
        - Array Traversal
            
        - Math (Range Calculations)

- **781. Rabbits in Forest** [🔗](https://leetcode.com/problems/rabbits-in-forest/)
    
    - Problem Summary (What is given and what is needed?) 
	    #flashcards/leetcode/Arrays
        - You are given an array `answers` where `answers[i]` represents the number of other rabbits with the same color as rabbit `i`.You need to return the minimum number of rabbits that could be in the forest. ::[Answer](obsidian://open?vault=Obsidian%20Vault&file=Leetcode%2FArray%2FRandom%20Problems)<!--SR:!2025-04-29,2,248-->
        
    - My Initial Thoughts
        
        - I observed that for each rabbit answering `i`, there must be `i + 1` rabbits of that color in total.
            
        - I thought initially that rabbits with the same answer could all be part of one group, but realized that if there are more rabbits than `i + 1`, we need multiple groups.
            
        - We must group rabbits in batches of `i + 1` to minimize the total number of rabbits.
            
        - Rabbits answering `0` are alone and each immediately adds one to the total.
            
    - Mistakes Made
        
        - Initially, I wrongly assumed all rabbits with the same answer belonged to one group regardless of count.
            
        - Forgot to account for the fact that once we exceed `i + 1` rabbits with the same answer, new groups must start.
            
    - Key Takeaways
        
        - Group rabbits with the same answer into batches of `i + 1`.
            
        - Use ceiling division (`ceil(count / (i + 1))`) to determine how many groups we need for each answer value.
            
        - Carefully handle rabbits who answered `0` separately.
            
    - Step-by-Step Approach
        
        - Initialize a hashmap to count the occurrences of each answer.
            
        - Track rabbits who answered `0` separately since they don't need grouping.
            
        - For each distinct non-zero answer `i`:
            
            - Calculate the number of groups needed as `ceil(count[i] / (i + 1))`.
                
            - Add `groups * (i + 1)` rabbits to the total.
                
        - Add the count of `0`-answer rabbits directly to the total.
        
    - Time Complexity Analysis
        
        - O(n), where n is the number of rabbits (`answers.length`).
            
        - One pass to build the frequency map, and one pass to compute the result.
            
    - Space Complexity Analysis
        
        - O(n), extra space for the hashmap to store the frequency of each unique answer.
            
    - Related Concepts and Topics
        
        - Hash Map
            
        - Greedy Strategy
            
        - Math (Ceiling Division)

- **2799. Count Complete Subarrays in an Array** [🔗](https://leetcode.com/problems/count-complete-subarrays-in-an-array/)
    
    - **Problem Summary**  
        You are given an array `nums` consisting of positive integers.  
        A subarray of an array is complete if the number of distinct elements in the subarray is equal to the number of distinct elements in the whole array.  
        Return the number of complete subarrays.
        
    - **My Initial Thoughts**
        
        - Initially, I thought of brute-forcing the solution by checking all possible subarrays and counting distinct elements, but this would be inefficient for large arrays.
            
        - Then, I realized that the key to solving this efficiently is tracking the distinct elements in the array and considering how to avoid overlapping subarrays.
            
    - **Mistakes Made**
        
        - My initial approach was to check all subarrays and count distinct elements manually, which was too slow for larger inputs.
            
        - I misunderstood the optimization around how to efficiently track the distinct elements in both the subarray and the whole array. Once I figured that out, the approach became much clearer.
            
        - After realizing that I could use a sliding window technique along with a stack for identifying next distinct elements, I corrected my approach.
            
    - **Key Takeaways**
        
        - Using a sliding window to dynamically adjust the subarray is an effective way to handle problems where we need to count distinct elements.
            
        - The stack-based solution for tracking the next distinct element was crucial in reducing time complexity, making the solution feasible even for larger arrays.
            
    - **Step-by-Step Approach**
        
        - **Step 1**: Identify the number of distinct elements in the entire array (`distinct`).
            
        - **Step 2**: Use a sliding window to iterate through subarrays and maintain a count of distinct elements within the window.
            
        - **Step 3**: Utilize a stack to find the next distinct element efficiently.
            
        - **Step 4**: Track subarrays that contain exactly the same number of distinct elements as the entire array, and avoid double-counting.
            
        - **Step 5**: Return the count of complete subarrays.
            
    - **Time Complexity Analysis**
        
        - The time complexity is O(n), where `n` is the length of the array. This is because the algorithm uses a sliding window approach, where each element is processed a constant number of times (for each `l` and `r` pointer shift).
            
    - **Space Complexity Analysis**
        
        - The space complexity is O(n), primarily due to the usage of the `nextdistinct` array and the dictionary for tracking counts of elements in the sliding window. In the worst case, we could have O(n) distinct elements.
            
    - **Related Concepts and Topics**
        
        - Sliding Window
            
        - Stack
            
        - Hashing/Hashmap
            
        - Two Pointers
            
        - Distinct Elements Count
            
- **[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
    
    - Problem Summary (What is given and what is needed?) 
    - #flashcards/leetcode/Arrays 
	    - Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`. :: [Answer](obsidian://open?vault=Obsidian%20Vault&file=Leetcode/[Category]/[Problem Title])
            
    - Key Takeaways
	    - We maintain:
		    - A running total called `prefix_sum` (the sum of elements from the start up to the current index).
		        
		    - A **hash map** (`prefix_counts`) where:
		        
		        - **Key** = a prefix sum value.
		            
		        - **Value** = how many times that prefix sum has occurred so far.
	            
	- At each index `i`:
	    1. We add `nums[i]` to `prefix_sum`.
	        
	    2. We want to know: **Has there been a prefix sum earlier such that removing it would give us exactly k?**
	        
	        - i.e., Is `(prefix_sum - k)` already in our `prefix_counts`?
	            
	    3. If yes, **the count of that earlier prefix_sum** tells us how many subarrays (ending at the current `i`) have a sum of exactly `k`.
	        
	        - We add that number to our final `count`.
	            
	    4. Then, we update the `prefix_counts` by incrementing `prefix_sum`'s frequency.       
	 - Time Complexity Analysis
	        
	        - (Describe the time complexity, e.g., O(n), and explain briefly why.)
		    O(n)​        
    - Space Complexity Analysis
        
        - O(n)​

- **[2962. Count Subarrays Where Max Element Appears at Least K Times](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/)**  
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - You are given an integer array `nums` and a **positive** integer `k`.
    - Return the **number of subarrays** where the **maximum element** of `nums` appears **at least `k` times**.

    ---

    ### 💭 My Initial Thoughts
    - Initially thought about precomputing next max element positions.
    - Realized we can track the count of max as we iterate using a sliding window.

    ---

    ### ❌ Mistakes Made
    - Tried a flawed approach using a `while` loop and manually managing `r` and `l`.
    - Specifically, incrementing `r` incorrectly outside the loop caused bugs.
    - Here's the problematic sketch:
      ```python
      l = 0
      r = 0
      c = 0
      res = 0
      maxi = max(nums)
      n = len(nums)
      
      while l <= r and r < n:
          if c < k:
              if nums[r] == maxi:
                  c += 1
          if c == k:
              res += (n - r)
              if nums[l] == maxi:
                  c -= 1
              l += 1
              continue
          r += 1
      return res
      ```

    ---

    ### ✅ Key Takeaways
    - Sliding window problems often require careful ordering of `l` and `r`.
    - When shrinking `l` while `r` is fixed, use `while` loop to count valid subarrays.
    - `res += (n - r)` works because once the window satisfies the condition, all subarrays ending beyond `r` are valid.

    ---

    ### 🧭 Step-by-Step Approach
    - Set `maxi = max(nums)` to fix the max element to track.
    - Iterate with `r` (right boundary), increment `count` if `nums[r] == maxi`.
    - If `count >= k`, move `l` rightward until it's no longer valid.
    - Each time condition is valid, count subarrays with `res += (n - r)`.

    ---

    ### ✅ Final Code

    ```python
    class Solution:
        def countSubarrays(self, nums: List[int], k: int) -> int:
            l = 0
            c = 0
            n = len(nums)
            res = 0
            maxi = max(nums)
            for r in range(n):
                if nums[r] == maxi:
                    c += 1
                while c >= k:
                    res += (n - r)
                    if nums[l] == maxi:
                        c -= 1
                    l += 1
            return res
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** — each element is visited at most twice (once by `r`, once by `l`).

    ### 🗃 Space Complexity
    - **O(1)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics
    - Sliding Window
    - Two Pointers
    - Arrays
    - Frequency Counting
