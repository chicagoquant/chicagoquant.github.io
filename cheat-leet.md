
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

Source: [Youtube ACM UCR](https://www.youtube.com/watch?v=g6TLB_tAaCI&list=WL&index=12&t=1688s)

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

<details> <summary> sliding window <a href="https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold">[No of subarrays of size k and average &ge; threshold]</a> </summary>

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

<details> <summary> two pointers <a href="https://leetcode.com/problems/container-with-most-water">[container with most water]</a> </summary>

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

<details> <summary> two pointers <a href="https://leetcode.com/problems/trapping-rain-water/">[Trapping rain water]</a> </summary>

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

## Graphs, Trees
<details> <summary>Graphs, Trees</summary>

graph - vertex, edge

undirected, directed, acyclic, weighted, adjacency

connected, disconnected

tree = directed, acyclic, connected graph

graph algorithms
- search (dfs, bfs)
- detect a cycle
- shortest path (dijkstra, )
- minimum spanning tree (kruskal, prim)

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

Shortest Path

Single Source Shortest Path (SSSP) in DAG

Single Source Shortest Path (SSSP) in General Graphs (Bellman Ford)

All Pairs Shortest Path (APSP) in General Graphs $O(V^4)$

All Pairs Shortest Path (APSP) in General Graphs (Floyd Warshall) $O(V^3)$

## Tree traversal


```cpp
void preorder(TreeNode* root)               |   void iterativePreorder(TreeNode* root)
{                                           |   {
  if (root == nullptr) { return; }          |       if (root == nullptr) return;
                                            |       stack<TreeNode*> tree_stack;
  process(root->value);                     |       TreeNode* curr;
                                            |       tree_stack.push(root);
  preorder(root->left);                     |       while (!tree_stack.empty()) {
  preorder(root->right);                    |           curr = tree_stack.top();
}                                           |           tree_stack.pop();
                                            |           process(curr->value);
                                            |           if (curr->right) { tree_stack.push(curr->right); }
                                            |           if (curr->left)  { tree_stack.push(curr->left); }
                                            |       }
                                            |   }
                                            |
void inorder(TreeNode* root)                |   void iterativeInorder(TreeNode* root)
{                                           |   {
  if (root == nullptr) { return; }          |       if (root == nullptr) return;
                                            |       stack<TreeNode*> tree_stack;
  inorder(root->left);                      |       TreeNode* curr = root;
                                            |       while (!tree_stack.empty() || curr != nullptr) {
  process(root->value);                     |           if (curr != nullptr) {
                                            |               tree_stack.push(curr);
  inorder(root->right);                     |               curr = curr->left;
}                                           |           }
                                            |           else {
                                            |               curr = tree_stack.top();
                                            |               tree_stack.pop();
                                            |               process(curr->value);
                                            |               curr = curr->right;
                                            |           }
                                            |       }
                                            |   }
                                            |
void postorder(TreeNode* root)              |   void postorderTraversalSingleStack(TreeNode* root)
{                                           |   {
  if (root == nullptr) { return; }          |       if (root == nullptr) return;
                                            |       stack<TreeNode*> tree_stack;
  postorder(root->left);                    |       TreeNode* prev = nullptr;
  postorder(root->right);                   |       while (root || !tree_stack.empty()) {
  process(root->value);                     |           if (root) {
}                                           |               tree_stack.push(root);
                                            |               root = root->left;
                                            |           }
                                            |           else {
                                            |               TreeNode* curr = tree_stack.top();
                                            |               if (curr->right && curr->right != prev) {
                                            |                   root = curr->right;
                                            |               }
                                            |               else {
                                            |                   process(curr->value);
                                            |                   prev = curr;
                                            |                   tree_stack.pop();
                                            |               }
                                            |           }
                                            |       }
                                            |   }
```

BFS

```cpp
void iterativeLevelOrder(TreeNode* root)
{
    if (root == nullptr) { return; }
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* curr = q.front();
        q.pop();
        process(curr->value);
        if (curr->left)  { q.push(curr->left); }
        if (curr->right) { q.push(curr->right); }
    }
}
```


## Verify binary search tree (in-order dfs)
<details> <summary>Verify binary search tree (in-order dfs)</summary>

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

## verify tree is balanced
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

## Lowest common ancestor

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

## Binary Search Tree

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

## Backtracking

<details><summary>backtracking</summary>

backtracking -- to enumerate all states, bound function check to prune the tree to optimize
- feasible solution to a decision problem -- whether true / false?
- solve optimization problems
- enumerate all feasible solutions

example problems:
- n queen placement
- all subsets of numbers, that sum up to a target T
- graph coloring: minimum colors to color a graph
- hamiltonian path (from S to T, visits all the vertices of the graph)
</details>

### Backtracking - combinations

<details><summary>(backtracking) combinations - K numbers from 1..N</summary>

remember, we are picking combinations: like `(1,2,3)` once, we do not consider permutations `(2,3,1), ...`.

i.e. order does not matter

for each number, pick it or drop it recursively, only going upto length K

$$ {N \choose K} = {N-1 \choose K} + {N-1 \choose K-1}$$

```cpp
vector<vector<int>> findKCombinations(int K, int N)
{
  vector<vector<int>> output;
  vector<int> temp(K, 0);

  kCombination(0, N, 0, K, temp, output);

  return output;
}

// index = slot being filled
// i+1 = current value from [1..N] being used.
// so i is the 0-based index of current value i+1
void kCombination(int index, int N, int i, int K, vector<int>& temp, vector<vector<int>>& output)
{
  if (index == K)
  {
      output.push_back(temp);
      return;
  }

  if (i+1 > N) return;

  temp[index] = i+1;
  kCombination(index+1, N, i+1, K, temp, output); // pick i+1
  kCombination(index  , N, i+1, K, temp, output); // drop i+1
}
```

fix a number for slot `index`, try all available combinations for slot `index+1`
, and so on recursively upto K slots

$$ {N \choose K} = {N-1 \choose K} \times N $$

```cpp
vector<vector<int>> findKCombinations(int K, int N)
{
    vector<vector<int>> output;
    vector<int> temp(K, 0);

    kCombination(0, 0, N, K, temp, output);

    return output;
}

// index = slot being filled
// i+1 = current value from [1..N] being used.
// so i is the 0-based index of current value i+1
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

### Backtracking - permutations

<details><summary>(backtracking) permutations</summary>

```cpp
void next_permutation(vector<int>& A)
{
    int N = A.size();
    int j = N-2;
    // find until where (from right) is A sorted
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
    // invariant: A[j] < A[k]
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

1. find the right portion of the array that is in decreasing order `A[j+1, end)` is decreasing
2. find first element in that right portion that is upper bound of `A[j]`, ie, `A[j] < A[k]`
3. swap `A[j]` and `A[k]`
4. reverse A[j+1..end)

STL next permutation
```cpp
template<class BidirIt>
bool next_permutation(BidirIt first, BidirIt last)
{
    auto r_first = std::make_reverse_iterator(last);
    auto r_last = std::make_reverse_iterator(first);
    auto left = std::is_sorted_until(r_first, r_last);

    if (left != r_last)
    {
        auto right = std::upper_bound(r_first, left, *left);
        std::iter_swap(left, right);
    }

    std::reverse(left.base(), last);
    return left != r_last;
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

heaps algorithm
```cpp
void all_permutations(vector<int>& A)
{
    recursive_heaps_permutation(A, A.size());
}

void recursive_heaps_permutations(vector<int>& A, int n)
{
    if (n == 1) {
        // print permutation
        return;
    }

    for (int i = 0; i < n-1; ++i) {         // note loop ends at n-1
        heaps_recursive_permutations(A, n-1);     // all permutations without ith item
        if (is_odd(n)) {
            swap(A[n-1], A[0]);             // swap the 1st item, when n is odd
        }
        else {
            swap(A[n-1], A[i]);             // when even swap the ith item
        }
    }
    // because the loop stops at n-1, we do this once in the end
    heaps_recursive_permutations(A, n-1);
}
```
</details>

## Graphs - Union Find

<details><summary>Graphs - Union-Find API, Connected Components</summary>

The UnionFind interface

```cpp
struct UF {
  UF(int N);                        // graph with N nodes [0, N-1]
  void union(int p, int q);         // connection between p, q
  int find(int p);                  // component id for p

  int count() { return count_; }    // number of components
  bool connected(int p, int q)      // are p and q in the same component
    { return find(p) == find(q); }

private:
  vector<int> id_;              // component ids
  int count_;                   // number of components
};

UF::UF(int N) : id_ {N, 0}, count_ { N }
{
  for (size_t i = 0; i < N; ++i)
  {
    id_[i] = i;
  }
}

void main()
{
  UF uf(N);
  for (auto& [p, q] : G.edges()) {
    uf.union(p, q);
  }
}
```

Implementation: 1) Quick-Find -- `find()` operation is very quick, `O(1)`, but `union()` is very slow `O(N)`

```cpp
int UF::find(int p) {
  return id_[p];
}

void UF::union(int p, int q) {
  int pID = find(p);
  int qID = find(q);

  if (pID == qID) { return; }       // already in the same component

  // change all id's for one component to component id of the other
  for (int i = 0; i < id_.size(); ++i) {
    if (id_[i] == pID) { id_[i] = qID; }
  }
  --count;
}
```

Implementation: 2) Quick-Union -- `find()` is slow `O(tree height)`, but `union()` is quick `O(tree height)`

```cpp
int UF::find(int p) {
  while (p != id_[p]) { p = id_[p]; }
  return p;
}

void UF::union(int p, int q) {
  int pRoot = find(p);
  int qRoot = find(q);

  if (pRoot == qRoot) { return; }       // already in the same component

  id_[pRoot] = qRoot;
  --count;
}
```

Implementation: 3) Weighted quick-union (always attach smaller component as a child of larger components' root).
`find()` is `O(log N)`, and `union()` is also `O(log N)`

```cpp
struct WeightedQuickUnionUF
{
  UF(int N);                        // graph with N nodes [0, N-1]
  void union(int p, int q);         // connection between p, q
  int find(int p);                  // component id for p

  int count() { return count_; }    // number of components
  bool connected(int p, int q)      // are p and q in the same component
    { return find(p) == find(q); }

private:
  vector<int> id_;              // component ids
  int count_;                   // number of components
  vector<int> size_;            // component size (for roots)
};

WeightedQuickUnionUF::WeightedQuickUnionUF(int N) : id_ {N, 0}, count_ { N }, size_ {N, 1}
{
  for (size_t i = 0; i < N; ++i)
  {
    id_[i] = i;
  }
}

int WeightedQuickUnionUF::find(int p) {
  while (p != id_[p]) { p = id_[p]; }
  return p;
}

void UF::union(int p, int q) {
  int pRoot = find(p);
  int qRoot = find(q);

  if (pRoot == qRoot) { return; }       // already in the same component

  if (size_[pRoot] < size_[qRoot]) { id_[pRoot] = qRoot; size_[qRoot] += size_[pRoot]; }
  else                             { id_[qRoot] = pRoot; size_[pRoot] += size_[qRoot]; }
  --count;
}
```

Implementation: 4) Weighted quick-union with path compression -- during `find()` we keep updating component `id_` for nodes encountered to the root node of the component, to flatten the `id_` tree.
`find()` is amortized `~O(1)`, and `union()` is also amortized `~O(1)`

```cpp
int WeightedQuickUnionUFPathCompression::find(int p) {
  int root = p;
  while (root != id_[root]) { root = id_[root]; }

  while (id_[p] != root) { int parent = id_[p]; id_[p] = root; p = parent; } // flatten the tree

  return root;
}
```

Connected Components - DFS

Connected components can also be counted by doing a DFS traversal on the graph

```cpp
int connected_components_dfs(G)
{
  int count = 0;
  int N = G.N;
  vector<bool> visited {N, false};
  vector<int> id {N, 0};

  for (int v = 0; v < N; ++v) {
    if (!visited[v]) {
      ++count;
      dfs_connected(v, count, G, visited, id);
    }
  }

  return count;
}

void dfs_connected(int v, int component_id, Graph& G, vector<bool>& visited, vector<int>& id) {
  visited[v] = true;
  id[v] = component_id;
  for (auto w : G.adj(v)) {
    if (!visited[w]) {
      dfs_connected(w, component_id, G, visited, id);
    }
  }
}
```

</details>

## Graphs - Topological Sort

<details><summary>Graphs - Topological Sort (postorder dfs) on a DAG</summary>

```cpp
vector<int> topological(DirectedAcyclicGraph& G)
{
  int N = G.N;
  vector<bool> visited { N, false };    //
  vector<int> topo_order { N, 0 };      // vertices in topological order
  int count = 0;                        // num vertices placed in topological order

  for (int v = 0; v < N; ++v) {
    dfs_topological_sort(v, count, G, visited, topo_order);
  }

  // assert(G.N == count), otherwise there is a cycle in the graph

  return topo_order;
}

void dfs_topological_sort(int v, int& count, Graph& G, vector<bool>& visited, vector<int>& topo_order) {
  if (visited[v]) { return; }

  visited[v] = true;
  for (auto w : G.adj(v)) {
    if (!visited[w]) {
      dfs_topological_sort(w, count, G, visited, topo_order);
    }
  }

  // post-order steps -- all children nodes have been visited
  ++count;
  topo_order[G.N - count] = v;
}
```

In a topological ordering of the vertices of a dag, all the descendents of a given vertex must
come after that vertex. A recursive depth-first search starting from a vertex v first visits v and then
recursively visits all the descendents of v. If we list the vertices in the order in which they are visited,
they will be in topological order, since every vertex will be listed before its descendents. A single
traversal, starting from a given vertex, will not necessarily visit every vertex in the graph (only the
descendents of the starting vertex). To obtain a topological sort of all vertices, if there are unvisited
vertices after the first traversal, we must do another traversal starting from an unvisited vertex and
visiting only vertices that were not already visited in the first traversal. In the topological order,
all vertices encountered during the second traversal precede all vertices encountered during the first
traversal. Further traversals will be needed if there are still unvisited vertices.

</details>

## Dynamic Programming
<details><summary>dynamic programming</summary>

### Fibonacci
- fibonacci
  ```cpp
  int memoized_fibo(int n) {
    if (n == 0) { return 0; }
    if (n == 1) { return 1; }
    if (F[n] == invalid) {
      F[n] = memoized_fibo(n-1) + memoized_fibo(n-2)
    }
    return F[n];
  }

  /*
  memoized_fibo(5)          -> 8 => F[5]
    memoized_fibo(4)        -> 5 => F[4]
      memoized_fibo(3)      -> 3 => F[3]
        memoized_fibo(2)    -> 2 => F[2]
          memoized_fibo(1)  -> 1
          memoized_fibo(0)  -> 0
        memoized_fibo(1)    -> 1
      memoized_fibo(2)      .. F[2] = 2
        memoized_fibo(1)    x
        memoized_fibo(0)    x
    memoized_fibo(3)        .. F[3] = 3
      memoized_fibo(2)      x
        memoized_fibo(1)    x
        memoized_fibo(0)    x
      memoized_fibo(1)      x
  */
  ```

  ```cpp
  int iterative_fibo(n) {
    vector<int> F {n};
    F[0] = 0;
    F[1] = 1;
    for (int i = 2; i <= n; ++i) {
      F[i] = F[i-1] + F[i-2]; // we don't need to store these all
    }
    return F[n];
  }

  int better_iterative_fibo(n) {
    int prev = 1;   // weird base case F[-1] = 1, so that fibo(0) = 0
    int curr = 0;
    for (int i = 1; i <= n; ++i) {
      int next = curr + prev;
      prev = curr;
      curr = next;
    }
    return curr;
  }
  ```

### LIS

- (LIS) length of the longest increasing subsequence `A[1..n]`

  Example: `LIS(CARBOHYDRATE) = ABORT`, `LIS(EMPATHY) = EMPTY`

  Goal: find the longest sequence of indices

  $$
  1 \le i_1 \lt i_2 \lt \cdots \lt i_l \le n\\
  \text{ s.t. } A[i_k] \lt A[i_{k+1}], \forall k
  $$

  `LISbigger(prev, j)` - given 2 indices `prev < j`, find the longest increasing subsequence of `A[j..n]`, s.t. all its elements are larger than `A[prev]`

  Compute `A[0] = INT_MIN; LISBigger(prev=0, j=1)`. i.e. we are looking for longest subsequence in `A[1..n]`, where `A[i] > INT_MIN` for all `i in [1..n]`

  See UIUC Algo course notes: [CS 473](https://courses.engr.illinois.edu/cs473/fa2019/lectures/lecture6.handout.pdf)

  $$
  \text{LISbigger}(i,j) =
  \left\{
    \begin{array}{ll}
    0 & \text{if } j > n \\
    \text{LISbigger}(i, j+1) & \text{if } A[i] \ge A[j] \\
    \text{max}(\text{LISbigger}(i, j+1), 1+\text{LISbigger}(j, j+1)) & \text{otherwise}
    \end{array}
  \right.
  $$

  Another recurrence, longest increasing subsequence of `A[i..n]` that begins with `A[i]`
  $$
  \text{LISfirst}(i) = 1 + \max \left\{ \text{LISfirst}(j) | j > i \text{ and } A[j] > A[i] \right\}
  $$

  $O(N^2)$ algorithm

  ```cpp
  int dp_lis(vector<int>& A, int N) {
    A[0] = INT_MIN;       // sentinel
    vector<int> LISfirst (N+1, 1);
    for (int i = N; i >= 0; --i) {
      for (int j = i+1; j < N; ++j) {
        if (A[j] > A[i]) {
          LISfirst[i] = max(LISfirst[i], 1 + LISfirst[j]);
        }
      }
    }
    return LISfirst[0]-1;  // don't count the sentinel
  }
  ```

  [16. Dynamic Programming, Part 2: LCS, LIS, Coins](https://youtu.be/KLBCUx1is2c?t=1310)

  ```python
  # https://www.youtube.com/watch?v=KLBCUx1is2c
  # https://learning-modules.mit.edu/materials/index.html?uuid=/course/6/sp20/6.006#materials
  # lecture 16
  def lis(A):
    a = len(A)
    x = [1] * a
    for i in reversed(range(a)):
      for j in range(i, a):
        if A[j] > A[i]:
          x[i] = max(x[i], 1+x[j])
    return max(x)
  ```

### LCS

- (LCS) longest common subsequence, given 2 strings, find longest subsequence, by dropping some characters from the strings, `LCS(A, B)`

  Example: `LCS(HIEROGLYPHOLOGY, MICHAELANGELO) = HELLO / HEGLO / IELLO / IEGLO`, `LCS(HABIT, THEIRS) = HI`

  Subproblem:
  $$
  \text{LCS(A[i:], B[j:])} = \begin{cases}
  \max \left\{ \text{LCS(A[i+1:], B[j:])}, \text{LCS(A[i:], B[j+1:])} \right\} & \text{if } \text{A[i]} \ne \text{B[j]} \\
  1 + \text{LCS(A[i+1:], B[j+1:])} & \text{when A[i] } = \text{B[j]}
  \end{cases}
  $$

  Base cases: $\text{LCS}(A, \empty) = 0, \text{LCS}(\empty, B) = 0$

  Complexity: $O(|A| \times |B|)$

  ```python
  def LCS(A,B):
    a, b = len(A), len(B)
    x = [ [0] * (b+1) for _ in range(a+1) ]
    for i in reversed(range(a)):
      for j in reversed(range(b)):
        if A[i] == B[j]:
          x[i][j] = 1 + x[i+1][j+1]
        else:
          x[i][j] = max(x[i+1][j], x[i][j+1])
    return x[0][0]
  ```

### Alternating Coin Game

- alternating coin game https://www.youtube.com/watch?v=KLBCUx1is2c&t=2564s

  $X(i,j,\text{player}=p)$ is my max value playing from coins $v_i, \ldots, v_j$ where player $p \in \{me, you\}$ moves first

  $$
  X(i, j, me) = \max \left\{ v_i + X(i+1, j, you), v_j + X(i, j-1, you) \right\} \\
  X(i, j, you) = \min \left\{ X(i+1, j, me), v_j + X(i, j-1, me) \right\} \\
  X(i, i, me) = v_i \\
  X(i, i, you) = 0
  $$

  Goal: $X(0, n-1, me)$, in $O(n^2)$

  ```python
  def max_wins(v):
      n = len(v)
      me, you = 0, 1
      X = [ [ [0, 0] for i in range(n) ] for j in range(n) ]
      for i in range(n):
          X[i][i][me] = v[i]
          X[i][i][you] = 0

      for i in reversed(range(n-1)):
          for j in range(i+1, n):
              print(i, j)
              X[i][j][me] = max(v[i] + X[i+1][j][you], v[j] + X[i][j-1][you])
              X[i][j][you] = min(X[i+1][j][me], X[i][j-1][me])

      return X[0][n-1][me]
  print(max_wins([5, 10, 100, 25]))
  # 105
  ```

### More DP problems (unsolved)
- longest common substring, can not drop characters
- longest palindromic sequence, can reorder characters and drop some
- longest repeating subsequence

- edit distance

- subset sum
- equal subset, partition a given set into 2 parts, such that sums of them are equal

- bellman-ford shortest path
- floyd-warshall shortest path

- knapsack (0-1) bounded, given `N` items with `profits`, `weights`. find the number of items that can be put in a knapsack with weight capacity `W`, with max profit
- 0/1 knapsack bounded

- coin change minimum problem
- coin change ways

Eric Demaine:
  - DP1 (merge_sort, fibonacci, bowling),
  - DP2 (LCS, LIS, Alternate Coin Game)

</details>

## Rest

<details><summary>divide and conquer</summary></details>

<details><summary>greedy</summary></details>

<details><summary>network flow</summary></details>

<details><summary>tbd</summary></details>


