# max
* latch[meta header]
* std[meta namespace]
* latch[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
static constexpr ptrdiff_t max() noexcept;
```
* ptrdiff_t[link /reference/cstddef/ptrdiff_t.md]

## 概要
処理系がサポートするカウンタ最大値


## 戻り値
処理系がサポートするカウンタの最大値を返す。


## 例外
投げない


## 例
```cpp example
#include <iostream>
#include <latch>

int main()
{
  std::cout << std::latch::max() << std::endl;
}
```
* max()[color ff0000]

### 出力例
```
9223372036854775807
```


## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 11.0
- [GCC](/implementation.md#gcc): ??
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): ??
