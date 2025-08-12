# The Fundamentals S-Tier Patterns Playbook

## Overview: 4 Patterns to Rule Them All

We will master four fundamental patterns that cover the bulk of S-Tier problems.

1.  **The One-Pass Hash Map:** Frequencies, duplicates, or lookups.
2.  **The Sliding Window / Two Pointers:** Finding an optimal value in a contiguous subarray or sequence.
3.  **The Recursive Tree Traversal (DFS):** Hierarchical data, validation, or pathfinding in a tree.
4.  **The LIFO Stack:** Matching pairs or sequential validation.

---

### **Pattern 1: The One-Pass Hash Map**

🧠 **Core Idea:** Iterate through your data once. Use a hash map (a Python `dict`) to store information you've already seen. On each new element, use your map to make an immediate decision.

💡 **When to Use (Problem Triggers):**

- "Find duplicates"
- "Check for anagrams"
- "Find two numbers that sum to a target"
- "Group items by a certain property"
- "Count frequencies"

⚙️ **The Code Template:**

```python
def hash_map_pattern(items: list) -> any:
    seen_map: dict = {}

    for i, item in enumerate(items):
        # 1. Check the map for a condition
        if some_condition_based_on(item, seen_map):
            # 2. Return the result immediately
            return create_result_from(item, seen_map)

        # 3. If no condition met, update the map with current item info
        update_map_with(item, i, seen_map)

    # 4. Return a default value if the loop finishes
    return default_result()
```

🔧 **Worked Example: `Two Sum`**
_Problem: Find two numbers in a list that add up to a target._

```python
def two_sum(nums: List[int], target: int) -> List[int]:
    # Our hash map will store: {number_needed: index_of_current_number}
    seen_map: dict = {} # e.g., {5: 0} means we need a 5 to complete a pair with the number at index 0.

    for i, num in enumerate(nums):
        # 1. Check the map: Is the current number something we need?
        if num in seen_map:
            # 2. Yes! We found the pair. Return current index and the stored index.
            return [seen_map[num], i]

        # 3. No. Update the map with what we *now* need and the current index.
        needed = target - num
        seen_map[needed] = i

    # 4. No solution found.
    return []
```

This single pattern also solves `Contains Duplicate`, `Valid Anagram`, and `Group Anagrams` with minor logic changes inside the loop.

---

### **Pattern 2: The Sliding Window**

🧠 **Core Idea:** Use two pointers (`left`, `right`) to define a "window" over a sequence. Expand the window by moving `right`. When a condition is violated, contract the window by moving `left` until the condition is valid again.

💡 **When to Use (Problem Triggers):**

- "Longest/shortest subarray/substring"
- "Best time to buy/sell"
- "Find a subarray/substring that meets a criteria"
- Problems on contiguous arrays/strings.

⚙️ **The Code Template:**

```python
def sliding_window_pattern(items: list) -> int:
    left: int = 0
    best_result: int = 0
    current_window_state: any = initialize_state() # e.g., a hash map, a set, a sum

    for right, item in enumerate(items):
        # 1. Add the rightmost element to the window
        update_state_add(item, current_window_state)

        # 2. Check if the window is now invalid. If so, shrink it from the left.
        while window_is_invalid(current_window_state):
            left_item = items[left]
            update_state_remove(left_item, current_window_state)
            left += 1

        # 3. The window is now valid. Update the best result seen so far.
        best_result = max(best_result, calculate_current_result(left, right))

    return best_result
```

🔧 **Worked Example: `Longest Substring Without Repeating Characters`**
_Problem: Find the length of the longest substring with no duplicate characters._

```python
def length_of_longest_substring(s: str) -> int:
    left: int = 0
    best_result: int = 0
    # The "state" is the set of characters currently in our window
    char_set: set = set()

    for right, char in enumerate(s):
        # 1. Add to window (implicitly done by the loop)

        # 2. Check for invalid state (duplicate character) and shrink
        while char in char_set:
            left_char = s[left]
            char_set.remove(left_char)
            left += 1

        # The window is now valid (no duplicates). Add the new char.
        char_set.add(char)

        # 3. Update best result. The current window length is (right - left + 1).
        best_result = max(best_result, right - left + 1)

    return best_result
```

