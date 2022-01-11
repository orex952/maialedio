# empty
* set[meta header]
* std[meta namespace]
* multiset[meta class]
* function[meta id-type]

```cpp
bool empty() const;                        // C++03
bool empty() const noexcept;               // C++11
[[nodiscard]] bool empty() const noexcept; // C++20
```

## 概要
コンテナが空かどうかをテストする。  
`multiset` コンテナが空（[`size()`](size.md) が 0）の場合に `true` を返す。

この関数はコンテナ内のコンテンツを変化させない。コンテンツをクリアするには [`clear()`](clear.md) メンバを使う。


## 戻り値
コンテナサイズが 0 のときに `true`, そうでないときに `false`。


## 計算量
定数時間。


## 例
```cpp example
#include <iostream>
#include <set>

int main ()
{
  std::multiset<int> c;

  std::cout << c.empty() << std::endl;

  c.insert(42);

  std::cout << c.empty() << std::endl;
}
```
* empty()[color ff0000]
* c.insert[link insert.md]

### 出力
```
1
0
```

## 関連項目

| 名前                                   | 説明           |
|----------------------------------------|----------------|
| [`insert`](insert.md)                | 要素を挿入する |
| [`(constructor)`](op_constructor.md) | コンストラクタ |


## 参照
- [P0600R1 `[[nodiscard]]` in the Library](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0600r1.pdf)
