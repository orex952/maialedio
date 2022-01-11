# cmp_equal
* utility[meta header]
* std[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std {
  template <class T, class U>
  constexpr bool cmp_equal(T t, U u) noexcept;
}
```

## 概要
整数を安全に等値比較する。

この関数は、型`T`と型`U`がそれぞれ符号付き整数と符号なし整数のどちらであったとしても、安全に比較できる関数である。以下のように符号付き整数のインデックス変数と符号なし整数の配列要素数の比較によってコンパイラに警告が出力されてしまうような状況で使用できる：

```cpp
std::vector<X> v;

// 警告：式`i < v.size()`で、符号付き整数と符号なし整数の間で比較しようとした
for (int i = 0; i < v.size(); ++i) {}
```


## 適格要件
- 型`T`と型`U`はどちらも、符号なし整数型もしくは符号付き整数型であること


## 効果
以下と等価：

```cpp
using UT = make_unsigned_t<T>;
using UU = make_unsigned_t<U>;
if constexpr (is_signed_v<T> == is_signed_v<U>)
  return t == u;
else if constexpr (is_signed_v<T>)
  return t < 0 ? false : UT(t) == u;
else
  return u < 0 ? false : t == UU(u);
```
* make_unsigned_t[link /reference/type_traits/make_unsigned.md]
* is_signed_v[link /reference/type_traits/is_signed.md]


## 例外
投げない


## 例
```cpp example
#include <iostream>
#include <utility>

int main() {
  std::cout << std::boolalpha;

  // 符号付き整数型同士の比較
  std::cout << std::cmp_equal(1, 1) << std::endl;

  // 符号なし整数型同士の比較
  std::cout << std::cmp_equal(1u, 1u) << std::endl;

  // 符号付き整数型と符号なし整数型の比較
  std::cout << std::cmp_equal(1, 1u) << std::endl;
  std::cout << std::cmp_equal(1u, 1) << std::endl;
}
```
* std::cmp_equal[color ff0000]

### 出力
```
true
true
true
true
```

## バージョン
### 言語
- C++20

## 処理系
- [Clang](/implementation.md#clang):
- [GCC](/implementation.md#gcc): 10.1
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 7


## 参照
- [P0586R2 Safe integral comparisons](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p0586r2.html)