This pattern, with slight variations, is the key to `Best Time to Buy and Sell Stock` and `Container With Most Water`.

---

### **Pattern 3: Recursive Tree Traversal (DFS)**

🧠 **Core Idea:** To solve a problem for a tree, solve it for the root's `left` and `right` children, then combine their results. This naturally leads to a recursive function that is called on the left and right subtrees. The base case is almost always `if not root: return ...`.

💡 **When to Use (Problem Triggers):**

- Any problem involving a binary tree.
- "Find the depth/height"
- "Validate a property of the tree" (e.g., is it a valid BST?)
- "Find a path"
- "Invert/modify the tree"

⚙️ **The Code Template:**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

def dfs_tree_pattern(root: Optional[TreeNode]) -> any:
    # 1. Base Case: What happens at the end of a branch?
    if not root:
        return base_case_value()

    # 2. Recursive Step: Call the function on the children
    left_result = dfs_tree_pattern(root.left)
    right_result = dfs_tree_pattern(root.right)

    # 3. Combine & Return: Use the root's value and the children's results
    #    to calculate the result for the current node's subtree.
    return combine_results(root.val, left_result, right_result)
```

🔧 **Worked Example: `Maximum Depth of Binary Tree`**
_Problem: Find the longest path from the root to a leaf._

```python
def max_depth(root: Optional[TreeNode]) -> int:
    # 1. Base Case: An empty tree has a depth of 0.
    if not root:
        return 0

    # 2. Recursive Step: Find the depth of the left and right subtrees.
    left_depth = max_depth(root.left)
    right_depth = max_depth(root.right)

    # 3. Combine & Return: The depth of this tree is 1 (for the current node)
    #    plus the depth of the deeper of its two children.
    return 1 + max(left_depth, right_depth)
```

This DFS template is the direct solution for `Invert Tree`, `Same Tree`, `Subtree of Another Tree`, `Validate BST`, and `LCA of BST`.

---

### **Pattern 4: The LIFO Stack**

🧠 **Core Idea:** For problems involving matching pairs or nested structures, use a stack. When you see an "opening" item, push it onto the stack. When you see a "closing" item, pop from the stack and check if it's a valid match.

💡 **When to Use (Problem Triggers):**

- "Valid parentheses/brackets/braces"
- "Matching pairs"
- Evaluating expressions in Reverse Polish Notation.

⚙️ **The Code Template:**

```python
def stack_pattern(items: str) -> bool:
    stack: list = []
    # A map can be useful for matching pairs
    matching_map: dict = { '(': ')', '{': '}', '[': ']' }

    for item in items:
        # 1. If it's an "opening" item, push it onto the stack.
        if item in opening_items:
            stack.append(item)
        # 2. If it's a "closing" item...
        elif item in closing_items:
            # Check for an empty stack or a mismatch.
            if not stack or matching_map[stack.pop()] != item:
                return False # Invalid

    # 3. After the loop, a valid sequence has an empty stack.
    return not stack
```

🔧 **Worked Example: `Valid Parentheses`**

```python
def is_valid(s: str) -> bool:
    stack: list = []
    close_to_open_map: dict = {')': '(', '}': '{', ']': '['}

    for char in s:
        # 1. Is it a closing parenthesis?
        if char in close_to_open_map:
            # 2. If so, check for empty stack or mismatch with the top item.
            # The `stack.pop()` will raise an error on an empty stack if we don't check `stack` first.
            if stack and stack[-1] == close_to_open_map[char]:
                stack.pop()
            else:
                return False # Invalid sequence
        else:
            # 3. It's an opening parenthesis. Push it onto the stack.
            stack.append(char)

    # 4. A valid string will result in an empty stack.
    return not stack
