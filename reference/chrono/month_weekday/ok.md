# ok
* chrono[meta header]
* std::chrono[meta namespace]
* month_weekday[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
constexpr bool ok() const noexcept; // (1) C++20
```

## 概要
`month_weekday`オブジェクトの値が有効な日付の範囲内かを判定する。


## 戻り値
以下の全ての条件を満たす場合にこの関数は`true`を返し、そうでなければ`false`を返す：

- [`month()`](month.md)`.`[`ok()`](/reference/chrono/month/ok.md) `== true`であること
- [`weekday_indexed()`](weekday_indexed.md)`.`[`ok()`](/reference/chrono/weekday_indexed/ok.md) `== true`であること


## 例
```cpp example
#include <cassert>
#include <chrono>

namespace chrono = std::chrono;

int main()
{
  assert((chrono::March/chrono::Sunday[1]).ok()  == true);
  assert((chrono::March/chrono::Sunday[0]).ok()  == false);
}
```
* ok()[color ff0000]
* chrono::March[link /reference/chrono/month_constants.md]
* chrono::Sunday[link /reference/chrono/weekday_constants.md]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 8.0
- [GCC](/implementation.md#gcc): 11.1
- [Visual C++](/implementation.md#visual_cpp): (2019 Update 3時点で実装なし)
