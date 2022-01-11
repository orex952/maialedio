# operator<<
* chrono[meta header]
* std::chrono[meta namespace]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::chrono {
  template <class charT, class traits>
  std::basic_ostream<charT, traits>&
    operator<<(std::basic_ostream<charT, traits>& os, const weekday_last& wdl); // (1) C++20
}
```

## 概要
`weekday_last`オブジェクトを出力ストリームに出力する。


## 戻り値
便宜上のリテラルキャスト`STATICALLY-WIDEN`を導入する。`STATICALLY-WIDEN<charT>("...")`は、`charT`が`char`である場合は`"..."`、`charT`が`wchar_t`である場合は`L"..."`を意味する。

- (1) : 以下と等価：
    ```cpp
    return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{:L}[last]"), wdl.weekday());
    ```
    * format[link /reference/chrono/format.md]
    * wdl.weekday()[link weekday.md]
    * os.getloc()[link /reference/ios/ios_base/getloc.md]


## 例
```cpp example
#include <iostream>
#include <chrono>

namespace chrono = std::chrono;

int main()
{
  std::cout << chrono::Sunday[chrono::last] << std::endl;
}
```
* chrono::Sunday[link /reference/chrono/weekday_constants.md]
* chrono::last[link /reference/chrono/last_spec.md]

### 出力
```
Sun[last]
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


## 参照
- [P2372R1 Fixing locale handling in chrono formatters](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p2372r1.html)
    - この提案文書はC++20の策定後に採択されたが、実装が追いついていない時期の採択だったために、C++20の仕様として扱われる

