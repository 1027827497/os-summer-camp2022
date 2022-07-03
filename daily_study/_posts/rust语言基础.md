---
title: rust语言基础
date: 2022-07-01 17:24:56
summary:
tags:
categories:
---

#### 1.变量

Rust 语言使用 `let` 关键字来声明和定义一个变量。

```
let 变量名=值
```

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

上面的代码中，我们并没有为每一个变量指定它们的数据类型。Rust 编译器会自动从 **等号 =** 右边的值中推断出该变量的类型。例如 Rust 会自动将 **双引号** 阔起来的数据推断为 **字符串**，把没有小数点的数字自动推断为 **整型**。把 `true` 或 `false` 值推断为 **布尔类型**。

Rust 语言中有四种标量数据类型：

- 整型
- 浮点型
- 布尔类型
- 字符类型

##### 整型

| 大小    | 有符号 | 无符号 |
| ------- | ------ | ------ |
| 8 bit   | i8     | u8     |
| 16 bit  | i16    | u16    |
| 32 bit  | i32    | u32    |
| 64 bit  | i64    | u64    |
| 128 bit | i128   | u128   |
| Arch    | isize  | usize  |

整型的长度还可以是 `arch`。`arch` 是由 CPU 构架决定的大小的整型类型。大小为 `arch` 的整数在 `x86` 机器上为 `32` 位，在 `x64` 机器上为 `64` 位。

```rust
fn main(){
let price1 = 100;  
let price2:u32 = 200;
let price3:i32 = -300;
let price4:isize = 400;
let price5:usize = 500;

println!("price1 is {}", price1);
//输出 price is 100

println!("price2 is {} and price3 is {}", price3, price2);
//输出 price2 is -300 and price3 is 200

println!("price4 is {} and price5 is {}", price4, price5);
//输出 price4 is 400 and price5 is 500
}
```

##### 浮点型

- `f32` 又称为 **单精度浮点型**。
- `f64` 又称为 **双精度浮点型**，它是 Rust 默认的浮点类型.

Rust 中不能将 `0.0` 赋值给任意一个整型，也不能将 `0` 赋值给任意一个浮点型。

当数字很大的时候，Rust 可以用 **(_下划线) ** ，来让数字变得可读性更好。

```rust
fn main(){
let price1:f32 = 1.111_111;  
let price2:u32 = 2000_00000;
println!("price1 is {}", price1);
println!("price2 is {} ",  price2);
}
```

##### 布尔类型

```rust
let checked:bool = true;
```

##### 字符类型

```rust
字符(char) ，就是字符串的基本组成部分，也就是单个字符或字。

Rust 使用 UTF-8 作为底层的编码 ，而不是常见的使用 ASCII 作为底层编码。

Rust 中的 字符数据类型 包含了 数字、字母、Unicode 和 其它特殊字符。

fn main(){
let price1 = '好';  
println!("price1 is {}", price1);
}
这一点和c语言不同,C语言底层使用ascall，字符不能是汉字
```

#### 2.常量

```rust
fn main(){
const PI:f64=3.141592653589793;
let price1 = '好';  
// 初始化:const和static都要求赋予它们一个值。它们必须只能被赋予一个常量表达式的值。换句话说，你不能用一个函数调用的返回值或任何相似的复合值或在运行时赋值。
// 使用 const 关键字定义常量。
// 定义常量时必须指定数据类型。
// 常量名称的命名规则和之前变量的命名规则一样，但常量名称一般都是 大写字母。
//Rust 中，常量不能被隐藏，也不能被重复定义。
// static：具有 ‘static 生命周期的，可以是可变的变量（须使用 static mut 关键字）。
// 有个特例就是 “string” 字面量。它可以不经改动就被赋给一个 static 变量，因为它 的类型标记：
// &’static str 就包含了所要求的生命周期 ‘static。其他的引用类型都 必须特地声明，使之拥有’static 生命周期。
//对于static，Rust以静态量的方式提供了类似“全局变量”的功能。它们与常量类似，不过静态量在使用时并不内联。这意味着对每一个值只有一个实例，并且位于内存中的固定位置。
static BOOK:&'static str = "asd";
static PEN:i32=5;
//因为这是可变的，一个线程可能在更新N同时另一个在读取它，导致内存不安全。
//因此访问和改变一个static mut是不安全（unsafe）的，因此必须在unsafe块中操作
static mut NUM:i32=10;
unsafe{
    NUM=NUM+1;
    println!("NUM= {}",NUM);//必须放在这里
}
println!("price1 is {}", price1);
println!("PI= {}",PI);
println!("BOOK= {}",BOOK);
println!("PEN= {}",PEN);
}
```

