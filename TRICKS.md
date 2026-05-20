# 🧠 DSA Common Patterns — Complete Handbook

> Master the **patterns**, not just the problems. Once you recognize the pattern, the solution follows naturally.

---

## 📌 Why Patterns Matter

DSA problems number in the thousands — but the **underlying patterns** are fewer than 20. Top interviewers at FAANG companies don't expect you to memorize every problem. They expect you to **recognize the pattern** and adapt.

This handbook covers every major DSA pattern with:
- What it is and when to use it
- Visual intuition
- Template code (Python)
- Classic problems
- Time & Space complexity

---

## 📋 Table of Contents

1. [Two Pointers](#1-two-pointers)
2. [Sliding Window](#2-sliding-window)
3. [Fast & Slow Pointers](#3-fast--slow-pointers-floyds-cycle)
4. [Binary Search](#4-binary-search)
5. [Prefix Sum](#5-prefix-sum)
6. [HashMap / Frequency Count](#6-hashmap--frequency-count)
7. [Monotonic Stack](#7-monotonic-stack)
8. [BFS — Level Order Traversal](#8-bfs--level-order-traversal)
9. [DFS — Tree & Graph](#9-dfs--tree--graph)
10. [Backtracking](#10-backtracking)
11. [Dynamic Programming](#11-dynamic-programming)
12. [Greedy](#12-greedy)
13. [Merge Intervals](#13-merge-intervals)
14. [Linked List In-Place Reversal](#14-linked-list-in-place-reversal)
15. [Heap / Priority Queue](#15-heap--priority-queue)
16. [Trie](#16-trie)
17. [Union Find (Disjoint Set)](#17-union-find-disjoint-set)
18. [Bit Manipulation](#18-bit-manipulation)
19. [Pattern Recognition Cheatsheet](#19-pattern-recognition-cheatsheet)
20. [Complexity Quick Reference](#20-complexity-quick-reference)

---

## 1. Two Pointers

### 🔍 What is it?

Use two pointers (indices) that move through the array — usually from opposite ends or in the same direction — to avoid nested loops.

### ✅ When to Use
- Array/string is **sorted** (or needs to be)
- Looking for a **pair** that satisfies a condition
- Removing duplicates, partitioning
- Finding closest/smallest/largest pair sum

### 🧩 Visual

```
arr = [1, 2, 3, 4, 6],  target = 6

left=0  right=4
[1, 2, 3, 4, 6]
 L           R    → 1+6=7 > 6 → move R left

[1, 2, 3, 4, 6]
 L        R       → 1+4=5 < 6 → move L right

[1, 2, 3, 4, 6]
    L     R       → 2+4=6 ✅ FOUND
```

### 📝 Template

```python
def two_pointer(arr, target):
    left, right = 0, len(arr) - 1

    while left < right:
        current = arr[left] + arr[right]

        if current == target:
            return [left, right]        # found
        elif current < target:
            left += 1                   # need bigger sum
        else:
            right -= 1                  # need smaller sum

    return []
```

### 🎯 Variant: Same Direction (Remove Duplicates)

```python
def remove_duplicates(arr):
    if not arr:
        return 0

    slow = 0                            # slow = last unique position
    for fast in range(1, len(arr)):
        if arr[fast] != arr[slow]:      # found new unique element
            slow += 1
            arr[slow] = arr[fast]

    return slow + 1                     # length of unique subarray
```

### 📚 Classic Problems

| Problem | Hint |
|---------|------|
| Two Sum II (sorted array) | Opposite ends |
| 3Sum | Fix one, two-pointer on rest |
| Container With Most Water | Opposite ends, move shorter side |
| Remove Duplicates from Sorted Array | Slow/fast same direction |
| Valid Palindrome | Opposite ends, skip non-alphanumeric |
| Trapping Rain Water | Two pointers or prefix/suffix max |

### ⏱️ Complexity
- **Time:** O(n) — replaces O(n²) brute force
- **Space:** O(1)

---

## 2. Sliding Window

### 🔍 What is it?

Maintain a **window** (subarray/substring) that slides through the data. Expand or shrink the window based on constraints instead of recomputing from scratch.

### ✅ When to Use
- Subarray/substring of **fixed or variable size**
- Keywords: "contiguous", "substring", "subarray"
- Maximum/minimum/average of a window
- Longest substring with some constraint

### 🧩 Visual

```
Fixed window (size k=3):
arr = [2, 1, 5, 1, 3, 2]

[2, 1, 5] → sum=8
   [1, 5, 1] → sum=7
      [5, 1, 3] → sum=9  ← max
         [1, 3, 2] → sum=6
```

### 📝 Template — Fixed Window

```python
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])           # initial window
    max_sum = window_sum

    for i in range(k, len(arr)):
        window_sum += arr[i]            # add new element
        window_sum -= arr[i - k]        # remove old element
        max_sum = max(max_sum, window_sum)

    return max_sum
```

### 📝 Template — Variable Window

```python
def longest_substring_k_distinct(s, k):
    char_count = {}
    left = 0
    max_len = 0

    for right in range(len(s)):
        # expand: add right character to window
        char_count[s[right]] = char_count.get(s[right], 0) + 1

        # shrink: window violated constraint
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1

        # valid window: update answer
        max_len = max(max_len, right - left + 1)

    return max_len
```

### 📚 Classic Problems

| Problem | Type |
|---------|------|
| Max Sum Subarray of Size K | Fixed |
| Longest Substring Without Repeating | Variable |
| Minimum Window Substring | Variable (shrink to minimum) |
| Longest Subarray with Sum ≤ K | Variable |
| Find All Anagrams in a String | Fixed |
| Fruits Into Baskets | Variable (at most 2 distinct) |

### ⏱️ Complexity
- **Time:** O(n) — each element enters and leaves window once
- **Space:** O(k) for the window data structure

---

## 3. Fast & Slow Pointers (Floyd's Cycle)

### 🔍 What is it?

Two pointers move at **different speeds** through a linked list or sequence. The fast pointer moves 2 steps, the slow pointer moves 1 step.

### ✅ When to Use
- Detect a **cycle** in a linked list
- Find the **middle** of a linked list
- Find the **start of a cycle**
- Detect happy numbers

### 🧩 Visual

```
Cycle detection:

1 → 2 → 3 → 4 → 5
            ↑       ↓
            8 ← 7 ← 6

Slow: 1→2→3→4→5→6→7
Fast: 1→3→5→7→4→6→3

They meet inside the cycle → cycle exists!
```

### 📝 Template — Cycle Detection

```python
def has_cycle(head):
    slow = fast = head

    while fast and fast.next:
        slow = slow.next            # 1 step
        fast = fast.next.next       # 2 steps

        if slow == fast:
            return True             # they met → cycle exists

    return False
```

### 📝 Template — Find Middle

```python
def find_middle(head):
    slow = fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow                     # slow is at middle when fast reaches end
```

### 📝 Template — Start of Cycle

```python
def find_cycle_start(head):
    slow = fast = head

    # Phase 1: detect cycle
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None                 # no cycle

    # Phase 2: find start
    slow = head                     # reset one pointer to head
    while slow != fast:
        slow = slow.next
        fast = fast.next            # both move 1 step now

    return slow                     # they meet at cycle start
```

### 📚 Classic Problems

| Problem | Trick |
|---------|-------|
| Linked List Cycle (LC 141) | Fast/slow meet → cycle |
| Linked List Cycle II (LC 142) | Reset one pointer to find start |
| Find Middle of Linked List | Slow is at middle when fast ends |
| Happy Number | Cycle in number sequence |
| Palindrome Linked List | Find middle, reverse second half |
| Reorder List | Find middle, reverse, merge |

### ⏱️ Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 4. Binary Search

### 🔍 What is it?

Eliminate **half the search space** at each step. Works on sorted arrays, but also applies to answer-space problems (binary search on the answer).

### ✅ When to Use
- Array is **sorted**
- Looking for a specific value, or first/last occurrence
- Problem says "find minimum X such that condition holds"
- Search space can be halved each iteration

### 🧩 Visual

```
arr = [1, 3, 5, 7, 9, 11, 13], target = 7

lo=0, hi=6, mid=3 → arr[3]=7 ✅ Found
```

### 📝 Template — Classic Binary Search

```python
def binary_search(arr, target):
    lo, hi = 0, len(arr) - 1

    while lo <= hi:
        mid = lo + (hi - lo) // 2      # avoids overflow

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1

    return -1                           # not found
```

### 📝 Template — Find First Occurrence (Left Boundary)

```python
def find_first(arr, target):
    lo, hi = 0, len(arr) - 1
    result = -1

    while lo <= hi:
        mid = lo + (hi - lo) // 2
        if arr[mid] == target:
            result = mid                # record, but keep searching left
            hi = mid - 1
        elif arr[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1

    return result
```

### 📝 Template — Binary Search on Answer

```python
# "Find minimum speed such that all packages arrive in D days"
def min_capacity(weights, D):
    def can_ship(capacity):
        days, current = 1, 0
        for w in weights:
            if current + w > capacity:
                days += 1
                current = 0
            current += w
        return days <= D

    lo, hi = max(weights), sum(weights)

    while lo < hi:
        mid = lo + (hi - lo) // 2
        if can_ship(mid):
            hi = mid                    # might do better
        else:
            lo = mid + 1                # too small, increase

    return lo
```

### 📚 Classic Problems

| Problem | Variant |
|---------|---------|
| Binary Search (LC 704) | Classic |
| Search in Rotated Sorted Array | Modified — check which half is sorted |
| Find Minimum in Rotated Array | Modified |
| Koko Eating Bananas | Search on answer |
| Capacity to Ship Packages | Search on answer |
| Median of Two Sorted Arrays | Advanced |
| Search a 2D Matrix | Treat as 1D array |

### ⏱️ Complexity
- **Time:** O(log n)
- **Space:** O(1) iterative, O(log n) recursive

---

## 5. Prefix Sum

### 🔍 What is it?

Precompute cumulative sums so any **subarray sum** can be answered in O(1).

`prefix[i] = arr[0] + arr[1] + ... + arr[i]`
`sum(l, r) = prefix[r] - prefix[l-1]`

### ✅ When to Use
- Multiple queries on subarray sums
- Subarray sum equals K
- Count of subarrays with a property
- 2D range sum queries

### 📝 Template

```python
def build_prefix(arr):
    prefix = [0] * (len(arr) + 1)
    for i, val in enumerate(arr):
        prefix[i + 1] = prefix[i] + val
    return prefix

def range_sum(prefix, l, r):
    # sum of arr[l..r] (0-indexed)
    return prefix[r + 1] - prefix[l]
```

### 📝 Subarray Sum Equals K (HashMap + Prefix)

```python
def subarray_sum(arr, k):
    count = 0
    prefix = 0
    seen = {0: 1}                       # prefix sum → frequency

    for num in arr:
        prefix += num
        # if (prefix - k) was seen before, those subarrays sum to k
        count += seen.get(prefix - k, 0)
        seen[prefix] = seen.get(prefix, 0) + 1

    return count
```

### 📚 Classic Problems

| Problem | Key Idea |
|---------|----------|
| Subarray Sum Equals K | prefix + hashmap |
| Range Sum Query | precompute prefix |
| Product of Array Except Self | prefix product + suffix product |
| Count of Nice Subarrays | prefix parity |
| 2D Matrix Range Sum | 2D prefix |

### ⏱️ Complexity
- **Build:** O(n)
- **Query:** O(1)

---

## 6. HashMap / Frequency Count

### 🔍 What is it?

Use a dictionary to **count occurrences**, **store indices**, or **group elements** — turning O(n²) lookups into O(1).

### ✅ When to Use
- Count frequency of elements
- Two Sum: find complement
- Anagram detection
- Group elements by property
- First unique / most frequent element

### 📝 Templates

```python
# Frequency count
from collections import Counter
freq = Counter(arr)                     # {element: count}

# Two Sum — find indices of pair summing to target
def two_sum(nums, target):
    seen = {}                           # value → index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

# Group anagrams
def group_anagrams(strs):
    groups = {}
    for s in strs:
        key = tuple(sorted(s))          # sorted letters as key
        groups.setdefault(key, []).append(s)
    return list(groups.values())
```

### 📚 Classic Problems

| Problem | Technique |
|---------|-----------|
| Two Sum | complement hashmap |
| Valid Anagram | frequency comparison |
| Group Anagrams | sorted string as key |
| Top K Frequent Elements | counter + heap |
| Longest Consecutive Sequence | set for O(1) lookup |
| Ransom Note | frequency subtraction |

### ⏱️ Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 7. Monotonic Stack

### 🔍 What is it?

A stack that is always maintained in **strictly increasing or decreasing order**. Efficiently answers "next greater/smaller element" queries.

### ✅ When to Use
- Next Greater Element / Previous Smaller Element
- Largest rectangle in histogram
- Daily Temperatures
- Stock Span problem
- Trapping Rain Water

### 🧩 Visual

```
arr = [2, 1, 5, 3, 6]  — find Next Greater Element

Process 2: stack = [2]
Process 1: stack = [2, 1]
Process 5: 5 > 1 → NGE(1)=5, 5 > 2 → NGE(2)=5. stack = [5]
Process 3: stack = [5, 3]
Process 6: 6 > 3 → NGE(3)=6, 6 > 5 → NGE(5)=6. stack = [6]

NGE = [5, 5, 6, 6, -1]
```

### 📝 Template — Next Greater Element

```python
def next_greater(arr):
    n = len(arr)
    result = [-1] * n
    stack = []                          # stores indices (monotonic decreasing values)

    for i in range(n):
        # pop all elements smaller than current — current is their NGE
        while stack and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)

    return result
```

### 📝 Template — Largest Rectangle in Histogram

```python
def largest_rectangle(heights):
    stack = []                          # monotonic increasing
    max_area = 0
    heights.append(0)                   # sentinel to flush stack

    for i, h in enumerate(heights):
        while stack and heights[stack[-1]] > h:
            height = heights[stack.pop()]
            width = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)

    return max_area
```

### 📚 Classic Problems

| Problem | Stack Type |
|---------|------------|
| Next Greater Element I & II | Decreasing |
| Daily Temperatures | Decreasing |
| Largest Rectangle in Histogram | Increasing |
| Trapping Rain Water | Decreasing |
| 132 Pattern | Decreasing |
| Stock Span Problem | Decreasing |

### ⏱️ Complexity
- **Time:** O(n) — each element pushed/popped once
- **Space:** O(n)

---

## 8. BFS — Level Order Traversal

### 🔍 What is it?

Explore all nodes at the **current level** before moving to the next. Uses a **queue**. Guarantees shortest path in unweighted graphs.

### ✅ When to Use
- Shortest path in an **unweighted** graph or grid
- Level-by-level tree processing
- Multi-source BFS (start from multiple points)
- Word ladder, rotten oranges

### 📝 Template — Tree BFS

```python
from collections import deque

def level_order(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)         # number of nodes at current level
        level = []

        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            if node.left:  queue.append(node.left)
            if node.right: queue.append(node.right)

        result.append(level)

    return result
```

### 📝 Template — Graph BFS (Shortest Path)

```python
def bfs_shortest_path(graph, start, end):
    visited = {start}
    queue = deque([(start, 0)])         # (node, distance)

    while queue:
        node, dist = queue.popleft()

        if node == end:
            return dist

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, dist + 1))

    return -1                           # unreachable
```

### 📝 Template — Grid BFS

```python
def bfs_grid(grid, start_r, start_c):
    rows, cols = len(grid), len(grid[0])
    directions = [(0,1),(0,-1),(1,0),(-1,0)]
    visited = {(start_r, start_c)}
    queue = deque([(start_r, start_c, 0)])  # (row, col, distance)

    while queue:
        r, c, dist = queue.popleft()

        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and (nr,nc) not in visited:
                if grid[nr][nc] != '#':     # not a wall
                    visited.add((nr, nc))
                    queue.append((nr, nc, dist + 1))
```

### 📚 Classic Problems

| Problem | Variant |
|---------|---------|
| Binary Tree Level Order | Tree BFS |
| Rotting Oranges | Multi-source BFS |
| Word Ladder | Graph BFS |
| 01 Matrix | Multi-source BFS |
| Walls and Gates | Multi-source BFS |
| Shortest Path in Binary Matrix | Grid BFS |

### ⏱️ Complexity
- **Time:** O(V + E) for graphs, O(m×n) for grids
- **Space:** O(V) for the queue

---

## 9. DFS — Tree & Graph

### 🔍 What is it?

Explore as **deep as possible** along each branch before backtracking. Uses recursion (implicit stack) or explicit stack.

### ✅ When to Use
- Tree: path sums, heights, diameter, LCA
- Graph: connected components, cycle detection, topological sort
- Flood fill, number of islands
- When you need to explore all possibilities

### 📝 Template — Tree DFS

```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))

def has_path_sum(root, target):
    if not root:
        return False
    if not root.left and not root.right:    # leaf node
        return root.val == target
    return (has_path_sum(root.left, target - root.val) or
            has_path_sum(root.right, target - root.val))
```

### 📝 Template — Graph DFS (Number of Islands)

```python
def num_islands(grid):
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == '0':
            return
        grid[r][c] = '0'               # mark visited (sink the island)
        dfs(r+1, c); dfs(r-1, c)
        dfs(r, c+1); dfs(r, c-1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                dfs(r, c)
                count += 1

    return count
```

### 📝 Template — Topological Sort (DFS)

```python
def topo_sort(n, edges):
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)

    visited = [0] * n                  # 0=unvisited, 1=visiting, 2=done
    result = []
    has_cycle = [False]

    def dfs(node):
        if visited[node] == 1:          # back edge → cycle
            has_cycle[0] = True; return
        if visited[node] == 2:
            return

        visited[node] = 1
        for neighbor in graph[node]:
            dfs(neighbor)
        visited[node] = 2
        result.append(node)

    for i in range(n):
        if visited[i] == 0:
            dfs(i)

    return [] if has_cycle[0] else result[::-1]
```

### 📚 Classic Problems

| Problem | Technique |
|---------|-----------|
| Maximum Depth of Binary Tree | Tree DFS |
| Path Sum I & II | Tree DFS with target |
| Number of Islands | Grid DFS |
| Clone Graph | DFS with hashmap |
| Course Schedule | DFS cycle detection |
| Binary Tree Diameter | DFS, track max at each node |
| Lowest Common Ancestor | DFS |

### ⏱️ Complexity
- **Time:** O(V + E)
- **Space:** O(V) for recursion stack

---

## 10. Backtracking

### 🔍 What is it?

Build a solution incrementally — at each step, **try** each option, and **undo** (backtrack) if it leads to an invalid state. Explores all possibilities systematically.

### ✅ When to Use
- Generate all permutations, combinations, subsets
- Solve constraint satisfaction (N-Queens, Sudoku)
- Word search on a grid
- Anytime you need to "try all valid paths"

### 🧩 The Backtracking Blueprint

```
choose → explore → unchoose
```

### 📝 Template — Subsets

```python
def subsets(nums):
    result = []

    def backtrack(start, current):
        result.append(current[:])      # add current subset

        for i in range(start, len(nums)):
            current.append(nums[i])    # choose
            backtrack(i + 1, current)  # explore
            current.pop()              # unchoose (backtrack)

    backtrack(0, [])
    return result
```

### 📝 Template — Permutations

```python
def permutations(nums):
    result = []

    def backtrack(current):
        if len(current) == len(nums):
            result.append(current[:])
            return

        for num in nums:
            if num not in current:         # skip used
                current.append(num)        # choose
                backtrack(current)         # explore
                current.pop()              # unchoose

    backtrack([])
    return result
```

### 📝 Template — N-Queens

```python
def solve_n_queens(n):
    result = []
    cols = set()
    diag1 = set()                      # row - col
    diag2 = set()                      # row + col

    def backtrack(row, board):
        if row == n:
            result.append(["".join(r) for r in board])
            return

        for col in range(n):
            if col in cols or (row-col) in diag1 or (row+col) in diag2:
                continue                # invalid position

            cols.add(col); diag1.add(row-col); diag2.add(row+col)
            board[row][col] = 'Q'

            backtrack(row + 1, board)  # explore

            cols.remove(col); diag1.remove(row-col); diag2.remove(row+col)
            board[row][col] = '.'      # backtrack

    board = [['.']*n for _ in range(n)]
    backtrack(0, board)
    return result
```

### 📚 Classic Problems

| Problem | Key Decision |
|---------|-------------|
| Subsets / Subsets II | include or skip |
| Permutations I & II | which unused element next |
| Combination Sum | reuse allowed or not |
| Word Search | mark visited, unmark on backtrack |
| N-Queens | valid column/diagonal check |
| Sudoku Solver | valid number per cell |
| Palindrome Partitioning | partition at valid positions |

### ⏱️ Complexity
- **Time:** O(2ⁿ) for subsets, O(n!) for permutations
- **Space:** O(n) recursion depth

---

## 11. Dynamic Programming

### 🔍 What is it?

Break the problem into **overlapping subproblems**, solve each once, and **store results** (memoization/tabulation) to avoid recomputation.

### ✅ When to Use
- Problem asks for **count**, **minimum**, **maximum**, or **whether possible**
- Overlapping subproblems + optimal substructure
- Keywords: "number of ways", "minimum cost", "can you reach", "longest"

### 🧩 DP Decision Framework

```
1. Is the problem asking for optimal/count over choices?
2. Can you define the state? (what changes at each step)
3. Can the larger problem be solved from smaller subproblems?
→ If yes to all three → try DP
```

### 📝 Template — 1D DP (Climbing Stairs)

```python
# How many ways to climb n stairs (1 or 2 steps at a time)?
def climb_stairs(n):
    if n <= 2:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2

    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]     # come from i-1 or i-2

    return dp[n]
```

### 📝 Template — 2D DP (Unique Paths)

```python
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]   # base case: edges = 1 path

    for r in range(1, m):
        for c in range(1, n):
            dp[r][c] = dp[r-1][c] + dp[r][c-1]

    return dp[m-1][n-1]
```

### 📝 Template — Knapsack (0/1)

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # don't take item i
            dp[i][w] = dp[i-1][w]
            # take item i (if it fits)
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i][w], dp[i-1][w - weights[i-1]] + values[i-1])

    return dp[n][capacity]
```

### 📝 Template — LCS / Edit Distance

```python
# Longest Common Subsequence
def lcs(s1, s2):
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

### 📚 Classic Problems by Category

| Category | Problems |
|----------|---------|
| Linear DP | Climbing Stairs, House Robber, Coin Change |
| Grid DP | Unique Paths, Minimum Path Sum |
| Knapsack | 0/1 Knapsack, Partition Equal Subset |
| String DP | LCS, Edit Distance, Palindromic Substrings |
| Interval DP | Burst Balloons, Matrix Chain Multiplication |
| Tree DP | House Robber III, Binary Tree Cameras |

### ⏱️ Complexity
- **Time:** O(n²) or O(n×m) typically
- **Space:** O(n) to O(n×m), often reducible to O(n)

---

## 12. Greedy

### 🔍 What is it?

Make the **locally optimal choice** at each step, trusting that local optima lead to a global optimum. No backtracking.

### ✅ When to Use
- Interval scheduling / activity selection
- Minimum spanning tree
- Huffman encoding
- Jump game, gas station
- When a greedy "exchange argument" can be proven

> ⚠️ **Warning:** Greedy doesn't always work. Prove it or test with examples before using it.

### 📝 Template — Activity Selection (Interval Scheduling)

```python
def max_activities(intervals):
    # sort by end time — greedy: finish earliest, free up most time
    intervals.sort(key=lambda x: x[1])

    count = 1
    last_end = intervals[0][1]

    for start, end in intervals[1:]:
        if start >= last_end:           # no overlap
            count += 1
            last_end = end

    return count
```

### 📝 Template — Jump Game

```python
def can_jump(nums):
    max_reach = 0

    for i, jump in enumerate(nums):
        if i > max_reach:
            return False                # can't reach this position
        max_reach = max(max_reach, i + jump)

    return True
```

### 📚 Classic Problems

| Problem | Greedy Choice |
|---------|---------------|
| Activity Selection | Sort by end time |
| Jump Game | Track max reachable index |
| Gas Station | Circular greedy |
| Assign Cookies | Sort both, match greedily |
| Minimum Number of Arrows | Sort by end, shoot at end |
| Task Scheduler | Most frequent task first |

### ⏱️ Complexity
- **Time:** O(n log n) (usually dominated by sorting)
- **Space:** O(1)

---

## 13. Merge Intervals

### 🔍 What is it?

Sort intervals by start time, then **merge overlapping** intervals by comparing the end of the last merged interval with the start of the next.

### ✅ When to Use
- Overlapping intervals/ranges
- Insert an interval, merge, find gaps
- Meeting rooms, calendar conflicts
- Employee free time

### 📝 Template — Merge Overlapping Intervals

```python
def merge(intervals):
    if not intervals:
        return []

    intervals.sort(key=lambda x: x[0])     # sort by start
    merged = [intervals[0]]

    for start, end in intervals[1:]:
        last_end = merged[-1][1]

        if start <= last_end:               # overlap
            merged[-1][1] = max(last_end, end)  # extend
        else:
            merged.append([start, end])     # no overlap, add new

    return merged
```

### 📝 Template — Insert Interval

```python
def insert(intervals, new_interval):
    result = []
    i = 0
    n = len(intervals)

    # add all intervals that end before new starts
    while i < n and intervals[i][1] < new_interval[0]:
        result.append(intervals[i])
        i += 1

    # merge all overlapping intervals
    while i < n and intervals[i][0] <= new_interval[1]:
        new_interval[0] = min(new_interval[0], intervals[i][0])
        new_interval[1] = max(new_interval[1], intervals[i][1])
        i += 1

    result.append(new_interval)

    # add remaining
    while i < n:
        result.append(intervals[i])
        i += 1

    return result
```

### 📚 Classic Problems

| Problem | Technique |
|---------|-----------|
| Merge Intervals | Sort + merge |
| Insert Interval | Three phases |
| Meeting Rooms I | Check for any overlap |
| Meeting Rooms II | Min-heap for active meetings |
| Employee Free Time | Merge all, find gaps |

### ⏱️ Complexity
- **Time:** O(n log n) for sorting
- **Space:** O(n)

---

## 14. Linked List In-Place Reversal

### 🔍 What is it?

Reverse a linked list (or part of it) **without extra space** by relinking pointers.

### ✅ When to Use
- Reverse entire or part of a linked list
- Palindrome check
- Reorder list
- Reverse every k-group

### 📝 Template — Reverse Entire List

```python
def reverse_list(head):
    prev = None
    curr = head

    while curr:
        next_node = curr.next           # save next
        curr.next = prev                # reverse link
        prev = curr                     # move prev forward
        curr = next_node                # move curr forward

    return prev                         # new head
```

### 📝 Template — Reverse a Sublist (position l to r)

```python
def reverse_between(head, left, right):
    dummy = ListNode(0)
    dummy.next = head
    prev = dummy

    # reach node just before 'left'
    for _ in range(left - 1):
        prev = prev.next

    curr = prev.next

    # reverse from left to right
    for _ in range(right - left):
        next_node = curr.next
        curr.next = next_node.next
        next_node.next = prev.next
        prev.next = next_node

    return dummy.next
```

### 📝 Template — Reverse K-Group

```python
def reverse_k_group(head, k):
    # check if k nodes remain
    node, count = head, 0
    while node and count < k:
        node = node.next
        count += 1

    if count < k:
        return head                     # less than k nodes, don't reverse

    prev, curr = None, head
    for _ in range(k):
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node

    head.next = reverse_k_group(curr, k)  # recurse on rest
    return prev
```

### 📚 Classic Problems

| Problem | Technique |
|---------|-----------|
| Reverse Linked List | Basic reversal |
| Reverse Linked List II | Sublist reversal |
| Reverse Nodes in K-Group | K-group + recursion |
| Palindrome Linked List | Reverse second half |
| Reorder List | Find mid + reverse + merge |

### ⏱️ Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 15. Heap / Priority Queue

### 🔍 What is it?

A **heap** is a complete binary tree that always gives you the minimum (min-heap) or maximum (max-heap) in O(1), with O(log n) insert/delete.

Python's `heapq` is a **min-heap** by default. For max-heap, negate the values.

### ✅ When to Use
- Kth largest / Kth smallest
- Merge K sorted lists/arrays
- Scheduling / task priority
- Dijkstra's shortest path
- Sliding window maximum

### 📝 Template — K Largest Elements

```python
import heapq

def k_largest(nums, k):
    # min-heap of size k: the minimum in the heap is the kth largest
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)         # remove smallest
    return list(heap)                   # top k elements
```

### 📝 Template — Merge K Sorted Lists

```python
def merge_k_lists(lists):
    heap = []
    dummy = ListNode(0)
    curr = dummy

    # initialize with head of each list
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))

    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))

    return dummy.next
```

### 📝 Template — Dijkstra's Algorithm

```python
def dijkstra(graph, start):
    dist = {node: float('inf') for node in graph}
    dist[start] = 0
    heap = [(0, start)]                 # (distance, node)

    while heap:
        d, node = heapq.heappop(heap)

        if d > dist[node]:
            continue                    # outdated entry

        for neighbor, weight in graph[node]:
            new_dist = d + weight
            if new_dist < dist[neighbor]:
                dist[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))

    return dist
```

### 📚 Classic Problems

| Problem | Heap Type |
|---------|-----------|
| Kth Largest Element | Min-heap of size k |
| Top K Frequent Elements | Min-heap |
| Merge K Sorted Lists | Min-heap |
| Find Median from Data Stream | Two heaps (max + min) |
| Task Scheduler | Max-heap |
| Dijkstra's Shortest Path | Min-heap |

### ⏱️ Complexity
- **Push/Pop:** O(log n)
- **Peek min/max:** O(1)

---

## 16. Trie

### 🔍 What is it?

A tree where each node represents a **character**, and paths from root to a marked node spell out a word. Enables O(L) insert and search where L is word length.

### ✅ When to Use
- Auto-complete / search suggestions
- Word search with prefix
- Longest common prefix
- Boggle / Word Search II

### 📝 Template

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for ch in word:
            if ch not in node.children:
                node.children[ch] = TrieNode()
            node = node.children[ch]
        node.is_end = True

    def search(self, word):
        node = self.root
        for ch in word:
            if ch not in node.children:
                return False
            node = node.children[ch]
        return node.is_end

    def starts_with(self, prefix):
        node = self.root
        for ch in prefix:
            if ch not in node.children:
                return False
            node = node.children[ch]
        return True
```

### 📚 Classic Problems

| Problem | Technique |
|---------|-----------|
| Implement Trie | Basic implementation |
| Word Search II | Trie + DFS backtracking |
| Design Search Autocomplete | Trie + BFS/DFS for completions |
| Replace Words | Trie prefix matching |
| Longest Word in Dictionary | Trie + BFS |

### ⏱️ Complexity
- **Insert/Search:** O(L) — L = word length
- **Space:** O(alphabet_size × L × N) — N = number of words

---

## 17. Union Find (Disjoint Set)

### 🔍 What is it?

Efficiently tracks which elements are in the same **connected component**. Supports union (merge) and find (which group?) in near O(1) with path compression + union by rank.

### ✅ When to Use
- Number of connected components
- Detect cycle in undirected graph
- Kruskal's minimum spanning tree
- Accounts merge problem

### 📝 Template

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))    # each node is its own parent
        self.rank = [0] * n
        self.components = n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # path compression
        return self.parent[x]

    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False                # already connected

        # union by rank
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1

        self.components -= 1
        return True

    def connected(self, x, y):
        return self.find(x) == self.find(y)
```

### 📝 Usage — Number of Islands

```python
def num_islands_uf(grid):
    rows, cols = len(grid), len(grid[0])
    uf = UnionFind(rows * cols)
    land_count = 0

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                land_count += 1
                for dr, dc in [(0,1),(1,0)]:
                    nr, nc = r+dr, c+dc
                    if 0<=nr<rows and 0<=nc<cols and grid[nr][nc]=='1':
                        uf.union(r*cols+c, nr*cols+nc)

    return land_count - (land_count - uf.components)  # simplifies to uf.components among land
```

### 📚 Classic Problems

| Problem | Use |
|---------|-----|
| Number of Provinces | Count components |
| Redundant Connection | Detect cycle (union returns False) |
| Accounts Merge | Union by common email |
| Number of Islands | Union adjacent land cells |
| Kruskal's MST | Sort edges, union greedily |

### ⏱️ Complexity
- **Find/Union:** O(α(n)) ≈ O(1) amortized (α = inverse Ackermann function)

---

## 18. Bit Manipulation

### 🔍 What is it?

Operate directly on binary representations of numbers using bitwise operators. Often the key to O(1) or O(n) solutions for number problems.

### 📝 Bit Operations Reference

```python
# Common bit tricks
n & 1           # check if n is odd (last bit)
n >> 1          # divide by 2
n << 1          # multiply by 2
n & (n-1)       # clear lowest set bit  (e.g., 6=110 → 4=100)
n & (-n)        # isolate lowest set bit (e.g., 6=110 → 2=010)
n ^ n           # = 0  (XOR with itself)
n ^ 0           # = n  (XOR with 0)
~n              # flip all bits
```

### 📝 Classic Templates

```python
# Single Number — find the element that appears once (rest appear twice)
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num               # XOR cancels duplicates
    return result

# Count set bits (Hamming Weight)
def count_bits(n):
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count

# Is power of 2?
def is_power_of_two(n):
    return n > 0 and (n & (n-1)) == 0

# Reverse bits
def reverse_bits(n):
    result = 0
    for _ in range(32):
        result = (result << 1) | (n & 1)
        n >>= 1
    return result
```

### 📚 Classic Problems

| Problem | Trick |
|---------|-------|
| Single Number | XOR cancels pairs |
| Single Number II | Count bits mod 3 |
| Number of 1 Bits | `n & (n-1)` loop |
| Reverse Bits | Shift and OR |
| Missing Number | XOR with indices |
| Power of Two | `n & (n-1) == 0` |
| Subsets | Bitmask for all 2ⁿ subsets |

### ⏱️ Complexity
- **Time:** O(1) or O(n) — typically very fast
- **Space:** O(1)

---

## 19. Pattern Recognition Cheatsheet

Use this to quickly identify which pattern a problem belongs to.

### 🔍 By Keywords

| Keyword / Clue | Pattern to Try |
|---------------|---------------|
| "sorted array" + pair | Two Pointers |
| "subarray" / "substring" + max/min length | Sliding Window |
| "linked list" + cycle / middle | Fast & Slow Pointers |
| "sorted" + find target / minimize | Binary Search |
| "sum of subarray" + multiple queries | Prefix Sum |
| "count frequency" / "find duplicate" | HashMap |
| "next greater" / "nearest smaller" | Monotonic Stack |
| "shortest path" / "level by level" | BFS |
| "all paths" / "connected components" | DFS |
| "all combinations" / "all permutations" | Backtracking |
| "minimum cost" / "number of ways" | Dynamic Programming |
| "interval overlap" / "meeting rooms" | Merge Intervals |
| "kth largest" / "top K" | Heap |
| "prefix search" / "autocomplete" | Trie |
| "connected groups" / "union merge" | Union Find |
| "XOR" / "appear once" / "bit count" | Bit Manipulation |
| "locally optimal = globally optimal" | Greedy |

### 🔍 By Data Structure

| Input Type | Common Patterns |
|-----------|----------------|
| Sorted Array | Two Pointers, Binary Search, Sliding Window |
| Unsorted Array | HashMap, Prefix Sum, Monotonic Stack |
| Linked List | Fast/Slow, In-Place Reversal |
| Binary Tree | DFS (recursion), BFS (level order) |
| Graph | BFS (shortest), DFS (components), Union Find |
| String | Sliding Window, HashMap, Trie |
| Numbers | Bit Manipulation, Math, DP |
| Intervals | Merge Intervals, Heap |

---

## 20. Complexity Quick Reference

### Time Complexity

| Complexity | Name | Example |
|-----------|------|---------|
| O(1) | Constant | Array index access, HashMap lookup |
| O(log n) | Logarithmic | Binary Search |
| O(n) | Linear | Single loop, Two Pointers |
| O(n log n) | Linearithmic | Merge Sort, sorting-based problems |
| O(n²) | Quadratic | Nested loops, brute force |
| O(2ⁿ) | Exponential | Subsets, Backtracking |
| O(n!) | Factorial | Permutations |

### Space Complexity

| Pattern | Space |
|---------|-------|
| Two Pointers | O(1) |
| Sliding Window | O(k) |
| HashMap | O(n) |
| DFS (recursive) | O(h) — tree height |
| BFS | O(w) — max width of tree/graph |
| DP (1D) | O(n) or O(1) optimized |
| DP (2D) | O(n×m) or O(n) optimized |

### Pattern Complexity Summary

| Pattern | Time | Space |
|---------|------|-------|
| Two Pointers | O(n) | O(1) |
| Sliding Window | O(n) | O(k) |
| Binary Search | O(log n) | O(1) |
| Prefix Sum | O(n) build, O(1) query | O(n) |
| BFS | O(V+E) | O(V) |
| DFS | O(V+E) | O(V) |
| Backtracking | O(2ⁿ) or O(n!) | O(n) |
| DP | O(n²) typical | O(n) to O(n²) |
| Heap | O(n log k) | O(k) |
| Trie | O(L) per op | O(N×L) |
| Union Find | O(α(n)) ≈ O(1) | O(n) |

---

## ✅ How to Approach Any DSA Problem

```
Step 1: UNDERSTAND
  → Read carefully. What is the input? What is the output?
  → What are the constraints? (n size, negative numbers, sorted?)
  → Work through examples by hand.

Step 2: IDENTIFY THE PATTERN
  → Use the Pattern Recognition Cheatsheet above.
  → Think about which data structures naturally fit.

Step 3: PLAN
  → Write pseudocode or explain the approach out loud.
  → State the time and space complexity before coding.

Step 4: CODE
  → Start with the simplest correct solution.
  → Handle edge cases: empty input, single element, all same values.

Step 5: TEST
  → Test with the provided examples.
  → Test with edge cases.
  → Trace through the code manually for one example.

Step 6: OPTIMIZE
  → Can you do better? Is there a pattern that gives O(n) instead of O(n²)?
```

---

> 🚀 **Remember:** The goal is pattern recognition. Once you've solved 2-3 problems per pattern, the next one becomes much easier. Practice consistently, not intensely.

---

*Last Updated: 2025 | Covers LeetCode, Codeforces, and interview-level DSA*
