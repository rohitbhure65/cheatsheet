# 🧠 DSA Common Patterns — Complete Handbook (C++ & STL)

> Master the **patterns**, not just the problems. Once you recognize the pattern, the solution follows naturally.

---

## 📌 Why Patterns Matter

DSA problems number in the thousands — but the **underlying patterns** are fewer than 20. Top interviewers at FAANG don't expect you to memorize every problem. They expect you to **recognize the pattern** and adapt.

Each pattern below includes:
- **Raw C++** — manual implementation (understand internals)
- **STL C++** — production-ready using `<algorithm>`, `<map>`, `<queue>`, etc.

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
19. [STL Quick Reference](#19-stl-quick-reference)
20. [Pattern Recognition Cheatsheet](#20-pattern-recognition-cheatsheet)
21. [Complexity Quick Reference](#21-complexity-quick-reference)

---

## 1. Two Pointers

### 🔍 What is it?
Two indices that move through the array — usually from opposite ends or same direction — to avoid O(n²) nested loops.

### ✅ When to Use
- Sorted array pair/triplet problems
- Remove duplicates, partitioning
- Container with most water, valid palindrome

### 🧩 Visual
```
arr = [1, 2, 3, 4, 6],  target = 6

[1, 2, 3, 4, 6]
 L           R    → 1+6=7 > 6 → move R left

[1, 2, 3, 4, 6]
 L        R       → 1+4=5 < 6 → move L right

[1, 2, 3, 4, 6]
    L     R       → 2+4=6 ✅ FOUND
```

### 📝 Raw C++ — Opposite Ends (Pair Sum)
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Find pair with given target sum in sorted array
pair<int,int> twoPointer(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target)
            return {left, right};       // found
        else if (sum < target)
            left++;                     // need bigger sum
        else
            right--;                    // need smaller sum
    }
    return {-1, -1};                    // not found
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 6};
    auto [l, r] = twoPointer(arr, 6);
    cout << "Indices: " << l << ", " << r << endl; // 1, 3
}
```

### 📝 STL C++ — Same Direction (Remove Duplicates)
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Remove duplicates from sorted array in-place, return new length
int removeDuplicates(vector<int>& arr) {
    if (arr.empty()) return 0;

    // STL approach: unique() moves duplicates to end, returns iterator to new end
    auto newEnd = unique(arr.begin(), arr.end());
    arr.erase(newEnd, arr.end());       // optional: actually shrink the vector
    return arr.size();
}

// Manual slow/fast pointer approach
int removeDuplicatesManual(vector<int>& arr) {
    int slow = 0;
    for (int fast = 1; fast < arr.size(); fast++) {
        if (arr[fast] != arr[slow]) {   // found new unique element
            slow++;
            arr[slow] = arr[fast];
        }
    }
    return slow + 1;
}

int main() {
    vector<int> arr = {1, 1, 2, 3, 3, 4};
    int len = removeDuplicates(arr);
    cout << "New length: " << len << endl;          // 4
}
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
Maintain a window (subarray/substring) that slides through data. Expand or shrink based on constraints — avoids recomputing from scratch.

### ✅ When to Use
- Subarray/substring of fixed or variable size
- Keywords: "contiguous", "substring", "subarray"
- Longest substring with some constraint

### 🧩 Visual
```
Fixed window (k=3):
arr = [2, 1, 5, 1, 3, 2]

[2, 1, 5] → sum=8
   [1, 5, 1] → sum=7
      [5, 1, 3] → sum=9  ← max
         [1, 3, 2] → sum=6
```

### 📝 Raw C++ — Fixed Window (Max Sum)
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int maxSumSubarray(vector<int>& arr, int k) {
    int n = arr.size();
    if (n < k) return -1;

    // compute first window sum manually
    int windowSum = 0;
    for (int i = 0; i < k; i++)
        windowSum += arr[i];

    int maxSum = windowSum;

    for (int i = k; i < n; i++) {
        windowSum += arr[i];            // add new right element
        windowSum -= arr[i - k];        // remove old left element
        maxSum = max(maxSum, windowSum);
    }
    return maxSum;
}

int main() {
    vector<int> arr = {2, 1, 5, 1, 3, 2};
    cout << maxSumSubarray(arr, 3) << endl;  // 9
}
```

### 📝 STL C++ — Variable Window (Longest Substring K Distinct)
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

int longestKDistinct(string& s, int k) {
    unordered_map<char, int> charCount;  // STL hash map
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.size(); right++) {
        charCount[s[right]]++;           // expand: add right char

        // shrink: while window has more than k distinct chars
        while ((int)charCount.size() > k) {
            charCount[s[left]]--;
            if (charCount[s[left]] == 0)
                charCount.erase(s[left]);// remove from map when count hits 0
            left++;
        }

        maxLen = max(maxLen, right - left + 1);  // valid window
    }
    return maxLen;
}

// STL C++ — Minimum Window Substring
string minWindow(string s, string t) {
    unordered_map<char, int> need, have;
    for (char c : t) need[c]++;

    int left = 0, formed = 0, required = need.size();
    int minLen = INT_MAX, minLeft = 0;

    for (int right = 0; right < s.size(); right++) {
        have[s[right]]++;
        if (need.count(s[right]) && have[s[right]] == need[s[right]])
            formed++;

        while (formed == required) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minLeft = left;
            }
            have[s[left]]--;
            if (need.count(s[left]) && have[s[left]] < need[s[left]])
                formed--;
            left++;
        }
    }
    return minLen == INT_MAX ? "" : s.substr(minLeft, minLen);
}

int main() {
    string s = "araaci";
    cout << longestKDistinct(s, 2) << endl;   // 4 (araa)
}
```

### 📚 Classic Problems
| Problem | Type |
|---------|------|
| Max Sum Subarray of Size K | Fixed |
| Longest Substring Without Repeating | Variable |
| Minimum Window Substring | Variable (shrink to minimum) |
| Find All Anagrams in a String | Fixed |
| Fruits Into Baskets | Variable (at most 2 distinct) |

### ⏱️ Complexity
- **Time:** O(n) — each element enters/leaves window once
- **Space:** O(k)

---

## 3. Fast & Slow Pointers (Floyd's Cycle)

### 🔍 What is it?
Two pointers move at different speeds. Fast moves 2 steps, slow moves 1 step. Used for cycle detection and finding the middle.

### ✅ When to Use
- Detect cycle in linked list
- Find middle of linked list
- Find start of cycle
- Happy number detection

### 🧩 Visual
```
1 → 2 → 3 → 4 → 5
            ↑       ↓
            8 ← 7 ← 6

Slow: 1→2→3→4→5→6→7
Fast: 1→3→5→7→4→6→3
They meet → cycle exists!
```

### 📝 Raw C++ — Cycle Detection
```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;              // 1 step
        fast = fast->next->next;        // 2 steps

        if (slow == fast)
            return true;                // they met → cycle
    }
    return false;
}

// Find middle of linked list
ListNode* findMiddle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;                        // slow is at middle
}

// Find start of cycle
ListNode* findCycleStart(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;

    // Phase 1: detect cycle
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) break;
    }
    if (!fast || !fast->next) return nullptr;   // no cycle

    // Phase 2: find entry point
    slow = head;                        // reset to head
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;              // both move 1 step
    }
    return slow;                        // meeting point = cycle start
}
```

### 📝 STL C++ — Happy Number (Cycle in Number Sequence)
```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int digitSquareSum(int n) {
    int sum = 0;
    while (n > 0) {
        int d = n % 10;
        sum += d * d;
        n /= 10;
    }
    return sum;
}

