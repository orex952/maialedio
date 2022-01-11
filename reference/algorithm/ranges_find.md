# find
* algorithm[meta header]
* std::ranges[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<input_iterator I, sentinel_for<I> S, class T, class Proj = identity>
    requires indirect_binary_predicate<ranges::equal_to, projected<I, Proj>, const T*>
  constexpr I find(I first, S last, const T& value, Proj proj = {});

  template<input_range R, class T, class Proj = identity>
    requires indirect_binary_predicate<ranges::equal_to, projected<iterator_t<R>, Proj>, const T*>
  constexpr borrowed_iterator_t<R> find(R&& r, const T& value, Proj proj = {});
}
```
- input_iterator[link /reference/iterator/input_iterator.md]
- sentinel_for[link /reference/iterator/sentinel_for.md]
- borrowed_iterator_t[link /reference/ranges/borrowed_iterator_t.md]
- iterator_t[link /reference/ranges/iterator_t.md]
- identity[link /reference/functional/identity.md]
- indirect_binary_predicate[link /reference/iterator/indirect_binary_predicate.md]
- ranges::equal_to[link /reference/functional/ranges_equal_to.md]
- input_range[link /reference/ranges/input_range.md]
- projected[link /reference/iterator/projected.md]

## 概要
指定された値を検索する。


## 戻り値
`[first,last)` あるいは `r` 内のイテレータ i について、[`invoke`](/reference/functional/invoke.md)`(proj, *i) == value` であるような最初のイテレータを返す。そのようなイテレータが見つからなかった場合は `last` を返す。

## 計算量
最大で `last - first` 回比較を行う


## 例
```cpp example
#include <algorithm>
#include <iostream>
#include <array>

int main() {
  constexpr std::array v = { 3, 1, 4 };
  constexpr auto result = std::ranges::find(v, 1);
  if (result == v.end()) {
    std::cout << "not found" << std::endl;
  } else {
    std::cout << "found: " << *result << std::endl;
  }
}
```
* std::ranges::find[color ff0000]

### 出力
```
found: 1
```


## 実装例
```cpp
struct find_impl {
  template<input_iterator I, sentinel_for<I> S, class T, class Proj = identity>
    requires indirect_binary_predicate<ranges::equal_to, projected<I, Proj>, const T*>
  constexpr I operator()(I first, S last, const T& value, Proj proj = {}) {
    for ( ; first != last; ++first)
      if (*first == value) return first;
    return last;
  }

  template<input_range R, class T, class Proj = identity>
    requires indirect_binary_predicate<ranges::equal_to, projected<iterator_t<R>, Proj>, const T*>
  constexpr borrowed_iterator_t<R> operator()(R&& r, const T& value, Proj proj = {}) {
    return (*this)(begin(r), end(r), value, ref(proj));
  }
};

inline constexpr find_impl find;
```
* sentinel_for[link /reference/iterator/sentinel_for.md]
* identity[link /reference/functional/identity.md]
* indirect_binary_predicate[link /reference/iterator/indirect_binary_predicate.md]
* ranges::equal_to[link /reference/functional/ranges_equal_to.md]
* projected[link /reference/iterator/projected.md]
* invoke[link /reference/functional/invoke.md]
* begin[link /reference/ranges/begin.md]
* end[link /reference/ranges/end.md]
* ref[link /reference/functional/ref.md]

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 10.1.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10

## 参照
- [N4821 25 Algorithms library](https://timsong-cpp.github.io/cppwp/n4861/algorithms)
