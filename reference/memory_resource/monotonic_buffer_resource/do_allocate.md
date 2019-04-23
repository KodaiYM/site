# do_allocate
* memory_resource[meta header]
* function[meta id-type]
* std::pmr[meta namespace]
* monotonic_buffer_resource[meta class]
* cpp17[meta cpp]

```cpp
void* do_allocate(size_t bytes, size_t alignment) override;
```

## 概要
要求されたサイズおよびアライメントでメモリを割り当てる。

割り当てられた領域のサイズと配置・要件等は[`memory_resource::do_allocate()`](/reference/memory_resource/memory_resource/do_allocate.md)に従う。

## 要件
`alignment`は2のべき乗であること

## 引数

- `bytes` -- 割り当てるメモリのサイズ
- `alignment` -- 割り当てる領域へのアライメント要求

## 効果
内部メモリ領域から指定された`bytes`と`alignment`でメモリを割り当てることができる場合は（内部メモリにそのような空き領域がある場合は）内部メモリ領域から割り当てを行う。  
それができない場合、上流メモリリソースから内部メモリ領域を補充し割り当てを行う。

内部メモリ領域を補充する場合、[`this->upstream_resource()`](upstream_resource.md)[`->allocate(n, m)`](/reference/memory_resource/memory_resource/allocate.md)のように上流メモリリソースから追加のメモリを取得する。  
次に補充する予定のメモリ領域サイズを`next_buffer_size`という変数に保持しているとすると`n, m`は`n = max(bytes, next_buffer_size)`、`m >= alignment `となる値をそれぞれ用いる。  
その後、`next_buffer_size`を実装定義の増加分（整数とは限らない）だけ増やす。

少なくとも`bytes`のメモリを割り当て、`alignment`にアラインすることができない場合は`alignof(std::max_align_t)`にアラインする。

## 戻り値
割り当てた領域の先頭へのポインタ

## 例外
[`this->upstream_resource()`](upstream_resource.md)[`->allocate()`](/reference/memory_resource/memory_resource/allocate.md)が例外を投げないのならば、この関数も例外を投げない。

## バージョン
### 言語
- C++17

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 9.1
- [Visual C++](/implementation.md#visual_cpp): 2017 update 6

## 関連項目
- [`memory_resource`](/reference/memory_resource/memory_resource.md)