// STL approach: use unordered_set to detect cycle
bool isHappySTL(int n) {
    unordered_set<int> seen;
    while (n != 1 && seen.find(n) == seen.end()) {
        seen.insert(n);
        n = digitSquareSum(n);
    }
    return n == 1;
}

// Fast/slow pointer approach (O(1) space)
bool isHappy(int n) {
    int slow = n;
    int fast = digitSquareSum(n);

    while (fast != 1 && slow != fast) {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(digitSquareSum(fast));
    }
    return fast == 1;
}
```

### 📚 Classic Problems
| Problem | Trick |
|---------|-------|
| Linked List Cycle (LC 141) | Fast/slow meet → cycle |
| Linked List Cycle II (LC 142) | Reset one pointer to find start |
| Find Middle of Linked List | Slow is at middle when fast ends |
| Happy Number | Cycle in number sequence |
| Palindrome Linked List | Find middle, reverse second half |

### ⏱️ Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 4. Binary Search

### 🔍 What is it?
Eliminate half the search space at each step. Works on sorted arrays, also applies to "search on answer" problems.

### ✅ When to Use
- Array is sorted
- First/last occurrence of a value
- "Find minimum X such that condition holds"
- Monotonic function — answer space can be halved

### 🧩 Visual
```
arr = [1, 3, 5, 7, 9, 11, 13], target = 7
lo=0, hi=6, mid=3 → arr[3]=7 ✅ Found
```

### 📝 Raw C++ — Classic Binary Search
```cpp
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(vector<int>& arr, int target) {
    int lo = 0, hi = arr.size() - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;  // avoids integer overflow

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            lo = mid + 1;
        else
            hi = mid - 1;
    }
    return -1;                          // not found
}

// Find first occurrence (left boundary)
int findFirst(vector<int>& arr, int target) {
    int lo = 0, hi = arr.size() - 1, result = -1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) {
            result = mid;               // record, keep searching left
            hi = mid - 1;
        } else if (arr[mid] < target)
            lo = mid + 1;
        else
            hi = mid - 1;
    }
    return result;
}
```

### 📝 STL C++ — Using `<algorithm>` Built-ins
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13};

    // binary_search: returns true/false only
    bool found = binary_search(arr.begin(), arr.end(), 7);

    // lower_bound: iterator to first element >= target
    auto it = lower_bound(arr.begin(), arr.end(), 7);
    int idx = it - arr.begin();         // convert to index

    // upper_bound: iterator to first element > target
    auto it2 = upper_bound(arr.begin(), arr.end(), 7);

    // Count occurrences of target
    int count = upper_bound(arr.begin(), arr.end(), 7)
              - lower_bound(arr.begin(), arr.end(), 7);

    cout << "Found: " << found << endl;
    cout << "First index: " << idx << endl;
    cout << "Count: " << count << endl;
}
```

### 📝 Binary Search on Answer Template
```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

// "Find minimum capacity to ship packages within D days"
bool canShip(vector<int>& weights, int D, int capacity) {
    int days = 1, current = 0;
    for (int w : weights) {
        if (current + w > capacity) {
            days++;
            current = 0;
        }
        current += w;
    }
    return days <= D;
}

int minCapacity(vector<int>& weights, int D) {
    int lo = *max_element(weights.begin(), weights.end()); // STL max_element
    int hi = accumulate(weights.begin(), weights.end(), 0);// STL accumulate

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (canShip(weights, D, mid))
            hi = mid;                   // might do better
        else
            lo = mid + 1;               // too small
    }
    return lo;
}
```

### 📚 Classic Problems
| Problem | Variant |
|---------|---------|
| Binary Search (LC 704) | Classic |
| Search in Rotated Sorted Array | Check which half is sorted |
| Find Minimum in Rotated Array | Modified |
| Koko Eating Bananas | Search on answer |
| Capacity to Ship Packages | Search on answer |
| Search a 2D Matrix | Treat as 1D array |

### ⏱️ Complexity
- **Time:** O(log n)
- **Space:** O(1) iterative

---

## 5. Prefix Sum

### 🔍 What is it?
Precompute cumulative sums so any subarray sum is answered in O(1).

`prefix[i] = arr[0] + arr[1] + ... + arr[i-1]`
`sum(l, r) = prefix[r+1] - prefix[l]`

### ✅ When to Use
- Multiple subarray sum queries
- Subarray sum equals K
- Product of array except self
- 2D range sum queries

### 📝 Raw C++ — Build & Query
```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> buildPrefix(vector<int>& arr) {
    int n = arr.size();
    vector<int> prefix(n + 1, 0);

    for (int i = 0; i < n; i++)
        prefix[i + 1] = prefix[i] + arr[i];

    return prefix;
}

int rangeSum(vector<int>& prefix, int l, int r) {
    // sum of arr[l..r] (0-indexed, inclusive)
    return prefix[r + 1] - prefix[l];
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    auto prefix = buildPrefix(arr);
    cout << rangeSum(prefix, 1, 3) << endl;  // 2+3+4 = 9
}
```

### 📝 STL C++ — Subarray Sum Equals K
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> seen;       // prefix sum → frequency
    seen[0] = 1;                        // empty prefix
    int count = 0, prefix = 0;

    for (int num : nums) {
        prefix += num;
        // if (prefix - k) was seen before, those subarrays sum to k
        count += seen[prefix - k];      // unordered_map returns 0 if key missing
        seen[prefix]++;
    }
    return count;
}

// Product of Array Except Self (prefix + suffix product)
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, 1);

    // left pass: result[i] = product of all elements left of i
    int left = 1;
    for (int i = 0; i < n; i++) {
        result[i] = left;
        left *= nums[i];
    }

    // right pass: multiply by product of all elements right of i
    int right = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= right;
        right *= nums[i];
    }
    return result;
}
```

### 📚 Classic Problems
| Problem | Key Idea |
|---------|----------|
| Subarray Sum Equals K | prefix + unordered_map |
| Range Sum Query | precompute prefix |
| Product of Array Except Self | prefix + suffix product |
| 2D Matrix Range Sum | 2D prefix |

### ⏱️ Complexity
- **Build:** O(n) | **Query:** O(1)

---

## 6. HashMap / Frequency Count

### 🔍 What is it?
Use `unordered_map` (hash map) or `map` to count occurrences, store indices, or group elements — turning O(n²) lookups into O(1).

### ✅ When to Use
- Count frequency of elements
- Two Sum: find complement
- Anagram detection
- Group elements by property

### 📝 Raw C++ — Manual Hash (Array for ASCII)
```cpp
#include <iostream>
#include <string>
using namespace std;

