# 📊 Big O Notation — Complete Handbook (C++ Edition)

> **The ultimate Big O guide for beginners, software engineers, and competitive programmers.**
> Every complexity class explained with real C++ code — from constant time to factorial explosion.

---

## 📌 What is Big O Notation?

**Big O Notation** is a mathematical notation used to describe how the **runtime or memory usage of an algorithm scales** as the input size `n` grows. It gives you a language to compare algorithms independently of hardware, compiler, or implementation details.

It answers the single most important engineering question:
> *"How does this code behave when the input gets very large?"*

Big O describes the **worst-case upper bound** — drop constants, drop lower-order terms, keep the dominant growth factor.

```cpp
// f(n) = 3n² + 5n + 12
// Big O: O(n²)  ← constants and lower terms are dropped
```

---

## 🧠 Why Does Big O Matter?

| Input Size `n` | O(log n) | O(n) | O(n²) | O(2ⁿ) | O(n!) |
|---------------|----------|------|-------|-------|-------|
| 10 | 3 | 10 | 100 | 1,024 | 3.6M |
| 100 | 7 | 100 | 10,000 | 10³⁰ | 10¹⁵⁷ |
| 1,000 | 10 | 1,000 | 1,000,000 | 💀 | 💀 |
| 1,000,000 | 20 | 1,000,000 | 10¹² | 💀 | 💀 |

> The difference between `O(n)` and `O(n²)` on 1 million records is the difference between **~1 ms** and **~16 minutes**.

---

## 📈 Growth Rate Visualization

```
Operations
    |
    |                                              O(n!)
    |                                           ↗
    |                                      O(2ⁿ)
    |                                   ↗
    |                             O(n⁴)
    |                          ↗
    |                    O(n³)
    |                 ↗
    |           O(n²)
    |         ↗
    |     O(n log n)
    |   ↗
    | O(n)
    |↗ O(log n)
    |— O(1)
    └─────────────────────────────────────────── n
```

---

## 📖 Table of Contents

