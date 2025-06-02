
# Two pass algorithm

Absolutely! Here's a clean and organized **note-style summary** of the **Two-Pass Greedy Algorithm** technique, specifically formatted for **Obsidian Markdown**.

---

### 📘 Two-Pass Greedy Algorithm

---

#### 🔍 **Concept**

The **two-pass greedy algorithm** is used when:

- Each element must satisfy constraints based on **its neighbors** (often left and right).
    
- You can resolve the problem by doing two linear scans: one **left-to-right** and one **right-to-left**.
    

---

#### ✅ **When to Use**

- Problems with **local comparisons**: e.g. `arr[i] > arr[i+1]` implies `score[i] > score[i+1]`
    
- Each element depends on adjacent elements.
    
- You can’t fully determine the final state from a single direction.
    

---

#### 🧠 **General Steps**

1. **Initialize** a helper array `result[]` (e.g., all 1s).
    
2. **Left to Right Pass**
    
    - If `arr[i] > arr[i - 1]`, then `result[i] = result[i - 1] + 1`
        
3. **Right to Left Pass**
    
    - If `arr[i] > arr[i + 1]`, then `result[i] = max(result[i], result[i + 1] + 1)`
        
4. **Sum up** the result to get the final answer (if needed)
    

---

#### 🧑‍🏫 **Example: Candy Distribution**

```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n

    # Left to right
    for i in range(1, n):
        if ratings[i] > ratings[i - 1]:
            candies[i] = candies[i - 1] + 1

    # Right to left
    for i in range(n - 2, -1, -1):
        if ratings[i] > ratings[i + 1]:
            candies[i] = max(candies[i], candies[i + 1] + 1)

    return sum(candies)
```

---

#### 🧩 **Key Observations**

- The **first pass** handles strictly increasing sequences.
    
- The **second pass** corrects for decreasing sequences missed by the first pass.
    
- Taking the **maximum** in the second pass avoids breaking the first pass logic.
    

---

#### 📚 **Other Problems That Use This Pattern**

|Problem|Explanation|
|---|---|
|Trapping Rain Water|First pass: max height to the left, second: to the right|
|Longest Mountain|One pass for up sequence, one for down|
|Gas Station (circular)|Sometimes solved by analyzing two directions|
|Min Jumps with constraints|Forward and backward adjustment needed|

---

#### 🧭 **When NOT to Use**

- When constraints are **global** or **non-linear**
    
- When decisions depend on **far elements**, not just neighbors
    
- When a **graph or tree** structure is involved — prefer DFS/BFS or DP
    

---

Let me know if you'd like this exported as a `.md` file or if you want it tailored for another topic like "Trapping Rain Water" or "Longest Mountain."



# 🔖 TL;DR Table for Obsidian

|Pattern|Description|Example|
|---|---|---|
|Two-pass|Greedy left → right & right → left|Candy, Rain Water|
|Sort-based|Sort by strategy & pick|Activity Select, Knapsack|
|Heap-based|Best next via heap|Dijkstra, Task Scheduling|
|Interval jump|Maximize distance|Jump Game II, Stitching|
|MST Greedy|Pick smallest edge|Kruskal, Prim|
|Local greedy|Pick local optimum|Cookies, Intervals|
|Monotonic|Maintain order stack|Histogram, Sliding Max|