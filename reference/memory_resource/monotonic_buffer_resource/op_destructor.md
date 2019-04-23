# デストラクタ
* memory_resource[meta header]
* function[meta id-type]
* std::pmr[meta namespace]
* monotonic_buffer_resource[meta class]
* cpp17[meta cpp]

```cpp
virtual ~monotonic_buffer_resource();
```

## 概要

管理しているすべてのメモリを解放する。

## 効果

[`this->release()`](release.md)を呼び出す。

## バージョン
### 言語
- C++17

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 9.1
- [Visual C++](/implementation.md#visual_cpp): 2017 update 6

## 関連項目
- [`release`](release.md)