1. [O(1) — Constant Time](#1-o1--constant-time)
2. [O(log n) — Logarithmic Time](#2-olog-n--logarithmic-time)
3. [O(n) — Linear Time](#3-on--linear-time)
4. [O(n log n) — Linearithmic Time](#4-on-log-n--linearithmic-time)
5. [O(n²) — Quadratic Time](#5-on²--quadratic-time)
6. [O(n³) — Cubic Time](#6-on³--cubic-time)
7. [O(n⁴) — Quartic Time](#7-on⁴--quartic-time)
8. [O(2ⁿ) — Exponential Time](#8-o2ⁿ--exponential-time)
9. [O(n!) — Factorial Time](#9-on--factorial-time)
10. [Space Complexity](#10-space-complexity)
11. [Comparison Tables](#11-comparison-tables)
12. [Identifying Complexity — Rules](#12-identifying-complexity--rules)
13. [Interview Tips](#13-interview-tips)
14. [Exercises & Challenges](#14-exercises--challenges)
15. [Conclusion & Resources](#15-conclusion--resources)

---

## 1. O(1) — Constant Time

### Definition

An algorithm runs in **O(1)** when the number of operations is **fixed regardless of input size**. Whether `n = 5` or `n = 5,000,000`, it always takes the same number of steps.

### Theory

The "1" doesn't mean exactly one operation. It means a **bounded constant** — `O(3)`, `O(100)`, `O(500)` all simplify to `O(1)` because they don't grow with `n`.

### Real-World Use Cases

- Array/vector index access
- `unordered_map` (hash table) insert/lookup
- Stack `push` and `pop`
- Arithmetic operations
- Swapping two variables

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <stack>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Array index access
// Direct memory offset — always one step
// ─────────────────────────────────────────

int getElement(const vector<int>& arr, int index) {
    return arr[index]; // O(1) — direct memory access
}

// ─────────────────────────────────────────
// Example 2: unordered_map lookup
// Hash table → average O(1) lookup
// ─────────────────────────────────────────

string getUserById(const unordered_map<int, string>& users, int id) {
    auto it = users.find(id); // O(1) average — hash lookup
    if (it != users.end())
        return it->second;
    return "Not found";
}

// ─────────────────────────────────────────
// Example 3: Stack push / pop
// Only touches the top element — no traversal
// ─────────────────────────────────────────

void stackDemo() {
    stack<int> s;
    s.push(10); // O(1)
    s.push(20); // O(1)
    s.push(30); // O(1)
    s.pop();    // O(1) — removes 30
    cout << s.top() << "\n"; // O(1) — prints 20
}

// ─────────────────────────────────────────
// Example 4: Swap two elements
// Fixed 3 assignments no matter what n is
// ─────────────────────────────────────────

void swapElements(vector<int>& arr, int i, int j) {
    int temp = arr[i]; // O(1)
    arr[i] = arr[j];   // O(1)
    arr[j] = temp;     // O(1)
    // Total: O(1) — constant regardless of array size
}

int main() {
    vector<int> data = {5, 10, 15, 20, 25};
    cout << getElement(data, 3) << "\n"; // 20

    unordered_map<int, string> users = {{1, "Alice"}, {2, "Bob"}, {3, "Carol"}};
    cout << getUserById(users, 2) << "\n"; // Bob

    stackDemo(); // 20

    swapElements(data, 0, 4);
    cout << data[0] << " " << data[4] << "\n"; // 25 5

    return 0;
}
```

### Important Points

- ✅ Best possible complexity — the gold standard
- ✅ `unordered_map` is O(1) **average** — O(n) worst case (hash collisions)
- ✅ `map` (red-black tree) is O(log n) — not O(1)
- ❌ O(1) doesn't mean "fast" — it means "doesn't grow with n"

### Best Practices

- Use `unordered_map` over `map` when you need fast lookup and don't need sorted keys
- Prefer array index access over search when index is known
- Avoid confusing `std::map` (O(log n)) with `std::unordered_map` (O(1))

### Common Mistakes

```cpp
// ❌ This looks O(1) but is actually O(n) — list has no random access
list<int> lst = {1, 2, 3, 4, 5};
auto it = lst.begin();
advance(it, 3); // O(n) — has to walk the linked list

// ✅ Use vector for O(1) index access
vector<int> vec = {1, 2, 3, 4, 5};
int val = vec[3]; // O(1) — direct memory access
```

---

## 2. O(log n) — Logarithmic Time

### Definition

An algorithm is **O(log n)** when it **eliminates half the remaining possibilities each step**. The work grows proportionally to the logarithm of the input, not the input itself.

### Theory

`log₂(n)` = how many times you can halve `n` before reaching 1.

```
n = 8    → 8→4→2→1       = 3 steps  (log₂ 8  = 3)
n = 1024 → 1024→512→...→1 = 10 steps (log₂ 1024 = 10)
n = 10⁶  →                 = 20 steps (log₂ 10⁶ ≈ 20)
```

Doubling `n` only adds **one more step**. That's the power of logarithmic algorithms.

### Real-World Use Cases

- Binary search on a sorted array
- `std::lower_bound`, `std::upper_bound`
- Operations on balanced BST (`std::map`, `std::set`)
- Exponentiation by squaring
- Segment trees, Fenwick trees (BIT)

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Binary Search (iterative)
// Each iteration cuts the search space in half
// ─────────────────────────────────────────

int binarySearch(const vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {            // Runs at most log₂(n) times
        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
            return mid;                // Found
        else if (arr[mid] < target)
            left = mid + 1;            // Discard LEFT half
        else
            right = mid - 1;           // Discard RIGHT half
    }

    return -1; // Not found
}

// ─────────────────────────────────────────
// Example 2: Binary Search (recursive)
// Same logic — each call halves the range
// ─────────────────────────────────────────

int binarySearchRecursive(const vector<int>& arr, int target, int left, int right) {
    if (left > right) return -1;       // Base case: not found

    int mid = left + (right - left) / 2;

    if (arr[mid] == target)   return mid;
    if (arr[mid] < target)    return binarySearchRecursive(arr, target, mid + 1, right);
    return binarySearchRecursive(arr, target, left, mid - 1);
}

// ─────────────────────────────────────────
// Example 3: Fast Exponentiation (Power by squaring)
// x^n computed in O(log n) instead of O(n)
// x^8 = ((x²)²)²  →  3 multiplications instead of 7
// ─────────────────────────────────────────

long long fastPow(long long base, long long exp) {
    long long result = 1;

    while (exp > 0) {               // O(log exp) iterations
        if (exp % 2 == 1)
            result *= base;         // Odd exponent: multiply result
        base *= base;               // Square the base
        exp /= 2;                   // Halve the exponent
    }

    return result;
}

// ─────────────────────────────────────────
// Example 4: Count digits in a number
// Halving via log10 — O(log n)
// ─────────────────────────────────────────

int countDigits(int n) {
    if (n == 0) return 1;
    return (int)log10(abs(n)) + 1; // O(log n)
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};

    cout << binarySearch(arr, 7) << "\n";            // 3 (index)
    cout << binarySearchRecursive(arr, 15, 0, arr.size()-1) << "\n"; // 7
    cout << fastPow(2, 10) << "\n";                  // 1024
    cout << countDigits(123456) << "\n";             // 6

    return 0;
}
```

### Important Points

- ✅ Extremely efficient — handles billions of elements in ~30 steps
- ✅ `std::map` and `std::set` are O(log n) for all operations (balanced BST)
- ✅ `std::lower_bound` is O(log n) on random-access iterators
- ❌ Binary search requires a **sorted** array — sorting is O(n log n) itself

### Best Practices

- Always verify the array is sorted before binary search
- Use `left + (right - left) / 2` instead of `(left + right) / 2` to avoid integer overflow
- Prefer `std::lower_bound` / `std::upper_bound` from `<algorithm>` over manual binary search

---

## 3. O(n) — Linear Time

### Definition

An algorithm is **O(n)** when it must **visit each element exactly once** (or a fixed number of times). Doubling the input doubles the work.

### Theory

Linear time is the minimum complexity for most problems that require reading all input — you can't solve "what's the sum of all elements?" in less than O(n) because you must read every element at least once.

### Real-World Use Cases

- Linear search (unsorted array)
- Array sum, max, min
- Counting elements
- Single-pass string processing
- Copying an array

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Linear Search
// Must check every element until found (worst case)
// ─────────────────────────────────────────

int linearSearch(const vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) { // O(n) — up to n iterations
        if (arr[i] == target)
            return i;
    }
    return -1;
}

// ─────────────────────────────────────────
// Example 2: Find max element
// Must look at every element to be sure
// ─────────────────────────────────────────

int findMax(const vector<int>& arr) {
    int maxVal = arr[0];
    for (int i = 1; i < arr.size(); i++) { // O(n)
        if (arr[i] > maxVal)
            maxVal = arr[i];
    }
    return maxVal;
}

// ─────────────────────────────────────────
// Example 3: Reverse an array in-place
// Visit each element once using two pointers
// ─────────────────────────────────────────

void reverseArray(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;
    while (left < right) {             // O(n/2) = O(n)
        swap(arr[left], arr[right]);
        left++;
        right--;
    }
}

// ─────────────────────────────────────────
// Example 4: Check if string is palindrome
// One pass with two pointers
// ─────────────────────────────────────────

bool isPalindrome(const string& s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {             // O(n)
        if (s[left] != s[right])
            return false;
        left++;
        right--;
    }
    return true;
}

// ─────────────────────────────────────────
// Example 5: Two Sum (using hash map)
// Single pass — O(n) instead of O(n²)
// ─────────────────────────────────────────

pair<int,int> twoSum(const vector<int>& arr, int target) {
    unordered_map<int, int> seen; // value → index

    for (int i = 0; i < arr.size(); i++) {   // O(n)
        int complement = target - arr[i];
        if (seen.count(complement))
            return {seen[complement], i};
        seen[arr[i]] = i;
    }

    return {-1, -1}; // not found
}

int main() {
    vector<int> arr = {64, 34, 25, 12, 22, 11, 90};

    cout << linearSearch(arr, 22) << "\n"; // 4
    cout << findMax(arr) << "\n";          // 90

    reverseArray(arr);
    for (int x : arr) cout << x << " ";   // 90 11 22 12 25 34 64
    cout << "\n";

    cout << boolalpha << isPalindrome("racecar") << "\n"; // true
    cout << isPalindrome("hello") << "\n";                // false

    vector<int> nums = {2, 7, 11, 15};
    auto [i, j] = twoSum(nums, 9);
    cout << i << " " << j << "\n"; // 0 1  (nums[0] + nums[1] = 9)

    return 0;
}
```

### Important Points

- ✅ Optimal for problems that must read every element
- ✅ Two-pointer technique often reduces O(n²) to O(n)
- ✅ Hash maps turn many O(n²) search problems into O(n)
- ❌ Cannot do better than O(n) if all elements must be examined

### Best Practices

- Use two-pointer technique for array/string problems involving pairs
- Use hash maps to reduce nested loop problems to a single pass
- Range-based for loops (`for (auto x : arr)`) are cleaner and equally O(n)

---

## 4. O(n log n) — Linearithmic Time

### Definition

An algorithm is **O(n log n)** when it **performs a logarithmic operation for each of the n elements**. This is the complexity class of efficient, comparison-based sorting algorithms.

### Theory

O(n log n) is the **theoretical lower bound** for comparison-based sorting. You cannot sort by comparison in less than O(n log n) — it's mathematically proven.

```
Merge Sort on [5, 2, 4, 1, 3]:
Split:    [5,2,4,1,3]          ← 1 level
Split:    [5,2] [4,1,3]        ← 2 levels  (log n levels total)
Split:    [5][2] [4][1][3]     ← 3 levels
Merge:    [2,5] [1,4] [3]      ← Each level does O(n) merge work
Merge:    [1,2,4,5] [3]
Merge:    [1,2,3,4,5]
Total: O(n) work × O(log n) levels = O(n log n)
```

### Real-World Use Cases

- `std::sort` (introsort — O(n log n) guaranteed)
- Merge sort (stable sort)
- Heap sort
- FFT (Fast Fourier Transform)
- Many divide-and-conquer algorithms

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Merge Sort
// Divide into halves (log n levels), merge (n work per level)
// ─────────────────────────────────────────

void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    vector<int> L(arr.begin() + left, arr.begin() + mid + 1);
    vector<int> R(arr.begin() + mid + 1, arr.begin() + right + 1);

    int i = 0, j = 0, k = left;

    // Merge the two halves — O(n) per call
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else               arr[k++] = R[j++];
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left >= right) return;          // Base case

    int mid = left + (right - left) / 2;

    mergeSort(arr, left, mid);          // Sort left half  — recurse
    mergeSort(arr, mid + 1, right);     // Sort right half — recurse
    merge(arr, left, mid, right);       // Merge — O(n)
    // Recursion depth = log n levels → Total: O(n log n)
}

// ─────────────────────────────────────────
// Example 2: Quick Sort (average O(n log n))
// Partition around pivot, recurse on each side
// ─────────────────────────────────────────

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) { // O(n) per partition
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // O(n) partition
        quickSort(arr, low, pi - 1);        // Recurse left
        quickSort(arr, pi + 1, high);       // Recurse right
        // Average: O(n log n) — worst case O(n²) on sorted input
    }
}

// ─────────────────────────────────────────
// Example 3: Using std::sort (O(n log n) guaranteed)
// Introsort: quicksort + heapsort fallback + insertion sort
// ─────────────────────────────────────────

void stdSortDemo() {
    vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    sort(arr.begin(), arr.end());            // O(n log n)

    // Custom comparator — sort descending
    sort(arr.begin(), arr.end(), [](int a, int b) {
        return a > b;                        // O(n log n)
    });

    for (int x : arr) cout << x << " ";
    cout << "\n";
}

int main() {
    vector<int> arr1 = {64, 34, 25, 12, 22, 11, 90};
    mergeSort(arr1, 0, arr1.size() - 1);
    for (int x : arr1) cout << x << " "; // 11 12 22 25 34 64 90
    cout << "\n";

    vector<int> arr2 = {10, 7, 8, 9, 1, 5};
    quickSort(arr2, 0, arr2.size() - 1);
    for (int x : arr2) cout << x << " "; // 1 5 7 8 9 10
    cout << "\n";

    stdSortDemo(); // 90 64 34 25 22 12 11

    return 0;
}
```

### Important Points

- ✅ The best you can do for general-purpose comparison sorting
- ✅ `std::sort` is the practical choice — always use it unless you need stability
- ✅ Merge sort is stable; `std::sort` is not (use `std::stable_sort`)
- ❌ Quick sort degrades to O(n²) on already-sorted input without randomization

### Best Practices

- Use `std::sort` for general sorting — it's highly optimized
- Use `std::stable_sort` when relative order of equal elements matters
- Randomize the pivot in quicksort to avoid worst-case O(n²)

---

## 5. O(n²) — Quadratic Time

### Definition

An algorithm is **O(n²)** when it uses **two nested loops**, each iterating proportionally to `n`. Doubling the input **quadruples** the work.

### Theory

For every element in the outer loop, the inner loop runs `n` times.

```
n = 10   → 100 operations
n = 100  → 10,000 operations
n = 1000 → 1,000,000 operations   ← Gets slow fast
```

### Real-World Use Cases

- Bubble Sort
- Insertion Sort
- Selection Sort
- Finding all pairs in an array
- Naive string matching
- Simple matrix operations on n×n grids

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Bubble Sort
// For each element, compare with every other → n × n
// ─────────────────────────────────────────

void bubbleSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) {         // Outer: O(n)
        for (int j = 0; j < n - i - 1; j++) { // Inner: O(n)
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
    // Total: O(n) × O(n) = O(n²)
}

// ─────────────────────────────────────────
// Example 2: Selection Sort
// Find the minimum in remaining array — n times
// ─────────────────────────────────────────

void selectionSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) {      // Outer: O(n)
        int minIdx = i;

        for (int j = i + 1; j < n; j++) {  // Inner: O(n)
            if (arr[j] < arr[minIdx])
                minIdx = j;
        }
        swap(arr[i], arr[minIdx]);
    }
    // Total: O(n²)
}

// ─────────────────────────────────────────
// Example 3: Insertion Sort
// Insert each element into its sorted position
// ─────────────────────────────────────────

void insertionSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 1; i < n; i++) {       // Outer: O(n)
        int key = arr[i];
        int j = i - 1;

        // Shift larger elements right — O(n) worst case
        while (j >= 0 && arr[j] > key) { // Inner: O(n) worst case
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
    // Total: O(n²) worst — O(n) best (nearly sorted input)
}

// ─────────────────────────────────────────
// Example 4: Find all pairs that sum to target
// Check every pair: n * (n-1) / 2 combinations = O(n²)
// ─────────────────────────────────────────

vector<pair<int,int>> findAllPairs(const vector<int>& arr, int target) {
    vector<pair<int,int>> result;
    int n = arr.size();

    for (int i = 0; i < n; i++) {          // Outer: O(n)
        for (int j = i + 1; j < n; j++) { // Inner: O(n)
            if (arr[i] + arr[j] == target)
                result.push_back({arr[i], arr[j]});
        }
    }
    return result; // O(n²)
}

// ─────────────────────────────────────────
// Example 5: Naive pattern search
// For each position in text, check if pattern matches
// ─────────────────────────────────────────

int naivePatternSearch(const string& text, const string& pattern) {
    int n = text.size(), m = pattern.size();

    for (int i = 0; i <= n - m; i++) {     // Outer: O(n)
        int j = 0;
        while (j < m && text[i + j] == pattern[j]) { // Inner: O(m) ≈ O(n)
            j++;
        }
        if (j == m)
            return i; // Found at index i
    }
    return -1; // Not found
}

int main() {
    vector<int> arr1 = {64, 34, 25, 12, 22, 11, 90};
    bubbleSort(arr1);
    for (int x : arr1) cout << x << " "; // 11 12 22 25 34 64 90
    cout << "\n";

    vector<int> arr2 = {29, 10, 14, 37, 13};
    selectionSort(arr2);
    for (int x : arr2) cout << x << " "; // 10 13 14 29 37
    cout << "\n";

    vector<int> arr3 = {1, 3, 5, 2, 8, 4};
    auto pairs = findAllPairs(arr3, 9);
    for (auto [a, b] : pairs)
        cout << a << "+" << b << "=9  "; // 1+8=9  5+4=9
    cout << "\n";

    cout << naivePatternSearch("hello world", "world") << "\n"; // 6

    return 0;
}
```

### Important Points

- ✅ Fine for small inputs (n < 1,000)
- ✅ Insertion sort is fast in practice on nearly-sorted data
- ❌ Avoid for n > 10,000 — becomes noticeably slow
- ❌ The most common "interview trap" — nested loops are almost always O(n²)

### Best Practices

- Replace O(n²) pair-finding with hash maps for O(n)
- Use `std::sort` + two-pointer instead of nested loops for sorted-array problems
- Insertion sort is acceptable for small arrays (used inside `std::sort` for n < ~16)

### Common Mistakes

```cpp
// ❌ This looks like O(n) but is O(n²) — erase() on vector is O(n)
for (int i = 0; i < vec.size(); i++) {
    if (vec[i] == target)
        vec.erase(vec.begin() + i); // O(n) shift! Makes the loop O(n²)
}

// ✅ Use erase-remove idiom — O(n)
vec.erase(remove(vec.begin(), vec.end(), target), vec.end());
```

---

## 6. O(n³) — Cubic Time

### Definition

An algorithm is **O(n³)** when it uses **three nested loops**, each proportional to `n`. The work grows as the cube of the input.

### Theory

```
n = 10   →        1,000 operations
n = 100  →    1,000,000 operations
n = 500  →  125,000,000 operations   ← Starts hurting
n = 1000 → 1,000,000,000 operations  ← Very slow
```

### Real-World Use Cases

- Naive matrix multiplication (n×n matrices)
- Floyd-Warshall all-pairs shortest path
- Some dynamic programming problems
- Naive 3-sum problem

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

const int INF = INT_MAX / 2; // Avoid overflow when adding

// ─────────────────────────────────────────
// Example 1: Naive Matrix Multiplication
// For each cell (i,j), compute dot product of row i and col j
// ─────────────────────────────────────────

vector<vector<int>> matrixMultiply(
    const vector<vector<int>>& A,
    const vector<vector<int>>& B)
{
    int n = A.size();
    vector<vector<int>> C(n, vector<int>(n, 0));

    for (int i = 0; i < n; i++) {           // Outer:   O(n)
        for (int j = 0; j < n; j++) {       // Middle:  O(n)
            for (int k = 0; k < n; k++) {   // Inner:   O(n)
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    // Total: O(n) × O(n) × O(n) = O(n³)
    return C;
}

// ─────────────────────────────────────────
// Example 2: Floyd-Warshall — All-Pairs Shortest Path
// Find shortest path between EVERY pair of vertices
// dist[i][j] = min distance from vertex i to vertex j
// ─────────────────────────────────────────

void floydWarshall(vector<vector<int>>& dist) {
    int V = dist.size();

    // Try every vertex k as an intermediate point
    for (int k = 0; k < V; k++) {           // Intermediate: O(n)
        for (int i = 0; i < V; i++) {       // Source:       O(n)
            for (int j = 0; j < V; j++) {   // Destination:  O(n)
                // If path i→k→j is shorter than direct i→j, update
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }
    // Total: O(V³) — works for any graph with no negative cycles
}

// ─────────────────────────────────────────
// Example 3: 3-Sum Problem (naive)
// Find all triplets a+b+c = 0
// ─────────────────────────────────────────

vector<tuple<int,int,int>> threeSum(const vector<int>& arr) {
    int n = arr.size();
    vector<tuple<int,int,int>> result;

    for (int i = 0; i < n - 2; i++) {         // O(n)
        for (int j = i + 1; j < n - 1; j++) { // O(n)
            for (int k = j + 1; k < n; k++) { // O(n)
                if (arr[i] + arr[j] + arr[k] == 0)
                    result.push_back({arr[i], arr[j], arr[k]});
            }
        }
    }
    return result; // O(n³) — can be reduced to O(n²) with sorting + two pointer
}

int main() {
    // Matrix multiplication
    vector<vector<int>> A = {{1,2},{3,4}};
    vector<vector<int>> B = {{5,6},{7,8}};
    auto C = matrixMultiply(A, B);
    // C = [[19,22],[43,50]]
    for (auto& row : C) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }

    // Floyd-Warshall
    vector<vector<int>> dist = {
        {0,   3,   INF, 7  },
        {8,   0,   2,   INF},
        {5,   INF, 0,   1  },
        {2,   INF, INF, 0  }
    };
    floydWarshall(dist);
    cout << "Shortest path 0→2: " << dist[0][2] << "\n"; // 5

    // 3-Sum
    vector<int> nums = {-1, 0, 1, 2, -1, -4};
    auto triplets = threeSum(nums);
    for (auto [a, b, c] : triplets)
        cout << a << " " << b << " " << c << "\n";

    return 0;
}
```

### Important Points

- ✅ Acceptable for small n (n < 200 or so)
- ✅ Floyd-Warshall is the textbook all-pairs shortest path solution
- ❌ Avoid on large graphs or matrices — Strassen's algorithm reduces matrix multiply to ~O(n²·⁸)
- ❌ The 3-sum naive solution can be reduced to O(n²) using sorting + two pointers

---

## 7. O(n⁴) — Quartic Time

### Definition

An algorithm is **O(n⁴)** when it requires **four nested loops** over the input. Extremely rare in practice but appears in certain DP problems and exhaustive combinatorial searches.

### Theory

```
n = 10   →          10,000 operations
n = 50   →       6,250,000 operations
n = 100  →     100,000,000 operations
n = 500  → 62,500,000,000 operations  ← Not practical
```

### Real-World Use Cases

- Counting quadruplets with a given sum
- Some naive 2D DP problems
- Exhaustive rectangle search in a 2D grid
- Naive edit distance on 2D structures

### Code Examples

```cpp
#include <iostream>
#include <vector>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Find all quadruplets summing to target
// 4 nested loops — each of n elements
// ─────────────────────────────────────────

vector<tuple<int,int,int,int>> fourSum(const vector<int>& arr, int target) {
    int n = arr.size();
    vector<tuple<int,int,int,int>> result;

    for (int i = 0; i < n - 3; i++) {             // O(n)
        for (int j = i + 1; j < n - 2; j++) {     // O(n)
            for (int k = j + 1; k < n - 1; k++) { // O(n)
                for (int l = k + 1; l < n; l++) {  // O(n)
                    if (arr[i] + arr[j] + arr[k] + arr[l] == target)
                        result.push_back({arr[i], arr[j], arr[k], arr[l]});
                }
            }
        }
    }
    return result; // O(n⁴) — reducible to O(n²) with sorting + hash
}

// ─────────────────────────────────────────
// Example 2: Count rectangles in a binary matrix
// For each pair of rows (i1,i2) and pair of cols (j1,j2)
// check if all 4 corners are 1
// ─────────────────────────────────────────

int countRectangles(const vector<vector<int>>& grid) {
    int n = grid.size();    // rows
    int m = grid[0].size(); // cols
    int count = 0;

    for (int i1 = 0; i1 < n; i1++) {             // O(n)
        for (int i2 = i1 + 1; i2 < n; i2++) {    // O(n)
            for (int j1 = 0; j1 < m; j1++) {      // O(m)
                for (int j2 = j1 + 1; j2 < m; j2++) { // O(m)
                    // All four corners must be 1
                    if (grid[i1][j1] == 1 && grid[i1][j2] == 1 &&
                        grid[i2][j1] == 1 && grid[i2][j2] == 1) {
                        count++;
                    }
                }
            }
        }
    }
    return count; // O(n² × m²) — for square grid: O(n⁴)
}

// ─────────────────────────────────────────
// Example 3: Naive O(n⁴) DP — max sum sub-rectangle
// (Better solutions exist in O(n³))
// For each top-left (r1,c1) and bottom-right (r2,c2) corner
// ─────────────────────────────────────────

int maxSubRectangleNaive(const vector<vector<int>>& grid) {
    int n = grid.size(), m = grid[0].size();
    int maxSum = INT_MIN;

    for (int r1 = 0; r1 < n; r1++) {             // O(n)
        for (int c1 = 0; c1 < m; c1++) {         // O(m)
            for (int r2 = r1; r2 < n; r2++) {    // O(n)
                for (int c2 = c1; c2 < m; c2++) {// O(m)
                    // Compute sum of rectangle (r1,c1) to (r2,c2)
                    int sum = 0;
                    for (int r = r1; r <= r2; r++)
                        for (int c = c1; c <= c2; c++)
                            sum += grid[r][c];    // Inner O(n²) makes this O(n⁶) total!

                    maxSum = max(maxSum, sum);
                }
            }
        }
    }
    return maxSum;
}

int main() {
    vector<int> arr = {1, 0, -1, 0, -2, 2};
    auto quads = fourSum(arr, 0);
    for (auto [a, b, c, d] : quads)
        cout << a << " " << b << " " << c << " " << d << "\n";

    vector<vector<int>> grid = {
        {1, 0, 1},
        {0, 1, 0},
        {1, 0, 1}
    };
    cout << "Rectangles: " << countRectangles(grid) << "\n"; // 2

    return 0;
}
```

### Important Points

- ⚠️ Practical limit: n ≤ 50 or so
- ✅ Sometimes appears in competitive programming with tight constraints
- ❌ Almost always has a better solution — look for it before accepting O(n⁴)
- ❌ The 4-sum problem reduces to O(n²) with sorting + hash map

---

## 8. O(2ⁿ) — Exponential Time

### Definition

An algorithm is **O(2ⁿ)** when each additional element **doubles the total work**. The classic examples are generating all subsets and naive recursive Fibonacci.

### Theory

```
n=1 → 2 subsets       ({}, {1})
n=2 → 4 subsets       ({}, {1}, {2}, {1,2})
n=3 → 8 subsets       (2³)
n=32 → 4,294,967,296  (4 billion — already too slow)
n=64 → 1.8 × 10¹⁹    (decades on modern hardware)
```

Every element either IS or IS NOT in a subset — two choices per element, multiplied across all elements.

### Real-World Use Cases

- Generating all subsets (power set)
- Naive recursive Fibonacci
- Brute-force backtracking (without pruning)
- Satisfiability problems (SAT)
- Subset-sum brute force

### Code Examples

```cpp
#include <iostream>
#include <vector>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Generate all subsets (Power Set)
// Each element: either include or don't → 2 choices
// n elements → 2ⁿ subsets total
// ─────────────────────────────────────────

void generateSubsets(const vector<int>& arr, int index, vector<int>& current) {
    if (index == arr.size()) {
        // Print the current subset
        cout << "{ ";
        for (int x : current) cout << x << " ";
        cout << "}\n";
        return;
    }

    // Choice 1: EXCLUDE arr[index]
    generateSubsets(arr, index + 1, current);

    // Choice 2: INCLUDE arr[index]
    current.push_back(arr[index]);
    generateSubsets(arr, index + 1, current);
    current.pop_back();

    // 2 recursive calls per level × n levels = O(2ⁿ) calls
}

// ─────────────────────────────────────────
// Example 2: Naive Fibonacci (recursive)
// fib(n) calls fib(n-1) AND fib(n-2) — tree of 2ⁿ calls
// ─────────────────────────────────────────

long long fibNaive(int n) {
    if (n <= 1) return n;           // Base case
    return fibNaive(n - 1)          // Left branch
         + fibNaive(n - 2);         // Right branch
    // Each call spawns 2 more → O(2ⁿ)
}

// Call tree for fib(5):
//                fib(5)
//             /         \
//          fib(4)       fib(3)
//         /    \        /    \
//      fib(3) fib(2) fib(2) fib(1)
//      ... (many repeated calls!)

// ─────────────────────────────────────────
// Example 2b: Fibonacci with memoization → O(n)
// Cache results — each subproblem computed only once
// ─────────────────────────────────────────

#include <unordered_map>
unordered_map<int, long long> memo;

long long fibMemo(int n) {
    if (n <= 1) return n;
    if (memo.count(n)) return memo[n]; // Cache hit — O(1)
    return memo[n] = fibMemo(n-1) + fibMemo(n-2); // O(n) unique calls
}

// ─────────────────────────────────────────
// Example 3: Subset Sum — does any subset sum to target?
// Try every subset: 2ⁿ possibilities
// ─────────────────────────────────────────

bool subsetSum(const vector<int>& arr, int index, int remaining) {
    if (remaining == 0) return true;   // Found a valid subset
    if (index == arr.size() || remaining < 0) return false;

    // Either include arr[index] or skip it — 2 branches
    return subsetSum(arr, index + 1, remaining - arr[index])  // Include
        || subsetSum(arr, index + 1, remaining);              // Exclude
    // O(2ⁿ) — with memoization becomes O(n × target)
}

// ─────────────────────────────────────────
// Example 4: Generate all binary strings of length n
// Each position is 0 or 1 → 2ⁿ strings
// ─────────────────────────────────────────

void generateBinaryStrings(int n, string current = "") {
    if (current.size() == n) {
        cout << current << "\n";
        return;
    }
    generateBinaryStrings(n, current + "0"); // Branch 0
    generateBinaryStrings(n, current + "1"); // Branch 1
    // 2 × 2 × 2 × ... (n times) = 2ⁿ strings
}

int main() {
    // Power set of {1, 2, 3} → 8 subsets
    vector<int> arr = {1, 2, 3};
    vector<int> current;
    cout << "All subsets of {1,2,3}:\n";
    generateSubsets(arr, 0, current);

    // Fibonacci — notice how slow naive gets vs memoized
    cout << "\nfib(10) naive:  " << fibNaive(10) << "\n";  // 55
    cout << "fib(10) memo:   " << fibMemo(10)  << "\n";  // 55
    cout << "fib(50) memo:   " << fibMemo(50)  << "\n";  // 12586269025

    // Subset sum
    vector<int> nums = {3, 34, 4, 12, 5, 2};
    cout << "\nSubset sums to 9: " << boolalpha << subsetSum(nums, 0, 9) << "\n"; // true

    // Binary strings of length 3 → 8 strings
    cout << "\nBinary strings of length 3:\n";
    generateBinaryStrings(3);

    return 0;
}
```

### Important Points

- ✅ Acceptable only for very small n (n ≤ 25 approximately)
- ✅ Often fixable with memoization / dynamic programming → reduces to O(n²) or O(n × target)
- ❌ Growing n by 1 doubles the runtime — 30 elements = 1 billion operations
- ❌ Naive recursive Fibonacci is the canonical example of O(2ⁿ) that should never be used in production

### Best Practices

- Whenever you see a recursive function with **two recursive calls**, suspect O(2ⁿ)
- Apply memoization (top-down DP) to turn O(2ⁿ) into polynomial time
- For subset generation, use bitmask iteration for cleaner code: `for (int mask = 0; mask < (1 << n); mask++)`

---

## 9. O(n!) — Factorial Time

### Definition

An algorithm is **O(n!)** when the work grows as the **factorial of the input**: `n! = n × (n-1) × (n-2) × ... × 1`. Every new element multiplies the work by `n`.

### Theory

```
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
10! = 3,628,800        ← Already millions
12! = 479,001,600      ← ~480 million
20! = 2,432,902,008,176,640,000  ← Heat-death territory
```

This is the **worst practical complexity class**. It grows faster than exponential. `n!` overtakes `2ⁿ` quickly — by n=13, `n!` is already larger.

### Real-World Use Cases

- Generating all permutations of n elements
- Brute-force Travelling Salesman Problem (TSP)
- Brute-force scheduling / assignment problems
- Exhaustive backtracking without pruning

### Code Examples

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

// ─────────────────────────────────────────
// Example 1: Generate all permutations
// For n elements: n choices for position 1,
// (n-1) choices for position 2, ... → n! total
// ─────────────────────────────────────────

void generatePermutations(vector<int>& arr, int start) {
    if (start == arr.size()) {
        // One complete permutation
        for (int x : arr) cout << x << " ";
        cout << "\n";
        return;
    }

    for (int i = start; i < arr.size(); i++) {
        swap(arr[start], arr[i]);                  // Choose element i for position start
        generatePermutations(arr, start + 1);       // Recurse on remaining
        swap(arr[start], arr[i]);                  // Backtrack (restore)
    }
    // At each level: n, n-1, n-2, ..., 1 choices → n! total calls
}

// ─────────────────────────────────────────
// Example 2: Brute-force Travelling Salesman Problem
// Try every possible route (permutation of cities)
// Find the shortest total distance
// ─────────────────────────────────────────

int tspBruteForce(const vector<vector<int>>& dist) {
    int n = dist.size();
    vector<int> cities;
    for (int i = 1; i < n; i++) cities.push_back(i); // Cities 1..n-1

    int minCost = INT_MAX;

    // Try every permutation of city order — n! permutations
    do {
        int cost = dist[0][cities[0]]; // Start at city 0

        for (int i = 0; i < cities.size() - 1; i++)
            cost += dist[cities[i]][cities[i + 1]];

        cost += dist[cities.back()][0]; // Return to city 0
        minCost = min(minCost, cost);

    } while (next_permutation(cities.begin(), cities.end())); // O(n!)

    return minCost;
}

// ─────────────────────────────────────────
// Example 3: Brute-force job assignment
// n workers, n jobs, each with a cost
// Find assignment of minimum total cost
// ─────────────────────────────────────────

int jobAssignment(const vector<vector<int>>& cost) {
    int n = cost.size();
    vector<int> jobs;
    for (int i = 0; i < n; i++) jobs.push_back(i);

    int minCost = INT_MAX;

    do {
        int total = 0;
        for (int i = 0; i < n; i++)
            total += cost[i][jobs[i]]; // Worker i does job jobs[i]

        minCost = min(minCost, total);

    } while (next_permutation(jobs.begin(), jobs.end())); // n! permutations

    return minCost;
    // Note: Hungarian Algorithm solves this in O(n³)
}

// ─────────────────────────────────────────
// Example 4: Count all permutations of a string
// n distinct characters → n! arrangements
// ─────────────────────────────────────────

void stringPermutations(string str, int start = 0) {
    if (start == str.size()) {
        cout << str << "\n";
        return;
    }
    for (int i = start; i < str.size(); i++) {
        swap(str[start], str[i]);
        stringPermutations(str, start + 1);
        swap(str[start], str[i]); // Backtrack
    }
    // n! total permutations for n distinct characters
}

int main() {
    // All permutations of {1, 2, 3} — 3! = 6
    cout << "Permutations of {1,2,3}:\n";
    vector<int> arr = {1, 2, 3};
    generatePermutations(arr, 0);

    // TSP — 4 cities (4-1)! = 6 routes to check
    cout << "\nTSP min cost:\n";
    vector<vector<int>> dist = {
        {0, 10, 15, 20},
        {10, 0, 35, 25},
        {15, 35, 0, 30},
        {20, 25, 30, 0}
    };
    cout << tspBruteForce(dist) << "\n"; // 80

    // Job assignment — 3 workers, 3 jobs
    cout << "\nMin job assignment cost:\n";
    vector<vector<int>> jobCost = {
        {9, 2, 7},
        {3, 6, 4},
        {1, 8, 5}
    };
    cout << jobAssignment(jobCost) << "\n"; // 13

    // All permutations of "ABC" — 3! = 6
    cout << "\nPermutations of ABC:\n";
    stringPermutations("ABC");

    return 0;
}
```

### Important Points

- ❌ Only feasible for n ≤ 12 or so
- ❌ n=20 is effectively impossible to brute-force (2.4 × 10¹⁸ operations)
- ✅ TSP has a DP solution (Held-Karp) that reduces it to O(n² × 2ⁿ)
- ✅ Job assignment has the Hungarian Algorithm at O(n³)
- ✅ Use backtracking with pruning to cut branches and avoid n! in practice

### Best Practices

- Always look for DP, greedy, or approximation alternatives before brute-forcing
- Use backtracking with constraint checking to prune the search tree early
- `std::next_permutation` is clean for small n but still O(n!) total iterations

---

## 10. Space Complexity

### Definition

**Space complexity** measures how much **additional memory** an algorithm uses as `n` grows. Same Big O rules apply — we measure the dominant term.

### Common Space Complexities in C++

```cpp
#include <vector>
#include <unordered_map>
using namespace std;

// O(1) space — fixed memory, no extra allocations
int sumArray(const vector<int>& arr) {
    int sum = 0;         // O(1) — one integer
    for (int x : arr) sum += x;
    return sum;
}

// O(n) space — grows linearly with input
vector<int> copyArray(const vector<int>& arr) {
    return vector<int>(arr); // O(n) — copies n elements
}

// O(n) space — hash map
void frequencyCount(const vector<int>& arr) {
    unordered_map<int, int> freq; // O(n) — up to n entries
    for (int x : arr) freq[x]++;
}

// O(log n) space — recursive binary search call stack
int binarySearch(const vector<int>& arr, int target, int l, int r) {
    if (l > r) return -1;
    int mid = l + (r - l) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target) return binarySearch(arr, target, mid+1, r);
    return binarySearch(arr, target, l, mid-1);
    // log n recursive calls on the stack
}

// O(n) space — merge sort auxiliary array
// O(log n) space — quicksort call stack (average)

// O(n²) space — 2D DP table
vector<vector<int>> dp(int n) {
    return vector<vector<int>>(n, vector<int>(n, 0)); // n×n table
}
```

### Time vs Space Tradeoffs

| Algorithm | Time | Space | Tradeoff |
|-----------|------|-------|----------|
| Naive Fibonacci | O(2ⁿ) | O(n) stack | Bad time |
| Memoized Fibonacci | O(n) | O(n) cache | Trade space for time |
| Bottom-up Fibonacci | O(n) | O(1) | Best of both |
| Merge Sort | O(n log n) | O(n) | Extra array for merging |
| Quick Sort | O(n log n) avg | O(log n) | No auxiliary array |
| Hash Map lookup | O(1) avg | O(n) | Space buys speed |

```cpp
// O(n) time, O(n) space — memoized
long long fibMemo(int n, vector<long long>& dp) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    return dp[n] = fibMemo(n-1, dp) + fibMemo(n-2, dp);
}

// O(n) time, O(1) space — bottom-up, space-optimized
long long fibOptimal(int n) {
    if (n <= 1) return n;
    long long a = 0, b = 1;
    for (int i = 2; i <= n; i++) {
        long long c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```

---

## 11. Comparison Tables

### All Complexities Side by Side

| Class | Name | Example | n=10 | n=100 | n=1000 | Practical Limit |
|-------|------|---------|------|-------|--------|-----------------|
| O(1) | Constant | Hash lookup | 1 | 1 | 1 | Any n |
| O(log n) | Logarithmic | Binary search | 3 | 7 | 10 | Any n |
| O(n) | Linear | Linear search | 10 | 100 | 1K | Any n |
| O(n log n) | Linearithmic | Merge sort | 33 | 664 | 10K | Any n |
| O(n²) | Quadratic | Bubble sort | 100 | 10K | 1M | n ≤ 10,000 |
| O(n³) | Cubic | Floyd-Warshall | 1K | 1M | 1B | n ≤ 500 |
| O(n⁴) | Quartic | 4-Sum naive | 10K | 100M | 1T | n ≤ 100 |
| O(2ⁿ) | Exponential | Subsets | 1K | 10³⁰ | 💀 | n ≤ 25 |
| O(n!) | Factorial | Permutations | 3.6M | 10¹⁵⁷ | 💀 | n ≤ 12 |

### C++ STL Container Complexity

| Operation | `vector` | `list` | `map` | `unordered_map` | `set` |
|-----------|----------|--------|-------|-----------------|-------|
| Access by index | O(1) | O(n) | — | — | — |
| Search | O(n) | O(n) | O(log n) | O(1) avg | O(log n) |
| Insert at end | O(1) amort | O(1) | O(log n) | O(1) avg | O(log n) |
| Insert at pos | O(n) | O(1) | O(log n) | O(1) avg | O(log n) |
| Delete | O(n) | O(1) | O(log n) | O(1) avg | O(log n) |
| Min/Max | O(n) | O(n) | O(log n) | O(n) | O(log n) |

### Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ |
| `std::sort` | O(n log n) | O(n log n) | O(n log n) | O(log n) | ❌ |
| `std::stable_sort` | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |

---

## 12. Identifying Complexity — Rules

### How to Read Complexity from Code

```cpp
// Rule 1: Single loop → O(n)
for (int i = 0; i < n; i++) { ... }

// Rule 2: Two nested loops → O(n²)
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++) { ... }

// Rule 3: Loop that halves → O(log n)
while (n > 1) { n /= 2; }

// Rule 4: Loop to n, inner halves → O(n log n)
for (int i = 0; i < n; i++)
    for (int j = 1; j < n; j *= 2) { ... }

// Rule 5: Two recursive calls → suspect O(2ⁿ)
f(n) = f(n-1) + f(n-2);  // Unless memoized

// Rule 6: Permutations/backtracking without pruning → O(n!)
for (int i = start; i < n; i++) {
    swap(a[start], a[i]);
    recurse(start + 1); // Full permutation tree
    swap(a[start], a[i]);
}
```

### Drop the Constants

```
O(3n)      → O(n)
O(n/2)     → O(n)
O(2n + 5)  → O(n)
O(n² + n)  → O(n²)   ← dominant term wins
O(log₃n)   → O(log n) ← base doesn't matter
```

---

## 13. Interview Tips

- **"What is the time complexity of your solution?"** → Always analyze before they ask. State both time AND space.
- **"Can you do better?"** → Know the common optimizations: nested loops → hash map (O(n²)→O(n)), recursion → DP (O(2ⁿ)→O(n²)), linear search → binary search (O(n)→O(log n)).
- **"Why is `std::map` O(log n) but `std::unordered_map` O(1)?"** → `map` is a red-black BST; `unordered_map` is a hash table.
- **"What's the worst case for quicksort?"** → Already-sorted input with no randomization → O(n²). `std::sort` avoids this with introsort.
- **"Two sum: O(n²) vs O(n)?"** → Nested loops vs hash map. Always demonstrate both.
- **"What's the space complexity of recursion?"** → Each call frame uses O(1) space. Depth of recursion determines total: binary search O(log n), naive Fibonacci O(n).

---

## 14. Exercises & Challenges

### 🟢 Beginner

1. **Identify the complexity**: What is the Big O of finding the maximum element in an unsorted `vector<int>`? Write the function and prove your answer.

2. **O(1) swap**: Implement a function that swaps two integers without using a temp variable. Is it O(1)?

3. **Binary search**: Implement binary search iteratively and recursively. Verify they produce identical results on the same input.

4. **Bubble sort step-by-step**: Trace through bubble sort on `{5, 3, 1, 4, 2}` by hand, counting comparisons. Confirm it matches O(n²).

### 🟡 Intermediate

5. **Two Sum upgrade**: Start with an O(n²) nested loop two-sum. Refactor it to O(n) using `unordered_map`. Benchmark both on n = 100,000.

6. **Merge sort**: Implement merge sort. Confirm it sorts correctly. Then modify it to count the number of comparisons made — verify it's close to n log n.

7. **Fibonacci race**: Implement naive O(2ⁿ), memoized O(n), and bottom-up O(n)/O(1) Fibonacci. Measure runtime at n = 35, 40, 45. Observe the difference.

8. **Subset generation**: Generate all subsets of `{1, 2, 3, 4}` using backtracking. Count them — confirm it's 2⁴ = 16.

### 🔴 Advanced

9. **Floyd-Warshall vs Dijkstra**: Implement both. Floyd-Warshall is O(V³); Dijkstra (with min-heap) is O((V + E) log V). For a dense graph (E ≈ V²), which is better? Prove your answer mathematically.

10. **TSP optimization**: Implement brute-force TSP (O(n!)) and Held-Karp DP (O(n² × 2ⁿ)) for the same graph. Compare runtimes at n = 4, 6, 8, 10, 12. At what n does the speedup become dramatic?

11. **3-Sum reduction**: Start with O(n³) 3-sum. Reduce to O(n²) using sorting + two pointers. Reduce further to check whether O(n log n) is achievable (hint: it's not for the full solution, but think about why).

12. **Complexity trap**: The following code looks O(n) — find the bug and state the real complexity:
    ```cpp
    vector<int> result;
    for (int i = 0; i < n; i++) {
        result.insert(result.begin(), i); // What's the real cost?
    }
    ```

---

## 15. Conclusion & Resources

### 🗺️ Learning Roadmap

```
Week 1: Foundations
  ├── Understand what Big O means (drop constants, dominant term)
  ├── O(1), O(log n), O(n)
  ├── Identify complexity from loops
  └── STL container complexities

Week 2: Sorting & Divide and Conquer
  ├── O(n²) sorts: bubble, selection, insertion
  ├── O(n log n) sorts: merge, quick
  ├── When to use which
  └── std::sort, std::stable_sort

Week 3: Exponential & Factorial
  ├── O(2ⁿ): subsets, recursive problems
  ├── O(n!): permutations, TSP brute force
  ├── Memoization → turning O(2ⁿ) into O(n²)
  └── Backtracking with pruning

Week 4: Space Complexity & Tradeoffs
  ├── Stack vs heap memory
  ├── Time-space tradeoffs
  ├── DP table vs rolling array
  └── Practical benchmarking in C++
```

### 💡 Golden Rules

- **One loop** → O(n). **Two nested** → O(n²). **Halving** → O(log n).
- **Two recursive calls** on `n-1` and `n-2` → O(2ⁿ) unless memoized.
- **Permutation backtracking** without pruning → O(n!).
- **Hash map** turns O(n) search into O(1) → use it to bust O(n²) loops.
- **Sort first** — many O(n²) problems become O(n log n) on sorted input.
- **DP** converts O(2ⁿ) or O(n!) into polynomial time by avoiding recomputation.

### 📚 Recommended Resources

| Resource | Link |
|----------|------|
| 📖 cppreference (STL complexities) | https://en.cppreference.com |
| 🎓 Big-O Cheat Sheet | https://www.bigocheatsheet.com |
| 📘 Competitive Programmer's Handbook | https://cses.fi/book/book.pdf |
| 🏆 LeetCode (practice) | https://leetcode.com |
| 🔷 Codeforces (competitive programming) | https://codeforces.com |
| 📊 VisuAlgo (algorithm visualizer) | https://visualgo.net |
| 📖 Introduction to Algorithms (CLRS) | MIT Press |

---

*Built with ❤️ for C++ developers and competitive programmers at every level.*
