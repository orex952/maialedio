# contains
* unordered_map[meta header]
* std[meta namespace]
* unordered_multimap[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
bool contains(const key_type& x) const; // (1)

template <class K>
bool contains(const K& k) const;        // (2)
```

## 概要
指定されたキーに一致する要素がコンテナに含まれているかを判定する。

- (1) : キー`x`を検索し、合致する要素が含まれるかを判定する
- (2) : キー`k`を透過的に検索し、合致する要素が含まれるかを判定する

(2)の透過的な検索は、`Pred::is_transparent`および`Hash::is_transparent`が定義される場合に有効になる機能であり、例として`unordered_multimap<string, int> m;`に対して`m.contains("key");`のように`string`型のキーを持つ連想コンテナの検索インタフェースに文字列リテラルを渡した際、`string`の一時オブジェクトが作られないようにできる。詳細は[`std::hash`](/reference/functional/hash.md)クラスのページを参照。


## テンプレートパラメータ制約
- (2) : `Pred::is_transparent`型および`Hash::is_transparent`型が定義されていること


## 戻り値
`x`と`k`を共通の変数`a`であるとして、以下と等価：

```cpp
return find(a) != end();
```
* find[link find.md]
* end()[link end.md]


## 計算量
- 平均： 定数時間
- 最悪： [`size`](size.md) について線形時間


## 例
```cpp example
#include <iostream>
#include <unordered_map>

int main()
{
  std::unordered_multimap<char, int> um = {
    {'a', 3},
    {'b', 1},
    {'c', 4}
  };

  // キー'b'の要素が含まれているか
  if (um.contains('b')) {
    std::cout << "contain" << std::endl;
  }
  else {
    std::cout << "doesn't contain" << std::endl;
  }
}
```
* contains[color ff0000]

### 出力
```
contain
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang):
- [GCC](/implementation.md#gcc): 9.1
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 1

## 参照
- [P0458R2 Checking for Existence of an Element in Associative Containers](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0458r2.html)
- [P0919R3 Heterogeneous lookup for unordered containers](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0919r3.html)
