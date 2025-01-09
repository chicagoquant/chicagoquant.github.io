# Jeff Garland, CppCon 2023, Effective Ranges

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
rng::sort(a);  // no begin-end
fmt::print("{}", a);
// {1, 2, 3, 4, 5, 6};
```

# find-if
```cpp
auto is_six = [](int i) -> bool { return i == 6; };
auto it = rng::find_if(a, is_six);  // no begin-end
if (it != rng::end(a))
{
  std::print("i: {}", *i); // i: 6
}
```

# filter-view
```cpp
using std::views::filter;
auto divisible_by_3 = filter([](int i) -> bool { return i%3 == 0; });
std::print("{}", a | divisible_by_3); // {3, 6}
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
- views = ranges with lazy evaluation, we control the iteration, view does the calculation on our demand

```

* c++2x Range Algorithms
** queries :~find~, ~find_if~, ~find_if_not~
** queries : ~find_last~, ~find_last_if~, ~find_last_if_not~ (23)
** queries : ~adjacent_find~
** queries :~any_of~, ~all_of~, ~none_of~
** queries: ~contains~, ~contains_subrange~ (23)
** queries:~is_partioned~
** queries:~is_sorted~, ~is_sorted_until~
** queries: ~lower_bound~, ~upper_bound~, ~partion_point~
** queries: ~clamp~
** queries: ~mismatch~
** queries:~starts_with~, ~ends_with~ (23)
** sampling :~copy~, ~copy_if~, ~copy_n~                               
** sampling :~rotate_copy~, ~unique_copy~                              
** sampling : ~stride~,~sample~, ~take~                                
** modifiers: merge, inplace_merge~                                    
** modifiers: ~move~, ~move_backward~                                  
** modifiers: ~partition~, ~partition_copy~                            
** modifiers: ~replace~,~replace_if~, ~replace_copy~, ~replace_copy_if~
** modifiers:~remove~,~remove_if~, ~remove_copy~, ~remove_copy_if~     
** modifiers: ~reverse~
** modifiers: ~shuffle~,~sort~
** modifiers: ~shift_left~, ~shift_right~ (23)
** modifiers: ~transform~, ~for_each~, ~for_each_n~
** modifiers: ~unique~
** modifiers: ~unitialized_value_construct~, ~unitialized_copy~
** calculation: ~count~, ~count_if~
** calculation: ~fold_left~, ~fold_left_first~, ~fold_right~, ~fold_right_last~ (23) ** calculation: ~min~, ~max~, ~minmax~
** generation : ~iota~ (23)
** generation : ~generate~
** generation : ~next_permutation~, ~prev_permutation~
```
