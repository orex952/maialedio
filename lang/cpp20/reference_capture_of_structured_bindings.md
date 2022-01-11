# 構造化束縛した変数の参照キャプチャを許可
* cpp20[meta cpp]

## 概要
構造化束縛した変数はラムダ式で参照キャプチャできない規定となっていたが、これを許可する。ただし、ビットフィールドを構造化束縛した変数は参照キャプチャできない。

```cpp
struct X {
  int a : 1; // ビットフィールドは参照キャプチャできない
  int b;     // 非ビットフィールドは参照キャプチャできる
};

int main() {
  auto [a, b] = X{};

//auto f1 = [&] { return a; };      // C++17:NG C++20:NG
//auto f2 = [&a = a] { return a; }; // C++17:NG C++20:NG
//auto f3 = [&a] { return a; };     // C++17:NG C++20:NG

  // デフォルト参照キャプチャをした場合、ビットフィールドはキャプチャされない
  auto g1 = [&] { return b; };      // C++17:NG C++20:OK
  auto g2 = [&b = b] { return b; }; // C++17:OK C++20:OK
  auto g3 = [&b] { return b; };     // C++17:NG C++20:OK
}
```


## 仕様
- 参照キャプチャできない要素として、ビットフィールド、構造化束縛した変数、無名共用体のメンバの3つがあったが、C++20ではこの不許可リストから「構造化束縛した変数」が削除された


## 関連項目
- [C++17 構造化束縛](/lang/cpp17/structured_bindings.md)


## 参照
- [P1381R1 Reference capture of structured bindings](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1381r1.html)
