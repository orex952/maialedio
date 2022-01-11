# operator+=
* chrono[meta header]
* std::chrono[meta namespace]
* duration[meta class]
* function[meta id-type]
* cpp11[meta cpp]

```cpp
duration& operator+=(const duration& d);           // C++11
constexpr duration& operator+=(const duration& d); // C++17
```

## 概要
現在の値に、他の`duration`の値を足す


## 効果
`rep_ += d.`[`count`](/reference/chrono/duration/count.md)`()`


## 戻り値
`*this`


## 例
```cpp example
#include <iostream>
#include <chrono>

using std::chrono::duration;
using std::nano; using std::micro;

int main()
{
  duration<int, nano> d1(2);
  duration<int, micro> d2(3);

  d1 += d2;

  std::cout << d1.count() << std::endl;
}
```
* nano[link /reference/ratio/si_prefix.md]
* micro[link /reference/ratio/si_prefix.md]
* count()[link count.md]

### 出力
```
3002
```

## バージョン
### 言語
- C++11


### 処理系
- [GCC](/implementation.md#gcc): 4.5.1, 4.6.1
- [Visual C++](/implementation.md#visual_cpp): 2012, 2013, 2015


## 参照
- [P0505R0 Wording for GB 50](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0505r0.html)
