# fetch_or
* atomic[meta header]
* std[meta namespace]
* atomic_ref[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
T fetch_or(T operand, memory_order order = memory_order_seq_cst) const noexcept;
```
* memory_order[link /reference/atomic/memory_order.md]
* memory_order_seq_cst[link /reference/atomic/memory_order.md]

## 概要
OR演算を行う


## 要件
- `std::atomic_ref<T*>`の場合、型`T`がオブジェクト型であること。型`T`が`void*`や関数ポインタであってはならない (C++17)


## 効果
`order`で指定されたメモリオーダーにしたがって、現在の値に`operand`をORした値でアトミックに置き換える


## 戻り値
変更前の値が返される


## 例外
投げない


## 備考
- この関数は、`atomic_ref`クラスの整数型に対する特殊化で定義される。
- 符号付き整数型に対しては、符号なし整数型に変換されたかのようにしたあと演算が行われ、結果は符号付き整数型になる。未定義動作はない


## 例
### 基本的な使い方
```cpp example
#include <iostream>
#include <atomic>
#include <bitset>

int main()
{
  int value = 0b1011;
  std::atomic_ref<int> x{value};

  x.fetch_or(0b1110);

  std::cout << std::bitset<4>(value).to_string() << std::endl;
}
```
* fetch_or[color ff0000]
* to_string()[link /reference/bitset/bitset/to_string.md]

#### 出力
```
1111
```

### 複数スレッドからビット複合演算を行う例
```cpp example
#include <iostream>
#include <atomic>
#include <thread>
#include <bitset>

int main()
{
  int value = 0b0110;

  // 複数スレッドでビット複合演算を呼んでも、
  // 最終的に全てのスレッドでのビット複合演算が処理された値になる
  std::thread t1 {[&value] {
    std::atomic_ref{value}.fetch_or(0b0001);
  }};
  std::thread t2 {[&value] {
    std::atomic_ref{value}.fetch_or(0b1000);
  }};

  t1.join();
  t2.join();

  std::cout << std::bitset<4>(value).to_string() << std::endl;
}
```
* fetch_or[color ff0000]
* to_string()[link /reference/bitset/bitset/to_string.md]

#### 出力
```
1111
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): (9.0時点で実装なし)
- [GCC](/implementation.md#gcc): 10.1
- [Visual C++](/implementation.md#visual_cpp): ??

