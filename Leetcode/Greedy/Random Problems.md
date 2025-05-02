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
        - 