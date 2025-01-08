# Jeff Garland, CppCon 2023, Effective Ranges

# namespace
```
std
  ranges
    views
      filter
  views = std::ranges::views
```

# sort
```
std::array<int, 6> a {4, 3, 1, 6, 2, 5};
rng::sort(a);  // no begin-end
std::print("{}", a);
// {1, 2, 3, 4, 5, 6};
```

# find-if
```
auto is_six = [](int i) -> bool { return i == 6; };
auto it = rng::find_if(a, is_six);  // no begin-end
if (it != rng::end(a))
{
  std::print("i: {}", *i); // i: 6
}
```

# filter-view
```
using std::views::filter;
auto divisible_by_3 = filter([](int i) -> bool { return i%3 == 0; });
std::print("{}", a | divisible_by_3); // {3, 6}
```

# keywords: range, range-algo, views, range-adapter
```
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
