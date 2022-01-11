# formatter
* chrono[meta header]
* std[meta namespace]
* class[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std {
  template <class charT>
  struct formatter<chrono::year_month, charT>;
}
```

## 概要
`year_month_day`クラスに対する[`std::formatter`](/reference/format/formatter.md)クラステンプレートの特殊化。

[`month`](/reference/chrono/month/formatter.md)と[`year`](/reference/chrono/year/formatter.md)で利用可能なフォーマットフラグを使用できる。


## 例
```cpp example
#include <iostream>
#include <chrono>
#include <format>

namespace chrono = std::chrono;
using namespace std::chrono_literals;

int main() {
  chrono::year_month date = 2020y/3;

  // デフォルトフォーマットはoperator<<と同じ
  std::cout << std::format("1 : {}", date) << std::endl;
  std::cout << std::format("2 : {:%Y/%b}", date) << std::endl;
  std::cout << std::format("3 : {:%Y年%m月}", date) << std::endl;
}
```
* std::format[link /reference/chrono/format.md]
* 2020y[link /reference/chrono/year/op_y.md]

### 出力
```
1 : 2020/Mar
2 : 2020/Mar
3 : 2020年03月
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): (9.0時点で実装なし)
- [GCC](/implementation.md#gcc): (9.2時点で実装なし)
- [Visual C++](/implementation.md#visual_cpp): (2019 Update 3時点で実装なし)


## 関連項目
- [chronoの`std::format()`](/reference/chrono/format.md) (フォーマットの詳細)
