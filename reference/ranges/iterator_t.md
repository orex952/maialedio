# iterator_t
* ranges[meta header]
* std::ranges[meta namespace]
* type-alias[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<class R>
  using iterator_t = decltype(ranges::begin(declval<R&>()));
}
```
* declval[link /reference/utility/declval.md]
* ranges::begin[link begin.md]

## 概要

任意のRange型`R`のイテレータの型を取得する。

## 例
```cpp example
#include <ranges>
#include <vector>

int main() {
  static_assert(std::same_as<std::ranges::iterator_t<std::vector<int>>, std::vector<int>::iterator>);
}
```
* std::ranges::iterator_t[color ff0000]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 13.0.0
- [GCC](/implementation.md#gcc): 10.1.0
- [ICC](/implementation.md#icc): ?
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10

## 参照
- [N4861 24 Ranges library](https://timsong-cpp.github.io/cppwp/n4861/ranges)
- [C++20 ranges](https://techbookfest.org/product/5134506308665344)
