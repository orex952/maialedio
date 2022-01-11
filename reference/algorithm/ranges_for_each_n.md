# for_each_n
* algorithm[meta header]
* std::ranges[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<class I, class F>
  using for_each_n_result = in_fun_result<I, F>;

  template<input_iterator I, class Proj = identity, indirectly_unary_invocable<projected<I, Proj>> Fun>
  constexpr for_each_n_result<I, Fun> for_each_n(I first, iter_difference_t<I> n, Fun f, Proj proj = {});
}
```
* input_iterator[link /reference/iterator/input_iterator.md]
* identity[link /reference/functional/identity.md]
* indirectly_unary_invocable[link /reference/iterator/indirectly_unary_invocable.md]
* projected[link /reference/iterator/projected.md]
* iter_difference_t[link /reference/iterator/iter_difference_t.md]
* in_fun_result[link /reference/algorithm/ranges_in_fun_result.md.nolink]

## 概要
範囲の先頭N個の要素に、指定された関数を適用する。

## テンプレートパラメータ制約
- `I`が[`input_iterator`](/reference/iterator/input_iterator.md)である
- `Fun`は`I`を`Proj`で射影した値を[参照で渡すことができる1引数の`invocable`](/reference/iterator/indirectly_unary_invocable.md)である

この他にFunは[`copy_constructible`](/reference/concepts/copy_constructible.md)のモデルであることが要求される。


## 事前条件
`n >= 0`

## 効果
範囲`[first, first + n)` 内の全てのイテレータ `i` に [`invoke`](/reference/functional/invoke.md)`(f, `[`invoke`](/reference/functional/invoke.md)`(proj, *i))` という操作を行う。

このアルゴリズムはその他のアルゴリズムと違い、[`invoke`](/reference/functional/invoke.md)`(proj, *i)` が書き換え可能な参照であれば、関数 `f` の内部でその値を書き換えても構わない。

## 戻り値
`{first + n, std::move(f)}`

## 備考
- 関数 `f` に戻り値がある場合、それは単に無視される

## 例
```cpp example
#include <iostream>
#include <algorithm>
#include <array>

void f(int& x)
{
  x *= 2;
}

int main()
{
  constexpr std::array<int> v = {3, 1, 4, 5, 2};

  // コンテナvの先頭3要素に、関数f()を適用する。
  // 関数f()は要素の変更を行う
  std::ranges::for_each_n(v.begin(), 3, f);

  // コンテナvの先頭3要素に、ラムダ式で記述した関数オブジェクトを適用する
  std::ranges::for_each_n(v.begin(), 3, [](int x) {
    std::cout << x << std::endl;
  });
}
```
* std::ranges::for_each_n[color ff0000]

### 出力
```
6
2
8
```


### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 10.1.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10


## 実装例
```cpp
struct for_each_n_impl {
  template<input_iterator I, class Proj = identity, indirectly_unary_invocable<projected<I, Proj>> Fun>
    requires copy_constructible<Fun>
  constexpr for_each_n_result<I, Fun> operator()(I first, iter_difference_t<I> n, Fun f, Proj proj = {}) {
    for (iter_difference_t<I> i = 0; i < n; ++i) {
      invoke(f, invoke(proj, *first));
      ++first;
    }
    return {move(first), move(f)};
  }
};

inline constexpr for_each_n_impl for_each_n;
```
* input_iterator[link /reference/iterator/input_iterator.md]
* identity[link /reference/functional/identity.md]
* indirectly_unary_invocable[link /reference/iterator/indirectly_unary_invocable.md]
* copy_constructible[link /reference/concepts/copy_constructible.md]
* projected[link /reference/iterator/projected.md]
* iter_difference_t[link /reference/iterator/iter_difference_t.md]
* move[link /reference/utility/move.md]


## 参照
- [N4821 25 Algorithms library](https://timsong-cpp.github.io/cppwp/n4861/algorithms)
