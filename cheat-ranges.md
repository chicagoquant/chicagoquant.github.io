# Jeff Garland, CppCon 2023, Effective Ranges
- [https://www.youtube.com/watch?v=QoaVRQvA6hI&t=2436s](https://www.youtube.com/watch?v=QoaVRQvA6hI&t=2436s)
- [https://github.com/JeffGarland/range_by_example](https://github.com/JeffGarland/range_by_example)
- [https://github.com/CppCon/CppCon2023/blob/main/Presentations/effective_ranges_cppcon2023.pdf](https://github.com/CppCon/CppCon2023/blob/main/Presentations/effective_ranges_cppcon2023.pdf)

# namespace
```
std
  ranges
    views
      filter
  views = std::ranges::views
```

#includes
```cpp
#include <fmt/ranges.h>
#include <array>
#include <ranges>
```

# sort
```cpp
std::array<int, 6> a {4, 3, 1, 6, 2, 5};
rng::sort(a);        // no begin-end     | std::sort(a.begin(), a.end());
fmt::print("{}", a); // fmt/std::print   | for (auto v : a) { cout << v << endl; }
// [1, 2, 3, 4, 5, 6]
```

# find-if
```cpp
auto is_six = [](int i) -> bool { return i == 6; };
auto it = rng::find_if(a, is_six);  // no begin-end
if (it != rng::end(a))
{
  std::print("i: {}", *it); // i: 6
}
```

# filter-view
```cpp
using std::views::filter;
auto divisible_by_3 = filter([](int i) -> bool { return i%3 == 0; });
fmt::print("{}", a | divisible_by_3); // [3, 6]
```

# keywords: range, range-algo, views, range-adapter
```cpp
boost::flat_map<string, int> fm;
fm["world"] = 2;
fm["hello"] = 1;
std::print("{}", fm); // {"hello": 1, "world": 2}

for (auto [k, v] : rng::reverse_view{fm})
{
  std::print("{}: {}", k, v);
}
// world: 2
// hello: 1

std::print("{}", rng::reverse_view{fm}); // {"world": 2, "hello": 1}
```

- STL algorithm - iteration of the range is controlled by the algorithm, we cant control the iteration
- range - can be iterated over
  - iterator pair, e.g rbegin(), rend()
  - an object with begin(), end(), that returns iterators
  - an iterator and a sentinel (end)
  - sentinel and iterator can be different types,
    for ranges typeof(begin()) != typeof(end())
  - example: stl containers, container adaptors (queue, priority-q, stack), strings, string_view, directory-iterator, stream-iterator, regex iter, span, mdspan
- range algo - takes a range
- views - lazy range, cheap to copy, ranges with lazy evaluation, we control the iteration, view does the calculation on our demand
- range adaptor - convert a range into a view

```

* c++2x Range Algorithms
** queries :~find~, ~find_if~, ~find_if_not~
** queries : ~find_last~, ~find_last_if~, ~find_last_if_not~ (23)
** queries : ~adjacent_find~
** queries :~any_of~, ~all_of~, ~none_of~
** queries: ~contains~, ~contains_subrange~ (23)
** queries:~is_partitioned~
** queries:~is_sorted~, ~is_sorted_until~
** queries: ~lower_bound~, ~upper_bound~, ~partition_point~
** queries: ~clamp~
** queries: ~mismatch~
** queries:~starts_with~, ~ends_with~ (23)
** sampling :~copy~, ~copy_if~, ~copy_n~                               
** sampling :~rotate_copy~, ~unique_copy~                              
** sampling : ~stride~, ~sample~, ~take~                                
** modifiers: ~merge~, ~inplace_merge~                                    
** modifiers: ~move~, ~move_backward~                                  
** modifiers: ~partition~, ~partition_copy~                            
** modifiers: ~replace~, ~replace_if~, ~replace_copy~, ~replace_copy_if~
** modifiers: ~remove~, ~remove_if~, ~remove_copy~, ~remove_copy_if~     
** modifiers: ~reverse~
** modifiers: ~shuffle~, ~sort~
** modifiers: ~shift_left~, ~shift_right~ (23)
** modifiers: ~transform~, ~for_each~, ~for_each_n~
** modifiers: ~unique~
** modifiers: ~uninitialized_value_construct~, ~uninitialized_copy~
** calculation: ~count~, ~count_if~
** calculation: ~fold_left~, ~fold_left_first~, ~fold_right~, ~fold_right_last~ (23)
** calculation: ~min~, ~max~, ~minmax~
** generation : ~iota~ (23)
** generation : ~generate~
** generation : ~next_permutation~, ~prev_permutation~
```

# godbolt
- 2-4 sort [https://godbolt.org/z/o478PEMff](https://godbolt.org/z/o478PEMff)
- 2-6 find-if [https://godbolt.org/z/4KEM3W939](https://godbolt.org/z/4KEM3W939)
- 2-7 filter-view [https://godbolt.org/z/bnchn9jaf](https://godbolt.org/z/bnchn9jaf)
- 3-6 flat-map [https://godbolt.org/z/Mdqh58zrM](https://godbolt.org/z/Mdqh58zrM)
- 4-6 projection [https://godbolt.org/z/8cvoEvd11](https://godbolt.org/z/8cvoEvd11)
- 4-8 find-last [https://godbolt.org/z/8KPjqYrG1](https://godbolt.org/z/8KPjqYrG1)
- 5-6 range-adaptor [https://godbolt.org/z/1863ce6sW](https://godbolt.org/z/1863ce6sW)
- 5-9 [https://godbolt.org/z/G5PE614ff](https://godbolt.org/z/G5PE614ff)
- [https://godbolt.org/z/c137bM8f4](https://godbolt.org/z/c137bM8f4)
- 6-3 cartesian-product [https://godbolt.org/z/rYehsTMxY](https://godbolt.org/z/rYehsTMxY)
- 7-5 ranges-to [https://godbolt.org/z/c137bM8f4](https://godbolt.org/z/c137bM8f4)
- 7-6 ranges-to [https://godbolt.org/z/bd558h47j](https://godbolt.org/z/bd558h47j)
- 8-2 sum-of-sqr [https://godbolt.org/z/qPh1hjdzo](https://godbolt.org/z/qPh1hjdzo)

