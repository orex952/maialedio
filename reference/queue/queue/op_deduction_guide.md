# 推論補助
* queue[meta header]
* std[meta namespace]
* queue[meta class]
* cpp17[meta cpp]

```cpp
namespace std {
  template <class Container>
  queue(Container)
    -> queue<typename Container::value_type, Container>; // (1)

  template<class InputIterator>
  queue(InputIterator, InputIterator)
    -> queue<<InputIterator>>;  // (2) C++23

  template <class Container, class Allocator>
  queue(Container, Allocator)
    -> queue<typename Container::value_type, Container>; // (3)

  template<class InputIterator, class Allocator>
  queue(InputIterator, InputIterator, Allocator)
    -> queue<iter-value-type<InputIterator>, deque<iter-value-type<InputIterator>,
             Allocator>>;  // (4) C++23
}
```
* iter-value-type[italic]

## 概要
`std::queue`クラステンプレートの型推論補助。元となるコンテナから推論する。


## 例
```cpp example
#include <iostream>
#include <queue>
#include <type_traits>

int main()
{
  std::deque d = {1, 2, 3};

  // 元となるコンテナから推論
  std::queue que {d};
  static_assert(std::is_same_v<
    decltype(que),
    std::queue<int>
  >);

  while (!que.empty()) {
    std::cout << que.front() << std::endl;
    que.pop();
  }
}
```
* que.empty()[link empty.md]
* que.front()[link front.md]
* que.pop()[link pop.md]

### 出力
```
1
2
3
```


## バージョン
### 言語
- C++17

### 処理系
- [Clang](/implementation.md#clang):
- [GCC](/implementation.md#gcc):
- [Visual C++](/implementation.md#visual_cpp): ??


## 関連項目
- [C++17 クラステンプレートのテンプレート引数推論](/lang/cpp17/type_deduction_for_class_templates.md)


## 参照
- [P0433R2 Toward a resolution of US7 and US14: Integrating template deduction for class templates into the standard library](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0433r2.html)
- [P1425R4 Iterators pair constructors for stack and queue](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p1425r4.pdf)
    - C++23でのイテレータペアへの対応
