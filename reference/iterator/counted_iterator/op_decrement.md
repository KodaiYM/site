# operator--
* iterator[meta header]
* std[meta namespace]
* counted_iterator[meta class]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
constexpr counted_iterator& operator--()
  requires bidirectional_iterator<I>;       // (1)

constexpr counted_iterator operator--(int)
  requires bidirectional_iterator<I>;       // (2)
```
* bidirectional_iterator[link /reference/iterator/bidirectional_iterator.md]


## 概要
イテレータをデクリメントする。

- (1) : 前置デクリメント
- (2) : 後置デクリメント

## 効果

現在のイテレータとカウントの値をそれぞれ、`current`、`length`メンバ変数に保持するとする。

- (1) : 以下と等価  
    ```cpp
    --current;
    ++length;
    return *this;
    ```

- (2) : 以下と等価  
    ```cpp
    counted_iterator tmp = *this;
    --*this;  // (1)に委譲
    return tmp;
    ```

## 例
```cpp example
#include <iostream>
#include <iterator>
#include <ranges>
#include <vector>

int main() {
  std::vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

  std::counted_iterator ci{std::ranges::begin(vec), 5};

  ++ci;
  ++ci;
  
  std::cout << *ci << '\n';
  
  --ci;
  
  std::cout << *ci << '\n';
  
  ci--;

  std::cout << *ci << '\n';
}
```
* --ci[color ff0000]
* ci--[color ff0000]
* ranges::begin[link /reference/ranges/begin.md.nolink]

### 出力
```
3
2
1
```

## バージョン
### 言語
- C++11

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 4.6.1
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): ??


## 参照
- [P0031R0 A Proposal to Add Constexpr Modifiers to `reverse_iterator`, `move_iterator`, `array` and Range Access](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0031r0.html)