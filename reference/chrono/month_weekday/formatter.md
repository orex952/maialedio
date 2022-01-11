# formatter
* chrono[meta header]
* std[meta namespace]
* class[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std {
  template <class charT>
  struct formatter<chrono::month_weekday, charT>;
}
```

## 概要
`month_weekday`クラスに対する[`std::formatter`](/reference/format/formatter.md)クラステンプレートの特殊化。

フォーマットフラグとしては、[`month`](/reference/chrono/month/formatter.md)と[`weekday_indexed`](/reference/chrono/weekday_indexed/formatter.md)で利用可能なフォーマットフラグを使用できる。


## 例
```cpp example
#include <iostream>
#include <chrono>
#include <format>

namespace chrono = std::chrono;

int main() {
  chrono::month_weekday date = chrono::March/chrono::Sunday[1];

  // デフォルトフォーマットはoperator<<と同じ
  std::cout << std::format("1 : {}", date) << std::endl;

  std::cout << std::format("2 : {:%B, %A}", date) << std::endl;
  std::cout << std::format("3 : {:%m, %a}", date) << std::endl;

  // ロケール依存の出力
  std::cout << std::format(std::locale("ja_JP.UTF-8"), "4 : {:%b, %a}", date) << std::endl;
  std::cout << std::format(std::locale("ja_JP.UTF-8"), "5 : {:%b, %A}", date) << std::endl;
}
```
* std::format[link /reference/chrono/format.md]
* std::locale[link /reference/locale/locale.md]
* chrono::March[link /reference/chrono/month_constants.md]

### 出力
```
1 : Mar/Sun[1]
2 : March, Sunday
3 : 03, Sun
4 : 3月, 日
5 : 3月, 日曜日
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
