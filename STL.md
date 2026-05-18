# 📦 C++ Standard Template Library (STL)
### The Complete Handbook — Beginner to Advanced

> *"The STL is a gift to C++ programmers — master it and your productivity multiplies."*

![C++](https://img.shields.io/badge/C++-17%2F20-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![STL](https://img.shields.io/badge/STL-Standard%20Template%20Library-orange?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-green?style=for-the-badge)

---

## 🤔 What is the STL?

The **Standard Template Library (STL)** is a powerful collection of **generic, reusable components** built into C++. It provides ready-to-use data structures and algorithms so you don't have to implement them from scratch.

The STL has **four main components:**

```
STL
├── 1. Containers     → Data structures (vector, map, set, stack...)
├── 2. Algorithms     → Operations (sort, search, count, transform...)
├── 3. Iterators      → Bridge between containers & algorithms
└── 4. Function Objects (Functors) → Callable objects for algorithms
```

---

## 🚀 Why Use STL?

| Benefit | Description |
|---|---|
| **Ready-made** | No need to implement linked lists, trees, hash maps from scratch |
| **Efficient** | Highly optimized implementations |
| **Generic** | Works with any data type via templates |
| **Standardized** | Same across all compilers and platforms |
| **Safe** | Well-tested, fewer bugs than handwritten code |
| **Expressive** | Algorithms + containers = clean, readable code |

---

## 📚 Table of Contents

1. [STL Overview & Headers](#1-stl-overview--headers)
2. [Iterators](#2-iterators)
3. [Sequence Containers](#3-sequence-containers)
   - [vector](#vector)
   - [array](#array)
   - [deque](#deque)
   - [list](#list)
   - [forward_list](#forward_list)
4. [Container Adaptors](#4-container-adaptors)
   - [stack](#stack)
   - [queue](#queue)
   - [priority_queue](#priority_queue)
5. [Associative Containers](#5-associative-containers)
   - [set & multiset](#set--multiset)
   - [map & multimap](#map--multimap)
6. [Unordered Containers](#6-unordered-containers)
   - [unordered_set](#unordered_set)
   - [unordered_map](#unordered_map)
7. [String & string_view](#7-string--string_view)
8. [pair & tuple](#8-pair--tuple)
9. [Algorithms — Sorting](#9-algorithms--sorting)
10. [Algorithms — Searching](#10-algorithms--searching)
11. [Algorithms — Modification](#11-algorithms--modification)
12. [Algorithms — Numeric](#12-algorithms--numeric)
13. [Algorithms — Min, Max & Partitioning](#13-algorithms--min-max--partitioning)
14. [Lambda Functions with STL](#14-lambda-functions-with-stl)
15. [Function Objects (Functors)](#15-function-objects-functors)
16. [Utility Library](#16-utility-library)
17. [Bitset](#17-bitset)
18. [Span (C++20)](#18-span-c20)
19. [Ranges (C++20)](#19-ranges-c20)
20. [STL in Competitive Programming](#20-stl-in-competitive-programming)
21. [Common STL Patterns & Idioms](#21-common-stl-patterns--idioms)
22. [Performance & Complexity](#22-performance--complexity)
23. [Best Practices](#23-best-practices)
24. [Exercises & Challenges](#24-exercises--challenges)
25. [Conclusion & Resources](#25-conclusion--resources)

---

# 1. STL Overview & Headers

```cpp
// Most commonly used STL headers

#include <vector>           // vector
#include <array>            // array (fixed size)
#include <deque>            // deque
#include <list>             // doubly linked list
#include <forward_list>     // singly linked list

#include <stack>            // stack (adaptor)
#include <queue>            // queue, priority_queue (adaptors)

#include <set>              // set, multiset
#include <map>              // map, multimap
#include <unordered_set>    // unordered_set, unordered_multiset
#include <unordered_map>    // unordered_map, unordered_multimap

#include <string>           // string
#include <string_view>      // string_view (C++17)

#include <algorithm>        // sort, find, count, transform, etc.
#include <numeric>          // accumulate, iota, inner_product, etc.
#include <functional>       // greater, less, function, bind, etc.
#include <iterator>         // iterator utilities

#include <utility>          // pair, make_pair, move, swap
#include <tuple>            // tuple, make_tuple, get
#include <bitset>           // bitset
#include <span>             // span (C++20)
#include <ranges>           // ranges (C++20)

// One-stop include for competitive programming (non-portable)
// #include <bits/stdc++.h>
```

---

# 2. Iterators

Iterators are **pointer-like objects** that point to elements in a container. They are the glue between containers and algorithms.

## Iterator Categories

```
Input Iterator      → read-only, single-pass       (e.g. istream_iterator)
Output Iterator     → write-only, single-pass      (e.g. ostream_iterator)
Forward Iterator    → read/write, single direction  (e.g. forward_list)
Bidirectional       → read/write, both directions   (e.g. list, set, map)
Random Access       → full arithmetic (+, -, [])    (e.g. vector, array, deque)
Contiguous (C++20)  → elements in contiguous memory (e.g. vector, array)
```

## Basic Iterator Usage

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <iterator>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};

    // ── Iterator types ──
    vector<int>::iterator       it;     // read-write
    vector<int>::const_iterator cit;    // read-only
    vector<int>::reverse_iterator rit;  // reverse direction

    // ── begin / end ──
    cout << "Forward: ";
    for (auto it = v.begin(); it != v.end(); ++it) {
        cout << *it << " ";     // dereference to get value
    }
    cout << endl;

    // ── rbegin / rend  (reverse) ──
    cout << "Reverse: ";
    for (auto it = v.rbegin(); it != v.rend(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    // ── cbegin / cend  (const — read-only) ──
    for (auto it = v.cbegin(); it != v.cend(); ++it) {
        // *it = 99;  // ❌ Error: const iterator
        cout << *it << " ";
    }
    cout << endl;

    // ── Iterator arithmetic (random-access only) ──
    auto first = v.begin();
    cout << "First element : " << *first       << endl;  // 10
    cout << "Third element : " << *(first + 2) << endl;  // 30
    cout << "Last element  : " << *(v.end()-1) << endl;  // 50
    cout << "Container size: " << (v.end() - v.begin()) << endl;  // 5

    advance(first, 3);                  // move iterator forward by 3
    cout << "After advance : " << *first << endl;  // 40

    auto it2 = v.begin();
    auto it3 = v.end();
    cout << "Distance      : " << distance(it2, it3) << endl;  // 5

    // ── Insert & move iterators ──
    vector<int> dest;
    copy(v.begin(), v.end(), back_inserter(dest));   // append to dest

    // ── Stream iterators ──
    cout << "Elements: ";
    copy(v.begin(), v.end(), ostream_iterator<int>(cout, " "));
    cout << endl;

    return 0;
}
```

## Iterator Helper Functions

```cpp
#include <iterator>

vector<int> v = {1, 2, 3, 4, 5};
auto it = v.begin();

advance(it, 3);          // moves it 3 positions forward → points to 4
auto it2 = next(it, 1);  // returns iterator 1 step ahead (doesn't modify it)
auto it3 = prev(it, 2);  // returns iterator 2 steps back
int  d   = distance(v.begin(), it);  // number of steps between iterators

cout << *it  << endl;  // 4
cout << *it2 << endl;  // 5
cout << *it3 << endl;  // 2
cout << d    << endl;  // 3
```

---

# 3. Sequence Containers

Sequence containers store elements in **linear order**.

---

## vector

`vector` is a **dynamic array** — the most commonly used STL container. Elements are stored contiguously in memory.

### Definition & Key Properties

- Random access in O(1)
- Insert/delete at **end**: O(1) amortized
- Insert/delete at **middle/front**: O(n)
- Automatically resizes when full (doubles capacity)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // ── Declaration ──
    vector<int>    v1;                    // empty
    vector<int>    v2(5);                 // 5 elements, default-initialized to 0
    vector<int>    v3(5, 42);             // 5 elements, all 42
    vector<int>    v4 = {10, 20, 30, 40, 50};
    vector<int>    v5(v4.begin(), v4.begin() + 3);  // {10, 20, 30}
    vector<string> words = {"hello", "world", "cpp"};

    // ── Access ──
    cout << v4[0]      << endl;   // 10  — no bounds check
    cout << v4.at(1)   << endl;   // 20  — throws out_of_range if invalid
    cout << v4.front() << endl;   // 10  — first element
    cout << v4.back()  << endl;   // 50  — last element
    int* ptr = v4.data();         // raw pointer to underlying array

    // ── Modifiers ──
    v1.push_back(100);            // add at end
    v1.push_back(200);
    v1.emplace_back(300);         // construct in-place at end (faster)

    v1.pop_back();                // remove last element

    v1.insert(v1.begin(), 0);                 // insert 0 at beginning
    v1.insert(v1.begin() + 1, 2, 99);         // insert 2 copies of 99 at index 1
    v1.insert(v1.end(), {400, 500, 600});      // insert range at end

    v1.erase(v1.begin());                      // erase first element
    v1.erase(v1.begin(), v1.begin() + 2);      // erase range [begin, begin+2)

    v1.clear();                   // remove all elements (size → 0)

    // ── Size & Capacity ──
    cout << v4.size()     << endl;  // 5  — number of elements
    cout << v4.capacity() << endl;  // ≥5 — allocated memory
    cout << v4.empty()    << endl;  // false
    cout << v4.max_size() << endl;  // max possible size

    v4.resize(8);          // resize to 8 (new elements = 0)
    v4.resize(3);          // shrink to 3 (extra elements removed)
    v4.reserve(100);       // pre-allocate for 100 elements (avoids reallocation)
    v4.shrink_to_fit();    // release unused capacity

    // ── Iteration ──
    for (int x : v5) cout << x << " ";     // range-based for
    cout << endl;

    for (auto& x : v5) x *= 2;             // modify elements
    for (const auto& x : v5) cout << x << " ";
    cout << endl;

    // ── 2D vector (matrix) ──
    int rows = 3, cols = 4;
    vector<vector<int>> matrix(rows, vector<int>(cols, 0));
    matrix[1][2] = 42;
    for (auto& row : matrix) {
        for (int val : row) cout << val << " ";
        cout << endl;
    }

    // ── Sorting & searching ──
    vector<int> nums = {5, 3, 1, 4, 2};
    sort(nums.begin(), nums.end());           // ascending
    sort(nums.begin(), nums.end(), greater<int>()); // descending

    bool found = binary_search(nums.begin(), nums.end(), 3);
    auto pos   = find(nums.begin(), nums.end(), 3);

    return 0;
}
```

### Common vector Operations Complexity

| Operation | Time Complexity |
|---|---|
| `operator[]`, `at()`, `front()`, `back()` | O(1) |
| `push_back()`, `emplace_back()` | O(1) amortized |
| `pop_back()` | O(1) |
| `insert()` / `erase()` at middle | O(n) |
| `size()`, `empty()`, `capacity()` | O(1) |
| `sort()` (via `<algorithm>`) | O(n log n) |

> 💡 **Best Practice:** Use `reserve()` when you know the final size — avoids repeated reallocation.
> Use `emplace_back()` over `push_back()` for complex objects — avoids extra copy.

---

## array

`array` is a **fixed-size array** wrapper — same performance as C arrays, but with STL interface.

```cpp
#include <array>
using namespace std;

int main() {
    // Declaration — size is PART of the type
    array<int, 5>    a1 = {1, 2, 3, 4, 5};
    array<int, 5>    a2;                    // uninitialized
    array<int, 5>    a3 = {};               // all zeros
    array<string, 3> names = {"Rohit", "Priya", "Aditya"};

    // Access
    cout << a1[0]      << endl;   // 1
    cout << a1.at(4)   << endl;   // 5  (bounds-checked)
    cout << a1.front() << endl;   // 1
    cout << a1.back()  << endl;   // 5

    // Size — known at compile time!
    cout << a1.size() << endl;    // 5
    cout << a1.empty() << endl;   // false

    // Fill all elements
    a2.fill(99);

    // Swap two arrays of same type & size
    a1.swap(a2);

    // Works with all STL algorithms
    sort(a1.begin(), a1.end());
    reverse(a1.begin(), a1.end());

    for (int x : a1) cout << x << " ";
    cout << endl;

    // ── array vs vector ──
    // array: fixed size, stack-allocated, no overhead
    // vector: dynamic size, heap-allocated, more flexible
}
```

---

## deque

`deque` (double-ended queue) supports **fast insert/delete at both front and back**.

```cpp
#include <deque>
using namespace std;

int main() {
    deque<int> dq = {30, 40, 50};

    // Insert at both ends — O(1)
    dq.push_front(20);    // {20, 30, 40, 50}
    dq.push_front(10);    // {10, 20, 30, 40, 50}
    dq.push_back(60);     // {10, 20, 30, 40, 50, 60}

    dq.emplace_front(5);  // {5, 10, 20, 30, 40, 50, 60}
    dq.emplace_back(70);

    // Remove at both ends — O(1)
    dq.pop_front();
    dq.pop_back();

    // Random access — O(1)
    cout << dq[0]      << endl;  // 10
    cout << dq.at(2)   << endl;  // 30
    cout << dq.front() << endl;  // 10
    cout << dq.back()  << endl;  // 60

    // Size
    cout << dq.size()  << endl;

    // Insert in middle — O(n)
    dq.insert(dq.begin() + 2, 99);
    dq.erase(dq.begin() + 2);

    for (int x : dq) cout << x << " ";
    cout << endl;
}
```

### vector vs deque vs list

| Operation | vector | deque | list |
|---|---|---|---|
| Random access | O(1) ✅ | O(1) ✅ | O(n) ❌ |
| Push back | O(1) amortized | O(1) | O(1) |
| Push front | O(n) ❌ | O(1) ✅ | O(1) |
| Insert middle | O(n) | O(n) | O(1) ✅ |
| Memory | Contiguous | Chunked | Non-contiguous |
| Cache friendly | ✅ Best | Good | ❌ Poor |

---

## list

`list` is a **doubly linked list** — O(1) insert/delete anywhere if you have an iterator.

```cpp
#include <list>
using namespace std;

int main() {
    list<int> lst = {30, 10, 50, 20, 40};

    // Insert at both ends
    lst.push_front(5);     // {5, 30, 10, 50, 20, 40}
    lst.push_back(60);     // {5, 30, 10, 50, 20, 40, 60}

    // Insert in middle — O(1) with iterator
    auto it = lst.begin();
    advance(it, 3);            // move to 4th element
    lst.insert(it, 99);        // insert before 4th

    // Remove by value — removes ALL matching elements
    lst.remove(99);

    // Remove by condition
    lst.remove_if([](int x) { return x % 2 == 0; });  // remove evens

    // List-specific algorithms
    lst.sort();                // O(n log n) merge sort
    lst.reverse();             // O(n)
    lst.unique();              // remove consecutive duplicates (sort first!)

    // Merge two sorted lists
    list<int> lst2 = {2, 4, 6};
    lst.sort();
    lst.merge(lst2);           // lst2 becomes empty, lst is merged & sorted

    // Splice — move elements from one list to another — O(1)!
    list<int> src = {100, 200, 300};
    lst.splice(lst.begin(), src);         // move all of src to start of lst
    // src is now empty

    for (int x : lst) cout << x << " ";
    cout << endl;
}
```

---

## forward_list

`forward_list` is a **singly linked list** — less memory than `list`, only forward traversal.

```cpp
#include <forward_list>
using namespace std;

int main() {
    forward_list<int> fl = {10, 20, 30, 40};

    fl.push_front(5);       // {5, 10, 20, 30, 40}
    fl.pop_front();         // {10, 20, 30, 40}

    // No push_back! Use insert_after
    auto it = fl.before_begin();  // special iterator before first element
    fl.insert_after(it, 0);       // {0, 10, 20, 30, 40}

    fl.remove(20);
    fl.sort();
    fl.reverse();
    fl.unique();

    for (int x : fl) cout << x << " ";
    cout << endl;
}
```

---

# 4. Container Adaptors

Container adaptors are **wrappers** over sequence containers that provide a **restricted interface**.

---

## stack

`stack` — LIFO (Last In, First Out). Built on top of `deque` by default.

```cpp
#include <stack>
using namespace std;

int main() {
    stack<int> st;

    // Push elements
    st.push(10);    // [10]
    st.push(20);    // [10, 20]
    st.push(30);    // [10, 20, 30]
    st.emplace(40); // construct in-place

    cout << "Top   : " << st.top()   << endl;  // 40
    cout << "Size  : " << st.size()  << endl;  // 4
    cout << "Empty : " << st.empty() << endl;  // false

    // Pop (removes top — no return value)
    st.pop();                                   // removes 40
    cout << "New top: " << st.top() << endl;   // 30

    // Process all elements
    cout << "Stack (top to bottom): ";
    while (!st.empty()) {
        cout << st.top() << " ";
        st.pop();
    }
    cout << endl;

    // ── Real-world use: Balanced Parentheses Checker ──
    auto isBalanced = [](const string& s) -> bool {
        stack<char> st;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[') {
                st.push(c);
            } else if (c == ')' || c == '}' || c == ']') {
                if (st.empty()) return false;
                char top = st.top(); st.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) return false;
            }
        }
        return st.empty();
    };

    cout << boolalpha;
    cout << isBalanced("{[()]}") << endl;    // true
    cout << isBalanced("{[(])}") << endl;    // false
    cout << isBalanced("((()))") << endl;    // true

    // Change underlying container
    stack<int, vector<int>> vecStack;     // uses vector instead of deque
    stack<int, list<int>>   listStack;    // uses list
}
```

---

## queue

`queue` — FIFO (First In, First Out). Built on top of `deque` by default.

```cpp
#include <queue>
using namespace std;

int main() {
    queue<string> q;

    // Enqueue
    q.push("Task 1");
    q.push("Task 2");
    q.push("Task 3");
    q.emplace("Task 4");

    cout << "Front : " << q.front() << endl;  // Task 1
    cout << "Back  : " << q.back()  << endl;  // Task 4
    cout << "Size  : " << q.size()  << endl;  // 4

    // Dequeue (removes front)
    q.pop();
    cout << "New front: " << q.front() << endl;  // Task 2

    // Process all
    cout << "Processing: ";
    while (!q.empty()) {
        cout << q.front() << " | ";
        q.pop();
    }
    cout << endl;

    // ── Real-world use: BFS (Breadth-First Search) ──
    // Graph represented as adjacency list
    auto bfs = [](int start, int n, vector<vector<int>>& adj) {
        vector<bool> visited(n, false);
        queue<int>   q;

        visited[start] = true;
        q.push(start);

        cout << "BFS order: ";
        while (!q.empty()) {
            int node = q.front(); q.pop();
            cout << node << " ";
            for (int neighbor : adj[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.push(neighbor);
                }
            }
        }
        cout << endl;
    };

    int n = 6;
    vector<vector<int>> adj(n);
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0, 5};
    adj[3] = {1};
    adj[4] = {1};
    adj[5] = {2};

    bfs(0, n, adj);  // BFS order: 0 1 2 3 4 5
}
```

---

## priority_queue

`priority_queue` — elements are served in **priority order** (max element first by default). Internally uses a **max-heap**.

```cpp
#include <queue>
#include <vector>
#include <functional>
using namespace std;

int main() {
    // ── Max-heap (default) ──
    priority_queue<int> maxPQ;
    maxPQ.push(30);
    maxPQ.push(10);
    maxPQ.push(50);
    maxPQ.push(20);
    maxPQ.push(40);

    cout << "Max-heap order: ";
    while (!maxPQ.empty()) {
        cout << maxPQ.top() << " ";  // 50 40 30 20 10
        maxPQ.pop();
    }
    cout << endl;

    // ── Min-heap ──
    priority_queue<int, vector<int>, greater<int>> minPQ;
    minPQ.push(30); minPQ.push(10); minPQ.push(50);
    minPQ.push(20); minPQ.push(40);

    cout << "Min-heap order: ";
    while (!minPQ.empty()) {
        cout << minPQ.top() << " ";  // 10 20 30 40 50
        minPQ.pop();
    }
    cout << endl;

    // ── Custom comparator ──
    struct Task {
        string name;
        int    priority;
    };

    auto cmp = [](const Task& a, const Task& b) {
        return a.priority < b.priority;  // higher priority value = higher priority
    };

    priority_queue<Task, vector<Task>, decltype(cmp)> taskQueue(cmp);
    taskQueue.push({"Low priority task",    1});
    taskQueue.push({"High priority task",   5});
    taskQueue.push({"Medium priority task", 3});
    taskQueue.push({"Critical task",        10});

    cout << "Task order:\n";
    while (!taskQueue.empty()) {
        auto t = taskQueue.top(); taskQueue.pop();
        cout << "  [" << t.priority << "] " << t.name << "\n";
    }

    // ── Real-world use: Dijkstra's Algorithm ──
    // {distance, node} — min-heap by distance
    priority_queue<
        pair<int,int>,
        vector<pair<int,int>>,
        greater<pair<int,int>>
    > dijkstraPQ;

    dijkstraPQ.push({0, 0});  // {distance=0, node=0}

    // ── Initialize from vector ──
    vector<int> nums = {5, 1, 4, 2, 3};
    priority_queue<int> pqFromVec(nums.begin(), nums.end());
    cout << "Top of heap from vector: " << pqFromVec.top() << endl;  // 5
}
```

---

## 📝 Exercises — Section 3 & 4

1. Use a `stack` to **reverse a string**.
2. Implement a **task scheduler** using `priority_queue` — tasks with deadlines.
3. Use `deque` to implement a **sliding window maximum** problem.
4. Implement a **queue using two stacks**.

---

# 5. Associative Containers

Associative containers store elements in **sorted order** and provide fast lookup by key (O(log n)). Internally use **Red-Black Trees**.

---

## set & multiset

`set` — sorted unique elements. `multiset` — sorted, allows duplicates.

```cpp
#include <set>
using namespace std;

int main() {
    // ── set — unique sorted elements ──
    set<int> s = {5, 3, 1, 4, 2, 3, 5};  // duplicates ignored
    // Internal order: {1, 2, 3, 4, 5}

    cout << "Set: ";
    for (int x : s) cout << x << " ";  // 1 2 3 4 5
    cout << endl;

    // Insert — O(log n)
    s.insert(6);
    s.insert(3);   // duplicate — ignored, returns {iterator, false}

    auto [it, success] = s.insert(10);
    cout << "Inserted 10: " << boolalpha << success << endl;  // true

    // Erase — O(log n)
    s.erase(3);                      // erase by value
    s.erase(s.begin());              // erase by iterator (erases 1)
    s.erase(s.begin(), s.find(4));   // erase range

    // Search — O(log n)
    auto it2 = s.find(4);
    if (it2 != s.end()) cout << "Found: " << *it2 << endl;

    cout << "Count of 5: " << s.count(5) << endl;  // 1 or 0

    // contains (C++20)
    // if (s.contains(5)) { ... }

    // lower_bound / upper_bound
    auto lb = s.lower_bound(4);  // first element >= 4
    auto ub = s.upper_bound(4);  // first element > 4

    cout << "lower_bound(4): " << *lb << endl;
    cout << "upper_bound(4): " << *ub << endl;

    // Size
    cout << "Size : " << s.size()  << endl;
    cout << "Empty: " << s.empty() << endl;

    // ── Descending order ──
    set<int, greater<int>> descSet = {3, 1, 4, 1, 5, 9};
    for (int x : descSet) cout << x << " ";  // 9 5 4 3 1
    cout << endl;

    // ── Custom comparator for set ──
    auto cmp = [](const string& a, const string& b) {
        return a.length() < b.length();  // sort by string length
    };
    set<string, decltype(cmp)> byLength(cmp);
    byLength.insert("banana");
    byLength.insert("fig");
    byLength.insert("apple");
    byLength.insert("kiwi");
    for (const auto& s : byLength) cout << s << " ";  // fig kiwi apple banana
    cout << endl;

    // ── multiset — allows duplicates ──
    multiset<int> ms = {1, 2, 2, 3, 3, 3, 4};
    cout << "\nmultiset: ";
    for (int x : ms) cout << x << " ";  // 1 2 2 3 3 3 4
    cout << endl;

    cout << "Count of 3: " << ms.count(3) << endl;  // 3

    ms.erase(3);                     // removes ALL 3s
    ms.erase(ms.find(2));            // removes ONE 2

    // equal_range — get range of elements equal to key
    auto range = ms.equal_range(2);
    for (auto it = range.first; it != range.second; ++it) {
        cout << *it << " ";
    }
    cout << endl;
}
```

---

## map & multimap

`map` — key-value pairs, sorted by key, unique keys. `multimap` — allows duplicate keys.

```cpp
#include <map>
#include <string>
using namespace std;

int main() {
    // ── map ──
    map<string, int> scores;

    // Insert — three ways
    scores["Rohit"]  = 95;                               // [] operator (creates if not found)
    scores["Priya"]  = 88;
    scores.insert({"Aditya", 72});                       // insert pair
    scores.insert(make_pair("Anjali", 91));
    scores.emplace("Vikram", 85);                        // construct in-place

    // Access
    cout << "Rohit's score: " << scores["Rohit"]  << endl;  // 95
    cout << "Priya's score: " << scores.at("Priya") << endl; // 88 (throws if not found)

    // ❗ WARNING: [] creates default entry if key not found!
    cout << scores["NewKey"] << endl;  // creates "NewKey" with value 0

    // Safe check before access
    if (scores.count("Rohit") > 0) {
        cout << "Found: " << scores["Rohit"] << endl;
    }

    // Find
    auto it = scores.find("Priya");
    if (it != scores.end()) {
        cout << "Key: " << it->first
             << " | Value: " << it->second << endl;
    }

    // Erase
    scores.erase("NewKey");          // erase by key
    scores.erase(scores.begin());    // erase by iterator

    // Iterate — always sorted by key
    cout << "\nAll scores (sorted by name):\n";
    for (const auto& [name, score] : scores) {  // structured bindings (C++17)
        cout << "  " << name << " : " << score << "\n";
    }

    // lower_bound / upper_bound
    auto lb = scores.lower_bound("P");  // first key >= "P"
    auto ub = scores.upper_bound("R");  // first key > "R"

    // Size
    cout << "Size: " << scores.size() << endl;

    // ── Nested map (map of maps) ──
    map<string, map<string, int>> table;
    table["Rohit"]["Math"]    = 95;
    table["Rohit"]["Science"] = 88;
    table["Priya"]["Math"]    = 99;

    for (const auto& [student, subjects] : table) {
        cout << student << ":\n";
        for (const auto& [subject, marks] : subjects) {
            cout << "  " << subject << ": " << marks << "\n";
        }
    }

    // ── map with custom comparator ──
    map<string, int, greater<string>> descMap;
    descMap["Zebra"] = 1;
    descMap["Apple"] = 2;
    descMap["Mango"] = 3;
    for (const auto& [k, v] : descMap) {
        cout << k << " ";  // Zebra Mango Apple
    }
    cout << endl;

    // ── multimap — duplicate keys ──
    multimap<string, string> phonebook;
    phonebook.insert({"Rohit", "9876543210"});
    phonebook.insert({"Rohit", "8765432109"});  // same name, different number
    phonebook.insert({"Priya", "7654321098"});

    cout << "\nPhone book:\n";
    for (const auto& [name, number] : phonebook) {
        cout << "  " << name << " : " << number << "\n";
    }

    // Get all entries for a key
    auto range = phonebook.equal_range("Rohit");
    cout << "Rohit's numbers:\n";
    for (auto it = range.first; it != range.second; ++it) {
        cout << "  " << it->second << "\n";
    }
}
```

### set / map Complexity

| Operation | set / map | multiset / multimap |
|---|---|---|
| `insert()` | O(log n) | O(log n) |
| `find()` | O(log n) | O(log n) |
| `erase()` | O(log n) | O(log n) |
| `count()` | O(log n + k) | O(log n + k) |
| Iteration | O(n) | O(n) |
| Memory | O(n) | O(n) |

---

# 6. Unordered Containers

Unordered containers use **hash tables** — average O(1) lookup, but no ordering guarantee.

---

## unordered_set

```cpp
#include <unordered_set>
using namespace std;

int main() {
    unordered_set<int> us = {5, 3, 8, 1, 9, 3, 5};  // duplicates removed

    // No guaranteed order when iterating!
    cout << "unordered_set: ";
    for (int x : us) cout << x << " ";  // order varies
    cout << endl;

    // Operations — average O(1)
    us.insert(42);
    us.erase(3);

    cout << "Contains 5: " << (us.count(5) > 0) << endl;    // true
    // cout << "Contains 5: " << us.contains(5) << endl;    // C++20

    auto it = us.find(8);
    if (it != us.end()) cout << "Found: " << *it << endl;

    // Load factor & bucket info
    cout << "Load factor : " << us.load_factor()     << endl;
    cout << "Bucket count: " << us.bucket_count()    << endl;

    // Reserve for expected size (avoids rehashing)
    us.reserve(100);

    // ── Real-world use: Remove duplicates ──
    vector<int> nums = {1, 2, 3, 2, 1, 4, 3, 5};
    unordered_set<int> seen;
    vector<int> unique_nums;

    for (int n : nums) {
        if (seen.insert(n).second) {  // insert returns {iterator, bool}
            unique_nums.push_back(n);
        }
    }

    cout << "Unique (preserving order): ";
    for (int x : unique_nums) cout << x << " ";  // 1 2 3 4 5
    cout << endl;
}
```

---

## unordered_map

```cpp
#include <unordered_map>
#include <string>
using namespace std;

int main() {
    unordered_map<string, int> freq;

    // Word frequency counter
    vector<string> words = {"apple","banana","apple","cherry","banana","apple"};
    for (const string& w : words) {
        freq[w]++;   // default-constructs to 0, then increments
    }

    for (const auto& [word, count] : freq) {
        cout << word << ": " << count << "\n";
    }

    // Operations — average O(1)
    cout << "\nbanana count: " << freq["banana"] << endl;

    freq.erase("cherry");

    // Find (safe access — doesn't create entry)
    auto it = freq.find("apple");
    if (it != freq.end()) {
        cout << "apple: " << it->second << endl;
    }

    // ── Custom hash for user-defined types ──
    struct Point {
        int x, y;
        bool operator==(const Point& o) const {
            return x == o.x && y == o.y;
        }
    };

    struct PointHash {
        size_t operator()(const Point& p) const {
            return hash<int>()(p.x) ^ (hash<int>()(p.y) << 1);
        }
    };

    unordered_map<Point, string, PointHash> pointNames;
    pointNames[{0, 0}] = "Origin";
    pointNames[{1, 0}] = "East";
    pointNames[{0, 1}] = "North";

    cout << "Point (0,0): " << pointNames[{0, 0}] << endl;
}
```

### set vs unordered_set vs map vs unordered_map

| Feature | set / map | unordered_set / unordered_map |
|---|---|---|
| Ordering | Sorted ✅ | None ❌ |
| Lookup | O(log n) | O(1) average |
| Worst case | O(log n) | O(n) hash collision |
| Memory | Less | More (hash table) |
| Custom keys | Comparator | Hash function needed |
| Use when | Need order | Need speed |

---

# 7. String & string_view

## string

```cpp
#include <string>
#include <algorithm>
using namespace std;

int main() {
    // ── Declaration ──
    string s1 = "Hello";
    string s2("World");
    string s3(5, 'x');          // "xxxxx"
    string s4 = s1 + " " + s2; // "Hello World"

    // ── Access ──
    cout << s1[0]       << endl;  // 'H'
    cout << s1.at(1)    << endl;  // 'e'
    cout << s1.front()  << endl;  // 'H'
    cout << s1.back()   << endl;  // 'o'
    const char* cstr = s1.c_str(); // C-string pointer

    // ── Modification ──
    s1.push_back('!');           // "Hello!"
    s1.pop_back();               // "Hello"
    s1.append(" C++");           // "Hello C++"
    s1 += " World";              // "Hello C++ World"
    s1.insert(5, ",");           // "Hello, C++ World"
    s1.erase(5, 1);              // remove ',' at index 5
    s1.replace(6, 3, "STL");     // replace 3 chars at index 6 with "STL"
    s1.clear();                  // empty string

    // ── Info ──
    string test = "Hello World";
    cout << test.size()   << endl;  // 11
    cout << test.length() << endl;  // 11 (same as size)
    cout << test.empty()  << endl;  // false
    cout << test.capacity() << endl;

    // ── Search ──
    cout << test.find("World")     << endl;  // 6
    cout << test.find('o')         << endl;  // 4 (first 'o')
    cout << test.rfind('o')        << endl;  // 7 (last 'o')
    cout << test.find("xyz")       << endl;  // string::npos (not found)

    if (test.find("World") != string::npos) {
        cout << "Found!\n";
    }

    // ── Substring ──
    cout << test.substr(6)       << endl;   // "World"
    cout << test.substr(6, 3)    << endl;   // "Wor" (start, length)

    // ── Comparison ──
    string a = "apple", b = "banana";
    cout << (a == b)  << endl;  // false
    cout << (a < b)   << endl;  // true (lexicographic)
    cout << a.compare(b) << endl;  // negative (a < b)

    // ── Transform ──
    string upper = test;
    transform(upper.begin(), upper.end(), upper.begin(), ::toupper);
    cout << upper << endl;  // "HELLO WORLD"

    string lower = test;
    transform(lower.begin(), lower.end(), lower.begin(), ::tolower);
    cout << lower << endl;  // "hello world"

    // ── Split (no built-in — use stringstream) ──
    #include <sstream>
    string csv = "Rohit,25,Nagpur,Developer";
    stringstream ss(csv);
    string token;
    vector<string> tokens;
    while (getline(ss, token, ',')) {
        tokens.push_back(token);
    }
    for (const auto& t : tokens) cout << t << "\n";

    // ── Number conversions ──
    int    n  = stoi("42");          // string → int
    long   l  = stol("123456789");   // string → long
    double d  = stod("3.14");        // string → double
    string s  = to_string(42);       // int → string
    string ds = to_string(3.14);     // double → string
}
```

## string_view (C++17)

A lightweight, **non-owning view** of a string — avoids copying.

```cpp
#include <string_view>
using namespace std;

// ✅ Use string_view for read-only string parameters — no copy!
void printInfo(string_view sv) {
    cout << "Length: " << sv.length() << "\n";
    cout << "Data  : " << sv          << "\n";
    cout << "Sub   : " << sv.substr(0, 5) << "\n";
}

int main() {
    string      s = "Hello, World!";
    const char* c = "Hello, C-String!";
    string_view literal = "Hello, Literal!";

    printInfo(s);        // works with string
    printInfo(c);        // works with const char*
    printInfo(literal);  // works with string_view
    printInfo("Hello");  // works with string literal

    // string_view operations
    string_view sv = "Hello World";
    cout << sv.size()     << endl;  // 11
    cout << sv.front()    << endl;  // 'H'
    cout << sv.back()     << endl;  // 'd'
    cout << sv.substr(6)  << endl;  // "World"

    sv.remove_prefix(6);    // now sv = "World"
    sv.remove_suffix(1);    // now sv = "Worl"

    // ⚠️ string_view doesn't own memory — don't outlive the original!
    // string_view bad = string("temp"); // DANGER — dangling view!
}
```

---

# 8. pair & tuple

## pair

```cpp
#include <utility>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // ── pair ──
    pair<int, string> p1 = {1, "Rohit"};
    pair<int, string> p2 = make_pair(2, "Priya");
    auto p3 = make_pair(3.14, true);    // type deduced

    cout << p1.first  << " : " << p1.second  << endl;  // 1 : Rohit
    cout << p2.first  << " : " << p2.second  << endl;  // 2 : Priya

    // Structured bindings (C++17)
    auto [id, name] = p1;
    cout << id << " " << name << endl;

    // Comparison — compares first, then second
    pair<int, int> x = {1, 5};
    pair<int, int> y = {1, 3};
    cout << (x > y) << endl;   // true (same first, 5 > 3)

    // ── vector of pairs ──
    vector<pair<string, int>> students = {
        {"Rohit",  95},
        {"Priya",  88},
        {"Aditya", 72},
        {"Anjali", 91}
    };

    // Sort by score (descending)
    sort(students.begin(), students.end(),
         [](const auto& a, const auto& b) { return a.second > b.second; });

    for (const auto& [name, score] : students) {
        cout << name << ": " << score << "\n";
    }

    // Sort by name (ascending — default pair sort)
    sort(students.begin(), students.end());
}
```

## tuple

```cpp
#include <tuple>
using namespace std;

int main() {
    // ── tuple — generalized pair (any number of types) ──
    tuple<int, string, double, bool> t1 = {1, "Rohit", 9.2, true};
    auto t2 = make_tuple(2, "Priya", 8.8, false);

    // Access by index
    cout << get<0>(t1) << endl;   // 1
    cout << get<1>(t1) << endl;   // "Rohit"
    cout << get<2>(t1) << endl;   // 9.2

    // Structured bindings (C++17)
    auto [id, name, cgpa, active] = t1;
    cout << id << " " << name << " " << cgpa << endl;

    // tie — unpack into existing variables
    int    myId;
    string myName;
    double myCgpa;
    bool   myActive;
    tie(myId, myName, myCgpa, myActive) = t1;
    cout << myId << " " << myName << endl;

    // tie with ignore
    tie(myId, ignore, myCgpa, ignore) = t1;

    // tuple size & type
    cout << "Size: " << tuple_size<decltype(t1)>::value << endl;  // 4

    // Concatenate tuples
    auto t3 = tuple_cat(t1, t2);
    cout << "Combined size: " << tuple_size<decltype(t3)>::value << endl;  // 8

    // ── Returning multiple values from function ──
    auto getStudentInfo = [](int id) -> tuple<string, int, double> {
        return {"Rohit", id, 9.2};
    };

    auto [sName, sId, sCgpa] = getStudentInfo(101);
    cout << sName << " " << sId << " " << sCgpa << endl;
}
```

---

# 9. Algorithms — Sorting

All STL algorithms live in `<algorithm>` and work on iterator ranges `[begin, end)`.

```cpp
#include <algorithm>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<int> v = {5, 3, 8, 1, 9, 2, 7, 4, 6};

    // ── sort — O(n log n) ──
    sort(v.begin(), v.end());                          // ascending
    sort(v.begin(), v.end(), greater<int>());           // descending
    sort(v.begin(), v.begin() + 4);                    // sort only first 4

    // Custom comparator
    vector<string> words = {"banana", "fig", "apple", "date", "kiwi"};
    sort(words.begin(), words.end(),
         [](const string& a, const string& b) {
             return a.length() < b.length();   // sort by length
         });
    for (const auto& w : words) cout << w << " ";
    cout << endl;  // fig kiwi date apple banana

    // ── stable_sort — preserves relative order of equal elements ──
    vector<pair<int, string>> data = {{2,"b"}, {1,"a"}, {2,"a"}, {1,"b"}};
    stable_sort(data.begin(), data.end(),
                [](const auto& x, const auto& y) { return x.first < y.first; });
    // {1,"a"} comes before {1,"b"} — order preserved

    // ── partial_sort — sort only first k elements ──
    vector<int> nums = {5, 3, 8, 1, 9, 2};
    partial_sort(nums.begin(), nums.begin() + 3, nums.end());
    // first 3 are sorted: {1, 2, 3, 8, 9, 5}  (rest unspecified)

    // ── nth_element — k-th smallest in O(n) ──
    vector<int> n2 = {5, 3, 8, 1, 9, 2, 7};
    nth_element(n2.begin(), n2.begin() + 3, n2.end());
    // n2[3] is the 4th smallest element (0-indexed)
    cout << "4th smallest: " << n2[3] << endl;

    // ── is_sorted ──
    vector<int> sorted_v = {1, 2, 3, 4, 5};
    vector<int> unsorted_v = {1, 3, 2, 4, 5};
    cout << is_sorted(sorted_v.begin(), sorted_v.end())   << "\n";  // true
    cout << is_sorted(unsorted_v.begin(), unsorted_v.end()) << "\n"; // false

    // ── is_sorted_until — find first out-of-order element ──
    auto it = is_sorted_until(unsorted_v.begin(), unsorted_v.end());
    cout << "First unsorted: " << *it << endl;  // 2

    // ── Heap operations (used for priority queue) ──
    vector<int> h = {3, 1, 4, 1, 5, 9};
    make_heap(h.begin(), h.end());                  // create max-heap
    cout << "Heap max: " << h.front() << endl;      // 9

    h.push_back(7);
    push_heap(h.begin(), h.end());                  // add element to heap
    cout << "After push: " << h.front() << endl;    // still 9

    pop_heap(h.begin(), h.end());                   // move max to back
    cout << "Popped: " << h.back() << endl;         // 9
    h.pop_back();

    sort_heap(h.begin(), h.end());                  // sort (destroys heap)
}
```

---

# 10. Algorithms — Searching

```cpp
#include <algorithm>
#include <vector>
using namespace std;

int main() {
    // ── linear find — O(n) ──
    vector<int> v = {10, 20, 30, 40, 50};

    auto it = find(v.begin(), v.end(), 30);
    if (it != v.end()) {
        cout << "Found 30 at index: " << distance(v.begin(), it) << endl;  // 2
    }

    // ── find_if — find first matching condition — O(n) ──
    auto it2 = find_if(v.begin(), v.end(), [](int x) { return x > 25; });
    cout << "First > 25: " << *it2 << endl;  // 30

    // ── find_if_not ──
    auto it3 = find_if_not(v.begin(), v.end(), [](int x) { return x < 25; });
    cout << "First >= 25: " << *it3 << endl;  // 30

    // ── binary_search — O(log n) — REQUIRES SORTED INPUT ──
    vector<int> sorted = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    cout << binary_search(sorted.begin(), sorted.end(), 5) << endl;  // true
    cout << binary_search(sorted.begin(), sorted.end(), 10) << endl; // false

    // ── lower_bound — first element >= value — O(log n) ──
    auto lb = lower_bound(sorted.begin(), sorted.end(), 5);
    cout << "lower_bound(5): " << *lb << endl;         // 5
    cout << "Index: " << distance(sorted.begin(), lb) << endl;  // 4

    // ── upper_bound — first element > value — O(log n) ──
    auto ub = upper_bound(sorted.begin(), sorted.end(), 5);
    cout << "upper_bound(5): " << *ub << endl;         // 6

    // ── equal_range — both bounds ──
    vector<int> dups = {1, 2, 2, 2, 3, 4};
    auto [first, last] = equal_range(dups.begin(), dups.end(), 2);
    cout << "Range of 2s: [" << distance(dups.begin(), first)
         << ", " << distance(dups.begin(), last) << ")\n";  // [1, 4)
    cout << "Count of 2s: " << distance(first, last) << endl;  // 3

    // ── count — O(n) ──
    vector<int> nums = {1, 2, 2, 3, 2, 4};
    cout << "Count of 2: " << count(nums.begin(), nums.end(), 2) << endl;  // 3

    // ── count_if ──
    cout << "Evens: " << count_if(nums.begin(), nums.end(),
                                   [](int x) { return x % 2 == 0; }) << endl;  // 4

    // ── search — find subsequence — O(n*m) ──
    vector<int> haystack = {1, 2, 3, 4, 5, 3, 4};
    vector<int> needle   = {3, 4};
    auto pos = search(haystack.begin(), haystack.end(),
                      needle.begin(),   needle.end());
    cout << "First occurrence at: " << distance(haystack.begin(), pos) << endl; // 2

    // ── find_end — find LAST occurrence of subsequence ──
    auto pos2 = find_end(haystack.begin(), haystack.end(),
                         needle.begin(),   needle.end());
    cout << "Last occurrence at: " << distance(haystack.begin(), pos2) << endl; // 5

    // ── all_of, any_of, none_of ──
    vector<int> positives = {1, 2, 3, 4, 5};
    vector<int> mixed     = {-1, 2, 3};

    cout << all_of(positives.begin(), positives.end(), [](int x) { return x > 0; })
         << endl;  // true
    cout << any_of(mixed.begin(), mixed.end(), [](int x) { return x < 0; })
         << endl;  // true
    cout << none_of(positives.begin(), positives.end(), [](int x) { return x < 0; })
         << endl;  // true
}
```

---

# 11. Algorithms — Modification

```cpp
#include <algorithm>
#include <vector>
#include <numeric>
using namespace std;

int main() {
    // ── copy ──
    vector<int> src = {1, 2, 3, 4, 5};
    vector<int> dst(5);
    copy(src.begin(), src.end(), dst.begin());

    // copy_if
    vector<int> evens;
    copy_if(src.begin(), src.end(), back_inserter(evens),
            [](int x) { return x % 2 == 0; });
    // evens = {2, 4}

    // ── transform — apply function to each element ──
    vector<int> doubled(src.size());
    transform(src.begin(), src.end(), doubled.begin(),
              [](int x) { return x * 2; });
    // doubled = {2, 4, 6, 8, 10}

    // Binary transform (two input ranges)
    vector<int> a = {1, 2, 3};
    vector<int> b = {4, 5, 6};
    vector<int> sums(3);
    transform(a.begin(), a.end(), b.begin(), sums.begin(),
              [](int x, int y) { return x + y; });
    // sums = {5, 7, 9}

    // ── fill & fill_n ──
    vector<int> filled(5);
    fill(filled.begin(), filled.end(), 42);           // all 42
    fill_n(filled.begin(), 3, 99);                    // first 3 → 99

    // ── generate & generate_n ──
    vector<int> gen(5);
    int counter = 0;
    generate(gen.begin(), gen.end(), [&]() { return counter++ * counter; });

    // ── iota — fill with incrementing values ──
    vector<int> seq(6);
    iota(seq.begin(), seq.end(), 0);      // {0, 1, 2, 3, 4, 5}
    iota(seq.begin(), seq.end(), 10);     // {10, 11, 12, 13, 14, 15}

    // ── replace ──
    vector<int> v = {1, 2, 3, 2, 4, 2};
    replace(v.begin(), v.end(), 2, 99);       // replace all 2 with 99
    // v = {1, 99, 3, 99, 4, 99}

    // replace_if
    replace_if(v.begin(), v.end(), [](int x) { return x > 90; }, 0);
    // replaces all elements > 90 with 0

    // ── remove (doesn't resize!) ──
    vector<int> r = {1, 2, 3, 2, 4, 2, 5};
    auto newEnd = remove(r.begin(), r.end(), 2);    // "remove" 2s
    r.erase(newEnd, r.end());                        // actual erase
    // r = {1, 3, 4, 5}

    // Idiom: erase-remove
    vector<int> er = {1, 2, 3, 2, 4, 2, 5};
    er.erase(remove(er.begin(), er.end(), 2), er.end());  // one-liner!

    // remove_if with erase
    vector<int> odds = {1, 2, 3, 4, 5, 6};
    odds.erase(remove_if(odds.begin(), odds.end(),
                         [](int x) { return x % 2 == 0; }),
               odds.end());
    // odds = {1, 3, 5}

    // ── unique — remove consecutive duplicates ──
    vector<int> u = {1, 1, 2, 3, 3, 3, 4, 4, 5};
    u.erase(unique(u.begin(), u.end()), u.end());
    // u = {1, 2, 3, 4, 5}

    // ── reverse ──
    vector<int> rev = {1, 2, 3, 4, 5};
    reverse(rev.begin(), rev.end());
    // rev = {5, 4, 3, 2, 1}

    // ── rotate — bring element at middle to front ──
    vector<int> rot = {1, 2, 3, 4, 5};
    rotate(rot.begin(), rot.begin() + 2, rot.end());
    // rot = {3, 4, 5, 1, 2}

    // ── shuffle ──
    #include <random>
    vector<int> cards = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    mt19937 rng(42);   // seeded random engine
    shuffle(cards.begin(), cards.end(), rng);

    // ── for_each ──
    for_each(src.begin(), src.end(), [](int& x) { x *= x; });  // square each

    // ── swap & iter_swap ──
    int x = 10, y = 20;
    swap(x, y);   // x=20, y=10

    vector<int> sv = {1, 2, 3, 4};
    iter_swap(sv.begin(), sv.end() - 1);  // swap first and last
    // sv = {4, 2, 3, 1}
}
```

---

# 12. Algorithms — Numeric

```cpp
#include <numeric>
#include <vector>
#include <functional>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    // ── accumulate — sum / product / custom reduction ──
    int sum = accumulate(v.begin(), v.end(), 0);         // 15
    int product = accumulate(v.begin(), v.end(), 1, multiplies<int>()); // 120

    string concat = accumulate(
        vector<string>{"Hello", " ", "World"}.begin(),
        vector<string>{"Hello", " ", "World"}.end(),
        string("")
    );  // "Hello World"

    // ── reduce (C++17) — like accumulate but potentially parallel ──
    int total = reduce(v.begin(), v.end(), 0);           // 15
    int prod  = reduce(v.begin(), v.end(), 1, multiplies<int>());  // 120

    // ── inner_product — dot product ──
    vector<int> a = {1, 2, 3};
    vector<int> b = {4, 5, 6};
    int dotProduct = inner_product(a.begin(), a.end(), b.begin(), 0);
    // 1*4 + 2*5 + 3*6 = 4 + 10 + 18 = 32

    // ── partial_sum — prefix sums ──
    vector<int> nums = {1, 2, 3, 4, 5};
    vector<int> prefixSum(5);
    partial_sum(nums.begin(), nums.end(), prefixSum.begin());
    // prefixSum = {1, 3, 6, 10, 15}

    // Prefix product
    vector<int> prefixProd(5);
    partial_sum(nums.begin(), nums.end(), prefixProd.begin(), multiplies<int>());
    // prefixProd = {1, 2, 6, 24, 120}

    // ── adjacent_difference — differences between neighbors ──
    vector<int> seq = {1, 3, 6, 10, 15};
    vector<int> diff(5);
    adjacent_difference(seq.begin(), seq.end(), diff.begin());
    // diff = {1, 2, 3, 4, 5}  (first element stays, rest are differences)

    // ── gcd & lcm (C++17) ──
    #include <numeric>
    cout << gcd(12, 18) << endl;   // 6
    cout << lcm(4, 6)   << endl;   // 12

    // ── min_element & max_element ──
    #include <algorithm>
    auto minIt = min_element(v.begin(), v.end());
    auto maxIt = max_element(v.begin(), v.end());
    cout << "Min: " << *minIt << " at index " << distance(v.begin(), minIt) << endl;
    cout << "Max: " << *maxIt << " at index " << distance(v.begin(), maxIt) << endl;

    // minmax_element — both in one pass
    auto [minEl, maxEl] = minmax_element(v.begin(), v.end());
    cout << "Min: " << *minEl << " | Max: " << *maxEl << endl;
}
```

---

# 13. Algorithms — Min, Max & Partitioning

```cpp
#include <algorithm>
#include <vector>
using namespace std;

int main() {
    // ── min & max ──
    cout << min(3, 5)   << endl;  // 3
    cout << max(3, 5)   << endl;  // 5
    cout << min({3, 1, 4, 1, 5, 9}) << endl;  // 1 (initializer list)
    cout << max({3, 1, 4, 1, 5, 9}) << endl;  // 9

    auto [lo, hi] = minmax(3, 7);
    cout << lo << " " << hi << endl;  // 3 7

    // Custom comparator
    string a = "fig", b = "apple";
    cout << min(a, b, [](const string& x, const string& y) {
        return x.length() < y.length();
    }) << endl;  // "fig" (shorter)

    // ── clamp (C++17) — keep value within range ──
    cout << clamp(15, 0, 10) << endl;   // 10 (too high → clamped)
    cout << clamp(-5, 0, 10) << endl;   // 0  (too low → clamped)
    cout << clamp(5,  0, 10) << endl;   // 5  (in range → unchanged)

    // ── Permutations ──
    vector<int> perm = {1, 2, 3};

    cout << "All permutations:\n";
    do {
        for (int x : perm) cout << x << " ";
        cout << "\n";
    } while (next_permutation(perm.begin(), perm.end()));
    // 1 2 3 | 1 3 2 | 2 1 3 | 2 3 1 | 3 1 2 | 3 2 1

    prev_permutation(perm.begin(), perm.end());  // previous permutation

    // ── Partitioning ──
    vector<int> v = {5, 3, 8, 1, 9, 2, 7, 4, 6};

    // partition — rearrange so all matching elements come first
    auto mid = partition(v.begin(), v.end(), [](int x) { return x % 2 == 0; });
    // evens first, then odds (order within each group not preserved)
    cout << "Partition point: " << *mid << endl;

    // stable_partition — preserves relative order
    vector<int> v2 = {5, 3, 8, 1, 9, 2, 7, 4, 6};
    stable_partition(v2.begin(), v2.end(), [](int x) { return x % 2 == 0; });

    // is_partitioned
    cout << is_partitioned(v.begin(), v.end(), [](int x) { return x % 2 == 0; })
         << endl;  // true (after partition above)

    // partition_point — like lower_bound for partitions
    auto pp = partition_point(v.begin(), v.end(), [](int x) { return x % 2 == 0; });

    // ── Set operations (on SORTED ranges) ──
    vector<int> A = {1, 2, 3, 4, 5};
    vector<int> B = {3, 4, 5, 6, 7};
    vector<int> result;

    // Union
    set_union(A.begin(), A.end(), B.begin(), B.end(), back_inserter(result));
    // {1, 2, 3, 4, 5, 6, 7}
    result.clear();

    // Intersection
    set_intersection(A.begin(), A.end(), B.begin(), B.end(), back_inserter(result));
    // {3, 4, 5}
    result.clear();

    // Difference (A - B)
    set_difference(A.begin(), A.end(), B.begin(), B.end(), back_inserter(result));
    // {1, 2}
    result.clear();

    // Symmetric difference
    set_symmetric_difference(A.begin(), A.end(), B.begin(), B.end(), back_inserter(result));
    // {1, 2, 6, 7}

    // includes — is B a subset of A?
    vector<int> sub = {2, 3};
    cout << includes(A.begin(), A.end(), sub.begin(), sub.end()) << endl;  // true

    // merge two sorted ranges
    vector<int> merged;
    merge(A.begin(), A.end(), B.begin(), B.end(), back_inserter(merged));
    // {1, 2, 3, 3, 4, 4, 5, 5, 6, 7}

    // inplace_merge
    vector<int> half = {1, 3, 5, 2, 4, 6};
    inplace_merge(half.begin(), half.begin() + 3, half.end());
    // {1, 2, 3, 4, 5, 6}
}
```

---

# 14. Lambda Functions with STL

Lambdas are **anonymous inline functions** — extremely powerful with STL algorithms.

```cpp
#include <algorithm>
#include <vector>
#include <functional>
using namespace std;

int main() {
    // ── Lambda syntax ──
    // [capture](parameters) -> returnType { body }

    // Basic lambda
    auto square = [](int x) { return x * x; };
    cout << square(5) << endl;   // 25

    // Lambda with explicit return type
    auto divide = [](double a, double b) -> double {
        if (b == 0) throw runtime_error("Division by zero");
        return a / b;
    };

    // ── Capture modes ──
    int base = 10;

    auto addBase = [base](int x) { return x + base; };    // capture by value
    auto mulBase = [&base](int x) { base *= x; return base; };  // capture by reference
    auto captAll = [=](int x) { return x + base; };        // capture all by value
    auto captRef = [&](int x) { base += x; };              // capture all by reference

    // ── Generic lambda (C++14) ──
    auto printAny = [](auto x) { cout << x << " "; };
    printAny(42);
    printAny("hello");
    printAny(3.14);
    cout << endl;

    // ── Mutable lambda ──
    int count = 0;
    auto counter = [count]() mutable { return ++count; };  // local copy can be modified
    cout << counter() << "\n";  // 1
    cout << counter() << "\n";  // 2
    cout << count     << "\n";  // 0 (original unchanged)

    // ── Lambdas with STL ──
    vector<int> nums = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3};

    // sort with lambda
    sort(nums.begin(), nums.end(), [](int a, int b) { return a > b; }); // desc

    // filter + count
    int evenCount = count_if(nums.begin(), nums.end(), [](int x) { return x % 2 == 0; });

    // transform
    vector<string> words = {"hello", "world", "cpp"};
    transform(words.begin(), words.end(), words.begin(),
              [](string s) {
                  transform(s.begin(), s.end(), s.begin(), ::toupper);
                  return s;
              });
    // {"HELLO", "WORLD", "CPP"}

    // find_if with closure
    int threshold = 5;
    auto it = find_if(nums.begin(), nums.end(),
                      [threshold](int x) { return x > threshold; });

    // ── Storing lambdas ──
    // Using function<> from <functional>
    function<int(int, int)> add = [](int a, int b) { return a + b; };
    function<bool(int)>     isEven = [](int x) { return x % 2 == 0; };

    cout << add(3, 4)     << endl;  // 7
    cout << isEven(4)     << endl;  // true

    // Vector of lambdas
    vector<function<int(int)>> ops = {
        [](int x) { return x + 10; },
        [](int x) { return x * 2;  },
        [](int x) { return x * x;  },
    };

    int val = 5;
    for (auto& op : ops) {
        cout << op(val) << " ";   // 15 10 25
    }
    cout << endl;

    // ── immediately invoked lambda ──
    int result = [](int x, int y) { return x + y; }(10, 20);
    cout << result << endl;  // 30
}
```

---

# 15. Function Objects (Functors)

A **functor** is a class that overloads `operator()` — making objects callable like functions.

```cpp
#include <functional>
#include <algorithm>
#include <vector>
using namespace std;

// Custom functor
class Multiplier {
    int factor;
public:
    Multiplier(int f) : factor(f) {}

    int operator()(int x) const {    // operator() makes it callable
        return x * factor;
    }
};

class InRange {
    int lo, hi;
public:
    InRange(int l, int h) : lo(l), hi(h) {}
    bool operator()(int x) const { return x >= lo && x <= hi; }
};

int main() {
    Multiplier triple(3);
    cout << triple(5) << endl;    // 15
    cout << triple(10) << endl;   // 30

    vector<int> v = {1, 2, 3, 4, 5};
    transform(v.begin(), v.end(), v.begin(), Multiplier(2));
    // v = {2, 4, 6, 8, 10}

    InRange between5and8(5, 8);
    vector<int> nums = {3, 5, 7, 9, 6, 2, 8};
    int cnt = count_if(nums.begin(), nums.end(), between5and8);
    cout << "Count in [5,8]: " << cnt << endl;  // 4

    // ── Built-in function objects from <functional> ──
    vector<int> n = {5, 3, 8, 1};

    sort(n.begin(), n.end(), less<int>());      // ascending (default)
    sort(n.begin(), n.end(), greater<int>());   // descending

    // Arithmetic
    int result1 = plus<int>()(3, 4);       // 7
    int result2 = minus<int>()(10, 4);     // 6
    int result3 = multiplies<int>()(3, 4); // 12
    int result4 = divides<int>()(10, 4);   // 2
    int result5 = modulus<int>()(10, 3);   // 1
    int result6 = negate<int>()(5);        // -5

    // Comparison
    bool r1 = equal_to<int>()(5, 5);      // true
    bool r2 = not_equal_to<int>()(3, 5);  // true
    bool r3 = less<int>()(3, 5);          // true
    bool r4 = greater_equal<int>()(5, 5); // true

    // Logical
    bool l1 = logical_and<bool>()(true, false);  // false
    bool l2 = logical_or<bool>()(true, false);   // true
    bool l3 = logical_not<bool>()(true);          // false

    // ── bind — partial function application ──
    auto add = [](int a, int b) { return a + b; };

    using namespace std::placeholders;
    auto add5    = bind(add, _1, 5);    // first arg is placeholder, second is 5
    auto add5_10 = bind(add, 5, _1);    // first is 5, second is placeholder

    cout << add5(3)     << endl;   // 8
    cout << add5_10(10) << endl;   // 15

    // ── mem_fn — wrap member function ──
    struct Widget {
        int value;
        Widget(int v) : value(v) {}
        int getValue() const { return value; }
        void setValue(int v) { value = v; }
    };

    vector<Widget> widgets = {{1}, {2}, {3}};
    vector<int> values;
    transform(widgets.begin(), widgets.end(), back_inserter(values),
              mem_fn(&Widget::getValue));
    // values = {1, 2, 3}
}
```

---

# 16. Utility Library

```cpp
#include <utility>
#include <optional>   // C++17
#include <variant>    // C++17
#include <any>        // C++17
using namespace std;

// ── optional — may or may not have a value ──
optional<string> findUser(int id) {
    if (id == 1) return "Rohit";
    if (id == 2) return "Priya";
    return nullopt;    // no value
}

// ── variant — type-safe union ──
using NumberOrString = variant<int, double, string>;

void processValue(const NumberOrString& v) {
    visit([](auto&& arg) {
        using T = decay_t<decltype(arg)>;
        if constexpr (is_same_v<T, int>)    cout << "int: "    << arg << "\n";
        if constexpr (is_same_v<T, double>) cout << "double: " << arg << "\n";
        if constexpr (is_same_v<T, string>) cout << "string: " << arg << "\n";
    }, v);
}

// ── any — holds any type ──
#include <any>

int main() {
    // optional
    auto user = findUser(1);
    if (user.has_value()) {
        cout << "Found: " << user.value() << endl;
        cout << "Found: " << *user        << endl;  // dereference
    }
    cout << findUser(99).value_or("Guest") << endl;  // "Guest" if not found

    auto u2 = findUser(99);
    // u2.value();  // throws bad_optional_access

    // variant
    NumberOrString v1 = 42;
    NumberOrString v2 = 3.14;
    NumberOrString v3 = string("hello");

    processValue(v1);   // int: 42
    processValue(v2);   // double: 3.14
    processValue(v3);   // string: hello

    // get by type or index
    cout << get<int>(v1)    << endl;   // 42
    cout << get<0>(v1)      << endl;   // 42 (index)
    cout << holds_alternative<int>(v1) << endl;   // true

    // index()
    cout << v1.index() << endl;  // 0 (int is first in variant)

    // any
    any a = 42;
    cout << any_cast<int>(a) << endl;  // 42
    a = string("hello");
    cout << any_cast<string>(a) << endl;  // "hello"
    a = 3.14;

    // Check type
    if (a.type() == typeid(double)) {
        cout << "It's a double: " << any_cast<double>(a) << endl;
    }

    // ── move ──
    string s1 = "Hello World";
    string s2 = move(s1);   // s1 is now empty (moved from)
    cout << s2 << endl;     // "Hello World"
    cout << s1.empty() << endl;  // true

    // ── swap ──
    int x = 10, y = 20;
    swap(x, y);
    cout << x << " " << y << endl;  // 20 10

    // ── forward (perfect forwarding) ──
    // Used in template functions to forward arguments efficiently
}
```

---

# 17. Bitset

`bitset` is a fixed-size sequence of bits — very memory efficient and fast for bit manipulation.

```cpp
#include <bitset>
#include <string>
using namespace std;

int main() {
    // Declaration
    bitset<8>  b1;              // 00000000
    bitset<8>  b2(42);          // 00101010 (42 in binary)
    bitset<8>  b3("11001010");  // from string
    bitset<16> b4(255);         // 0000000011111111

    cout << b2 << endl;         // 00101010
    cout << b3 << endl;         // 11001010

    // Access individual bits
    cout << b2[1] << endl;      // bit at position 1 (from right)
    cout << b2.test(3) << endl; // true/false if bit 3 is set

    // Modify bits
    b1.set();                   // set all bits → 11111111
    b1.reset();                 // clear all → 00000000
    b1.flip();                  // toggle all → 11111111
    b1.set(3);                  // set bit 3 → 00001000
    b1.reset(3);                // clear bit 3 → 00000000
    b1.flip(4);                 // toggle bit 4 → 00010000

    // Info
    cout << b2.count()  << endl;  // number of set bits = 3
    cout << b2.size()   << endl;  // total bits = 8
    cout << b2.any()    << endl;  // true if any bit is set
    cout << b2.none()   << endl;  // true if no bit is set
    cout << b2.all()    << endl;  // true if all bits are set

    // Bitwise operations
    bitset<8> a("11001010");
    bitset<8> b("10101100");

    cout << (a & b)  << endl;  // AND  → 10001000
    cout << (a | b)  << endl;  // OR   → 11101110
    cout << (a ^ b)  << endl;  // XOR  → 01100110
    cout << (~a)     << endl;  // NOT  → 00110101

    cout << (a << 2) << endl;  // left shift  → 00101000
    cout << (a >> 1) << endl;  // right shift → 01100101

    // Conversions
    cout << b2.to_ulong()   << endl;  // to unsigned long = 42
    cout << b2.to_ullong()  << endl;  // to unsigned long long
    cout << b2.to_string()  << endl;  // to string "00101010"

    // ── Real-world use: Sieve of Eratosthenes ──
    const int LIMIT = 50;
    bitset<LIMIT + 1> isPrime;
    isPrime.set();          // mark all as prime
    isPrime[0] = isPrime[1] = 0;

    for (int i = 2; i * i <= LIMIT; i++) {
        if (isPrime[i]) {
            for (int j = i*i; j <= LIMIT; j += i) {
                isPrime[j] = 0;
            }
        }
    }

    cout << "Primes up to " << LIMIT << ": ";
    for (int i = 2; i <= LIMIT; i++) {
        if (isPrime[i]) cout << i << " ";
    }
    cout << endl;
}
```

---

# 18. Span (C++20)

`span` is a lightweight, non-owning view over a contiguous sequence.

```cpp
#include <span>
#include <vector>
#include <array>
using namespace std;

// Function accepting any contiguous range (no copy!)
void printAll(span<const int> s) {
    cout << "Size: " << s.size() << " | Elements: ";
    for (int x : s) cout << x << " ";
    cout << endl;
}

void doubleAll(span<int> s) {
    for (int& x : s) x *= 2;
}

int main() {
    // span works with vector, array, C-arrays
    vector<int>   v = {1, 2, 3, 4, 5};
    array<int, 4> a = {10, 20, 30, 40};
    int           c[] = {100, 200, 300};

    printAll(v);    // all of v
    printAll(a);    // all of a
    printAll(c);    // all of c

    // Subspan
    span<int> sv(v);
    printAll(sv.subspan(1, 3));    // elements 1,2,3 from v (indices 1..3)
    printAll(sv.first(2));         // first 2 elements
    printAll(sv.last(2));          // last 2 elements

    // Modify through span
    doubleAll(v);
    printAll(v);   // {2, 4, 6, 8, 10}
}
```

---

# 19. Ranges (C++20)

Ranges bring a cleaner, composable alternative to iterator-based algorithms.

```cpp
#include <ranges>
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;
namespace rng = std::ranges;
namespace vw  = std::views;   // range adaptors

int main() {
    vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // ── ranges algorithms — no need to spell out begin/end ──
    rng::sort(v);                                    // sort the whole container
    rng::sort(v, greater<int>());                    // descending
    bool found = rng::binary_search(v, 5);
    auto it    = rng::find(v, 7);

    // ── Views — lazy, composable transformations ──
    // Filter evens
    auto evens = v | vw::filter([](int x) { return x % 2 == 0; });
    cout << "Evens: ";
    for (int x : evens) cout << x << " ";  // 2 4 6 8 10
    cout << endl;

    // Transform — square each
    auto squared = v | vw::transform([](int x) { return x * x; });
    cout << "Squared: ";
    for (int x : squared) cout << x << " ";  // 100 81 64 ... 1
    cout << endl;

    // take / drop
    auto first3 = v | vw::take(3);   // first 3 elements
    auto skip3  = v | vw::drop(3);   // skip first 3

    // ── Chaining views (pipe operator) ──
    auto result = v
        | vw::filter([](int x) { return x % 2 == 0; })   // evens only
        | vw::transform([](int x) { return x * x; })      // square them
        | vw::take(3);                                     // first 3

    cout << "Evens squared (first 3): ";
    for (int x : result) cout << x << " ";  // 100 64 36 (descending, so 10,8,6 → 100,64,36)
    cout << endl;

    // reverse view
    auto rev = v | vw::reverse;

    // iota view — generate range
    auto naturals = vw::iota(1, 11);   // 1, 2, 3, ..., 10
    cout << "1 to 10: ";
    for (int x : naturals) cout << x << " ";
    cout << endl;

    // keys / values from map
    map<string, int> m = {{"a", 1}, {"b", 2}, {"c", 3}};
    for (auto& k : m | vw::keys)   cout << k << " ";   // a b c
    for (auto& v : m | vw::values) cout << v << " ";   // 1 2 3

    // ── ranges to container (C++23 — use workaround in C++20) ──
    vector<int> squaredVec;
    auto sq = v | vw::transform([](int x) { return x * x; });
    rng::copy(sq, back_inserter(squaredVec));
}
```

---

# 20. STL in Competitive Programming

A collection of high-impact patterns for competitive programming.

```cpp
#include <bits/stdc++.h>  // include everything
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);  // faster I/O
    cin.tie(NULL);

    // ── Frequency map ──
    string s = "programming";
    map<char, int> freq;
    for (char c : s) freq[c]++;
    // OR
    unordered_map<char, int> ufreq;
    for (char c : s) ufreq[c]++;

    // ── Two pointers ──
    vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    int target = 10, lo = 0, hi = (int)v.size() - 1;
    while (lo < hi) {
        int sum = v[lo] + v[hi];
        if (sum == target) { cout << v[lo] << " " << v[hi] << "\n"; lo++; hi--; }
        else if (sum < target) lo++;
        else hi--;
    }

    // ── Coordinate compression ──
    vector<int> arr = {100, 5, 50, 100, 25, 50};
    vector<int> sorted_unique = arr;
    sort(sorted_unique.begin(), sorted_unique.end());
    sorted_unique.erase(unique(sorted_unique.begin(), sorted_unique.end()),
                        sorted_unique.end());
    for (int& x : arr) {
        x = lower_bound(sorted_unique.begin(), sorted_unique.end(), x)
            - sorted_unique.begin();
    }
    // arr = {2, 0, 1, 2, ... } (compressed indices)

    // ── Sliding window maximum ──
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    deque<int> dq;  // stores indices
    vector<int> maxes;

    for (int i = 0; i < (int)nums.size(); i++) {
        // Remove elements outside window
        while (!dq.empty() && dq.front() < i - k + 1) dq.pop_front();
        // Remove smaller elements from back
        while (!dq.empty() && nums[dq.back()] < nums[i]) dq.pop_back();
        dq.push_back(i);
        if (i >= k - 1) maxes.push_back(nums[dq.front()]);
    }
    // maxes = {3, 3, 5, 5, 6, 7}

    // ── Top K elements ──
    vector<int> data = {3, 1, 4, 1, 5, 9, 2, 6};
    int K = 3;
    // Min-heap of size K
    priority_queue<int, vector<int>, greater<int>> minHeap;
    for (int x : data) {
        minHeap.push(x);
        if ((int)minHeap.size() > K) minHeap.pop();
    }
    cout << "Top " << K << " largest:\n";
    while (!minHeap.empty()) { cout << minHeap.top() << " "; minHeap.pop(); }
    cout << endl;

    // ── Next greater element ──
    vector<int> nge_arr = {4, 5, 2, 10, 8};
    vector<int> nge(nge_arr.size(), -1);
    stack<int> st;  // store indices

    for (int i = 0; i < (int)nge_arr.size(); i++) {
        while (!st.empty() && nge_arr[st.top()] < nge_arr[i]) {
            nge[st.top()] = nge_arr[i];
            st.pop();
        }
        st.push(i);
    }
    // nge = {5, 10, 10, -1, -1}

    // ── Prefix sum ──
    vector<int> arr2 = {1, 2, 3, 4, 5};
    vector<int> prefix(arr2.size() + 1, 0);
    for (int i = 0; i < (int)arr2.size(); i++) prefix[i+1] = prefix[i] + arr2[i];
    // Range sum [l, r] (0-indexed, inclusive):
    auto rangeSum = [&](int l, int r) { return prefix[r+1] - prefix[l]; };
    cout << "Sum [1,3]: " << rangeSum(1, 3) << endl;  // 9

    // ── Sorting tricks ──
    // Sort indices by value
    vector<int> idx(arr2.size());
    iota(idx.begin(), idx.end(), 0);
    sort(idx.begin(), idx.end(), [&](int a, int b) { return arr2[a] > arr2[b]; });

    // ── GCD / LCM of vector ──
    vector<int> gcdArr = {12, 18, 24};
    int g = gcdArr[0];
    for (int x : gcdArr) g = gcd(g, x);
    cout << "GCD: " << g << endl;  // 6
}
```

---

# 21. Common STL Patterns & Idioms

```cpp
// ── Erase-Remove Idiom ──
vector<int> v = {1, 2, 3, 2, 4, 2};
v.erase(remove(v.begin(), v.end(), 2), v.end());
// OR with condition:
v.erase(remove_if(v.begin(), v.end(), [](int x){ return x%2==0; }), v.end());

// ── Copy unique elements (preserving order) ──
vector<int> src = {3, 1, 4, 1, 5, 9, 2, 6, 5};
unordered_set<int> seen;
vector<int> unique_ordered;
copy_if(src.begin(), src.end(), back_inserter(unique_ordered),
        [&seen](int x) { return seen.insert(x).second; });

// ── Flattening a vector of vectors ──
vector<vector<int>> nested = {{1,2,3},{4,5},{6,7,8,9}};
vector<int> flat;
for (auto& row : nested) flat.insert(flat.end(), row.begin(), row.end());
// OR:
for (auto& row : nested) copy(row.begin(), row.end(), back_inserter(flat));

// ── Counting distinct elements ──
vector<int> nums = {3,1,4,1,5,9,2,6,5,3,5};
int distinct = set<int>(nums.begin(), nums.end()).size();

// ── Sort then unique count ──
sort(nums.begin(), nums.end());
int uniqueCount = unique(nums.begin(), nums.end()) - nums.begin();

// ── Map/set from vector ──
vector<string> words = {"apple","banana","apple","cherry"};
map<string,int> wfreq;
for (auto& w : words) wfreq[w]++;

// ── Group by key ──
vector<pair<string,int>> scores = {{"A",1},{"B",2},{"A",3},{"B",4}};
map<string, vector<int>> grouped;
for (auto& [k, v] : scores) grouped[k].push_back(v);

// ── Invert a map (value → key) ──
map<string,int> original = {{"one",1},{"two",2},{"three",3}};
map<int,string> inverted;
for (auto& [k,v] : original) inverted[v] = k;

// ── Sorted map by value (using vector of pairs) ──
map<string,int> freq = {{"apple",3},{"banana",1},{"cherry",5}};
vector<pair<string,int>> sortedByVal(freq.begin(), freq.end());
sort(sortedByVal.begin(), sortedByVal.end(),
     [](auto& a, auto& b){ return a.second > b.second; });

// ── Check if two vectors are equal ──
vector<int> a = {1,2,3}, b = {1,2,3};
bool eq = (a == b);  // ✅ Direct comparison works!

// ── Move from set to vector ──
set<int> s = {5,3,1,4,2};
vector<int> fromSet(s.begin(), s.end());  // already sorted!

// ── Priority queue with pairs (min-heap by first) ──
priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
pq.push({2, 100});
pq.push({1, 200});
pq.push({3, 300});
while (!pq.empty()) {
    auto [dist, node] = pq.top(); pq.pop();
    cout << dist << " " << node << "\n";
}
```

---

# 22. Performance & Complexity

## Container Complexity Table

| Operation | vector | deque | list | set/map | unordered |
|---|---|---|---|---|---|
| Access by index | O(1) | O(1) | O(n) | ❌ | ❌ |
| Access front/back | O(1) | O(1) | O(1) | ❌ | ❌ |
| Insert/erase front | O(n) | **O(1)** | O(1) | — | — |
| Insert/erase back | O(1) | O(1) | O(1) | — | — |
| Insert/erase middle | O(n) | O(n) | **O(1)** | — | — |
| Find/count | O(n) | O(n) | O(n) | **O(log n)** | **O(1) avg** |
| Insert (sorted) | — | — | — | O(log n) | O(1) avg |
| Sorted iteration | O(n log n) | O(n log n) | O(n log n) | **O(n)** | ❌ |

## Algorithm Complexity Table

| Algorithm | Average | Notes |
|---|---|---|
| `sort` | O(n log n) | Introsort (hybrid) |
| `stable_sort` | O(n log n) | Merge sort |
| `partial_sort` | O(n log k) | k = size of sorted part |
| `nth_element` | O(n) | Average — quickselect |
| `binary_search` | O(log n) | Sorted input required |
| `lower/upper_bound` | O(log n) | Sorted input required |
| `find`, `count` | O(n) | Linear scan |
| `accumulate`, `reduce` | O(n) | |
| `set_union/intersection` | O(n+m) | Both inputs sorted |

## Memory Considerations

```cpp
// vector capacity growth
vector<int> v;
for (int i = 0; i < 1000; i++) {
    v.push_back(i);
    // capacity doubles when full: 1→2→4→8→16→...
}

// ✅ Avoid: reserve when you know size
vector<int> v2;
v2.reserve(1000);   // allocate once for 1000 elements

// ✅ shrink_to_fit — release unused capacity
v.shrink_to_fit();

// ✅ Use emplace_back over push_back for complex objects
vector<pair<int,string>> vp;
vp.push_back({1, "hello"});    // creates temporary, then copies/moves
vp.emplace_back(2, "world");   // constructs in-place — no temporary!

// ✅ Use string_view for read-only string params
void process(string_view sv);      // no copy
void processOld(const string& s);  // may copy

// ✅ Reserve unordered_map before bulk insert
unordered_map<int,int> um;
um.reserve(10000);
um.max_load_factor(0.25);  // reduce collisions
```

---

# 23. Best Practices

```cpp
// ✅ 1. Prefer range-based for loops
for (const auto& elem : container) { }    // ✅ clean and safe
// for (int i = 0; i < v.size(); i++) { } // ❌ verbose

// ✅ 2. Use auto for iterators
auto it = myMap.find("key");    // ✅
// map<string,int>::iterator it = myMap.find("key");  // ❌ verbose

// ✅ 3. Use structured bindings (C++17)
for (const auto& [key, val] : myMap) { }  // ✅
// for (const auto& p : myMap) { p.first; p.second; }  // ❌ old style

// ✅ 4. emplace over push/insert for complex types
v.emplace_back(args...);        // ✅ constructs in-place
v.push_back(T(args...));        // ❌ creates temporary then moves

// ✅ 5. Erase-remove idiom
v.erase(remove(v.begin(), v.end(), val), v.end());

// ✅ 6. Check find() result before using it
auto it = myMap.find("key");
if (it != myMap.end()) {
    use(it->second);            // ✅ safe
}
// myMap["key"];               // ❌ creates entry if missing!

// ✅ 7. Reserve containers when size is known
v.reserve(expectedSize);

// ✅ 8. Use const when not modifying
const vector<int>& getItems() const { return items; }

// ✅ 9. Prefer algorithms over raw loops
sort(v.begin(), v.end());        // ✅
auto it2 = find(v.begin(), v.end(), x);  // ✅

// ✅ 10. Use cbegin/cend for read-only iteration
for (auto it = v.cbegin(); it != v.cend(); ++it) { }

// ✅ 11. string_view for read-only string params
void print(string_view sv) { cout << sv; }

// ✅ 12. Don't compare signed/unsigned
// for (int i = 0; i < v.size(); i++)   // ❌ warning: signed/unsigned mismatch
for (int i = 0; i < (int)v.size(); i++) // ✅
for (size_t i = 0; i < v.size(); i++)   // ✅
```

---

# 24. Exercises & Challenges

## 🟢 Beginner

1. **Frequency Counter** — Count frequency of each character in a string using `map`. Print sorted by frequency.
2. **Duplicate Finder** — Given a vector of integers, find all duplicates using `unordered_set`.
3. **Stack-based Reverse Polish Notation** — Evaluate expressions like `"3 4 + 2 *"` using `stack`.
4. **Phone Book** — Implement a phone book using `map<string, vector<string>>` with add, remove, and lookup.

## 🟡 Intermediate

5. **Top K Frequent Elements** — Given a list of numbers, return the K most frequent using `priority_queue` and `unordered_map`.
6. **Anagram Grouping** — Group words that are anagrams of each other using `map<string, vector<string>>`.
7. **LRU Cache** — Implement Least Recently Used cache using `list` and `unordered_map`.
8. **Sliding Window** — Find the maximum sum of any subarray of size K using `deque`.

## 🔴 Advanced

9. **Graph Algorithms** — Implement BFS (queue), DFS (stack/recursion), and Dijkstra (priority_queue) using STL containers.
10. **Trie using map** — Implement a Trie (prefix tree) using `map<char, TrieNode*>` for autocomplete.
11. **Interval Merge** — Given a vector of `{start, end}` intervals, merge overlapping ones using `sort` + `vector`.

```cpp
// Starter for Challenge 7: LRU Cache
class LRUCache {
    int capacity;
    list<pair<int,int>>              cache;    // {key, value}
    unordered_map<int, list<pair<int,int>>::iterator> pos;

public:
    LRUCache(int cap) : capacity(cap) {}

    int get(int key) {
        if (pos.find(key) == pos.end()) return -1;
        cache.splice(cache.begin(), cache, pos[key]); // move to front
        return pos[key]->second;
    }

    void put(int key, int value) {
        if (pos.count(key)) {
            pos[key]->second = value;
            cache.splice(cache.begin(), cache, pos[key]);
        } else {
            if ((int)cache.size() == capacity) {
                pos.erase(cache.back().first);
                cache.pop_back();
            }
            cache.emplace_front(key, value);
            pos[key] = cache.begin();
        }
    }
};
```

---

# 25. Conclusion & Resources

## 🎯 STL Mastery Roadmap

```
Beginner
├── vector, array
├── string
├── pair, tuple
├── Basic algorithms (sort, find, count)
└── Range-based for & auto

Intermediate
├── stack, queue, priority_queue
├── set, map, multiset, multimap
├── unordered_set, unordered_map
├── Iterators & iterator arithmetic
└── Lambdas with algorithms

Advanced
├── Algorithm deep-dive (all 100+ algos)
├── Custom comparators & hash functions
├── Performance tuning (reserve, emplace)
├── optional, variant, any
└── string_view, span

Expert (C++20)
├── Ranges & Views
├── Concepts
├── Coroutines
└── Template metaprogramming with STL
```

## 📚 Resources

| Resource | Link | What You Get |
|---|---|---|
| **cppreference** | cppreference.com | Complete STL reference |
| **cplusplus.com** | cplusplus.com | Beginner-friendly docs |
| **Compiler Explorer** | godbolt.org | See what your STL code compiles to |
| **LearnCpp** | learncpp.com | Structured tutorials |
| **LeetCode** | leetcode.com | STL practice problems |
| **Codeforces** | codeforces.com | Competitive programming |

## 📖 Recommended Books

| Book | Author | Focus |
|---|---|---|
| *The C++ Standard Library* | Nikolai Josuttis | Complete STL reference |
| *Effective STL* | Scott Meyers | 50 best practices |
| *C++ Templates* | Vandevoorde & Josuttis | Deep dive into generics |

## 🛠️ Useful STL Cheat Sheet

```
CONTAINERS          USE WHEN
vector              Default — fast random access, push_back
array               Fixed size known at compile time
deque               Need fast front & back insert
list                Frequent insert/erase in middle
stack               LIFO (undo, DFS, expression parsing)
queue               FIFO (BFS, task scheduling)
priority_queue      Always process highest/lowest priority first
set                 Sorted unique keys, fast lookup
map                 Sorted key-value, fast lookup
unordered_set       Fastest lookup, no order needed
unordered_map       Fastest key-value lookup, no order needed
multiset/multimap   Sorted, allows duplicates

ALGORITHMS          USE WHEN
sort                Sort a range
binary_search       Check if value exists (sorted)
lower/upper_bound   Find insertion point / range (sorted)
find/find_if        Linear search
count/count_if      Count elements
transform           Apply function to elements
remove/erase        Remove elements (use erase-remove idiom)
accumulate          Sum / fold / reduce
partial_sum         Prefix sums
set_union/etc.      Set operations (sorted ranges)
```

## 🎉 Conclusion

You've mastered the **C++ Standard Template Library**! Summary:

- ✅ **Containers** — vector, array, deque, list, stack, queue, priority_queue, set, map, unordered variants
- ✅ **Algorithms** — sort, search, modify, numeric, min/max, partition, set ops
- ✅ **Iterators** — all five categories, iterator helpers, stream iterators
- ✅ **Lambdas & Functors** — closures, captures, built-in functors, bind
- ✅ **Modern C++** — optional, variant, any, string_view, span, ranges
- ✅ **Patterns** — erase-remove, coordinate compression, sliding window, LRU cache

### The Golden Rules

1. **Know your complexity** — choose the right container for the job.
2. **Use algorithms over raw loops** — they're tested, readable, and fast.
3. **Prefer emplace over push/insert** for complex types.
4. **Reserve when size is known** — save reallocations.
5. **Always check find() ≠ end()** before using the result.
6. **Use string_view for read-only strings** — zero-copy reads.

---

> 💙 *"The STL is not just a library — it's a way of thinking about reusable, composable, generic code."*

**Keep Coding! Keep Building! 🚀**

---

*Made with ❤️ | C++17/20 | STL Complete Reference | Last updated: 2024*