// Valid Anagram using fixed-size frequency array (only lowercase letters)
bool isAnagram(string s, string t) {
    if (s.size() != t.size()) return false;

    int freq[26] = {0};                 // array as hash map for a-z

    for (char c : s) freq[c - 'a']++;
    for (char c : t) freq[c - 'a']--;

    for (int i = 0; i < 26; i++)
        if (freq[i] != 0) return false;

    return true;
}
```

### 📝 STL C++ — unordered_map Templates
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <string>
#include <algorithm>
using namespace std;

// Two Sum — find indices of pair summing to target
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> seen;       // value → index

    for (int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];
        if (seen.count(complement))
            return {seen[complement], i};
        seen[nums[i]] = i;
    }
    return {};
}

// Group Anagrams
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> groups;

    for (string& s : strs) {
        string key = s;
        sort(key.begin(), key.end());   // sorted string as key
        groups[key].push_back(s);
    }

    vector<vector<string>> result;
    for (auto& [key, group] : groups)
        result.push_back(group);

    return result;
}

// Longest Consecutive Sequence — O(n) with unordered_set
#include <unordered_set>
int longestConsecutive(vector<int>& nums) {
    unordered_set<int> numSet(nums.begin(), nums.end());
    int maxLen = 0;

    for (int num : numSet) {
        // only start counting from the beginning of a sequence
        if (!numSet.count(num - 1)) {
            int current = num, len = 1;
            while (numSet.count(current + 1)) {
                current++;
                len++;
            }
            maxLen = max(maxLen, len);
        }
    }
    return maxLen;
}
```

### 📝 STL Map vs Unordered_map
```cpp
#include <map>
#include <unordered_map>

// map: sorted keys, O(log n) operations — use when order matters
map<int, int> ordered;

// unordered_map: O(1) avg operations — use for frequency/lookup
unordered_map<int, int> fast;

// Frequency count idiom
unordered_map<int, int> freq;
for (int x : nums) freq[x]++;          // auto-initializes to 0
```

### 📚 Classic Problems
| Problem | Technique |
|---------|-----------|
| Two Sum | complement unordered_map |
| Valid Anagram | frequency array or map |
| Group Anagrams | sorted string as key |
| Top K Frequent Elements | map + priority_queue |
| Longest Consecutive Sequence | unordered_set |

### ⏱️ Complexity
- **Time:** O(n) avg (unordered_map), O(n log n) (map)
- **Space:** O(n)

---

## 7. Monotonic Stack

### 🔍 What is it?
A stack maintained in strictly increasing or decreasing order. Efficiently answers "next greater/smaller element" queries in O(n).

### ✅ When to Use
- Next Greater Element / Previous Smaller Element
- Largest rectangle in histogram
- Daily Temperatures
- Trapping Rain Water

### 🧩 Visual
```
arr = [2, 1, 5, 3, 6]  — find Next Greater Element

Process 2: stack = [2]
Process 1: stack = [2, 1]
Process 5: 5>1 → NGE(1)=5, 5>2 → NGE(2)=5. stack=[5]
Process 3: stack = [5, 3]
Process 6: 6>3 → NGE(3)=6, 6>5 → NGE(5)=6. stack=[6]

Result = [5, 5, 6, 6, -1]
```

### 📝 Raw C++ — Next Greater Element (Manual Stack Array)
```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> nextGreater(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);

    // manual stack using array
    int stk[100000];
    int top = -1;

    for (int i = 0; i < n; i++) {
        // pop all elements smaller than current
        while (top >= 0 && arr[stk[top]] < arr[i]) {
            result[stk[top]] = arr[i];
            top--;
        }
        stk[++top] = i;                 // push current index
    }
    return result;
}
```

### 📝 STL C++ — Using `stack<int>`
```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

// Next Greater Element
vector<int> nextGreaterSTL(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);
    stack<int> stk;                     // STL stack, stores indices

    for (int i = 0; i < n; i++) {
        while (!stk.empty() && arr[stk.top()] < arr[i]) {
            result[stk.top()] = arr[i];
            stk.pop();
        }
        stk.push(i);
    }
    return result;
}

// Largest Rectangle in Histogram
int largestRectangle(vector<int>& heights) {
    heights.push_back(0);               // sentinel to flush remaining stack
    stack<int> stk;
    int maxArea = 0;

    for (int i = 0; i < heights.size(); i++) {
        while (!stk.empty() && heights[stk.top()] > heights[i]) {
            int height = heights[stk.top()]; stk.pop();
            int width  = stk.empty() ? i : i - stk.top() - 1;
            maxArea = max(maxArea, height * width);
        }
        stk.push(i);
    }
    heights.pop_back();                 // restore original
    return maxArea;
}

// Daily Temperatures — days to wait for warmer temperature
vector<int> dailyTemperatures(vector<int>& T) {
    int n = T.size();
    vector<int> result(n, 0);
    stack<int> stk;                     // decreasing monotonic stack

    for (int i = 0; i < n; i++) {
        while (!stk.empty() && T[stk.top()] < T[i]) {
            result[stk.top()] = i - stk.top();
            stk.pop();
        }
        stk.push(i);
    }
    return result;
}
```

### 📚 Classic Problems
| Problem | Stack Type |
|---------|------------|
| Next Greater Element I & II | Decreasing |
| Daily Temperatures | Decreasing |
| Largest Rectangle in Histogram | Increasing |
| Trapping Rain Water | Decreasing |
| 132 Pattern | Decreasing |

### ⏱️ Complexity
- **Time:** O(n) — each element pushed/popped once
- **Space:** O(n)

---

## 8. BFS — Level Order Traversal

### 🔍 What is it?
Explore all nodes at the current level before moving to the next. Uses a queue. Guarantees shortest path in unweighted graphs.

### ✅ When to Use
- Shortest path in unweighted graph or grid
- Level-by-level tree processing
- Multi-source BFS (rotten oranges, walls & gates)
- Word ladder

### 📝 Raw C++ — Tree BFS (Manual Queue with Array)
```cpp
#include <iostream>
#include <vector>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

vector<vector<int>> levelOrderRaw(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;

    // manual queue using array
    TreeNode* q[10000];
    int front = 0, back = 0;
    q[back++] = root;

    while (front < back) {
        int levelSize = back - front;
        vector<int> level;

        for (int i = 0; i < levelSize; i++) {
            TreeNode* node = q[front++];
            level.push_back(node->val);
            if (node->left)  q[back++] = node->left;
            if (node->right) q[back++] = node->right;
        }
        result.push_back(level);
    }
    return result;
}
```

### 📝 STL C++ — Using `queue<>`
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_set>
using namespace std;

// Tree BFS
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;

    queue<TreeNode*> q;                 // STL queue
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        vector<int> level;

        for (int i = 0; i < levelSize; i++) {
            TreeNode* node = q.front(); q.pop();
            level.push_back(node->val);
            if (node->left)  q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}

// Graph BFS — Shortest Path
int bfsShortestPath(vector<vector<int>>& adj, int start, int end) {
    int n = adj.size();
    vector<bool> visited(n, false);
    queue<pair<int,int>> q;             // {node, distance}

    visited[start] = true;
    q.push({start, 0});

    while (!q.empty()) {
        auto [node, dist] = q.front(); q.pop();

        if (node == end) return dist;

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push({neighbor, dist + 1});
            }
        }
    }
    return -1;
}

