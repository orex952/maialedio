# to_string
* stacktrace[meta header]
* std[meta namespace]
* basic_stacktrace[meta class]
* function[meta id-type]
* cpp23[meta cpp]

```cpp
namespace std {
  template <class Allocator>
  string to_string(const basic_stacktrace<Allocator>& st);
}
```
* string[link /reference/string/basic_string.md]

## 概要
文字列化する。


## 戻り値
`st`のスタックトレース情報を説明する文字列を返す。


## 備考
- 戻り値となる文字列の行数は、[`size()`](size.md)と等値であるという保証はない


## 例
```cpp example
#include <iostream>
#include <stacktrace>

void g() {
  std::string trace = std::stacktrace::current().to_string();
  std::cout << trace << std::endl;
}

void f() {
  g();
}

int main() {
  f();
}
```
* to_string()[color ff0000]
* current()[link current.md]

### 出力例
```
 0# g() at main.cpp:5
 1# f() at main.cpp:10
 2# main at main.cpp:14
```


## バージョン
### 言語
- C++23

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): ??
- [Visual C++](/implementation.md#visual_cpp): ??
