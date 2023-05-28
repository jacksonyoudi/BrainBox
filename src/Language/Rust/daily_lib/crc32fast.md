# crc32fast

## 1. 描述

Fast, SIMD-accelerated CRC32 (IEEE) checksum computation 
快速、使用 SIMD 加速的 CRC32（IEEE）校验和计算

[crate](https://crates.io/crates/crc32fast)

[github](https://github.com/srijs/rust-crc32fast)

## 2. 什么是CRC32?

CRC32是一种循环冗余校验码（Cyclic Redundancy Check）算法， 用于检测或校验数据传输或存储过程中是否出现错误。 它通过对数据进行多项式除法运算，生成一个32位的校验和，用于检测数据是否被篡改或损坏。
CRC32广泛应用于数据通信、数据存储、文件校验等领域。

## 3. 应用场景

### 网络通信

在网络通信中，数据包可能会在传输过程中出现错误，使用CRC32校验和可以检测数据包是否被篡改或损坏。

### 存储介质

在存储介质中，如硬盘、U盘等，数据可能会因为磁盘损坏或其他原因出现错误，使用CRC32校验和可以检测数据是否被篡改或损坏。

### 文件校验

在下载文件或者接收文件时，使用CRC32校验和可以检测文件是否被篡改或损坏。

### 数据库校验

在数据库中，使用CRC32校验和可以检测数据是否被篡改或损坏，确保数据的完整性。

总之，任何需要保证数据完整性的场景都可以使用CRC32校验和来检测数据是否被篡改或损坏。

## crc32fast

crc32fast是Rust中最常用的计算CRC32的库.
![crc32fast crate](https://cdn.jsdelivr.net/gh/jacksonyoudi/images@main/uPic/2023/05/27/uIKDiH.png)

和其他库对比

|crate    |version|    variant    |ns/iter|    MB/s|
|----|----|----|----|----|
|crc    |1.8.1|    n/a|    4,926|    207|
|crc32fast (this crate)|    1.0.0|    baseline|    683    |1499|
|crc32fast (this crate)    |1.0.0|    pclmulqdq|    140|    7314|
    
## 使用
首先安装
```bash
cargo add crc32fast

或在 cargo.toml添加

[dependencies]
crc32fast = "1.3.2"
```

简单实用

```rust
use crc32fast;

fn main() {
    let checksum = crc32fast::hash(b"foo bar baz");
    println!("{}", checksum);
}
```

高级使用:
```rust
use crc32fast::Hasher;

fn main() {
    let mut hasher = Hasher::new();
    hasher.update(b"foo bar baz");
    let checksum = hasher.finalize();
    println!("{}", checksum);
}
```

上面都是官方的东西


## 源码解析

