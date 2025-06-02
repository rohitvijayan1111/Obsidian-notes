
# Two pass



-  **Rabbits in Forest** [🔗](https://leetcode.com/problems/rabbits-in-forest/description/?envType=daily-question&envId=2025-04-26)
    
    -  **What did I learn?**
        
        - When multiple rabbits report the same number, it doesn’t always mean they belong to the same group.
            
        - Always account for grouping based on the _maximum possible size_ a number implies (i.e., `i + 1`).
            
        - Using `ceil(count / (i + 1))` helps to figure out the minimum number of groups needed.
            
    -  **Where did I go wrong?**
        
        - I assumed that if rabbits reported the same number, they must be from the same group.
            
        - I missed edge cases:
            
            - If the answer is 0, it means _only one rabbit_ claimed no others are of their color.
                
            - If there are _more occurrences_ than `i + 1`, it requires multiple groups.
                
    -  **Notes**
        
        - Use a `Counter` to count how many rabbits give the same answer.
            
        - For each unique answer `i`, the number of groups needed = `ceil(count[i] / (i + 1))`.
            
        - Total rabbits for that answer = number of groups × (i + 1).
            
        - `math.ceil()` is important because you can't split a group.
            
    -  **Time Complexity**
        
        - `O(n)` where `n` is the number of rabbits (since you traverse the list once and then go through each unique number once).
            
    -  **Space Complexity**
        
        - `O(n)` for the hash map / Counter storing frequencies.
            
    -  **Related Topics**
        
        - Greedy
            
        - Hash Table
            
        - Math
            
        - Counting




- ### [135. Candy](https://leetcode.com/problems/candy/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.
	
	You are giving candies to these children subjected to the following requirements:
	
	- Each child must have at least one candy.
	- Children with a higher rating get more candies than their neighbors.
	
	Return _the minimum number of candies you need to have to distribute the candies to the children_.

    ---

    ### 💭 My Initial Thoughts
    -  I plotted this in an graph and found that we increased the nodes value when it was increasing edge and when we found an decreasing edge we try to find an position where an decreasing stops , and give the curr node such a value high so that every other element has one less value

    ---

    ### ❌ Mistakes Made

    ---

    ### ✅ Key Takeaways
    -  LEARNT TWO PASS ALGORITHM -> USEFUL WHEN PROBLEMS REVOLVE AROUND NEIGHBOURS

    ---

    ### 🧭 Step-by-Step Approach

	 - have an candies array, and set all the value to 1
	 - the go for the ascending order, increase it ,1 more than the prev value
	 - similarly for the decreasing order, by standing from n-2
	 
    ---

    ### ✅ Final Code

    ```python
    class Solution:
    def candy(self, ratings: List[int]) -> int:
        n=len(ratings)
        candies=[1 for _ in range(n)]
        for i in range(1,n):
            if(ratings[i]>ratings[i-1]):
                candies[i]=candies[i-1]+1
        
        for i in range(n-2,-1,-1):
            if(ratings[i]>ratings[i+1]):
                candies[i]=max(candies[i],candies[i+1]+1)
        return sum(candies)
     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(2n)** 

    ### 🗃 Space Complexity
    - **O(n)** 
    ---

    ### 📚 Related Concepts and Topics
