# operator==
* chrono[meta header]
* std::chrono[meta namespace]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::chrono {
  constexpr bool operator==(const weekday_last& x, const weekday_last& y) noexcept; // (1) C++20
}
```

## 概要
`weekday_last`同士の等値比較を行う。


## 戻り値
- (1) :

```cpp
return x.weekday() == y.weekday();
```
* weekday()[link weekday.md]


## 例外
投げない


## 備考
- この演算子により、`operator!=`が使用可能になる


## 例
```cpp example
#include <cassert>
#include <chrono>

namespace chrono = std::chrono;

int main()
{
  assert(chrono::Sunday[chrono::last] == chrono::Sunday[chrono::last]);
  assert(chrono::Sunday[chrono::last] != chrono::Monday[chrono::last]);
}
```
* chrono::Sunday[link /reference/chrono/weekday_constants.md]
* chrono::Monday[link /reference/chrono/weekday_constants.md]
* chrono::last[link /reference/chrono/last_spec.md]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 8.0
- [GCC](/implementation.md#gcc): (9.2時点で実装なし)
- [Visual C++](/implementation.md#visual_cpp): (2019 Update 3時点で実装なし)
