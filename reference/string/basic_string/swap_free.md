# swap (非メンバ関数)
* string[meta header]
* std[meta namespace]
* function template[meta id-type]

```cpp
namespace std {
    template <class CharT, class Traits, class Allocator>
  void swap(basic_string<CharT, Traits, Allocator>& x,
            basic_string<CharT, Traits, Allocator>& y);

  template <class CharT, class Traits, class Allocator>
  void swap(basic_string<CharT, Traits, Allocator>& x,
            basic_string<CharT, Traits, Allocator>& y)
    noexcept(noexcept(lhs.swap(rhs)));                 // C++17
}
```

## 概要
2つの`basic_string`オブジェクトを入れ替える


## 効果
`x.`[`swap`](swap.md)`(y)`


## 戻り値
なし


## 例
```cpp example
#include <iostream>
#include <string>

int main()
{
  std::string a = "hello";
  std::string b = "world";

  std::swap(a, b);

  std::cout << a << std::endl;
  std::cout << b << std::endl;
}
```
* std::swap[color ff0000]

### 出力
```
world
hello
```

## 参照
- [N4258 Cleaning-up noexcept in the Library, Rev 3](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4258.pdf)
    - `noexcept` 追加の経緯となる提案文書

