# formatter
* chrono[meta header]
* std[meta namespace]
* class[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std {
  template <class charT>
  struct formatter<chrono::weekday_last, charT>;
}
```

## 概要
`weekday_last`クラスに対する[`std::formatter`](/reference/format/formatter.md)クラステンプレートの特殊化。

フォーマットフラグとしては、以下を使用できる：

| フォーマットフラグ | 説明 |
|--------------------|------|
| `%a` | ロケール依存の曜日の略称 |
| `%A` | ロケール依存の曜日の完全名 |
| `%u` | 10進数での月曜を1とするISO曜日番号 (1-7) |
| `%Ou` | ロケール依存の`%u`の異なる表現 |
| `%w` | 10進数での日曜を0とするISO曜日番号 (0-6) |


## 例
```cpp example
#include <iostream>
#include <chrono>
#include <format>

namespace chrono = std::chrono;

int main()
{
  chrono::weekday_last wl = chrono::Sunday[chrono::last];

  // デフォルトフォーマットはoperator<<と同じ
  std::cout << std::format("{}", wl) << std::endl;

  std::cout << std::format("{:%a}", wl) << std::endl; // 曜日の略称
  std::cout << std::format("{:%A}", wl) << std::endl; // 曜日の完全名

  // ロケール依存の出力
  std::cout << std::format(std::locale("ja_JP.UTF-8"), "{}", wl) << std::endl;
  std::cout << std::format(std::locale("ja_JP.UTF-8"), "{:%a}", wl) << std::endl;
  std::cout << std::format(std::locale("ja_JP.UTF-8"), "{:%A}", wl) << std::endl;
}
```
* std::format[link /reference/chrono/format.md]
* chrono::Sunday[link /reference/chrono/weekday_constants.md]
* std::locale[link /reference/locale/locale.md]

### 出力
```
Sun[last]
Sun
Sunday
日[last]
日
日曜日
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
