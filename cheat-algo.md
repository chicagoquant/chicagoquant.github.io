
# string search

`search(pattern, s)`

idea: shift of the pattern in case of a mismatch
- prepare a table d used in case of shifting of the pattern in the string
- do string search using table

algos:
- Knuth Morris Pratt (KMP) - forward pattern matching
- Boyer Moore - backward pattern matching
- Rabin Karp - uses a rolling hash function (eg. rabin fingerprint hash)


# recursion

- iteration, reverse a linked list (recursive)
- breaking into subproblems, tower of hanoi
- selection (combinations), n-queens, knapsack, word break, phonespell
- ordering (permutations)
- divide and conquer (generate all bsts for a set of items)
- depth first search (search in a tree, knight tour)

# must know skills

- understand the core algorithm itself, make modification, ways you can adapt it
- 1 data structure manipulation (how to use it)
- 2 searching, dfs, bfs, in a tree, in a graph
- 3 combinations and permutations, use it for brute force
- 4 sorting, quick, merge, insertion sort, partition, quick-select
- 5 binary search, in a rotated array identify pivot point
- 6 topological sort, scheduling problem, prerequisite
- 7 recursion
- 8 dynamic programming