// Grid BFS — Multi-source (Rotten Oranges)
int orangesRotting(vector<vector<int>>& grid) {
    int rows = grid.size(), cols = grid[0].size();
    queue<pair<int,int>> q;
    int fresh = 0;

    // add all rotten oranges as sources
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == 2) q.push({r, c});
            if (grid[r][c] == 1) fresh++;
        }

    int minutes = 0;
    int dirs[4][2] = {{0,1},{0,-1},{1,0},{-1,0}};

    while (!q.empty() && fresh > 0) {
        int sz = q.size();
        for (int i = 0; i < sz; i++) {
            auto [r, c] = q.front(); q.pop();
            for (auto& d : dirs) {
                int nr = r + d[0], nc = c + d[1];
                if (nr>=0 && nr<rows && nc>=0 && nc<cols && grid[nr][nc]==1) {
                    grid[nr][nc] = 2;
                    fresh--;
                    q.push({nr, nc});
                }
            }
        }
        minutes++;
    }
    return fresh == 0 ? minutes : -1;
}
```

### 📚 Classic Problems
| Problem | Variant |
|---------|---------|
| Binary Tree Level Order | Tree BFS |
| Rotting Oranges | Multi-source BFS |
| Word Ladder | Graph BFS |
| 01 Matrix | Multi-source BFS |
| Shortest Path in Binary Matrix | Grid BFS |

### ⏱️ Complexity
- **Time:** O(V + E) for graphs, O(m×n) for grids
- **Space:** O(V)

---

## 9. DFS — Tree & Graph

### 🔍 What is it?
Explore as deep as possible along each branch before backtracking. Uses recursion (implicit stack) or explicit stack.

### ✅ When to Use
- Tree: path sums, heights, diameter, LCA
- Graph: connected components, cycle detection, topological sort
- Flood fill, number of islands

### 📝 Raw C++ — Tree DFS (Recursion)
```cpp
#include <iostream>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Max depth
int maxDepth(TreeNode* root) {
    if (!root) return 0;
    int leftDepth  = maxDepth(root->left);
    int rightDepth = maxDepth(root->right);
    return 1 + max(leftDepth, rightDepth);
}

// Path sum: does a root-to-leaf path sum equal target?
bool hasPathSum(TreeNode* root, int target) {
    if (!root) return false;
    if (!root->left && !root->right)   // leaf node
        return root->val == target;
    return hasPathSum(root->left,  target - root->val) ||
           hasPathSum(root->right, target - root->val);
}

// Diameter of binary tree
int diameter = 0;
int dfsDepth(TreeNode* node) {
    if (!node) return 0;
    int left  = dfsDepth(node->left);
    int right = dfsDepth(node->right);
    diameter = max(diameter, left + right); // update at each node
    return 1 + max(left, right);
}
```

### 📝 STL C++ — Graph DFS (Number of Islands)
```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

void dfs(vector<vector<char>>& grid, int r, int c) {
    int rows = grid.size(), cols = grid[0].size();
    if (r<0 || r>=rows || c<0 || c>=cols || grid[r][c]=='0') return;
    grid[r][c] = '0';                  // mark visited
    dfs(grid, r+1, c); dfs(grid, r-1, c);
    dfs(grid, r, c+1); dfs(grid, r, c-1);
}

int numIslands(vector<vector<char>>& grid) {
    int count = 0;
    for (int r = 0; r < grid.size(); r++)
        for (int c = 0; c < grid[0].size(); c++)
            if (grid[r][c] == '1') {
                dfs(grid, r, c);
                count++;
            }
    return count;
}

// Topological Sort (Kahn's BFS approach using STL)
#include <queue>
vector<int> topoSort(int n, vector<pair<int,int>>& edges) {
    vector<vector<int>> adj(n);
    vector<int> indegree(n, 0);

    for (auto [u, v] : edges) {
        adj[u].push_back(v);
        indegree[v]++;
    }

    queue<int> q;
    for (int i = 0; i < n; i++)
        if (indegree[i] == 0) q.push(i);

    vector<int> order;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        order.push_back(node);
        for (int neighbor : adj[node]) {
            if (--indegree[neighbor] == 0)
                q.push(neighbor);
        }
    }
    return order.size() == n ? order : vector<int>{}; // empty if cycle
}
```

### 📚 Classic Problems
| Problem | Technique |
|---------|-----------|
| Maximum Depth of Binary Tree | Tree DFS |
| Path Sum I & II | Tree DFS with target |
| Number of Islands | Grid DFS |
| Course Schedule | Topological Sort / Cycle Detection |
| Binary Tree Diameter | DFS, track max at each node |
| Lowest Common Ancestor | DFS |

### ⏱️ Complexity
- **Time:** O(V + E)
- **Space:** O(V) for recursion stack

---

## 10. Backtracking

### 🔍 What is it?
Build solution incrementally — try each option, and undo (backtrack) if it leads to invalid state. The blueprint: **choose → explore → unchoose**.

### ✅ When to Use
- All permutations, combinations, subsets
- N-Queens, Sudoku
- Word search on a grid

### 📝 Raw C++ — Subsets
```cpp
#include <iostream>
#include <vector>
using namespace std;

void backtrack(vector<int>& nums, int start,
               vector<int>& current, vector<vector<int>>& result) {
    result.push_back(current);         // add current subset (including empty)

    for (int i = start; i < nums.size(); i++) {
        current.push_back(nums[i]);    // choose
        backtrack(nums, i + 1, current, result);  // explore
        current.pop_back();            // unchoose (backtrack)
    }
}

vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> current;
    backtrack(nums, 0, current, result);
    return result;
}
```

### 📝 STL C++ — Permutations & N-Queens
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <set>
using namespace std;

// Permutations
void permuteHelper(vector<int>& nums, vector<bool>& used,
                   vector<int>& current, vector<vector<int>>& result) {
    if (current.size() == nums.size()) {
        result.push_back(current);
        return;
    }
    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) continue;
        used[i] = true;
        current.push_back(nums[i]);    // choose
        permuteHelper(nums, used, current, result); // explore
        current.pop_back();            // unchoose
        used[i] = false;
    }
}

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    vector<bool> used(nums.size(), false);
    vector<int> current;
    permuteHelper(nums, used, current, result);
    return result;
}

// STL: next_permutation for all permutations
#include <algorithm>
vector<vector<int>> permuteSTL(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> result;
    do {
        result.push_back(nums);
    } while (next_permutation(nums.begin(), nums.end()));
    return result;
}

// N-Queens
vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> result;
    vector<string> board(n, string(n, '.'));
    set<int> cols, diag1, diag2;       // STL sets for O(1) check

    function<void(int)> backtrack = [&](int row) {
        if (row == n) {
            result.push_back(board);
            return;
        }
        for (int col = 0; col < n; col++) {
            if (cols.count(col) || diag1.count(row-col) || diag2.count(row+col))
                continue;

            cols.insert(col);
            diag1.insert(row - col);
            diag2.insert(row + col);
            board[row][col] = 'Q';

            backtrack(row + 1);

            cols.erase(col);
            diag1.erase(row - col);
            diag2.erase(row + col);
            board[row][col] = '.';
        }
    };

    backtrack(0);
    return result;
}
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

### ⏱️ Complexity
- **Time:** O(2ⁿ) subsets, O(n!) permutations
- **Space:** O(n) recursion depth

---

## 11. Dynamic Programming

### 🔍 What is it?
Break problem into overlapping subproblems, solve each once, store results (memoization/tabulation).

### ✅ When to Use
- Count, minimum, maximum, or feasibility
- Keywords: "number of ways", "min cost", "longest", "can you reach"
- Overlapping subproblems + optimal substructure

### 🧩 DP Framework
```
1. Define state: what does dp[i] or dp[i][j] represent?
2. Base case: smallest valid inputs
3. Recurrence: how does dp[i] depend on smaller states?
4. Answer: which dp entry is the final answer?
```

### 📝 Raw C++ — 1D DP (Climbing Stairs)
```cpp
#include <iostream>
#include <vector>
using namespace std;

