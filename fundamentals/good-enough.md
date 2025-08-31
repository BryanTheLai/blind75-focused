| Tier | Pattern Category | Problem | Status | Pattern Used / Key Concept |
| :--: | :--------------- | :---------------------------------------------------- | :----: | :---------------------------------------------------- |
| S | **Arrays & Hashing** | | | **(Basic data structure lookups & counts)** |
| S | | [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) | ✅ | Hash Set (Boolean check) |
| S | | [Valid Anagram](https://leetcode.com/problems/valid-anagram/) | ✅ | Hash Map (Character counts) |
| S | | [Two Sum](https://leetcode.com/problems/two-sum/) | ✅ | Hash Map (Value-to-index lookup) |
| S | | [Group Anagrams](https://leetcode.com/problems/group-anagrams/) | ✅ | Hash Map (Key = sorted string/char counts) |
| S | | [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | ✅ | Hash Set (Efficient `num-1` check for start) |
| S | | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | ✅ | 2-Pass Iteration (Prefix/Suffix Products) |
| S | **Two Pointers & Sliding Window** | | | **(Optimizing array/string traversal)** |
| S | | [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) | ✅ | Two Pointers (In-place comparison) |
| S | | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | ✅ | Sliding Window (Greedy, single pass) |
| S | | [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | ✅ | Two Pointers (Greedy, move shorter height) |
| S | | [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | ✅ | Sliding Window + Hash Set (Shrink from left on duplicate) |
| S | | [3Sum](https://leetcode.com/problems/3sum/) | ✅ | Two Pointers (Nested in loop, duplicate handling) |
| S | **Stack** | | | **(LIFO for matching & processing)** |
| S | | [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) | ✅ | Stack (Matching opening/closing brackets) |
| S | **Linked Lists (NEW!)** | | | **(Pointer manipulation)** |
| S | | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | ⬜ | Iterative (Three pointers: `prev`, `curr`, `next`) |
| S | | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | ⬜ | Two Pointers (Iterative merging) |
| S | **Trees (DFS)** | | | **(Depth-first recursive exploration)** |
| S | | [Invert/Flip Binary Tree](https://leetcode.com/problems/invert-binary-tree/) | ✅ | Tree DFS (Swap children, simple recursion) |
| S | | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | ✅ | Tree DFS (Max of children's depth + 1) |
| S | | [Same Tree](https://leetcode.com/problems/same-tree/) | ✅ | Tree DFS (Recursive value & structure comparison) |
| S | | [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/) | ✅ | Tree DFS (Nested `isSameTree` checks) |
| S | | [Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary_search_tree/) | ✅ | Tree DFS (BST property for efficient traversal) |
| S | | [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) | ⬜ | Tree DFS (Pass `min_val` / `max_val` bounds) |
| S | **Breadth-First Search (BFS) (NEW!)** | | | **(Level-by-level exploration, uses a Queue)** |
| S | | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) | ⬜ | BFS (Queue-based iteration, current level processing) |
| A | **Binary Search (Advanced)** | | | **(Logarithmic search on sorted/partially sorted data)** |
| A | | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | ⬜ | Binary Search (Identify sorted side, narrow search) |
| A | | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | ⬜ | Binary Search (Locate pivot, then standard search) |
| A | **Heap / Priority Queue** | | | **(Efficient min/max retrieval)** |
| A | | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | ⬜ | Hash Map + Min-Heap (Maintain K largest elements) |
| A | | [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) | ⬜ | Two Heaps (Balance left Max-Heap, right Min-Heap) |
| A | **Dynamic Programming (NEW!)** | | | **(Breaking problems into overlapping subproblems)** |
| A | | [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) | ⬜ | DP (Memoization / Tabulation, Fibonacci pattern) |
| A | **Graphs (NEW!)** | | | **(Node & Edge relationships, traversal)** |
| A | | [Number of Islands](https://leetcode.com/problems/number-of-islands/) | ⬜ | Graph Traversal (DFS or BFS on 2D grid, mark visited) |