#### 3.字符串

```rust
fn show_name(name:&str){
    println!("看看这个{}", name);
}
fn main(){
let s1 = String::new();
println!("s1:{},s1-len:{}",s1,s1.len());

let s2 = String::from("你好世界");
println!("s2:{},s2-len:{}",s2,s2.len());

let mut s3=String::new();//创建一个新的字符串对象
s3.push_str("1111");//再字符串末尾追加字符串。
println!("{}",s3);
s3.push('o');//是在原字符上追加字符，而不是返回一个新的字符串
s3.push('k');
println!("{}",s3);
let s4= String::from("haooooo");
s4.replace("haooooo", "hahahahah");//指定字符串子串替换成另一个字符串
println!("{}",s4);
let a=s4.len();//返回字符串中的 总字节数。该方法会统计包括 制表符 \t、空格 ``、回车 \r、换行 \n 和回车换行 \r\n 等等。
println!("{}",a);
let s5="\tqqqqq\n".to_string();//将字符串转换为字符串对象，方便以后可以有更多的操作。

show_name(s5.as_str());//返回一个字符串对象的 字符串 字面量。

show_name(s5.trim());//去除字符串头尾的空白符。空白符是指 制表符 \t、空格 ``、回车 \r、换行 \n 和回车换行 \r\n 等等
println!("{}",s5.trim().len());

let s6="1,2,3,4,5,6,7,8,9,10,11";
for item in s6.split(",") {//将字符串根据某些指定的 字符串子串 分割，返回分割后的字符串子串组成的切片上的迭代器。
print!(" {}",item);}
for item in s6.chars() {//将一个字符串打散为所有字符组成的数组
    print!("字符: {}|",item);}

    let s7=s5+&s6;
    println!("{}",s7);
}
```

#### 4.运算符

**注：Rust 语言不支持自增自减运算符 `++` 和 `--`**

#### 5.条件语句

除if外无switch,switch用match代替

```rust
// match variable_expression {
//     constant_expr1 => {
//        // 语句;
//     },
//     constant_expr2 => {
//        // 语句;
//     },
//     _ => {
//        // 默认
//        // 其它语句
//     }
//  };
 fn main(){
 let code = "10010";
let choose = match code {
   "10010" => "联通",
   "10086" => "移动",
   _ => "Unknown"
};
println!("选择 {}", choose);
//输出 选择 联通


let code = "80010";
let choose = match code {
   "10010" => "联通",
   "10086" => "移动",
   _ => "Unknown"
};
println!("选择 {}", choose);}
//输出 选择 Unknown
```



#### 6.循环