// How many ways to climb n stairs (1 or 2 steps)
int climbStairs(int n) {
    if (n <= 2) return n;

    int dp[1001];                       // raw array (faster than vector for fixed size)
    dp[1] = 1;
    dp[2] = 2;

    for (int i = 3; i <= n; i++)
        dp[i] = dp[i-1] + dp[i-2];     // come from i-1 or i-2

    return dp[n];
}

// Space-optimized: only need last 2 values
int climbStairsOptimized(int n) {
    if (n <= 2) return n;
    int prev2 = 1, prev1 = 2;
    for (int i = 3; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

### 📝 STL C++ — 2D DP, Knapsack, LCS
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

// 2D DP — Unique Paths
int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n, 1)); // edges = 1 path

    for (int r = 1; r < m; r++)
        for (int c = 1; c < n; c++)
            dp[r][c] = dp[r-1][c] + dp[r][c-1];

    return dp[m-1][n-1];
}

// 0/1 Knapsack
int knapsack(vector<int>& weights, vector<int>& values, int capacity) {
    int n = weights.size();
    vector<vector<int>> dp(n + 1, vector<int>(capacity + 1, 0));

    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            dp[i][w] = dp[i-1][w];         // don't take item i
            if (weights[i-1] <= w)
                dp[i][w] = max(dp[i][w],
                               dp[i-1][w - weights[i-1]] + values[i-1]);
        }
    }
    return dp[n][capacity];
}

// Longest Common Subsequence
int lcs(string& s1, string& s2) {
    int m = s1.size(), n = s2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = (s1[i-1] == s2[j-1])
                       ? dp[i-1][j-1] + 1
                       : max(dp[i-1][j], dp[i][j-1]);

    return dp[m][n];
}

// Coin Change (minimum coins)
int coinChange(vector<int>& coins, int amount) {
    vector<int> dp(amount + 1, amount + 1); // init with "infinity"
    dp[0] = 0;

    for (int i = 1; i <= amount; i++)
        for (int coin : coins)
            if (coin <= i)
                dp[i] = min(dp[i], dp[i - coin] + 1);

    return dp[amount] > amount ? -1 : dp[amount];
}
```

### 📚 Classic Problems by Category
| Category | Problems |
|----------|---------|
| Linear DP | Climbing Stairs, House Robber, Coin Change |
| Grid DP | Unique Paths, Minimum Path Sum |
| Knapsack | 0/1 Knapsack, Partition Equal Subset Sum |
| String DP | LCS, Edit Distance, Palindromic Substrings |
| Interval DP | Burst Balloons, Matrix Chain Multiplication |

### ⏱️ Complexity
- **Time:** O(n²) or O(n×m) typically
- **Space:** Often reducible from O(n×m) to O(n)

---

## 12. Greedy

### 🔍 What is it?
Make the locally optimal choice at each step, trusting it leads to global optimum. No backtracking.

### ✅ When to Use
- Interval scheduling
- Jump game
- When exchange argument can be proven
- Minimum spanning tree (Prim's/Kruskal's)

> ⚠️ **Warning:** Greedy doesn't always work. Test on examples before committing.

### 📝 Raw C++ — Activity Selection
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Sort by end time, pick non-overlapping activities
int maxActivities(vector<pair<int,int>>& intervals) {
    // sort by end time (greedy: finish earliest, free up time)
    sort(intervals.begin(), intervals.end(),
         [](const pair<int,int>& a, const pair<int,int>& b) {
             return a.second < b.second;
         });

    int count = 1;
    int lastEnd = intervals[0].second;

    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i].first >= lastEnd) { // no overlap
            count++;
            lastEnd = intervals[i].second;
        }
    }
    return count;
}
```

### 📝 STL C++ — Jump Game & Gas Station
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Jump Game — can you reach the last index?
bool canJump(vector<int>& nums) {
    int maxReach = 0;

    for (int i = 0; i < nums.size(); i++) {
        if (i > maxReach) return false; // can't reach this index
        maxReach = max(maxReach, i + nums[i]);
    }
    return true;
}

// Jump Game II — minimum jumps to reach last index
int jump(vector<int>& nums) {
    int jumps = 0, currentEnd = 0, farthest = 0;

    for (int i = 0; i < nums.size() - 1; i++) {
        farthest = max(farthest, i + nums[i]);
        if (i == currentEnd) {          // must jump
            jumps++;
            currentEnd = farthest;
        }
    }
    return jumps;
}

// Gas Station — find starting position for circular trip
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int total = 0, tank = 0, start = 0;

    for (int i = 0; i < gas.size(); i++) {
        int net = gas[i] - cost[i];
        total += net;
        tank  += net;

        if (tank < 0) {                 // can't continue from 'start'
            start = i + 1;              // try next station as start
            tank  = 0;
        }
    }
    return total >= 0 ? start : -1;
}
```

### 📚 Classic Problems
| Problem | Greedy Choice |
|---------|---------------|
| Activity Selection / Non-overlapping Intervals | Sort by end time |
| Jump Game I & II | Track max reachable index |
| Gas Station | Circular greedy |
| Assign Cookies | Sort both, match greedily |
| Task Scheduler | Most frequent task first |

### ⏱️ Complexity
- **Time:** O(n log n) — dominated by sorting
- **Space:** O(1)

---

## 13. Merge Intervals

### 🔍 What is it?
Sort intervals by start time, then merge overlapping ones by extending the end of the last merged interval.

### ✅ When to Use
- Overlapping intervals/ranges
- Insert an interval and merge
- Meeting rooms, calendar conflicts

### 📝 Raw C++ — Merge Intervals
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<pair<int,int>> mergeIntervals(vector<pair<int,int>>& intervals) {
    if (intervals.empty()) return {};

    // sort by start time
    sort(intervals.begin(), intervals.end());

    vector<pair<int,int>> merged;
    merged.push_back(intervals[0]);

    for (int i = 1; i < intervals.size(); i++) {
        int start = intervals[i].first;
        int end   = intervals[i].second;

        if (start <= merged.back().second)              // overlap
            merged.back().second = max(merged.back().second, end);
        else
            merged.push_back({start, end});
    }
    return merged;
}
```

### 📝 STL C++ — Insert Interval & Meeting Rooms II
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <queue>
using namespace std;

// Insert and merge one new interval into sorted list
vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    vector<vector<int>> result;
    int i = 0, n = intervals.size();

    // add all intervals ending before new starts
    while (i < n && intervals[i][1] < newInterval[0])
        result.push_back(intervals[i++]);

    // merge overlapping
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = min(newInterval[0], intervals[i][0]);
        newInterval[1] = max(newInterval[1], intervals[i][1]);
        i++;
    }
    result.push_back(newInterval);

    // add remaining
    while (i < n) result.push_back(intervals[i++]);

    return result;
}

