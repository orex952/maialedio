# none_of
* algorithm[meta header]
* std::ranges[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<input_iterator I, sentinel_for<I> S, class Proj = identity, indirect_unary_predicate<projected<I, Proj>> Pred>
  constexpr bool none_of(I first, S last, Pred pred, Proj proj = {}); // (1)

  template<input_range R, class Proj = identity, indirect_unary_predicate<projected<iterator_t<R>, Proj>> Pred>
  constexpr bool none_of(R&& r, Pred pred, Proj proj = {});           // (2)
}
```
* input_iterator[link /reference/iterator/input_iterator.md]
* sentinel_for[link /reference/iterator/sentinel_for.md]
* identity[link /reference/functional/identity.md]
* indirect_unary_predicate[link /reference/iterator/indirect_unary_predicate.md]
* input_range[link /reference/ranges/input_range.md]
* projected[link /reference/iterator/projected.md]

## 概要
範囲の全ての要素が条件を満たさないかを判定する。

## テンプレートパラメータ制約
- (1):
    - `I`が[`input_iterator`](/reference/iterator/input_iterator.md)である
    - `S`が[`I`に対する番兵](/reference/iterator/sentinel_for.md)である
    - `Pred`は`I`を`Proj`で射影した値を[参照で渡すことができる1引数の述語](/reference/iterator/indirect_unary_predicate.md)である
- (2):
    - `R`が[`input_range`](/reference/ranges/input_range.md)である
    - `Pred`は`R`のイテレータを`Proj`で射影した値を[参照で渡すことができる1引数の述語](/reference/iterator/indirect_unary_predicate.md)である

## 戻り値
`[first,last)` あるいは `r` が空であったり、範囲内の全てのイテレータ `i` について [`invoke`](/reference/functional/invoke.md)`(pred, `[`invoke`](/reference/functional/invoke.md)`(proj, *i))` が `false` である場合は `true` を返し、そうでない場合は `false` を返す。


## 計算量
最大で `last - first` 回 `pred` を実行する。


### 備考
この関数は

```cpp
all_of(first, last, not_fn(pred));
```
* all_of[link /reference/algorithm/ranges_all_of.md]
* not_fn[link /reference/functional/not_fn.md]

とほぼ同じであるが、全ての要素が条件を満たしていないということを明示したい場合は `none_of()` を使う方が意図が伝わりやすい。


## 例
```cpp example
#include <algorithm>
#include <iostream>
#include <array>

int main() {
  constexpr std::array v = { 3, 1, 4 };

  std::cout << std::boolalpha;

  // 全ての要素が 3 以上であるか
  constexpr bool result1 = std::ranges::none_of(v, [](int x) { return x < 3; });
  std::cout << result1 << std::endl;

  // 全ての要素が 0 以外であるか
  constexpr bool result2 = std::ranges::none_of(v, [](int x) { return x == 0; });
  std::cout << result2 << std::endl;
}
```
* std::ranges::none_of[color ff0000]

### 出力
```
false
true
```

## 実装例
```cpp
struct none_of_impl {
  template<input_iterator I, sentinel_for<I> S, class Proj = identity, indirect_unary_predicate<projected<I, Proj>> Pred>
  constexpr bool operator()(I first, S last, Pred pred, Proj proj = {}) {
    for ( ; first != last; ++first)
      if (invoke(pred, invoke(proj, *first))) return false;
    return true;
  }

  template<input_range R, class Proj = identity, indirect_unary_predicate<projected<iterator_t<R>, Proj>> Pred>
  constexpr bool operator()(R&& r, Pred pred, Proj proj = {}) {
    return (*this)(begin(r), end(r), ref(pred), ref(proj));
  }
};

inline constexpr none_of_impl none_of;
```
* input_iterator[link /reference/iterator/input_iterator.md]
* sentinel_for[link /reference/iterator/sentinel_for.md]
* iterator_t[link /reference/ranges/iterator_t.md]
* identity[link /reference/functional/identity.md]
* indirect_unary_predicate[link /reference/iterator/indirect_unary_predicate.md]
* input_range[link /reference/ranges/input_range.md]
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


## 関連項目
- [`none_of`](/reference/algorithm/none_of.md)
- [`ranges::all_of`](/reference/algorithm/ranges_all_of.md)
- [`ranges::any_of`](/reference/algorithm/ranges_any_of.md)


## 参照
- [N4821 25 Algorithms library](https://timsong-cpp.github.io/cppwp/n4861/algorithms)