```rust

fn main(){
    for num in 1..5{
        println!("num is {}", num);//这是一个左闭右开的区间，1..5，那就只包含 1,2,3,4
     }
     for num in 1..=5 {
        println!("num is {}", num);//可以使用 a..=b 表示两端都包含在内的范围。
     }
     let a=vec!["a", "b", "c", "d", "e",];
     for nmae in a.iter() {  //iter - 在每次迭代中借用集合中的一个元素。这样集合本身不会被改变，循环之后仍可以使用。
      match nmae {
         &"a"=>println!("ok: {}", nmae),
         _=>println!("fatal: {}", nmae),
      }
   }
   for name in a.into_iter() {//into_iter - 会消耗集合。在每次迭代中，集合中的数据本身会被提供。一旦集合被消耗了，之后就无法再使用了，因为它已经在循环中被 “移除”（move）了。
      match name{
         "a"=>println!("ok: {}", name),
         _ => println!("fatal: {}", name),
      }
}
let mut  b=vec!["a", "b", "c", "d", "e", ];
for name in b.iter_mut() {
//    iter_mut - 可变地（mutably）借用集合中的每个元素，从而允许集合被就地修改。
// 就是停止本次执行剩下的语句，直接进入下一个循环。
   *name =match name {
      &mut "a" =>{"riscv"},
      &mut "b" =>{"riscv"},
      _ => *name,
   }
}
println!("b: {:?}", b);

let mut num=1;
while num<5{//上面的条件表达式为真，就会执行 while 循环。
   println!("{}", num);
   num+=1;
}


let mut c=1;
loop{//一种重复执行且永远不会结束的循环
   if c>5{
      break;
   }
   println!("{}", c);
   c=c+2;
}

}

```

#### 7.函数

```rust
fn get_name() -> String {
   return String::from("1111");
}
//Rust 语言的返回值定义语法，在 小括号后面使用 箭头 ( -> ) 加上数据类型 来定义的。

fn get_name2() -> String {
   String::from("2222")
}
//如果函数代码中没有使用 return 关键字，那么函数会默认使用最后一条语句的执行结果作为返回值。


fn double_price(mut price:i32){
   //值传递 是把传递的变量的值传递给函数的 形参，所以，函数体外的变量值和函数参数是各自保存了相同的值，互不影响
   price=price*2;
   println!("内部的price是{}",price)
}

fn double_price2(price:&mut i32){
   //值传递变量导致重新创建一个变量。但引用传递则不会，引用传递把当前变量的内存位置传递给函数。传递的变量和函数参数都共同指向了同一个内存位置。引用传递在参数类型的前面加上 & 符号。
   *price=*price*2;//星号（*） 用于访问变量 price 指向的内存位置上存储的变量的值。这种操作也称为 解引用。 因此 星号（*） 也称为 解引用操作符。
   println!("内部的price是{}",price)
}

fn main() {
   println!("r1:{}", get_name());
   println!("r2:{}", get_name2());

   let mut price:i32 = 1;
   double_price(price);
   println!("外部的price是{}",price);


   double_price2(&mut price);
   println!("外部的price是{}",price);

}
```

#### 8.元组

```rust

fn show_tuple(tuple:(&str,&str)){
   println!("{:?}",tuple);
}

fn main() {
   //Tuple 元组是一个 复合类型 ，可以存储多个不同类型的数据。 Rust 支持元组 tuple 类型。元组使用括号 () 来构造（construct）。函数可以使用元组来返回多个值，因为元组可以拥有任意多个值。
// 元组一旦定义，就不能再增长或缩小，长度是固定的。元组的下标从 0 开始。
   let t: (i32, f64, u8) = (500, 6.4, 1);
   let (x, y, z) = t;//解构元组
   println!("x:{} y:{} z:{}",x,y,z);
   println!("{}, {}, {}",t.0, t.1, t.2);//访问元组

   let t1:(&str, &str)=("aaaa","bbbb");
 show_tuple(t1);
}
```

#### 9.数组

```rust
// 数组 是用来存储一系列数据，拥有相同类型 T 的对象的集合，在内存中是连续存储的。使用中括号 [] 来创建，且它们的大小在编译时会被确定。数组下标是从0 开始。数组是在栈中分配的，数组可以自动被借用成为 切片(slice)

fn show_arr(arr:[&str;3]){
   let l = arr.len();
   for i in 0..l {
      println!("ok: {}",arr[i]);
   }
}


fn modify_arr(arr:&mut [&str;3]){
   let l = arr.len();
   for i in 0..l {
       arr[i]="";
   }
}

fn main() {
//let 变量名:[数据类型;数组长度]=[值1,值2,值3,...];
let mut a1:[&str;3]=["hello","world","hello world"];
// let 变量名=[值1,值2,值3,...];
let a2=["hello", "world", "hello world"];
//let 变量名:[数据类型;数组长度]=[默认值,数组长度];
let a3:[&str;3]=["";3];

for item in a1.iter() {
   println!("{}", item);}
   
   for item in a1{
      println!("{}", item);
   }

   show_arr(a1);//值传递 传递一个数组的副本，副本的修改，不会影响原数组。

   modify_arr(&mut a1);//引用传递 传递内存的地址给函数，修改数组的任何值都会修改原来的数组。
println!("{:?}\n", a1);


   }
```