```

---

### **The Learning Protocol: A Focused Approach**

1.  **Focused Block (90 mins):** Pick ONE pattern. Read the template. Understand its core idea.
2.  **Solve & Narrate:** Open the first problem for that pattern. Try to solve it by "filling in the blanks" of the template. Explain your logic out loud as you code.
3.  **Repeat:** Solve the other problems for that pattern. Notice how the template remains the same while the internal logic changes slightly.
4.  **Spaced Repetition:** The next day, before starting a new pattern, pick one problem from yesterday and solve it again from a blank slate. This solidifies the memory.

---

### Pattern Coverage Checklist (S & A Tiers)

This table shows how these four core patterns address the majority of high-priority problems.

| Tier  | Problem                                                                                                                         | Applicable Pattern                | Covered? |
| :---: | :------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------- | :------- |
| **S** | [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)                                                         | Hash Map                          | ✅       |
| **S** | [Valid Anagram](https://leetcode.com/problems/valid-anagram/)                                                                   | Hash Map                          | ✅       |
| **S** | [Two Sum](https://leetcode.com/problems/two-sum/)                                                                               | Hash Map                          | ✅       |
| **S** | [Group Anagrams](https://leetcode.com/problems/group-anagrams/)                                                                 | Hash Map                          | ✅       |
| **S** | [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)                                                             | Two Pointers                      | ✅       |
| **S** | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)                               | Sliding Window                    | ✅       |
| **S** | [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | Sliding Window                    | ✅       |
| **S** | [3Sum](https://leetcode.com/problems/3sum/)                                                                                     | Two Pointers (on sorted array)    | ✅       |
| **S** | [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)                                           | Two Pointers                      | ✅       |
| **S** | [Invert/Flip Binary Tree](https://leetcode.com/problems/invert-binary-tree/)                                                    | Tree DFS                          | ✅       |
| **S** | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)                                     | Tree DFS                          | ✅       |
| **S** | [Same Tree](https://leetcode.com/problems/same-tree/)                                                                           | Tree DFS                          | ✅       |
| **S** | [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)                                               | Tree DFS                          | ✅       |
| **S** | [Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)                  | Tree DFS                          | ✅       |
| **S** | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)                           | Tree BFS (Not DFS, but related)   | ✅       |
| **S** | [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)                                       | Tree DFS                          | ✅       |
| **S** | [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)                                                           | Stack                             | ✅       |
| **S** | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)                                     | _Specific Prefix/Postfix Pattern_ | ❌       |
| **S** | [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)                                     | Hash Set (Smart Iteration)        | ❌       |
| **A** | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)                                               | Hash Map + Heap                   | ✅       |
| **A** | [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)                                     | Heap (Two Heaps)                  | ✅       |
| **A** | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)                     | Binary Search                     | ✅       |
| **A** | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)                                 | Binary Search                     | ✅       |
| **A** | [Number of Islands](https://leetcode.com/problems/number-of-islands/)                                                           | Graph/Grid DFS                    | ✅       |
| **A** | [Clone Graph](https://leetcode.com/problems/clone-graph/)                                                                       | Graph DFS + Hash Map              | ✅       |
| **A** | [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)                                       | Graph/Grid DFS                    | ✅       |
| **A** | [Course Schedule](https://leetcode.com/problems/course-schedule/)                                                               | Graph DFS (Cycle Detection)       | ✅       |
| **A** | All 1D-DP & Backtracking problems                                                                                               | _DP/Backtracking Patterns_        | ❌       |
| **A** | All Linked List problems                                                                                                        | _Pointer Manipulation Patterns_   | ❌       |

**Statistics:**

- **S-Tier Coverage:** These 4 patterns directly solve **17 out of 19 (89%)** of the non-premium S-Tier problems.
- **Total Coverage:** They provide the foundational thinking for nearly all S and A tier problems, even those requiring specific patterns like Binary Search or Heaps. The two uncovered S-tier problems require their own unique, but simple, patterns.
