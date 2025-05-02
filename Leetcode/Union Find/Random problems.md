
### **[Path Existence Queries in a Graph I](https://leetcode.com/contest/weekly-contest-447/problems/path-existence-queries-in-a-graph-i/)**

#### **Problem Summary**

- You are given a graph with `n` nodes and an array `nums` representing values at each node.
- You need to determine if a path exists between two nodes given a maximum allowed difference `maxDiff`.

#### **My Initial Thoughts**

- The problem hints at using **Union-Find (Disjoint Set Union - DSU)** for connectivity checks.
- A naive approach would be to check all possible paths, but that would be inefficient.
- Instead, we can **connect consecutive nodes** if their difference is within `maxDiff`.

#### **Mistakes Made**

- **Path Compression Missing:** The `findparent` function does not fully implement path compression, which can lead to inefficiencies.
- **Incorrect Parent Check in Queries:** Instead of checking `parent[i] == parent[j]`, we should check `findparent(i) == findparent(j)`.
- **Union Logic:** The rank-based union logic is correct, but missing path compression reduces efficiency.
-  i did iterating the entire array , doing bs to find the min pair and moving towards right

#### **Key Takeaways**

- **Union-Find is powerful** for connectivity problems.
- **Path compression** is crucial for optimizing DSU operations.
- below method works because if b-a>maxDiff then c-a definently greater than maxDiff so only we can checking consecutive elements

#### **Step-by-Step Approach**

1. **Initialize DSU:** Create `parent` and `rank` arrays.
2. **Union Consecutive Nodes:** Iterate through `nums` and connect nodes where `abs(nums[i+1] - nums[i]) <= maxDiff`.
3. **Process Queries:** Use `findparent()` to check if two nodes belong to the same connected component.

#### **Time Complexity Analysis**

- **Union-Find operations** are nearly **O(1)** due to path compression.
- **Iterating through `nums`** takes **O(n)**.
- **Processing queries** takes **O(q)**.
- **Overall Complexity:** **O(n + q)**.

#### **Space Complexity Analysis**

- **DSU storage** requires **O(n)**.
- **Result storage** requires **O(q)**.
- **Overall Complexity:** **O(n + q)**.

#### **Related Concepts and Topics**

- **Union-Find (Disjoint Set Union - DSU)**
- **Graph Connectivity**
- **Path Compression**
