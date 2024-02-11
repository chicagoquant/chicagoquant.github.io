
# Topics

<table>
<tr>
<td>Hackernoon</td>
<td>Neetcode</td>
</tr>

<tr>
<td style="vertical-align:top">

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

</td>

<td style="vertical-align:top">

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

</td>
</tr>
</table>

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

<details>
<summary>
two pointers <a href="https://leetcode.com/problems/trapping-rain-water/">[Trapping rain water]</a>
</summary>

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int water = 0;
        int max_h = 0;
        for (int i = 0, j = height.size()-1; i < j;)
        {
            int h = min(height[i], height[j]);
            if (max_h < h) {
                max_h = h;
            }
            if (height[i] <= height[j]) {
                water += max_h - height[i];
                ++i;
            }
            else {
                water += max_h - height[j];
                --j;
            }
        }
        return water;
    }
};
```

Is keeping `max_h` not sufficient? why do people keep track of `left_max_h` and `right_max_h`.
</details>

# Concepts

<details>
<summary>graphs</summary>

graph - vertex, edge

undirected, directed, acyclic, weighted, adjacency

connected, disconnected

graph algorithms
- search
- detect a cycle
- shortest path

binary tree
- height or levels = `h`, min height = `log2(n)+1`
- leaf-nodes = `2**h = n = (N+1)/2`
- tree-nodes = `2**(h+1)-1 = N`
- internal-nodes = `2**h-1 = n-1`

```cpp
// 0-based indexing
parent(i) = (i-1)/2;                // parent of i-th node
left_child(i) = 2*i + 1;            // left child of i-th node
right_child(i) = 2*i + 2;           // right child of i-th node

// 1-based indexing
parent(i) = i/2;                    // parent of i-th node
left_child(i) = 2*i;                // left child of i-th node
right_child(i) = 2*i + 1;           // right child of i-th node
```
</details>

<details>
<summary>(in-order dfs) verify binary search tree</summary>

In-order dfs, check prev node is less

```cpp
bool is_bst(TreeNode* root) {
  if (root == nullptr) { return false; }
  stack<TreeNode*> stack;
  TreeNode *curr = root, *prev = nullptr;
  while (!(curr == nullptr && stack.empty())) {
    if (curr != nullptr) {
      stack.push(curr);     // save current node
      curr = curr->left;    // keep descending on left side
    }
    else {                  // curr == nullptr, reached a leaf node
      curr = stack.top();   // left side processed completely
      stack.pop();          // now looking at curr node

      // in-order step, do whatever with curr node
      if (prev != nullptr && curr->value < prev->value) { return false; }

      prev = curr;
      curr = curr->right;   // descend down right side
    }
  }
  return true;
}
```

it is as if we have laid the BST linearly like a list in-order. we expect the nodes to be in sorted order.
we can check all the adjacent items are in order.

recursive version
```cpp
bool is_bst(TreeNode* root)
{
    TreeNode* prev = nullptr;
    return recursive_is_bst(root, prev);
}

bool recursive_is_bst(TreeNode* root, TreeNode* &prev)
{
    if (root == nullptr) { return true; }

    bool left_is_bst = recursive_is_bst(root->left, prev);

    // in-order step
    if (prev != nullptr && root->value < prev->value) { return false; }

    prev = root;
    bool right_is_bst = recursive_is_bst(root->right, prev);

    return left_is_bst && right_is_bst;
}
```
</details>

<details><summary>verify tree is balanced</summary>

verify:
- left tree is balanced
- right tree is balanced
- difference of `height(left)` and `height(right)` is at most 1

```cpp
bool is_balanced(TreeNode* root)
{
    return recursive_is_balanced(root).has_value();
}

