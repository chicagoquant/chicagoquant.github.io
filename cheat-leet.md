
# Topics

- Sliding Window
  - Max sum subarray of size K
  - Longest substring with K distinct characters
  - String anagrams
  - Average >= Threshold, Window of size K
- Two Pointers or Iterators
  - Container with most water
- Fast and Slow pointers
- Merge Intervals
- Cyclic Sort
- In-place Reversal of Linked List
- Tree BFS
- Tree DFS
- Two Heaps
- Subsets
- Modified Binary Search
- Top K Elements
- K-Way Merge
- Topological Sort

Source: https://www.youtube.com/watch?v=g6TLB_tAaCI&list=WL&index=12&t=1688s

Source: https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed

See: https://seanprashad.com/leetcode-patterns/

- Arrays and Hashing
- Two Pointers
- Stack
- Binary Search
- Sliding Window
- Linked List
- Trees
- Tries
- Backtracking
- Heap / Priority Queue
- Intervals
- Greedy
- Graphs
- Advanced Graphs
- 1-d Dynamic Programming
- 2-d Dynamic Programming
- Bit Manipulation
- Math and Geometry

Source: https://neetcode.io/roadmap

# Problems

<details>
<summary>
sliding window <a href="https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold">[No of subarrays of size k and average &ge; threshold]</a>
</summary>

```cpp
#include <algorithm>

class Solution {
public:
    int numOfSubarrays(vector<int>& arr, int k, int threshold) {
        const int32_t sum_threshold = k*threshold;
        int count = 0;
        int32_t sum = std::accumulate(arr.begin(), arr.begin()+k, 0);
        if (sum >= sum_threshold) {
            ++count;
        }
        for(size_t i = k; i < arr.size(); ++i)
        {
            sum += arr[i]-arr[i-k];
            if (sum >= sum_threshold) {
                ++count;
            }
        }
        return count;
    }
};
```
</details>

<details>
<summary>
two pointers <a href="https://leetcode.com/problems/container-with-most-water">[container with most water]</a>
</summary>

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int max_area = 0;
        for (size_t i = 0, j = height.size()-1; i < j;)
        {
            int d = j-i;
            int area = min(height[j], height[i]) * d;
            if (area > max_area) {
                max_area = area;
            }
            if (height[i] <= height[j]) {
                ++i;
            }
            else {
                --j;
            }
        }
        return max_area;
    }
};
```
</details>
