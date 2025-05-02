
- [ ] **Is Binary Tree Heap** [🔗](https://www.geeksforgeeks.org/problems/is-binary-tree-heap/1)
    - [ ] What did I learn?
        - I learnt that we can use level order traversal.
        - Check if left and right children exist; add them to the queue (even None nodes).
        - Check heap maximum condition at every step.
        - As soon as we first encounter a `None`, set `nullSeen = True`.
        - If any node comes after `None`, the tree is not a valid heap (violates completeness).
    - [ ] Where did I go wrong?
        - I used DFS instead of BFS.
        - I didn't handle completeness properly.
        - I tried passing left node values to right node thinking in terms of depth instead of structure.
    - [ ] Notes
        - Level order traversal is crucial for heap property checking.
        - Completeness is *not* just depth-related, it's about node positioning.
    - [ ] Related Topics
        - Binary Tree
        - Heap
        - Breadth First Search


