# function template
```cpp
template<typename T>
T max(T a, T b) { return b < a ? a : b; }

// usage
max(10, i)
max(3.4, -7.6)
max("hello", "world")


template<typename T>
auto max(T a, T b) { return b < a ? a : b; }    // return type deduced from return statements

template<typename T1, typename T2>
auto max(T1 a, T2 b) -> decltype(b<a?a:b)         // trailing return type
{ return b < a ? a : b; }

template<typename T1, typename T2>
auto max(T1 a, T2 b) -> typename decay<decltype(b<a?a:b)>::type  // better, in case T1 or T2 is a reference type
{ return b < a ? a : b; }

// function overloads and templates
int max(int a, int b);                          // non-template definition
template<typename T> T max(T a, T b);           // pass by value? let the caller decide

// let the caller decide if wants to pass by reference
max(std::cref(s1), std::cref(s2));

// overloading function templates
template<typename T> int f(T);
template<typename T> int f(T*);         // overload
template<> int f(int);                  // full specialization
```

function templates can not be partially specialized, use overloading for that effect

# class templates
```cpp
template<typename T>
class Stack {
    vector<T> items;

    void push(T const& el);
    ...
};

template<typename T> void Stack<T>::push(T const& el) { ... }

template<>
class Stack<std::string> { ... };          // full specialization

template<typename T>
class Stack<T*> { ... };                   // partial specialization

template<typename T1, typename T2>
class Foo {..};
template<typename T>
class Foo<T, int> {...};                   // partial specialization
template<>
class Foo<string, int> {...}               // full specialization
```

# basics

```cpp
integral_constant<T, v>::value      // v
integral_contant<bool, true>::value // true
true_type::value                    // same as above

is_pointer<T>::value                // true if T is a pointer type
remove_pointer<T>::type             // part of T, without the pointer
add_pointer<T>::type

template<typename T>
void f(T p) {
    if constexpr (is_pointer<T>::value) {
        // code that gets compiled for pointer type
        cout << *p << endl;
    } else {
        // code that gets compiled for non-pointer type
        cout << p << endl;
    }
}

// https://github.com/QBouts/BitsOfQ/blob/master/Metaprogramming/

template<bool condition, typename THEN, typename ELSE>
struct if_;

template<typename THEN, typename ELSE>
struct if_<true, THEN, ELSE> {
    using type = THEN;
};

template<typename THEN, typename ELSE>
struct if_<false, THEN, ELSE> {
    using type = ELSE;
};

template<typename SEARCH, typename TUPLE, size_t start_from=0>
struct contains_type : if_<
    std::is_same<tuple_element_t<start_from, TUPLE>, SEARCH>::value,    // condition
    std::true_type,                                                     // then case
    typename if_<                                                       // else case
        (start_from == std::tuple_size<TUPLE>::value-1),                    // condition
        std::false_type,                                                    // then case
        contains_type<SEARCH, TUPLE, start_from+1>                          // else case
        >::type
>::type {
};

// variadic templates

template<typename LAST>
void printn(LAST&& t)
{
    cout << std::forward<LAST>>(t) << endl;
}

template<typename T0, typename ... T1toN>
void printn(T0&& t, T1toN&&... rest)
{
    cout << std::forward<T0>(t) << ", ";
    printn(std::forward<T1toN>(rest)...);
}

template<typename TUPLE, std::size_t ... indices>
void print_tuple_impl(TUPLE&& t, std::index_sequence<indices...>) {
    printn(std::get<indices>(std::forward<TUPLE>(t))...); // printn(std::get<0>(std::forward<T1>(t)), ...)
}

template<typename TUPLE>
void print_tuple(TUPLE&& t) {
    print_tuple_impl(std::forward<TUPLE>(t), std::make_index_sequence<std::tuple_size<std::remove_reference_t<TUPLE>>::value>{});
}

//

template<typename...>
struct type_list {};

template<typename LIST>
struct empty : std::false_type {};

template<>
struct empty<type_list<>> : std::true_type{};

static_assert(empty<type_list<>>::value);
static_assert(empty<type_list<float>>::value == false);

template<typename LIST>
struct front;

template<typename T0, typename... T1toN>
struct front<type_list<T0, T1toN...>> {
    using type = T0;
};

static_assert(std::is_same_v<front<type_list<int, bool>>::type, int>);

template<typename LIST>
struct pop_front;

template<typename T0, typename ... T1toN>
struct pop_front<type_list<T0, T1toN...>> {
    using type = type_list<T1toN...>;
};

static_assert(std::is_same_v<pop_front<type_list<int, bool, float>>::type, type_list<bool, float>>);

template<typename LIST>
using front_t = typename front<LIST>::type;

template<typename LIST>
using pop_front_t = typename pop_front<LIST>::type;

template<typename LIST>
static constexpr bool empty_v = empty<LIST>::value;             // template variable


template<typename SEARCH, typename LIST>
struct contains_type :
    if_<
        std::is_same_v<SEARCH, front_t<LIST>>,
        std::true_type,
        contains_type<SEARCH, pop_front_t<LIST>>
    >::type {};

template<typename SEARCH>
struct contains_type<SEARCH, type_list<>> : std::false_type {};     // SEARCH is not in empty type_list


type_list<int, bool, double> types;
cout << boolalpha;
cout << contains_type<bool, type_list<>>::value << endl;        // false
cout << contains_type<bool, decltype(types)>::value << endl;    // true
cout << contains_type<float, decltype(types)>::value << endl;   // false

// See: https://github.com/QBouts/BitsOfQ/blob/master/Metaprogramming/
// See: https://www.youtube.com/watch?v=vff3qCO2SQA&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh&index=5
```

Power of a number
```cpp
template<int m, int n>
struct Power {
    constexpr static int const value = m * Power<m, n-1>::value;
};

template<int m>
struct Power<m, 0> {
    constexpr static int const value = 1;
};

static_assert(Power<2, 10>::value == 1024);
```

hybrid, not pure compile time
```cpp
template<int n>
constexpr int power(int m) {
    return m * power<n-1>(m);
}

template<>
constexpr int power<0>(int /* unused */) {
    return 1;
}

static_assert(power<10>(2) == 1024);

int k = power<10>(2); // 1024
```