optional<int> recursive_is_balanced(TreeNode* root)
{
    if (root == nullptr) { return optional { 0 }; }     // is balanced

    optional<int> left_balanced_height = recursive_is_balanced(root->left);
    if (!left_balanced_height) { return left_balanced_height; }       // not balanced

    optional<int> right_balanced_height = recursive_is_balanced(root->right);
    if (!right_balanced_height) { return right_balanced_height; }     // not balanced

    int diff = abs(left_balanced_height.value() - right_balanced_height.value());
    if (diff <= 1) {
        return optional { 1 + max(left_balanced_height.value(), right_balanced_height.value()) };
    }
    return nullopt; // not balanced
}
```

</details>

<details><summary>find lowest common ancestor of 2 nodes in a tree</summary>

given a binary tree, root node, and 2 nodes p, q
- is either p, q in left subtree &rarr; `leftLCA`
- is either p, q in right subtree &rarr; `rightLCA`
- if both true, then `root` node is LCA
- otherwise, return `leftLCA` or `rightLCA`

`find_lca(root, p, q)` will return the lowest common ancestor if both `p` and `q` are in the binary tree.

if only 1 of them is found in the tree, the other is not a part of the tree, then it will return that node `p/q`

```cpp
TreeNode* find_lca(TreeNode* root, Data p, Data q)
{
    if (root == nullptr) { return nullptr; }

    // found one node, stop descending, node itself becomes the ancestor
    if (root->value == p || root->value == q) { return root; }

    TreeNode* left_lca = find_lca(root->left, p, q);

    TreeNode* right_lca = find_lca(root->right, p, q);

    // found 1 node on left, and the other node on the right, root is the LCA
    if (left_lca != nullptr && right_lca != nullptr) { return root; }

    // only found 1 node, on left
    if (left_lca != nullptr) { return left_lca; }

    // either only found 1 node, on right (right_lca != nullptr)
    // or no node found on left / right (right_lca == nullptr)
    return right_lca;
}
```
</details>

<details><summary>sorted array to binary search tree</summary>

```cpp
TreeNode* sorted_array_to_bst(const vector<int>& A)
{
    if (A.empty()) { return nullptr; }

    return recursive_sorted_array_to_bst(A, 0, A.size());
}

TreeNode* recursive_sorted_array_to_bst(const vector<int>& A, int l, int r)
{
    if (l >= r) { return nullptr; }

    int mid = l + (r-l)/2;
    TreeNode* root = new TreeNode { A[mid], nullptr, nullptr };
    root->left = recursive_sorted_array_to_bst(A, l, mid);
    root->right = recursive_sorted_array_to_bst(A, mid+1, r);
    return root;
}

```
</details>

<details><summary>combinations - K numbers from 1..N</summary>

remember, we are picking combinations: like `(1,2,3)` once, we do not consider permutations `(2,3,1), ...`.

i.e. order does not matter

for each number, pick it or drop it recursively, only going upto length K

```cpp
vector<vector<int>> findKCombinations(int K, int N)
{
    vector<vector<int>> output;
    vector<int> temp(K, 0);

    kCombination(0, N, 0, K, temp, output);

    return output;
}

void kCombination(int index, int N, int i, int K, vector<int>& temp, vector<vector<int>>& output)
{
    if (index == K)
    {
        output.push_back(temp);
        return;
    }

    if (i >= N) return;

    temp[index] = i+1;
    kCombination(index+1, N, i+1, K, temp, output); // pick i+1
    kCombination(index  , N, i+1, K, temp, output); // drop i+1
}
```

fix a number for slot `index`, try all available combinations for slot `index+1`
, and so on recursively upto K slots

```cpp
vector<vector<int>> findKCombinations(int K, int N)
{
    vector<vector<int>> output;
    vector<int> temp(K, 0);

    kCombination(0, 0, N, K, temp, output);

    return output;
}

void kCombination(int index, int start, int end, int K, vector<int>& temp, vector<vector<int>>& output)
{
    if (index == K)
    {
        output.push_back(temp);
        return;
    }

    for (int i = start; i < end && end-i+1 >= K-index; ++i)
    {
        temp[index] = i+1;
        kCombination(index+1, i+1, end, K, temp, output);
    }
}
```
</details>

<details><summary>next permutation</summary>

```cpp
void next_permutation(vector<int>& A)
{
    int N = A.size();
    int j = N-2;
    while (j+1 > 0 && A[j] > A[j+1])
    {
        --j;
    }
    // A[0] ... A[j] < A[j+1] ... A[N-1]

    // find A[k] in A[j+1 : N], s.t. A[j] < A[k]
    int k = N-1;
    while (j < k && A[j] > A[k])
    {
        --k;
    }
    swap(A[j], A[k]);

    // reverse A[j+1 : N]
    int r = N-1;
    int s = j+1;
    while (r > s) {
        swap(A[r], A[s]);
        --r;
        ++s;
    }
}
```

all permutations

```cpp
void all_permutations(vector<int>& A)
{
    recursive_permutation(A, A.size());
}

void recursive_permutations(vector<int>& A, int n)
{
    if (n == 1) {
        // print permutation
        return;
    }

    for (int i = 0; i < n; ++i) {
        swap(A[i], A[n-1]);                 // remove ith item
        recursive_permutations(A, n-1);     // all permutations without ith item
        swap(A[i], A[n-1]);                 // restore ith item
    }
}
```
</details>

<details><summary>tbd</summary></details>