#### 10.所有权和借用

Rust 的核心功能（之一）是 **所有权**（*ownership*）。虽然该功能很容易解释，但它对语言的其他部分有着深刻的影响。

引入：所有程序都必须管理其运行时使用计算机内存的方式。一些语言中具有垃圾回收机制，在程序运行时不断地寻找不再使用的内存；在另一些语言中，程序员必须亲自分配和释放内存。**Rust 则选择了第三种方式：通过所有权系统管理内存，编译器在编译时会根据一系列的规则进行检查。如果违反了任何这些规则，程序都不能编译。在运行时，所有权系统的任何功能都不会减慢程序。**

注：因为变量要负责释放它们拥有的资源，所以**资源只能拥有一个所有者**。这也防止了资源的重复释放。注意并非所有变量都拥有资源（例如引用）。

move：在进行赋值（let a = b）或通过值来传递函数参数（foo(a)）的时候，资源的所有权（ownership）会发生转移。按照 Rust 的规范，这被称为资源的移动（move）。

注：在移动资源之后，原来的所有者不能再被使用，这可避免悬挂指针（dangling pointer）的产生

当我们将 `s1` 赋值给 `s2`，`String` 的数据被复制了，这意味着我们从栈上拷贝了它的指针、长度和容量。我们并没有复制指针指向的堆上数据