// Meeting Rooms II — minimum rooms needed
int minMeetingRooms(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end());
    priority_queue<int, vector<int>, greater<int>> minHeap; // min-heap of end times

    for (auto& interval : intervals) {
        if (!minHeap.empty() && minHeap.top() <= interval[0])
            minHeap.pop();              // room becomes free
        minHeap.push(interval[1]);      // assign room (track end time)
    }
    return minHeap.size();
}
```

### 📚 Classic Problems
| Problem | Technique |
|---------|-----------|
| Merge Intervals | Sort + merge |
| Insert Interval | Three phases |
| Meeting Rooms I | Check any overlap |
| Meeting Rooms II | Min-heap of end times |
| Employee Free Time | Merge all, find gaps |

### ⏱️ Complexity
- **Time:** O(n log n) | **Space:** O(n)

---

## 14. Linked List In-Place Reversal

### 🔍 What is it?
Reverse a linked list (or part of it) without extra space by relinking pointers in-place.

### ✅ When to Use
- Reverse entire list or sublist
- Palindrome linked list check
- Reorder list
- Reverse every k-group

### 📝 Raw C++ — Reverse Entire List
```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;

    while (curr) {
        ListNode* nextNode = curr->next; // save next
        curr->next = prev;               // reverse link
        prev = curr;                     // advance prev
        curr = nextNode;                 // advance curr
    }
    return prev;                         // new head
}
```

### 📝 STL-style C++ — Reverse Sublist & K-Group
```cpp
#include <iostream>
using namespace std;

// Reverse sublist from position left to right (1-indexed)
ListNode* reverseBetween(ListNode* head, int left, int right) {
    ListNode dummy(0);
    dummy.next = head;
    ListNode* prev = &dummy;

    for (int i = 0; i < left - 1; i++)
        prev = prev->next;              // reach node before 'left'

    ListNode* curr = prev->next;

    for (int i = 0; i < right - left; i++) {
        ListNode* nextNode = curr->next;
        curr->next = nextNode->next;
        nextNode->next = prev->next;
        prev->next = nextNode;
    }
    return dummy.next;
}

