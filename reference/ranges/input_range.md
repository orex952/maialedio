# input_range
* ranges[meta header]
* concept[meta id-type]
* std::ranges[meta namespace]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<class T>
  concept input_range = range<T> && input_iterator<iterator_t<T>>;
}
```
* range[link range.md]
* input_iterator[link /reference/iterator/input_iterator.md]
* iterator_t[link iterator_t.md]

## 概要
`input_range`は、イテレータが[`input_iterator`](/reference/iterator/input_iterator.md)であるRangeを表すコンセプトである。

## モデル
型`T`が`input_range`のモデルとなるのは、`T`が[`range`](range.md)のモデルであり、かつそのイテレータが[`input_iterator`](/reference/iterator/input_iterator.md)のモデルである場合である。

## 例
```cpp example
#include <ranges>
#include <forward_list>
#include <iostream>

int main() {
  using namespace std;
  // istream_viewはforward_rangeではなく、input_range
  static_assert(!ranges::forward_range<decltype(ranges::istream_view<int>(cin))>);
  static_assert(ranges::input_range<decltype(ranges::istream_view<int>(cin))>);
}
```
* ranges::input_range[color ff0000]
* ranges::forward_range[link forward_range.md]
* ranges::istream_view[link basic_istream_view.md]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 13.0.0
- [GCC](/implementation.md#gcc): 10.1.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10

## 参照
- [N4861 24 Ranges library](https://timsong-cpp.github.io/cppwp/n4861/ranges)
- [C++20 ranges](https://techbookfest.org/product/5134506308665344)