![2022-07-03_200842](https://raw.githubusercontent.com/1027827497/tuchuang/main//2022-07-03_200842.png)

所有权管理内存的特点

 Rust 同时使第一个变量无效了，这个操作被称为 **移动**

另外，这里还隐含了一个设计选择：Rust 永远也不会自动创建数据的 “深拷贝”。因此，任何 **自动** 的复制可以被认为对运行时性能影响较小。

![2022-07-03_200207](https://raw.githubusercontent.com/1027827497/tuchuang/main//2022-07-03_200207.png)

栈：它是一种 **后进先出** 的机制，类似我们日常的落盘子，只能一个一个向上方，然后从最上面拿一个盘子。一个变量要放到栈上，那么它的大小在编译时就要明确。i32 类型的变量，它就占用 4 个字节。Rust 中可以放到栈上的数据类型，他们的大小都是固定的。如果是字符串，在运行时才会赋值的变量，在编译期的时候大小是未知或不确定的。所以字符串类型存储在**堆**上。

堆：用于编译时大小未知或不确定的，只有运行时才能确定的数据。在**堆**上存储一些动态类型的数据。**堆**是不受系统管理的，是用户自己管理的，也增加了内存溢出的风险。

注：入栈比在堆上分配内存要快，因为（入栈时）分配器无需为存储新数据去搜索内存空间；其位置总是在栈顶。相比之下，在堆上分配内存则需要更多的工作，这是因为分配器必须首先找到一块足够存放数据的内存空间，并接着做一些记录为下一次分配做准备。

访问堆上的数据比访问栈上的数据慢，因为必须通过指针来访问。现代处理器在内存中跳转越少就越快（缓存）

跟踪哪部分代码正在使用堆上的哪些数据，最大限度的减少堆上的重复数据的数量，以及清理堆上不再使用的数据确保不会耗尽空间，这些问题正是所有权系统要处理的。一旦理解了所有权，你就不需要经常考虑栈和堆了，不过明白了所有权的主要目的就是为了管理堆数据，能够帮助解释为什么所有权要以这种方式工作。

**所有权规则：**

1. Rust 中的每一个值都有一个被称为其 **所有者**（*owner*）的变量。

2. 值在任一时刻有且只有一个所有者。

3. 当所有者（变量）离开作用域，这个值将被丢弃

   **引用：**

    值传递，每个值都有一个所有权，允许使得一个新变量获取其所有权,就是让一个变量指向原来变量的即指向另一个变量的地址,由栈分配的资源不存在所有权如基本数据类型，只有由堆分配的资源才存在所有权如字符串

   ![2022-07-03_202009](https://raw.githubusercontent.com/1027827497/tuchuang/main//2022-07-03_202009.png)

   引用传递

   这些 & 符号就是 **引用**，它们允许你使用值但不获取其所有权,就是让这个变量指向另一个变量

   ![2022-07-03_200228](https://raw.githubusercontent.com/1027827497/tuchuang/main//2022-07-03_200228.png)

   ```rust
   把一个变量赋值给另一个变量
   fn main() {
      // 栈分配的整型
      let a = 88;
      // 将 `a` *复制*到 `b`——不存在资源移动，资源就存在栈上不需要移动
      let b = a;
      // 两个值各自都可以使用
      println!("a {}, and b {}", a, b);
   
     let v1 = vec!["aaa","bbb","ccc"];
     let v2 =v1;
    // println!("{:?}",v1);会出错因为字符串的内存资源分配由堆分配，资源不移动让所有权移动，v1的所有权被转移到了v2上，再次使用v1会出错
   }
   
   把变量传递给函数参数
   fn show(v:Vec<&str>){
      println!("v {:?}",v)
   }
   fn main() {
      let studyList = vec!["aaaa","bbbb","cccc"];
      //studyList 拥有堆上数据管理权
      let studyList2 = studyList;
      // studyList 将所有权转义给了 studyList2
      show(studyList2);
      // studyList2 将所有权转让给参数 v,studyList2 不再可用。
      println!("studyList2 {:?}",studyList2);
      //studyList2 已经不可用。
   }
   函数中的返回值
   fn show2(v:Vec<&str>) -> Vec<&str>{
       println!("v {:?}",v);
       return v;
   }
   
   fn main() {
       let studyList3 = vec!["aaaa","bbbb","ccc"];
       let studyList4 = studyList3;
       let result = show2(studyList4);
       println!("result {:?}",result);//不会报错所有权已从函数形参转到result变量
   }
   注：
   基础数据类型与所有权：所有权只会发生在堆上分配的数据，基础数据类型(整型，浮点型，布尔，字符)存储在栈上，所以没有所有权的概念。基础类型可以认为是值拷贝，在内存上另外的地方，存储和复制来的数据，然后让新的变量指向它，赋值并不是唯一涉及移动的操作。值在作为参数传递或从函数返回时也会被移动:
   
   ```

   借用：Rust 中，**Borrowing（借用）**，就是一个函数中的变量传递给另外一个函数作为参数暂时使用。也会要求函数参数离开自己作用域的时候将**所有权** 还给当初传递给它的变量（好借好还，再借不难嘛!）。

   ```rust
   //&变量名  //要把参数定义的时候这样定义。
   fn show(v:&Vec<&str>){
       println!("v:{:?}",v)
   }
   fn main() {
       let studyList = vec!["aaaa","bbbb","cccc"];
       let studyList2 =studyList;
       show2(&studyList2);
       println!("studyList2:{:?}",studyList2); //我们看到，函数show使用完v2后，我们仍然可以继续使用
   }
   ```

   ```rust
   //可变的借用：
   //如果我们要在Borrowing（借用）的时候改变其中的值：
   //1.变量要用mut关键字。
   //2.函数参数为可变的要用 &mut 关键字。
   //3.传递参数的时候，也要用 &mut 关键字
   fn show2(v:&mut Vec<&str>){
       v[0]="第一个充电项目已完成";
       println!("v:{:?}",v)
   }
   fn main() {
    let mut studyList3 = vec!["aaaa","bbbb","cccc"];
    println!("studyList3:{:?}",studyList3);
    show2(&mut studyList3);
    println!("调用后，studyList3:{:?}",studyList3);//不会出错并且被gai'b
    }
   ```

   

   
