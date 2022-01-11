# operator-=
* chrono[meta header]
* std::chrono[meta namespace]
* day[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
constexpr day& operator-=(const days& m) noexcept; // (1) C++20
```

## 概要
`day`の値に対して減算の複合代入を行う。

パラメータの型が、本クラスである`day`ではなく、日単位の時間間隔を表す[`days`](/reference/chrono/duration_aliases.md)であることに注意。


## 効果
- (1) : `*this = *this - d`


## 戻り値
- (1) : `*this`


## 例外
投げない


## 例
```cpp example
#include <cassert>
#include <chrono>

namespace chrono = std::chrono;

int main()
{
  chrono::day d{31};

  d -= chrono::days{2};
  assert(static_cast<unsigned int>(d) == 29);
}
```

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