// Reverse every K-Group
ListNode* reverseKGroup(ListNode* head, int k) {
    // check if k nodes remain
    ListNode* node = head;
    int count = 0;
    while (node && count < k) { node = node->next; count++; }
    if (count < k) return head;        // less than k nodes, don't reverse

    ListNode* prev = nullptr;
    ListNode* curr = head;
    for (int i = 0; i < k; i++) {
        ListNode* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head->next = reverseKGroup(curr, k); // recurse on remaining
    return prev;
}
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
- **Time:** O(n) | **Space:** O(1)

---

## 15. Heap / Priority Queue

### 🔍 What is it?
A complete binary tree giving O(1) min/max and O(log n) insert/delete. STL `priority_queue` is a **max-heap** by default.

### ✅ When to Use
- Kth largest / Kth smallest
- Merge K sorted lists
- Dijkstra's shortest path
- Sliding window maximum
- Task scheduling

### 📝 Raw C++ — Manual Min-Heap (Array-based)
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Manual min-heap using array
struct MinHeap {
    vector<int> heap;

    void push(int val) {
        heap.push_back(val);
        // sift up
        int i = heap.size() - 1;
        while (i > 0) {
            int parent = (i - 1) / 2;
            if (heap[parent] > heap[i]) {
                swap(heap[parent], heap[i]);
                i = parent;
            } else break;
        }
    }

    void pop() {
        heap[0] = heap.back();
        heap.pop_back();
        // sift down
        int i = 0, n = heap.size();
        while (true) {
            int smallest = i;
            int l = 2*i+1, r = 2*i+2;
            if (l < n && heap[l] < heap[smallest]) smallest = l;
            if (r < n && heap[r] < heap[smallest]) smallest = r;
            if (smallest == i) break;
            swap(heap[i], heap[smallest]);
            i = smallest;
        }
    }

    int top() { return heap[0]; }
    bool empty() { return heap.empty(); }
    int size() { return heap.size(); }
};
```

### 📝 STL C++ — `priority_queue` Templates
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

// STL max-heap (default)
priority_queue<int> maxHeap;

// STL min-heap
priority_queue<int, vector<int>, greater<int>> minHeap;

// Kth Largest Element — min-heap of size k
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> pq; // min-heap

    for (int num : nums) {
        pq.push(num);
        if (pq.size() > k) pq.pop();    // keep only k largest
    }
    return pq.top();                    // kth largest = smallest in heap
}

// Top K Frequent Elements
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    for (int n : nums) freq[n]++;

    // min-heap of {frequency, value}
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;

    for (auto& [val, cnt] : freq) {
        pq.push({cnt, val});
        if (pq.size() > k) pq.pop();
    }

    vector<int> result;
    while (!pq.empty()) {
        result.push_back(pq.top().second);
        pq.pop();
    }
    return result;
}

// Dijkstra's Algorithm
vector<int> dijkstra(vector<vector<pair<int,int>>>& adj, int start) {
    int n = adj.size();
    vector<int> dist(n, INT_MAX);
    dist[start] = 0;

    // min-heap: {distance, node}
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
    pq.push({0, start});

    while (!pq.empty()) {
        auto [d, node] = pq.top(); pq.pop();

        if (d > dist[node]) continue;   // outdated entry, skip

        for (auto [neighbor, weight] : adj[node]) {
            int newDist = d + weight;
            if (newDist < dist[neighbor]) {
                dist[neighbor] = newDist;
                pq.push({newDist, neighbor});
            }
        }
    }
    return dist;
}

// Find Median from Data Stream — two heaps
class MedianFinder {
    priority_queue<int> lo;             // max-heap (lower half)
    priority_queue<int, vector<int>, greater<int>> hi; // min-heap (upper half)
public:
    void addNum(int num) {
        lo.push(num);
        hi.push(lo.top()); lo.pop();    // balance: move max of lo to hi
        if (hi.size() > lo.size()) {    // keep lo size >= hi size
            lo.push(hi.top()); hi.pop();
        }
    }
    double findMedian() {
        return lo.size() > hi.size()
               ? lo.top()
               : (lo.top() + hi.top()) / 2.0;
    }
};
```

### 📚 Classic Problems
| Problem | Heap Type |
|---------|-----------|
| Kth Largest Element | Min-heap of size k |
| Top K Frequent Elements | Min-heap |
| Merge K Sorted Lists | Min-heap |
| Find Median from Data Stream | Two heaps |
| Dijkstra's Shortest Path | Min-heap |
| Task Scheduler | Max-heap |

### ⏱️ Complexity
- **Push/Pop:** O(log n) | **Top:** O(1)

---

## 16. Trie

### 🔍 What is it?
A tree where each node is a character. Paths root-to-marked-node spell out words. O(L) insert and search.

### ✅ When to Use
- Auto-complete / prefix search
- Word search with prefix matching
- Longest common prefix
- Word Search II (Boggle)

### 📝 Raw C++ — Array-based Trie (Faster for a-z)
```cpp
#include <iostream>
#include <string>
using namespace std;

struct TrieNode {
    TrieNode* children[26];
    bool isEnd;

    TrieNode() : isEnd(false) {
        for (int i = 0; i < 26; i++)
            children[i] = nullptr;
    }
};

class TrieRaw {
    TrieNode* root;
public:
    TrieRaw() { root = new TrieNode(); }

    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!node->children[idx])
                node->children[idx] = new TrieNode();
            node = node->children[idx];
        }
        node->isEnd = true;
    }

    bool search(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!node->children[idx]) return false;
            node = node->children[idx];
        }
        return node->isEnd;
    }

    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            int idx = c - 'a';
            if (!node->children[idx]) return false;
            node = node->children[idx];
        }
        return true;
    }
};
```

### 📝 STL C++ — HashMap-based Trie (Any Characters)
```cpp
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

struct TrieNodeSTL {
    unordered_map<char, TrieNodeSTL*> children;  // supports any char
    bool isEnd = false;
};

class TrieSTL {
    TrieNodeSTL* root;
public:
    TrieSTL() { root = new TrieNodeSTL(); }

    void insert(const string& word) {
        TrieNodeSTL* node = root;
        for (char c : word) {
            if (!node->children.count(c))
                node->children[c] = new TrieNodeSTL();
            node = node->children[c];
        }
        node->isEnd = true;
    }

    bool search(const string& word) {
        TrieNodeSTL* node = root;
        for (char c : word) {
            if (!node->children.count(c)) return false;
            node = node->children[c];
        }
        return node->isEnd;
    }

    bool startsWith(const string& prefix) {
        TrieNodeSTL* node = root;
        for (char c : prefix) {
            if (!node->children.count(c)) return false;
            node = node->children[c];
        }
        return true;
    }
};
```

### 📚 Classic Problems
| Problem | Technique |
|---------|-----------|
| Implement Trie | Basic implementation |
| Word Search II | Trie + DFS backtracking |
| Design Search Autocomplete | Trie + BFS/DFS |
| Replace Words | Trie prefix matching |
| Longest Word in Dictionary | Trie + BFS |

### ⏱️ Complexity
- **Insert/Search:** O(L) | **Space:** O(alphabet × L × N)

---

## 17. Union Find (Disjoint Set)

### 🔍 What is it?
Efficiently tracks connected components. Supports union (merge) and find (which group?) in near O(1) with path compression + union by rank.

### ✅ When to Use
- Number of connected components
- Detect cycle in undirected graph
- Kruskal's MST
- Accounts merge problem

### 📝 Raw C++ — Manual Union Find
```cpp
#include <iostream>
#include <vector>
using namespace std;

int parent[100001];
int rankArr[100001];

int find(int x) {
    if (parent[x] != x)
        parent[x] = find(parent[x]);   // path compression
    return parent[x];
}

bool unite(int x, int y) {
    int px = find(x), py = find(y);
    if (px == py) return false;        // already connected

    // union by rank
    if (rankArr[px] < rankArr[py]) swap(px, py);
    parent[py] = px;
    if (rankArr[px] == rankArr[py]) rankArr[px]++;

    return true;
}
```

### 📝 STL C++ — Class-based Union Find
```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

class UnionFind {
    vector<int> parent, rank_;
public:
    int components;

    UnionFind(int n) : parent(n), rank_(n, 0), components(n) {
        iota(parent.begin(), parent.end(), 0); // STL: fill 0,1,2,...,n-1
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // path compression
        return parent[x];
    }

    bool unite(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false;

        if (rank_[px] < rank_[py]) swap(px, py);
        parent[py] = px;
        if (rank_[px] == rank_[py]) rank_[px]++;

        components--;
        return true;
    }

    bool connected(int x, int y) {
        return find(x) == find(y);
    }
};

// Usage: Number of Provinces
int findCircleNum(vector<vector<int>>& isConnected) {
    int n = isConnected.size();
    UnionFind uf(n);

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (isConnected[i][j])
                uf.unite(i, j);

    return uf.components;
}

// Redundant Connection — find the edge that creates a cycle
vector<int> findRedundantConnection(vector<vector<int>>& edges) {
    int n = edges.size();
    UnionFind uf(n + 1);

    for (auto& edge : edges) {
        if (!uf.unite(edge[0], edge[1]))
            return edge;               // this edge created a cycle
    }
    return {};
}
```

### 📚 Classic Problems
| Problem | Use |
|---------|-----|
| Number of Provinces | Count components |
| Redundant Connection | Detect cycle |
| Accounts Merge | Union by common email |
| Number of Islands | Union adjacent land |
| Kruskal's MST | Sort edges + union |

### ⏱️ Complexity
- **Find/Union:** O(α(n)) ≈ O(1) amortized

---

## 18. Bit Manipulation

### 🔍 What is it?
Operate directly on binary representations using bitwise operators. Often gives O(1) or O(n) solutions for number problems.

### 📝 Bit Operations Reference
```cpp
n & 1           // check if n is odd
n >> 1          // divide by 2
n << 1          // multiply by 2
n & (n - 1)     // clear lowest set bit  (6=110 → 4=100)
n & (-n)        // isolate lowest set bit (6=110 → 2=010)
n ^ n           // = 0  (XOR with itself)
n ^ 0           // = n  (XOR with 0)
~n              // flip all bits
__builtin_popcount(n)   // GCC: count set bits (O(1))
__builtin_ctz(n)        // GCC: count trailing zeros
__builtin_clz(n)        // GCC: count leading zeros
```

### 📝 Raw C++ — Classic Templates
```cpp
#include <iostream>
#include <vector>
using namespace std;

// Single Number — find element appearing once (rest appear twice)
int singleNumber(vector<int>& nums) {
    int result = 0;
    for (int num : nums)
        result ^= num;                  // XOR cancels duplicates
    return result;
}

// Count set bits (Hamming Weight)
int hammingWeight(uint32_t n) {
    int count = 0;
    while (n) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Faster: Brian Kernighan's algorithm
int hammingWeightFast(uint32_t n) {
    int count = 0;
    while (n) {
        n &= (n - 1);                   // clears lowest set bit
        count++;
    }
    return count;
}

// Is power of 2?
bool isPowerOfTwo(int n) {
    return n > 0 && (n & (n - 1)) == 0;
}

// Reverse 32 bits
uint32_t reverseBits(uint32_t n) {
    uint32_t result = 0;
    for (int i = 0; i < 32; i++) {
        result = (result << 1) | (n & 1);
        n >>= 1;
    }
    return result;
}
```

### 📝 STL C++ — Bitmask for Subsets
```cpp
#include <iostream>
#include <vector>
#include <bitset>
using namespace std;

// Generate all subsets using bitmask
vector<vector<int>> subsetsWithBitmask(vector<int>& nums) {
    int n = nums.size();
    int total = 1 << n;                 // 2^n subsets
    vector<vector<int>> result;

    for (int mask = 0; mask < total; mask++) {
        vector<int> subset;
        for (int i = 0; i < n; i++)
            if (mask & (1 << i))        // bit i is set
                subset.push_back(nums[i]);
        result.push_back(subset);
    }
    return result;
}

// STL bitset for fixed-size bit operations
bitset<32> b(42);                       // 42 in binary
cout << b.count() << endl;             // number of set bits
cout << b.to_string() << endl;         // binary string

// Missing Number — XOR with indices
int missingNumber(vector<int>& nums) {
    int result = nums.size();
    for (int i = 0; i < nums.size(); i++)
        result ^= i ^ nums[i];
    return result;
}
```

### 📚 Classic Problems
| Problem | Trick |
|---------|-------|
| Single Number | XOR cancels pairs |
| Single Number II | Count bits mod 3 |
| Number of 1 Bits | `n & (n-1)` loop or `__builtin_popcount` |
| Reverse Bits | Shift and OR |
| Missing Number | XOR with indices |
| Power of Two | `n & (n-1) == 0` |
| Subsets | Bitmask enumeration |

### ⏱️ Complexity
- **Time:** O(1) or O(n) | **Space:** O(1)

---

## 19. STL Quick Reference

### Containers
```cpp
#include <vector>       // dynamic array
#include <deque>        // double-ended queue
#include <list>         // doubly linked list
#include <stack>        // LIFO (uses deque internally)
#include <queue>        // FIFO (uses deque internally)
#include <priority_queue> // heap (max-heap by default)
#include <set>          // sorted unique elements, O(log n)
#include <unordered_set>// hash set, O(1) avg
#include <map>          // sorted key-value, O(log n)
#include <unordered_map>// hash map, O(1) avg
#include <string>
```

### Common Patterns with STL
```cpp
// Max-heap
priority_queue<int> maxPQ;

// Min-heap
priority_queue<int, vector<int>, greater<int>> minPQ;

// Custom comparator (max-heap by frequency)
auto cmp = [](pair<int,int>& a, pair<int,int>& b) {
    return a.second < b.second;         // max by second element
};
priority_queue<pair<int,int>, vector<pair<int,int>>, decltype(cmp)> pq(cmp);

// Sort with custom comparator
sort(v.begin(), v.end(), [](int a, int b) { return a > b; }); // descending

// Sort pairs by second element
sort(intervals.begin(), intervals.end(),
     [](auto& a, auto& b) { return a.second < b.second; });

// Binary search
lower_bound(v.begin(), v.end(), target); // first element >= target
upper_bound(v.begin(), v.end(), target); // first element >  target

// Useful algorithms
reverse(v.begin(), v.end());
rotate(v.begin(), v.begin() + k, v.end());
accumulate(v.begin(), v.end(), 0);       // sum
*max_element(v.begin(), v.end());
*min_element(v.begin(), v.end());
next_permutation(v.begin(), v.end());
fill(v.begin(), v.end(), 0);
iota(v.begin(), v.end(), 0);            // fill 0,1,2,...
count(v.begin(), v.end(), val);
find(v.begin(), v.end(), val);
```

### STL Complexity Table
| Container | Access | Insert | Delete | Search |
|-----------|--------|--------|--------|--------|
| `vector` | O(1) | O(1) amort | O(n) | O(n) |
| `deque` | O(1) | O(1) front/back | O(n) mid | O(n) |
| `list` | O(n) | O(1) | O(1) | O(n) |
| `set` / `map` | O(log n) | O(log n) | O(log n) | O(log n) |
| `unordered_set` / `unordered_map` | O(1) avg | O(1) avg | O(1) avg | O(1) avg |
| `priority_queue` | O(1) top | O(log n) | O(log n) | — |
| `stack` / `queue` | O(1) top/front | O(1) | O(1) | — |

---

## 20. Pattern Recognition Cheatsheet

### 🔍 By Keywords
| Keyword / Clue | Pattern to Try |
|---------------|---------------|
| "sorted array" + pair | Two Pointers |
| "subarray" / "substring" + max/min length | Sliding Window |
| "linked list" + cycle / middle | Fast & Slow Pointers |
| "sorted" + find target / minimize | Binary Search |
| "sum of subarray" + multiple queries | Prefix Sum |
| "count frequency" / "find duplicate" | HashMap (`unordered_map`) |
| "next greater" / "nearest smaller" | Monotonic Stack |
| "shortest path" / "level by level" | BFS (`queue`) |
| "all paths" / "connected components" | DFS |
| "all combinations" / "all permutations" | Backtracking |
| "minimum cost" / "number of ways" | Dynamic Programming |
| "interval overlap" / "meeting rooms" | Merge Intervals |
| "kth largest" / "top K" | Heap (`priority_queue`) |
| "prefix search" / "autocomplete" | Trie |
| "connected groups" / "union merge" | Union Find |
| "XOR" / "appear once" / "bit count" | Bit Manipulation |
| "locally optimal = globally optimal" | Greedy |

### 🔍 By Data Structure / Input Type
| Input Type | Common Patterns |
|-----------|----------------|
| Sorted Array | Two Pointers, Binary Search, Sliding Window |
| Unsorted Array | HashMap, Prefix Sum, Monotonic Stack |
| Linked List | Fast/Slow, In-Place Reversal |
| Binary Tree | DFS (recursion), BFS (`queue`) |
| Graph | BFS (shortest), DFS (components), Union Find |
| String | Sliding Window, HashMap, Trie |
| Numbers | Bit Manipulation, DP |
| Intervals | Merge Intervals, Heap |

---

## 21. Complexity Quick Reference

### Time Complexity
| Complexity | Name | Example |
|-----------|------|---------|
| O(1) | Constant | `vector` index, `unordered_map` lookup |
| O(log n) | Logarithmic | Binary Search, `set`/`map` ops |
| O(n) | Linear | Single loop, Two Pointers |
| O(n log n) | Linearithmic | `sort()`, heap operations |
| O(n²) | Quadratic | Nested loops, brute force |
| O(2ⁿ) | Exponential | Subsets, Backtracking |
| O(n!) | Factorial | Permutations |

### Pattern Complexity Summary
| Pattern | Time | Space | STL Used |
|---------|------|-------|----------|
| Two Pointers | O(n) | O(1) | — |
| Sliding Window | O(n) | O(k) | `unordered_map` |
| Binary Search | O(log n) | O(1) | `lower_bound`, `upper_bound` |
| Prefix Sum | O(n) build, O(1) query | O(n) | `vector` |
| BFS | O(V+E) | O(V) | `queue` |
| DFS | O(V+E) | O(V) | `stack` / recursion |
| Backtracking | O(2ⁿ) or O(n!) | O(n) | `set`, `vector` |
| DP | O(n²) typical | O(n)–O(n²) | `vector` |
| Heap | O(n log k) | O(k) | `priority_queue` |
| Trie | O(L) per op | O(N×L) | `unordered_map` |
| Union Find | O(α(n)) ≈ O(1) | O(n) | `vector`, `iota` |
| Monotonic Stack | O(n) | O(n) | `stack` |

---

## ✅ How to Approach Any DSA Problem

```
Step 1: UNDERSTAND
  → What is the input? Output? Edge cases?
  → What are the constraints? (n size, sorted? negative numbers?)
  → Trace through examples by hand.

Step 2: IDENTIFY THE PATTERN
  → Use the Pattern Recognition Cheatsheet above.
  → Which data structures naturally fit?

Step 3: PLAN
  → Write pseudocode first.
  → State time and space complexity before coding.

Step 4: CODE (in C++)
  → Write the core logic first.
  → Then add edge case handling.
  → Prefer STL containers over manual implementations in interviews.

Step 5: TEST
  → Test provided examples.
  → Test edge cases: empty input, n=1, all same values, INT_MAX.

Step 6: OPTIMIZE
  → unordered_map over map when order doesn't matter (O(1) vs O(log n))
  → vector over list (cache friendliness)
  → Can you reduce O(n²) to O(n log n) with sort + two pointers?
```

### 💡 C++ Interview Tips
```cpp
// Use auto for cleaner code
for (auto& [key, val] : myMap) { ... }

// Structured bindings (C++17)
auto [lo, hi] = make_pair(0, n-1);

// Use INT_MAX / INT_MIN carefully — adding to INT_MAX overflows
int dist = INT_MAX;
if (dist != INT_MAX) dist += weight;   // safe addition

// Reserve vector size when known — avoids reallocations
vector<int> result;
result.reserve(n);

// Use emplace_back instead of push_back for objects
vec.emplace_back(1, 2);               // constructs in-place
```

---

> 🚀 **Remember:** STL mastery = interview advantage. Know your containers, know their complexities, and know which to reach for at first glance.

---

*Last Updated: 2025 | C++17 | Covers LeetCode, Codeforces, and FAANG interviews*
