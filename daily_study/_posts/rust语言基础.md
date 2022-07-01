---
title: rust语言基础
date: 2022-07-01 17:24:56
summary:
tags:
categories:
---

1.变量

```rust
const _MAX: u32=1000;
fn main() {
    let a=1;
    println!("a={}", a);
    let mut b: u32=1;//使用mut才是变量不用就是常量
    b=2;
    println!("b={}", b);

   let b:f32=1.1;
   println!("b={}", b);//原来的被隐藏

   println!("_MAX={}", _MAX);

}

```

