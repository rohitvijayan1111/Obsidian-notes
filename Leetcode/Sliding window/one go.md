

# Fixed window



- ### [1876. Substrings of Size Three with Distinct Characters](https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  A string is good if there are no repeated characters.

	Given a string s​​​​​, return the number of good substrings of length three in s​​​​​​.
	
	Note that if there are multiple occurrences of the same substring, every occurrence should be counted.
	
	A substring is a contiguous sequence of characters in a string.

    ---

    ### 💭 My Initial Thoughts
    - 

    ---

    ### ❌ Mistakes Made


	---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach
    - just maintain a sliding of 3 
    ---

    ### ✅ Final Code

    ```python
	    class Solution:
	    def countGoodSubstrings(self, s: str) -> int:
	        count = 0
	        for i in range(len(s) - 2):
	            window = s[i:i+3]
	            if len(set(window)) == 3:
	                count += 1
	        return count
	     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 
    ### 🗃 Space Complexity
    - **O(1)**
    
    ---

    ### 📚 Related Concepts and Topics




- ### [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  You are given an integer array `nums` consisting of `n` elements, and an integer `k`.
	
	Find a contiguous subarray whose **length is equal to** `k` that has the maximum average value and return _this value_. Any answer with a calculation error less than `10-5` will be accepted.

    ---

    ### 💭 My Initial Thoughts
    - 

    ---

    ### ❌ Mistakes Made
    
    ---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach
    - just a template 
    ---

    ### ✅ Final Code

    ```python
	class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        maxi=-float("inf")
        sums=0
        l=0
        n=len(nums)
        for r in range(n):
            if(r-l+1<k):
                sums+=nums[r]
            else:
                sums+=nums[r]
                maxi=max(maxi,round(sums/k,5))
                sums-=nums[l]
                l+=1
        return maxi     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 

    ### 🗃 Space Complexity
    - **O(1)** 

    ---

    ### 📚 Related Concepts and Topics



- ### [1461. Check If a String Contains All Binary Codes of Size K](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  Given a binary string `s` and an integer `k`, return `true` _if every binary code of length_ `k` _is a substring of_ `s`. Otherwise, return `false`.

    ---

    ### 💭 My Initial Thoughts
    - heheh boi , i could think of the permutations problem, to get the no of possible binary variations of length k

    ---

    ### ❌ Mistakes Made
    
    ---

    ### ✅ Key Takeaways
    -  just add the lengths of k strings into the set
    - and verify if the lengths are equal

    ---

    ### 🧭 Step-by-Step Approach
     - 
	
    ---

    ### ✅ Final Code

    ```python
	    class Solution:
    def hasAllCodes(self, s: str, k: int) -> bool:
        st=set()
        n=len(s)
        target=pow(2,k)
        for i in range(n-k+1):
            st.add(s[i:i+k])
            if(len(st)==(target)):
                return True
        return False  
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 

    ### 🗃 Space Complexity
    - **O(1)** 

    ---

    ### 📚 Related Concepts and Topics
