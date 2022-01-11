# operator[]
* stacktrace[meta header]
* std[meta namespace]
* basic_stacktrace[meta class]
* function[meta id-type]
* cpp23[meta cpp]

```cpp
const_reference operator[](size_type frame_no) const; // (1) C++23
```

## 概要
任意の位置の要素を取得する。


## 事前条件
- `frame_no <` [`size()`](size.md)であること


## 戻り値
保持しているスタックトレースの履歴の、`frame_no`番目の要素を返す。


## 例外
投げない


## 例
```cpp example
#include <iostream>
#include <stacktrace>

void g() {
  std::stacktrace st = std::stacktrace::current();
  std::cout << st[0] << std::endl;
}

void f() {
  g();
}

int main() {
  f();
}
```
* st[0][color ff0000]
* current()[link current.md]

### 出力例
```
g() at main.cpp:5
```


## バージョン
### 言語
- C++23

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): ??
- [Visual C++](/implementation.md#visual_cpp): ??
