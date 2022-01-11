# operator%=
* chrono[meta header]
* std::chrono[meta namespace]
* duration[meta class]
* function[meta id-type]
* cpp11[meta cpp]

```cpp
duration& operator%=(const rep& rhs);                // (1) C++11
constexpr duration& operator%=(const rep& rhs);      // (1) C++17

duration& operator%=(const duration& rhs);           // (2) C++11
constexpr duration& operator%=(const duration& rhs); // (2) C++17
```

## 概要
現在の値を`rhs`で割った余りを求める

## 効果
- `rep_ %= rhs`
- `rep_ %= rhs.count()`

## 戻り値
`*this`

## 例
```cpp example
#include <iostream>
#include <chrono>

using std::chrono::duration;
using std::micro;

int main()
{
  {
    duration<int, micro> d(9);

    d %= 2;
    std::cout << d.count() << std::endl;
  }
  {
    duration<int, micro> d1(9);
    duration<int, micro> d2(2);

    d1 %= d2;
    std::cout << d1.count() << std::endl;
  }
}
```
* micro[link /reference/ratio/si_prefix.md]
* count()[link count.md]

### 出力
```
1
1
```

## バージョン
### 言語
- C++11

### 処理系
- [GCC](/implementation.md#gcc): 4.5.1, 4.6.1
- [Visual C++](/implementation.md#visual_cpp): 2012, 2013, 2015


## 参照
- [P0505R0 Wording for GB 50](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0505r0.html)
