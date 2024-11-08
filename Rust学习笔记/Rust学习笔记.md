vscode+Rsut+\<[Rust语言圣经](https://course.rs/about-book.html))>+\<[Rust程序设计第二版](https://github.com/169LI/Rust_study/blob/main/%E3%80%8ARust%20%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%EF%BC%88%E7%AC%AC2%E7%89%88%EF%BC%89%E3%80%8B%E5%90%89%E5%A7%86%E2%80%A2%E5%B8%83%E5%85%B0%E8%BF%AA%E3%80%90%E6%96%87%E5%AD%97%E7%89%88_PDF%E7%94%B5%E5%AD%90%E4%B9%A6_%E9%9B%85%E4%B9%A6%E3%80%91.pdf)>+obsidian(笔记软件)+github(代码仓库)
# obsidian+github
# 搭建开发环境
&ensp;&ensp; &ensp;首先，需要安装最新版的 Rust 编译工具和 Visual Studio Code
Rust 编译工具：[安装 Rust ](https://www.rust-lang.org/zh-CN/tools/install)
Visual Studio Code：[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)

+ Rust 的编译工具依赖 C 语言的编译工具，这意味着你的电脑上至少已经存在一个 C 语言的编译环境。如果你使用的是 Linux 系统，往往已经具备了 GCC 或 clang。
+ 如果你使用的是 macOS，需要安装 Xcode。
+ 如果你是用的是 Windows 操作系统，你需要安装 Visual Studio 2013 或以上的环境（需要 C/C++ 支持）以使用 MSVC 或安装 MinGW + GCC 编译环境 

## 1 之前下载过vs2022 
&ensp;&ensp; &ensp;（没下过也不建议你下了     还不如开虚拟机用linux系统    或者用MinGW   vs2022有点大）
![|450](image/Pasted_image_20241105202526.png)

## 2 rust 编译工具
&ensp;  &ensp;官方下载地址: [rust](https://www.rust-lang.org/learn/get-started)  选择64bit，下载后的文件名为rustup-init.exe

![|475](image/Pasted_image_20241105202801.png)

## 3 运行rustup-init.exe

![|450](image/Pasted_image_20241105203307.png)

&ensp;&ensp; &ensp;上图显示的是一个命令行安装向导。

&ensp;&ensp; &ensp;如果你已经安装 MSVC （推荐），那么安装过程会非常的简单，输入 1 并回车，直接进入第二步。

![|475](image/Pasted_image_20241105203332.png)

&ensp;&ensp; &ensp;没有安装MSVC或者后续准备使用GNU得处理方法（ 后面可能会使用GNU,可能还得弄）

&ensp;&ensp; &ensp;如果你安装的是 MinGW，那么你需要输入 2 （自定义安装），然后系统会询问你 Default host triple? 请将上图中 default host triple 的 "msvc" 改为 "gnu" 再输入安装程序。

![|450](image/Pasted_image_20241105203348.png)

&ensp;&ensp; &ensp;设置完所有选项，会回到安装向导界面（第一张图），这是我们输入 1 并回车即可。
## 4 测试

`rustc -V        # 注意的大写的 V`

![|550](image/Pasted_image_20241105203418.png)
&ensp;&ensp; &ensp;环境成功配置

## 5 Visual Studio Code 开发环境
&ensp; analyzer 和 Native Debug 两个扩展   之后重启  选择一个新的文件夹

![|332](image/Pasted_image_20241105203442.png)

![|320](image/Pasted_image_20241105203450.png)

 选择菜单栏中的"终端"-"新建终端"，会打开一个新的终端并输入命令：
```
 创建新项目：cargo new <项目名>

 构建项目：cargo build

 运行项目：cargo run

 测试项目：cargo test
```

cargo new greeting  会自动构建一个名叫 greeting 的 Rust 工程目录。现在在终端里输入以下三个命令：
```
cd ./greeting
cargo build
cargo run
```
![|550](image/Pasted_image_20241105203519.png)
成功的构建了一个 Rust 命令行程序！
## 6 调试（debug）
&ensp;&ensp; &ensp;自带的那个是真不好用     自己配的这个也没好到哪里！  Rust后面会调试应该可能可以学快点，我也不清楚（学c++不会调试直接凉一半）

![|575](image/Pasted_image_20241105203553.png)

![|575](image/Pasted_image_20241105203605.png)

&ensp;&ensp; &ensp;直接粘贴下面的内容就ok了

```
{
    //调试哪一个就复制到哪一个文件夹下
    
    // 使用 IntelliSense 了解相关属性。
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(Windows) 启动",
            "type": "cppvsdbg",
            "request": "launch",
            "program": "${workspaceFolder}/target/debug/${workspaceFolderBasename}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "console": "internalConsole"
        }
    ]
}
```
## 7 卸载
&ensp;&ensp; &ensp;要卸载 Rust 和 rustup，在终端执行以下命令即可卸载：

&ensp;&ensp; &ensp;`rustup self uninstall（建议不要试）`

## 8 本地文档

&ensp;&ensp; &ensp;安装 Rust 的同时也会在本地安装一个文档服务，方便我们离线阅读：运行下面命令
```
 rustup doc
 cargo doc --help
```
&ensp;&ensp; &ensp; 用浏览器打开本地文档即可查看

&ensp;&ensp; &ensp;编程语言的学习尽头从不是书籍和视频教学中获取的知识而是能看懂懂官方文档的能力

## 9  .gitignore文件
 &ensp;&ensp; &ensp;如果有上传github需求  建议加一个.gitignore文件  把不想上传的文件写进去。他的target文件夹（编译的文件都在里面放）一运行就显示红色提示我上传   真的很烦。
```
target
.gitignore
```
# 一. 数据类型
&ensp;&ensp; &ensp;本章从简单的数值类型（如整数和浮点值）开始，后面转而介绍包含更多数据的类型：Box、元组（tuple）、数组和字符串。

>&ensp;&ensp; &ensp;**固定数值类型（整型+浮点型）**
 >
 &ensp;&ensp; &ensp;Rust 中数值类型的名称都遵循着一种统一的模式，类型定义的形式统一为：有无符号 + 类型大小(位数)。
![|475](image/Pasted_image_20241105203720.png)
 机器字是一个值，其大小等于运行此代码的机器上“地址”的大小，可能是 32 位，也可能是 64 位。
默认情况下，12.0 将表示 64 位浮点数 12表示有符号32位整数。

&ensp;&ensp;&ensp;`let x = -10.abs(); // 错误`

&ensp;&ensp;&ensp;方法调用的优先级高于前缀运算符，因此在对负值进行方法调用时，请务必正确地加上圆括号。

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;<font color="#2DC26B">进入正题：开始Rust!!!</font>

## 1.1 整型（Integer）
&ensp;&ensp; &ensp;整数型简称整型，按照比特位长度和有无符号分为以下种类
![|600](image/Pasted_image_20241105203729.png)
&ensp;&ensp; &ensp;为了让长数值更易读，可以在数字之间任意插入下划线。
  ![|600](image/Pasted_image_20241105203854.png)
### 1.1.1 整型溢出
&ensp;&ensp; &ensp;假设有一个 u8 ，它可以存放从 0 到 255 的值。那么当你将其修改为范围之外的值，比如 256，则会发生整型溢出。

&ensp;&ensp; &ensp;Rust 会检查整型溢出，若存在这些问题，则使程序在编译时 panic(崩溃,Rust 使用这个术语来表明程序因错误而退出)。在当使用release 参数进行 release 模式构建时，Rust 不检测溢出。相反，当检测到整型溢出时，Rust 会按照补码**循环溢出**（two’s complement wrapping）的规则处理。程序不会 panic，但是该变量的值可能不是你期望的值。依赖这种默认行为的代码都应该被认为是错误的代码。
### 1.1.2 溢出的处理
&ensp;&ensp; &ensp;要显式处理可能的溢出，可以使用标准库针对原始数字类型提供的这些方法，以下是常用的几个:
1. 加法
-  wrapping_add: 循环加法。
- checked_add: 溢出时返回 None。
- overflowing_add: 返回结果和溢出指示布尔值。
- saturating_add: 超过最大值时返回最大值。

```
   fn main() {
    // 加法 (Addition)
    println!("加法示例:");

    let wrapping_add_result = u8::MAX.wrapping_add(1);
    println!("wrapping_add: {}", wrapping_add_result); // 结果是 0

    let checked_add_result = u8::MAX.checked_add(1);
    println!("checked_add: {:?}", checked_add_result); // 返回 None

    let (overflowing_add_result, overflowing_add_overflowed) = u8::MAX.overflowing_add(1);
    println!("overflowing_add: result = {}, overflowed = {}", overflowing_add_result, overflowing_add_overflowed); // result = 0, overflowed = true

    let saturating_add_result = u8::MAX.saturating_add(1);
    println!("saturating_add: {}", saturating_add_result); // 结果是 255
    }
```
2. 减法
- wrapping_mul: 循环乘法。
- checked_mul: 如果发生溢出返回 None。
- overflowing_mul: 返回计算结果和是否溢出的布尔值。
- saturating_mul: 结果不会超过最大值。
```
fn main(){
 // 减法 (Subtraction)
    println!("\n减法示例:");

    let wrapping_sub_result = u8::MIN.wrapping_sub(1);
    println!("wrapping_sub: {}", wrapping_sub_result); // 结果是 255

    let checked_sub_result = u8::MIN.checked_sub(1);
    println!("checked_sub: {:?}", checked_sub_result); // 返回 None

    let (overflowing_sub_result, overflowing_sub_overflowed) = u8::MIN.overflowing_sub(1);
    println!("overflowing_sub: result = {}, overflowed = {}", overflowing_sub_result, overflowing_sub_overflowed); // result = 255, overflowed = true

    let saturating_sub_result = u8::MIN.saturating_sub(1);
    println!("saturating_sub: {}", saturating_sub_result); // 结果是 0
}
```

3. 乘法
- wrapping_mul: 循环乘法。
- checked_mul: 如果发生溢出返回 None。
- overflowing_mul: 返回计算结果和是否溢出的布尔值。
- saturating_mul: 结果不会超过最大值。
```
fn main(){
// 乘法 (Multiplication)
    println!("\n乘法示例:");

    let wrapping_mul_result = u8::MAX.wrapping_mul(2);
    println!("wrapping_mul: {}", wrapping_mul_result); // 结果是 254

    let checked_mul_result = u8::MAX.checked_mul(2);
    println!("checked_mul: {:?}", checked_mul_result); // 返回 None

    let (overflowing_mul_result, overflowing_mul_overflowed) = u8::MAX.overflowing_mul(2);
    println!("overflowing_mul: result = {}, overflowed = {}", overflowing_mul_result, overflowing_mul_overflowed); // result = 254, overflowed = true

    let saturating_mul_result = u8::MAX.saturating_mul(2);
    println!("saturating_mul: {}", saturating_mul_result); // 结果是 255
}
```

&ensp;&ensp;&ensp;还有除法 、移位置等操作的溢出判断，这里不在演示。可以看到关于回绕除法的这些方法还是很多的，但主要区别还是在数据类型：

![](image/{{数据类型}}-20241107.png)

&ensp;&ensp;&ensp;可以来看一下原文档里面是怎末说的(除法为例，这里选用i8作为举例)：

![](image/{{数据类型}}-20241107-2.png)

&ensp;&ensp; &ensp;在 Rust 中，`i8` 类型的整数范围是 -128 到 127。当 -128 被 -1 除时，结果应该是 128，但这会导致溢出，因为 128 超出了 `i8` 的表示范围。使用 `wrapping_div`，在这种情况下会返回 -128，因为溢出会按模 256 进行环绕。

&ensp;&ensp;&ensp;每种运算都有不同的处理方式，可以根据具体需求选择适合的方法来处理溢出和边界情况.

|      |      |                                       |     |
| ---- | ---- | ------------------------------------- | --- |
| 运算   | 名称后缀 | 例子                                    |     |
| 加法   | add  | 100_i8.checked_add(27) == Some(127)   |     |
| 减法   | sub  | 10_u8.checked_sub(11) == None         |     |
| 乘法   | mul  | 128_u8.saturating_mul(3) == 255       |     |
| 除法   | div  | 64_u16.wrapping_div(8) == 8           |     |
| 求余   | rem  | (-32768_i16).wrapping_rem(-1) == 0    |     |
| 取负   | neg  | (-128_i8).checked_neg() == None       |     |
| 绝对值  | abs  | (-32768_i16).wrapping_abs() == -32768 |     |
| 求幂   | pow  | 3_u8.checked_pow(4) == Some(81)       |     |
| 按位左移 | shl  | 10_u32.wrapping_shl(34) == 40         |     |
| 按位右移 | shr  | 40_u64.wrapping_shr(66) == 10         |     |


### 1.1.3 数字运算

&ensp;&ensp;&ensp;上面提到了基本运算下面简单的来介绍一下数字运算。Rust 支持所有数字类型的基本数学运算：加法、减法、乘法、除法和求模运算。
```
fn main() {
    // 加法
    let sum = 5 + 10;
    // 减法
    let difference = 95.5 - 4.3;
    // 乘法
    let product = 4 * 30;
    // 除法
    let quotient = 56.7 / 32.2;
    // 求模
    let remainder = 43 % 5;       
}
```
&ensp;&ensp;&ensp;许多运算符号之后加上 = 号是自运算的意思，例如：sum += 1 等同于 sum = sum + 1。（涉及**所有权问题需注意**）<span style="color:red">（后面遇到代码这里再补充）</span>


&ensp;&ensp;&ensp;**注意**：Rust **不支持 ++ 和 --**，因为这两个运算符出现在变量的前后会影响代码可读性，减弱了开发者对变量改变的意识能力。

### 1.1.4 位运算


&ensp;&ensp;&ensp;Rust 的位运算基本上和其他语言一样。

|                   |                              |
| ----------------- | ---------------------------- |
| 运算符               | 说明                           |
| & 位与 （注意与& 引用相区分） | 相同位置均为1时则为1，否则为0             |
| \| 位或             | 相同位置只要有1时则为1，否则为0            |
| ^ 异或              | 相同位置不相同则为1，相同则为0             |
| ! 位非              | 把位中的0和1相互取反，即0置为1，1置为0       |
| << 左移             | 所有位向左移动指定位数，右位补0             |
| >> 右移             | 所有位向右移动指定位数，带符号移动（正数补0，负数补1） |
```
fn main() {
	// 无符号8位整数，二进制为00000010
	let a: u8 = 2; // 也可以写 let a: u8 = 0b_0000_0010;// 二进制为00000011
	let b: u8 = 3;
	// {:08b}：左高右低输出二进制01，不足8位则高位补0
	println!("a value is        {:08b}", a);
	println!("b value is        {:08b}", b);
	println!("(a & b) value is  {:08b}", a & b);
	println!("(a | b) value is  {:08b}", a | b);
	println!("(a ^ b) value is  {:08b}", a ^ b);
	println!("(!b) value is     {:08b}", !b);
	println!("(a << b) value is {:08b}", a << b);
	println!("(a >> b) value is {:08b}", a >> b);
	let mut a = a;
	// 注意这些计算符除了!之外都可以加上=进行赋值 (因为!=要用来判断不等于)
	a <<= b;
	println!("(a << b) value is {:08b}", a);
}
```

## 1.2 浮点数型（Floating-Point）

&ensp;&ensp;&ensp;Rust 提供了 IEEE 单精度浮点类型和 IEEE 双精度浮点类型。这些类型包括**正无穷大和负无穷大、不同的正零值和负零值，以及非数值**。

&ensp;&ensp;&ensp;浮点类型数字是**带有小数点**的数字，在 Rust 中浮点类型数字也有两种基本类型： f32 和 f64，分别为 32 位和 64 位大小。**默认浮点类型是 f64**，在现代的 CPU 中它的速度与 f32 几乎相同，但精度更高。

```
fn main() {
    // f32 类型的特殊值
    let f32_infinity = f32::INFINITY;           // 正无穷大
    let f32_neg_infinity = f32::NEG_INFINITY;   // 负无穷大
    let f32_nan = f32::NAN;                      // 非数值
    let f32_min = f32::MIN;                      // 最小有限值
    let f32_max = f32::MAX;                      // 最大有限值
    println!("f32: INFINITY = {}, NEG_INFINITY = {}, NAN = {}, MIN = {}, MAX = {}", f32_infinity, f32_neg_infinity, f32_nan, f32_min, f32_max);
    // f64 类型的特殊值
    let f64_infinity = f64::INFINITY;           // 正无穷大
    let f64_neg_infinity = f64::NEG_INFINITY;   // 负无穷大
    let f64_nan = f64::NAN;                      // 非数值
    let f64_min = f64::MIN;                      // 最小有限值
    let f64_max = f64::MAX;                      // 最大有限值
    println!("f64: INFINITY = {}, NEG_INFINITY = {}, NAN = {}, MIN = {}, MAX = {}",f64_infinity, f64_neg_infinity, f64_nan, f64_min, f64_max);
}
```

### 1.2.1 NaN

&ensp;&ensp;&ensp;对于**数学上未定义**的结果，例如对负数取平方根会产生一个特殊的结果：Rust 的浮点数类型使用 NaN (not a number) 来处理这些情况.出于防御性编程的考虑，可以使用 is_nan() 等方法，可以用来判断一个数值是否是 NaN ：

```
fn main() {
    let x = (-42.0_f32).sqrt();
    if x.is_nan() {
        println!("未定义的数学行为")
    }
}
```

### 1.2.2 浮点数陷阱

1. 浮点数往往是你想要数字的近似表达
浮点数类型是基于二进制实现的，学过计组应该知道这里的问题了。例如 0.1 在二进制上并不存在精确的表达形式，但是在十进制上就存在。

2. 浮点数在某些特性上是反直觉的

&ensp;&ensp; &ensp;例如大家都会觉得浮点数可以进行比较，对吧？

&ensp;&ensp; &ensp;是的，它们确实可以使用 >，>= 等进行比较，f32 ， f64 上的比较运算实现的是std::cmp::PartialEq 特征，但是并没有实现 std::cmp::Eq 特征。感兴趣自己可以查一下这两个特征是什么。

&ensp;&ensp;&ensp;为了避免上面说的两个陷阱，你需要**遵守以下准则**：

- 避免在浮点数上测试相等性;
- 当结果在数学上可能存在未定义时，需要格外的小心。
```
fn main() {
    let abc: (f32, f32, f32) = (0.1, 0.2, 0.3);
    let xyz: (f64, f64, f64) = (0.1, 0.2, 0.3);

    println!("abc (f32)");
    println!("   0.1 + 0.2: {:x}", (abc.0 + abc.1).to_bits());
    println!("         0.3: {:x}", (abc.2).to_bits());
    println!();

    println!("xyz (f64)");
    println!("   0.1 + 0.2: {:x}", (xyz.0 + xyz.1).to_bits());
    println!("         0.3: {:x}", (xyz.2).to_bits());
    println!();

    assert!(abc.0 + abc.1 == abc.2);
    assert!(xyz.0 + xyz.1 == xyz.2);
}
```
![|549](image/Pasted_image_20241106164418.png)

&ensp;&ensp; &ensp;对 f32 类型做加法时，0.1 + 0.2 的结果是 3e99999a，0.3 也是 3e99999a，因此 f32 下的 0.1 + 0.2 == 0.3 通过测试。

&ensp;&ensp; &ensp;在f64 类型时，结果就不一样了，因为 f64 精度高很多，因此在小数点非常后面发生了一点微小的变化，0.1 + 0.2 以 4 结尾，但是 0.3 以3结尾，这个细微区别导致 f64 下的测试失败了，并且抛出了异常。

### 1.2.3 As 完成类型转换

&ensp;&ensp; &ensp;**Rust 几乎不会执行任何隐式的数值转换**。如果函数需要 f64参数，那么传入 i32 型参数是错误的。事实上，Rust 甚至不会隐式地将 i16 值转换为 i32 值，虽然每个 i16 值都必然在 i32 范围内。

不过，你随时可以用 as 运算符写出显式转换：i as f64 或 x as i32。隐式整数转换有着导致错误和安全漏洞的大量“前科”，特别是在用这种整数表示内存中某些内容的大小时，很可能发生意外溢出。Rust 这种要求明确写出数值类型转换的行为，会提醒我们注意到一些可能错过的问题。
```
// 显式转换
fn main() {
    let int_value: i32 = 42;
    let float_value: f64 = 3.14;
    let small_int: i16 = 100;
    let converted_to_float: f64 = int_value as f64; // 将 i32 转换为 f64
    let converted_to_int: i32 = small_int as i32;   // 将 i16 转换为 i32

    println!("int_value as f64: {}", converted_to_float);
    println!("small_int as i32: {}", converted_to_int);

    // 直接传递类型不匹配的参数会导致编译错误
    // let result = add_float(int_value); // 这行代码会导致错误

    // 正确的调用方式，使用显式转换
    let result = add_float(int_value as f64);
    println!("Result of adding float: {}", result);
}
// 函数需要 f64 类型参数
fn add_float(value: f64) -> f64 {
    value + 1.0 // 进行简单的加法
}
```

&ensp;&ensp; &ensp;Rust 中可以使用 As 来完成一个类型到另一个类型的转换，其最常用于将原始类型转换为其他原始类型，但是它也可以完成诸如将指针转换为地址、地址转换为指针以及将指针转换为其他指针等功能。<span style="color:red">（需要添加后续笔记链接）</span>
## 1.3 布尔类型(bool)

&ensp;&ensp; &ensp;Rust 中的布尔类型值**只能**是：true 和 false，布尔值占用内存的大小为 1 个字节。

&ensp;&ensp; &ensp;这个地方和C++语言有点不一样的地方： true能写成1,false能写成0吗？事实说话。

![|775](image/Pasted_image_20241105203927.png)
```
fn main() { 
	let t = true; 
	let f: bool = false; 
	// 使用类型标注,显式指定f的类型 if f { println!("这是段毫无意义的代码"); 
	}
 }
```

&ensp;&ensp; &ensp;使用布尔类型的场景**主要在于流程控制**，例如上述代码的中的 if 就是其中之一。

&ensp;&ensp; &ensp;Rust 的 **as 运算符可以将 bool 值转换为整型**，但是，as **无法进行另一个方向（从数值类型到 bool）的转换**。相反，你必须显式地写出比较表达式。

```
fn main(){
    assert_eq!(false as i32, 0);
    assert_eq!(true  as i32, 1);
}
```

## 1.4 字符类型(char)

&ensp;&ensp; &ensp;Rust 的字符不仅仅是 ASCII，**所有的 Unicode 值都可以作为 Rust 字符**，包括单个的中文、日文、韩文、emoji 表情符号等等，都是合法的字符类型。

&ensp;&ensp; &ensp;Unicode 值的范围从 U+0000 到 U+D7FF 和 U+E000 到 U+10FFFF （包括两端），char 永远不会是“半代用区”中的码点（0xD800 到 0xDFFF 范围内的码点， 它们不能单独使用）。

&ensp;&ensp; &ensp;一般推荐使用字符串储存 UTF-8 文字（非英文字符尽可能地出现在字符串中）。在 Rust 中字符串和字符都必须使用 UTF-8 编码，否则编译器会报错。

&ensp;&ensp; &ensp;字符的Unicode码点在 U+0000 到 U+007F 范围内（也就是说，如果它是从 ASCII 字 符集中提取的），就可以把字符写为 '\xHH'，其中 HH 是两个十六进制数。例 如，字符字面量 '*' 和 '\x2A' 是等效的。（ 后面关于Unicode码点的我是真看不懂  这个地方应该是不是学习重点，以后遇到具体问题再学习）
```
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let g = '国';
    let heart_eyed_cat = '😻';
}
```

&ensp;&ensp; &ensp;由于 Unicode 都是 4 个字节编码，因此**字符类型也是占用 4 个字节**。

&ensp;&ensp; &ensp;**切记Rust 的字符只能用 '  ' 来表示， " " 是留给字符串的。**


## 1.5 元组(Tuple)

&ensp;&ensp; &ensp;元组是各种类型值的值对或三元组、四元组、五元组等（因此称为 n-元组或元 组）。

&ensp;&ensp; &ensp;其实你可以把数组[ ]和元组叫做**复合类型**。因为可以包含不同种类的数据(这句话有毛病可以忽略)。但他俩还是有点不同的。

+ 定义：() 表示一个元组，可以包含多个不同类型的值。
	- 用法：
		* 元组可以用来组合不同类型的值。
		* 元组的长度是固定的，且长度在编译时已知。
	- 示例：	
	```
	fn main(){
		let tuple: (i32, f64, char) = (42, 3.14, 'a');  //不同类型是这个意思
		println!("Tuple values: {:?}", tuple);
	}
	```
+ 和数组[ ]做一个简单对比 后面有对数组的详细介绍[[#1.7 数组  |数组]]
    - 类型：
		* 元组可以包含不同类型的元素； 
		* 数组只能包含相同类型的元素。
     - 长度：
	     * 元组的长度是固定的，但长度可以是不同的（不同的元组可以有不同数量的元素）；
	     * 数组的长度在定义时确定，并且所有数组的长度都是相同的。
+ 访问方式：
	- 元组可以通过位置来访问元素， tuple.0、tuple.1。
	- 数组可以通过索引来访问， array[0]。 
	- 
```
	fn  main(){
		let text = "I see the eigenvalue in thine eye";
		let temp = text.split_at(21);
		let head = temp.0;
		let tail = temp.1;
		assert_eq!(head, "I see the eigenvalue ");
		assert_eq!(tail, "in thine eye");
	}
```
&ensp;&ensp; &ensp;还有一个常用的元组类型是**零元组 ()**。传统上，这叫作单元类型，因为此类型只有 一个值，写作 ( )。

&ensp;&ensp; &ensp;当无法携带任何有意义的值但其上下文仍然要求传入某种类型时， Rust 就会使用单元类型。main 函数就返回这个单元类型 ()，你不能说 main 函数无返回值，因为没有返回值的函数在 Rust 中是有单独的定义的：**发散函数**( diverge function )，顾名思义，无法收敛的函数。

&ensp;&ensp; &ensp;例如，不返回值的函数的返回类型为 ()。常见的 println!() 的返回值就是单元类型 ()。

&ensp;&ensp; &ensp;Rust 始终允许在所有能用逗号的地方（函数参数、 数组、结构体和枚举定义，等等）添加额外的尾随逗号。 为了保持一致性，甚至有包含单个值的元组。字面量 ("lonely hearts",) 就 是一个包含单个字符串的元组，它的类型是 (&str,)。在这里，**值后面的逗号是必需 的，以用于区分单值元组和简单的括号表达式。**

### 1.5.1 用模式匹配解构元组

```
fn main() {
    let tup = (500, 6.4, 1);
    let (x, y, z) = tup;
    println!("The value of y is: {}", y);
}
```

&ensp;&ensp; &ensp;使用 let (x, y, z) = tup; 来完成一次模式匹配，因为元组是 (n1, n2, n3) 形式的，因此我们用一模一样的 (x, y, z) 形式来进行匹配，元组中对应的值会绑定到变量 x， y， z上。这就是**解构：用同样的形式把一个复杂对象中的值匹配出来。**

### 1.5.2 用 . 来访问元组

&ensp;&ensp; &ensp;Rust 提供了 **. 的访问方式**：和其它语言的数组、字符串一样，元组的索引从 0 开始。

```
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);
    let five_hundred = x.0;
    let six_point_four = x.1;
    let one = x.2;
}
```


### 1.5.3 元组的使用示例

&ensp;&ensp; &ensp;元组在函数返回值场景很常用，例如下面的代码，可以使用元组返回多个值：
```
fn main() {
    let s1 = String::from("hello");
    let (s2, len) = calculate_length(s1);
    println!("The length of '{}' is {}.", s2, len);
}
fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() 返回字符串的长度
    (s, length)
}
```

&ensp;&ensp; &ensp;calculate_length 函数接收 s1 字符串的所有权，然后计算字符串的长度，接着把字符串所有权和字符串长度再返回给 s2 和 len 变量。

## 1.6 指针类型

&ensp;&ensp; &ensp;Rust 有多种表示内存地址的类型，接下来将讨论 3 种指针类型：引用、Box 和不安全指针。

### 1.6.1 引用

&ensp;&ensp; &ensp;最简单的方式是将引用视为 Rust 中的基本指针类型.  [<font color="#ff0000">点击跳转</font>](#三.引用)

&ensp;&ensp; &ensp;对 i32 的引用是一个保存着 i32 地址的机器字，这个地址可能位于栈或堆中。表达式 &x 会生成 一个对 x 的引用，在 Rust 术语中，我们会说它借用了对 x 的引用。给定一个引用 r，表达式 *r 会引用 r 指向的值。

&ensp;&ensp; &ensp;Rust 引用有两种形式：
+ &T	
 一个不可变的共享引用。你可以同时拥有多个对给定值的共享引用，但它们是只读的：禁止修改它们所指向的值，就像 C 中的 const T* 一样。
```
fn main() {
//用 s1 的引用作为参数传递给 calculate_length 函数，而不是把 s1 的所有权转移给该函数
    let s1 = String::from("hello");
    let len = calculate_length(&s1);      
    println!("The length of '{}' is {}.", s1, len);
}
fn calculate_length(s: &String) -> usize {
    s.len()
}
```
+ &mut T 一个可变的、独占的引用。你可以读取和修改它指向的值，就像 C 中的 T* 一样。但是只要该引用还存在，就不能对该值有任何类型的其他引用。事实上，访问该值的唯一途径就是使用这个可变引用。

&ensp;&ensp; &ensp;Rust 利用共享引用和可变引用之间的“**二选一**”机制（只有一个可变引用或者多个不可变引用）来强制执行“**单个写入者或多个读取者**”规则：或者独占写一个值，或者让任意数量的读取者共享，但二者只能选择其一。这种限制的好处就是使 Rust 在编译期就避免数据竞争，数据竞争可由以下行为造成：

1. 两个或更多的指针同时访问同一数据
2. 至少有一个指针被用来写入数据
3. 没有同步数据访问的机制

```
fn main() {
//用 s1 的引用作为参数传递给 calculate_length 函数，而不是把 s1 的所有权转移给该函数
    let s1 = String::from("hello");
    let len = calculate_length(&s1);      
    println!("The length of '{}' is {}.", s1, len);
}
fn calculate_length(s: &String) -> usize {
    s.len()
}
```

&ensp;&ensp; &ensp;来吧见识一下NLL吧！！（Rust 1.31 后引入）

&ensp;&ensp; &ensp;对于这种编译器优化行为，Rust 专门起了一个名字 —— Non-Lexical Lifetimes(NLL)，专门用于找到某个引用在作用域(})结束前就不再被使用的代码位置。（Rust编译器,天才第一步）

```
fn main() {
   let mut s = String::from("hello");
    let r1 = &s;
    let r2 = &s;
    //let r3 = &mut s;  //这里会报错
    println!("{} and {}", r1, r2);
    // 新编译器中，r1,r2作用域在这里结束
    let r3 = &mut s;
    //let r4 = &s;      //这里会报错
    println!("{}", r3);
} // 老编译器中，r1、r2、r3作用域在这里结束
// 新编译器中，r3作用域在这里结束
```

### 1.6.2 Box

&ensp;&ensp; &ensp;在堆中分配值的最简单方式是使用 Box::new。（这里**需要对内存的栈和堆有一个认识**，后面学习依旧要用到，这里不在做笔记）Box 是一个智能指针，它在堆上分配内存并提供对该内存的安全访问。使用 Box 可以在运行时动态分配内存，并且可以存储大小在编译时未知的类型。

```
fn main() {
    // 在堆上分配一个 i32 值
    let boxed_value = Box::new(42);
    // 访问堆上的值
    println!("The value in the box is: {}", boxed_value);
    // 通过解引用访问原始值
    let value = *boxed_value;
    println!("The unboxed value is: {}", value);
}
```

&ensp; &ensp; &ensp;Box\<T> 是指向存储在堆上的 T 类型值的指针。可以调用 Box::new(v) 分配一些堆空间，将值 v 移入其中，并返回一个指向该堆空间的 Box。因为 Box 拥有它所指向的空间，所以当丢弃 Box 时，也会释放此空间。
```
fn main(){
    let point = Box::new((0.625, 0.5));  // 在此分配了point
    let label = format!("{:?}", point);  // 在此分配了label
    assert_eq!(label, "(0.625, 0.5)");
}
```
![|675](image/{{所有权2.1}}-20241108-1.png)

&ensp; &ensp; &ensp;栈帧本身包含变量 point 和 label，其中每个变量都指向其拥有的堆中内存。label在栈帧中存储的是什莫？
![|337](image/{{所有权2.1}}-20241108-7.png)
&ensp; &ensp; &ensp;当丢弃它们时，它们拥有的堆中内存也会一起被释放。
### 1.6.3 不安全指针(裸指针)

&ensp;&ensp; &ensp;Rust 也有裸指针类型 *mut T 和 *const T。裸指针实际上和 C++ 中的指针很像。使用裸指针是不安全的，因为Rust 不会跟踪它指向的内容。例如，裸指针可能为空，或者它们可能指向已释放的内存或现在包含不同类型的值。C++ 的所有经典指针错误都可能“借尸还魂”。

&ensp;&ensp; &ensp;你只能在 unsafe 块中对裸指针解引用（dereference）。unsafe 块是Rust 高级语言特性中的可选机制，其安全性取决于你自己。如果代码中没有 unsafe块（或者虽然有但编写正确），那么本书中强调的安全保证就仍然有效。<span style="color:red">（需要进一步的代码补充 后面遇到会补充）</span>

## 1.7 数组
### 1.7.1 数组的基本声明

&ensp;&ensp; &ensp;在 Rust 中，数组的声明形式如下：

&ensp;&ensp; &ensp;`let lazy_caterer: [u32; 6] = [1, 2, 4, 7, 11, 16]; // 声明一个固定长度的数组`
- \[u32; 6] 说明这是一个长度为 6 的数组，元素类型是 u32类型。
- **数组是固定大小**的，在编译时长度就已经确定。

&ensp;&ensp; &ensp;还可以在数组中放入多个值：

```
fn main(){
	let taxonomy = ["Animalia", "Arthropoda", "Insecta"];  // 声明一个字符串数组
	assert_eq!(taxonomy.len(), 3);  // 数组长度是 3
	assert_eq!(taxonomy[1], "Arthropoda");  
}
// 索引从 0 开始，第二个元素是 "Arthropoda"
```

1.7.2 使用 \[V; N] 语法创建固定大小的数组

&ensp;&ensp; &ensp;Rust 允许使用 \[V; N] 的语法来创建一个元素都为 V 且长度为 N 的数组。

```
fn main(){
let mut sieve = [true; 10000];  // 创建一个长度为 10000 的数组，所有值为 true
for i in 2..100 {
    if sieve[i] {
        let mut j = i * i;
        while j < 10000 {
            sieve[j] = false;  // 标记非质数
            j += i;
        }
    }
}
assert!(sieve[211]);  // 211 是质数
assert!(!sieve[9876]);  // 9876 不是质数
}
```

- 使用 \[true; 10000] 创建一个布尔值数组，所有值初始化为 true。
- 该算法是著名的埃拉托斯特尼筛法，用于筛选质数。

### 1.7.3 数组和切片

&ensp;&ensp; &ensp;数组的一个重要特性是它可以作为切片来使用。切片是对数组（或向量）的引用，提供了一种更加灵活的访问方式，且切片的长度是可以变化的。

&ensp;&ensp; &ensp;Rust 中的数组方法大多是通过切片来实现的，常见的切片方法包括 sort、iter、len 等。

```
fn main(){
	let mut chaos = [3, 5, 4, 1, 2];
	chaos.sort();  // 排序
	assert_eq!(chaos, [1, 2, 3, 4, 5]);  // 排序后的数组是 [1, 2, 3, 4, 5]
}
```

- sort 方法是定义在切片上的，但它可以通过数组的引用来隐式地调用。
- Rust 会自动将数组 chaos 转换为 &mut [i32] 类型的切片引用，然后再调用 sort 方法。

### 1.7.4 数组的不可变和可变借用

&ensp;&ensp; &ensp;数组是栈上的固定大小的集合，您可以借用它们，但必须遵守不可变或可变借用规则：

- 不可变借用：允许您以只读方式访问数组中的元素。
- 可变借用：允许修改数组中的元素。
```
fn main(){
	let mut nums = [1, 2, 3];
	let nums_ref = &mut nums;  // 可变借用
	nums_ref[0] = 42;  // 修改 nums 的第一个元素
}
```

### 1.7.5 数组的大小是固定的

&ensp;&ensp; &ensp;Rust 的数组长度在编译时是固定的，因此不能在运行时动态改变数组的大小。

```
fn main(){
	let n = 5;
	let arr = [0; n];  // 错误：`n` 需要是常量
}
```

&ensp;&ensp; &ensp;为了处理大小动态的数组，Rust 提供了**向量（Vec）类型，它在运行时可以动态增长或缩小。**

### 1.7.6 数组的不可变和可变引用的例子

```
fn main() {
    let mut arr = [1, 2, 3];
    // 不可变借用
    let ref1 = &arr;  
    println!("ref1: {:?}", ref1);  // 引用数组，输出：[1, 2, 3]
    // 可变借用
    let ref2 = &mut arr;  
    ref2[0] = 42;  // 修改数组
    println!("ref2: {:?}", ref2);  // 引用修改后的数组，输出：[42, 2, 3]
    // 再次使用不可变借用
    let ref3 = &arr;
    println!("ref3: {:?}", ref3);  // 引用修改后的数组，输出：[42, 2, 3]
}
```

### 1.7.7 总结

- 固定大小：数组的大小在编译时确定，因此无法动态更改长度。
- 切片：数组可以作为切片使用，切片方法与数组操作非常相似，数组本身被隐式转换为切片。
- 不可变和可变引用：Rust 中的数组遵循严格的所有权和借用规则，可通过借用来访问和修改数组的元素。
- 初始化方法：使用 \[value; length] 可以初始化固定大小的数组，所有元素值都相同。
## 1.8 向量

&ensp;&ensp; &ensp;在 Rust 中，Vec 是一种非常重要的集合类型，代表一个可以动态增长和缩小的向量。它提供了一个灵活、可调整大小的数组，内存分配在堆上，使得我们可以在运行时动态地操作数据。

### 1.8.1 创建向量

+ 使用 vec! 宏    最简单的方式是使用 vec! 宏，它类似于数组字面量的语法，用于快速创建一个向量：

```
fn mian(){
	let mut primes = vec![2, 3, 5, 7];  // 创建一个包含质数的向量
	assert_eq!(primes.iter().product::<i32>(), 210);  // 计算元素的乘积
}
```

 &ensp;&ensp; &ensp;vec!\[2, 3, 5, 7] 创建一个包含指定元素的向量。

+ 动态添加元素    向量是动态可变的，我们可以使用 push 方法向向量添加元素：

```
fn mian(){
	let mut primes = vec![2, 3, 5, 7];  // 创建一个包含质数的向量
	primes.push(11);  // 向向量添加元素
	primes.push(13);
	assert_eq!(primes.iter().product::<i32>(), 30030);  // 更新后的元素乘积
}
```

+ 创建具有重复值的向量    可以通过指定元素和重复次数来创建一个具有重复值的向量：

```
fn new_pixel_buffer(rows: usize, cols: usize) -> Vec<u8> {
    vec![0; rows * cols]  // 创建一个大小为 rows * cols 的向量，每个元素都是 0
}
```

+ 使用 Vec::new 创建空向量

&ensp;&ensp; &ensp;另外，也可以通过 Vec::new() 来创建一个空的向量，然后逐个添加元素：

```
fn main(){
	let mut pal = Vec::new();
	pal.push("step");
	pal.push("on");
	pal.push("no");
	pal.push("pets");
	assert_eq!(pal, vec!["step", "on", "no", "pets"]);
}
```

+ 从迭代器创建向量

```
fn mian(){
	let v: Vec<i32> = (0..5).collect();  // 使用 collect 将迭代器生成的值收集成向量
	assert_eq!(v, [0, 1, 2, 3, 4]);	
}
```

&ensp;&ensp; &ensp;collect 方法根据上下文的类型推断，默认将结果收集为向量，但也可以指定其他类型的集合。

### 1.8.2 与数组的相似性

&ensp;&ensp; &ensp;虽然数组和向量在 Rust 中都是集合类型，数组的大小在编译时确定，而向量的大小在运行时动态变化。向量支持与切片类似的方法，比如 sort()、reverse() 等：

```
fn main(){
	let mut palindrome = vec!["a man", "a plan", "a canal", "panama"];
	palindrome.reverse();  // 反转向量
	assert_eq!(palindrome, vec!["panama", "a canal", "a plan", "a man"]);
}
```

### 1.8.3 向量的容量管理

&ensp;&ensp; &ensp;向量在堆上分配内存，并且随着元素的添加，向量会自动扩展。Vec 由 3 个部分组成：指向堆中元素的指针、缓冲区能存储的元素数量、以及当前实际包含的元素数量。

+ Vec::with_capacity

&ensp;&ensp; &ensp;如果知道向量的初始大小，可以使用 Vec::with_capacity 来避免不必要的内存分配：
```
fn main(){
	let mut v = Vec::with_capacity(2);
	assert_eq!(v.len(), 0);
	assert_eq!(v.capacity(), 2);
	v.push(1);
	v.push(2);
	assert_eq!(v.len(), 2);
	assert_eq!(v.capacity(), 2);  // 容量保持 2
	v.push(3);
	println!("capacity is now {}", v.capacity());  // 容量通常会扩展为 4
}
```

 - capacity() 返回当前向量能够容纳的最大元素数，而不需要进行内存重新分配。
 - 当向量超过容量时，它会自动增加容量。

### 1.8.4 向量的修改操作

+ 插入元素

&ensp;&ensp; &ensp;可以在任意位置插入元素：

```
fn main(){
	let mut v = vec![10, 20, 30, 40, 50];
	v.insert(3, 35);  // 在索引为 3 的位置插入 35
	assert_eq!(v, [10, 20, 30, 35, 40, 50]);
}
```

+  删除元素

&ensp;&ensp; &ensp;可以通过索引删除元素：

```
fn main(){
	v.remove(1);  // 移除索引为 1 的元素
	assert_eq!(v, [10, 30, 35, 40, 50]);
}
```

+ 弹出元素

&ensp;&ensp; &ensp;可以使用 pop 方法从向量中移除最后一个元素，并返回一个 Option：

```
fn main(){
	let mut v = vec!["Snow Puff", "Glass Gem"];
	assert_eq!(v.pop(), Some("Glass Gem"));  // 弹出 "Glass Gem"
	assert_eq!(v.pop(), Some("Snow Puff"));  // 弹出 "Snow Puff"
	assert_eq!(v.pop(), None);  // 向量为空，返回 None
}
```

### 1.8.5 遍历向量

&ensp;&ensp; &ensp;可以使用 for 循环遍历向量：
```
fn main(){
	let languages: Vec<String> = std::env::args().skip(1).collect();
	for l in languages {
	    println!("{}: {}", l,
	             if l.len() % 2 == 0 {
	                 "functional"
	             } else {
	                 "imperative"
	             });
	}
}
```

&ensp;&ensp; &ensp;这段代码展示了如何将命令行参数收集为向量，并根据字符串的长度判断其是函数式语言还是命令式语言。

### 1.8.6 总结

- Vec 是一个可动态增长的集合，适用于需要动态调整大小的场景。
- 通过 vec! 宏、Vec::new、Vec::with_capacity 和迭代器等方法可以创建和初始化向量。
- 向量可以通过切片方法进行操作（如 sort()、reverse()），也支持修改操作（如 push()、insert()、remove()）。
- 向量的内存管理会自动扩展，Vec::capacity() 和 Vec::with_capacity 提供了更高效的容量管理。
- 向量与数组的区别在于，向量的大小在运行时是动态的，而数组的大小在编译时是固定的。

&ensp;&ensp; &ensp;Rust 中的 Vec 类型非常灵活，适合用于处理需要动态增长的列表，几乎可以在任何需要动态集合的场景中使用。

## 1.9 字符串类型

&ensp;&ensp; &ensp;在 Rust 中，字符串的处理方式与 C++ 和其他编程语言有一些相似之处，但也有独特的设计。Rust 提供了多种方式来处理字符串，包括字符串字面量、字节串和动态字符串类型（String）。Rust 中的字符是 Unicode 类型，因此每个字符占据 4 个字节内存空间，但是在字符串中不一样，**字符串是 UTF-8 编码**，也就是字符串中的字符所占的字节数是变化的(1 - 4)，这样有助于大幅降低字符串所占用的内存空间。

&ensp;&ensp; &ensp;Rust 在语言级别，只有一种字符串类型： str，它通常是以引用类型出现 &str，也就是上文提到的字符串切片。虽然语言级别只有上述的 str 类型，但是在标准库里，还有多种不同用途的字符串类型，其中使用最广的即是 String 类型。

&ensp;&ensp; &ensp;str 类型是硬编码进可执行文件，也无法被修改，但是 String 则是一个可增长、可改变且具有所有权的 UTF-8 编码字符串，当 Rust 用户提到字符串时，往往指的就是 String 类型和 &str 字符串切片类型，这两个类型都是 UTF-8 编码。

&ensp;&ensp; &ensp;除了 String 类型的字符串，Rust 的标准库还提供了其他类型的字符串，例如 OsString， OsStr， CsString 和 CsStr 等

### 1.9.1 字符串字面量

&ensp; &ensp; &ensp;字符串字面量是在代码中直接书写的字符串，它们以双引号包围。可以使用**转义序列来处理特殊字符，如换行符、双引号**等。

- 基本的字符串字面量

```
let speech = "\"Ouch!\" said the well.\n";
```

&ensp; &ensp; &ensp;在这个例子中，\" 转义了双引号，\n 表示换行符。

- 多行字符串 Rust 支持跨多行的字符串字面量，自动包含换行符和空格：

```
fn main(){
println!("In the room the women come and go, Singing of Mount Abora");
}
```
&ensp; &ensp; &ensp;这里字符串包含换行符，甚至在第二行的开头有空格。

- 行连接 可以用反斜杠 \ 来连接多行字符串，连接时会丢弃换行符和多余的空格：

```
fn main(){
	println!("In the room the women come and go,
	Singing of Mount Abora");
}
```

&ensp; &ensp; &ensp;输出会是单行文本，注意反斜杠前的空格仍然会保留。

- 原始字符串 原始字符串用 r 前缀标记，允许字符串直接包含反斜杠而不进行转义，非常适合处理文件路径或正则表达式。

```
fn main(){
	let default_win_install_path = r"C:\Program Files\Gorillas";
	let pattern = Regex::new(r"\d+(\.\d+)*");
}
```
&ensp; &ensp; &ensp;为了处理包含双引号的字符串，可以使用 r###"..."### 语法：
```
fn main(){
println!(r###"
This raw string started with 'r###"'.
Therefore it does not end until we reach a quote mark ('"')
followed immediately by three pound signs ('###'):
"###);
}
```
### 1.9.2 字节串（Byte String）

&ensp; &ensp; &ensp;字节串以 b 前缀标记，用于表示由字节（u8）构成的字符串，而不是 Unicode 字符。它们通常用于处理原始二进制数据。

- 字节串的定义

```
fn main(){
	let method = b"GET";
	assert_eq!(method, &[b'G', b'E', b'T']);
}
```

- 字节串的多行表示

&ensp; &ensp; &ensp;与普通字符串类似，字节串也可以跨多行，并且可以使用反斜杠连接行：

```
let pattern = br"\d+(\.\d+)*";
```

&ensp; &ensp; &ensp;字节串的类型是 &\[u8]，它只支持 ASCII 字符和少数的 \xHH 转义序列。

### 1.9.3 内存中的字符串

&ensp; &ensp; &ensp;Rust 中的字符串是 UTF-8 编码的，这意味着它们可以高效地存储多种语言的字符。

- String和 &str：

	- String 是一个动态增长的字符串类型，存储在堆上，支持添加、修改等操作。
	- &str 是一个指向已有 UTF-8 字符数据的不可变引用，通常表示字符串字面量。

- String 和 &str 的内存布局：

	- String 存储在堆上，可以动态增长。
	- &str 是一个胖指针，包含指向数据的地址和长度。

```
let noodles = "noodles".to_string();  // 创建 String
let oodles = &noodles[1..];           // 创建 &str 切片
let poodles = "ಠ_ಠ";                 // 字符串字面量
```

&ensp; &ensp; &ensp;字符串的底层的数据存储格式实际上是\[ u8 ]，一个字节数组。对于

```
let hello = String::from("中国人");
```

&ensp; &ensp; &ensp;如果问你该字符串多长，你可能会说 3，但是实际上是 9 个字节的长度，因为大部分常用汉字在 UTF-8 中的长度是 3 个字节，因此这种情况下对 hello 进行索引，访问 &hello\[0] 没有任何意义，因为你取不到 中 这个字符，而是取到了这个字符三个字节中的第一个字节.<span style="color:red">（需要补充代码说明）</span>

### 1.9.4 String 类型

&ensp; &ensp; &ensp;String 是一个可变的、在堆上分配内存的字符串类型。它与 Vec 类似，但会保证其中的内容是有效的 UTF-8。
+ 创建 String：
     - 使用 .to_string() 方法将 &str 转换为 String：
	 - 使用  format! 宏生成新的 String：
	 - 连接多个字符串：
```
fn main(){
	let error_message = "too many pets".to_string();
	let formatted_string = format!("{}°{:02}′{:02}″N", 24, 5, 23);
	let bits = vec!["veni", "vidi", "vici"];
	assert_eq!(bits.concat(), "venividivici");
	assert_eq!(bits.join(", "), "veni, vidi, vici");
}
```

&ensp; &ensp; &ensp;那么如何将 String 类型转为 &str 类型呢？答案很简单，取引用即可：

```
fn main() {
    let s = String::from("hello,world!");
    say_hello(&s);
    say_hello(&s[..]);
    say_hello(s.as_str());
}

fn say_hello(s: &str) {
    println!("{}",s);
}
```

&ensp; &ensp; &ensp;实际上这种灵活用法是因为 deref 隐式强制转换.

### 1.9.5 使用字符串

&ensp; &ensp; &ensp;Rust 字符串类型支持许多操作，包括**比较、查找、替换和拆分 追加、插入、替换、删除、连接**等。
+ 字符串比较

&ensp; &ensp; &ensp;使用 == 和 != 进行字符串的比较：

```
assert!("ONE".to_lowercase() == "one");
```

+ 字符串查找和替换

```
assert!("peanut".contains("nut")); assert_eq!("ಠ_ಠ".replace("ಠ", "■"), "■_■");
```

+ 去除空白字符

```
assert_eq!(" clean\n".trim(), "clean");
```

+ 字符串拆分

```
for word in "veni, vidi, vici".split(", ") { assert!(word.starts_with("v")); }
```

+ 追加（Push）
   *  push(): 向字符串尾部追加一个字符（char）。
   * push_str(): 向字符串尾部追加一个字符串字面量（&str）。

&ensp; &ensp; &ensp;这两个方法会直接修改原有字符串，因此需要使用 mut 修饰字符串变量。

```
fn main() {
    let mut s = String::from("Hello ");
    s.push_str("rust");
    println!("追加字符串 push_str() -> {}", s);
    s.push('!');
    println!("追加字符 push() -> {}", s);
}
```
+ 插入（Insert）
	- insert(): 在指定位置插入一个字符。
	- insert_str(): 在指定位置插入一个字符串字面量（&str）。
	- 插入操作需要提供位置索引（从 0 开始）。
```
fn main() {
    let mut s = String::from("Hello rust!");
    s.insert(5, ',');
    println!("插入字符 insert() -> {}", s);
    s.insert_str(6, " I like");
    println!("插入字符串 insert_str() -> {}", s);
}
```
+ 替换（Replace）
	- replace(): 替换所有匹配的字符串，返回一个新的字符串。
	- replacen(): 替换前 n 个匹配的字符串，返回一个新的字符串。
	- replace_range(): 替换指定范围内的字符，直接修改原字符串。
```
fn main() {
    let string_replace = String::from("I like rust. Learning rust is my favorite!");
    let new_string_replace = string_replace.replace("rust", "RUST");
    dbg!(new_string_replace);

    let string_replacen = "I like rust. Learning rust is my favorite!";
    let new_string_replacen = string_replacen.replacen("rust", "RUST", 1);
    dbg!(new_string_replacen);

    let mut string_replace_range = String::from("I like rust!");
    string_replace_range.replace_range(7..8, "R");
    dbg!(string_replace_range);
}
```

+ 删除（Delete）
	- pop(): 删除并返回字符串的最后一个字符。
	- remove(): 删除指定位置的字符，返回被删除的字符。
	- truncate(): 从指定位置开始删除直到结尾。
	- clear(): 清空字符串。

```
fn main() {
    let mut string_pop = String::from("rust pop 中文!");
    let p1 = string_pop.pop();
    let p2 = string_pop.pop();
    dbg!(p1);  // Some('!')
    dbg!(p2);  // Some('文')
    dbg!(string_pop);  // "rust pop 中"

    let mut string_remove = String::from("测试remove方法");
    string_remove.remove(0);
    dbg!(string_remove);  // "试remove方法"

    let mut string_truncate = String::from("测试truncate");
    string_truncate.truncate(3);
    dbg!(string_truncate);  // "测"

    let mut string_clear = String::from("string clear");
    string_clear.clear();
    dbg!(string_clear);  // ""
}
```

+ 连接（Concatenate）
	- 使用 + 或 +=: 连接字符串时，右侧必须是 &str 类型切片，且 + 会转移所有权。
	- format!(): 格式化字符串并连接，不会转移所有权，适用于 String 和 &str。

```
fn main() {
    let string_append = String::from("hello ");
    let string_rust = String::from("rust");
    let result = string_append + &string_rust;
    let mut result = result + "!"; // `result + "!"` 会返回新的 String
    result += "!!!";
    println!("连接字符串 + -> {}", result);

    let s1 = "hello";
    let s2 = String::from("rust");
    let s = format!("{} {}!", s1, s2);
    println!("{}", s);  // "hello rust!"
}
```

总结
- Rust 的 String 类型是可变的堆分配字符串，而 &str 是对已经存在的字符串的借用。
- 常用操作包括追加（push_str()、push()）、插入（insert()、insert_str()）、替换（replace()、replacen()、replace_range()）、删除（pop()、remove()、truncate()、clear()）和连接（+、+=、format!()）。
- 在使用 + 进行连接时，要注意所有权转移的问题，避免误用未再赋值的变量。

### 1.9.6 其他类似字符串的类型

&ensp; &ensp; &ensp;Rust 提供了多种类似字符串的类型，处理不同的场景，特别是当与非 UTF-8 数据或系统进行互操作时：<span style="color:red">（后续遇到再补充）</span>
- PathBuf 和 Path：用于处理文件路径。
- Vec 和 &\[u8]：用于处理二进制数据。
- OsString 和 &OsStr：用于处理操作系统特有的字符串（如环境变量名、命令行参数）。
- CString 和 &CStr：用于与 C 语言的 null 结尾字符串进行互操作。

### 1.9.7 总结

&ensp; &ensp; &ensp;Rust 提供了灵活且强大的字符串处理方式，允许程序员高效地处理 UTF-8 字符串、字节串及其他格式的数据。在处理字符串时，&str 是不可变的引用类型，而 String 则是可变的、在堆上分配内存的类型。理解这些类型的区别，以及如何选择它们，将帮助你在 Rust 中更加高效地处理字符串。

## 1.10 切片(slice)

&ensp; &ensp; &ensp;在 Rust 中，切片（slices）是对数组或字符串的一部分的引用，允许你借用数据的一部分而不需要复制它。切片可以应用于数组、Vec 和 String 类型。

### 1.10.1 数组和 Vec 的切片

+ 切片的基本语法

&ensp; &ensp; &ensp;切片是对数组或 Vec 的引用，它没有所有权，并且是不可变的或可变的。切片的语法如下：
```let arr = [1, 2, 3, 4, 5];
let slice = &arr[1..4];  // 切片从索引1到3（不包括4），即 [2, 3, 4]
```
+ 数组切片示例
```
fn main(){
	let arr = [10, 20, 30, 40, 50];
    let slice = &arr[1..4];  // 从索引 1 到 3 的切片
    println!("{:?}", slice); // 输出: [20, 30, 40]
    let full_slice = &arr[..]; // 包含所有元素
    println!("{:?}", full_slice); // 输出: [10, 20, 30, 40, 50]
    let first_two = &arr[..2];  // 前两个元素
    println!("{:?}", first_two); // 输出: [10, 20]
}
```

+ Vec 的切片示例

```
fn main() {
    let vec = vec![10, 20, 30, 40, 50];
    
    let slice = &vec[1..4]; // 切片从索引 1 到 3
    println!("{:?}", slice); // 输出: [20, 30, 40]
}
```

### 1.10.2 字符串切片（&str）

&ensp; &ensp; &ensp;对于 String 和字符串字面量（&str），切片操作类似，但由于字符串的字符是 Unicode 编码的，所以切片的起止位置必须是有效的字符边界。可以使用 get() 方法避免索引越界。

+ 字符串切片示例

```
fn main() {
    let s = String::from("Hello, Rust!");
    let slice = &s[7..11]; // 字符串从第 7 到第 10 个字节
    println!("{}", slice); // 输出: Rust
}
```

+ 使用 get() 方法

&ensp; &ensp; &ensp;get() 方法返回一个 Option<&str>，**可以避免越界错误**：

```
fn main() {
    let s = String::from("Hello, Rust!");
    match s.get(7..11) {
        Some(slice) => println!("{}", slice), // 输出: Rust
        None => println!("Out of bounds!"),
    }
}
```

### 1.10.3 切片的特性

- 不可变切片：默认情况下，切片是不可变的。例如，&arr[1..4] 是一个不可变切片，不能修改原数据。
- 可变切片：可以通过使用 &mut 获取一个可变切片，它允许你修改原数组或 Vec 的部分内容。

```
fn main() {
    let mut arr = [10, 20, 30, 40, 50];
    let slice = &mut arr[1..4]; // 可变切片
    slice[0] = 100; // 修改切片内容
    println!("{:?}", arr); // 输出: [10, 100, 30, 40, 50]
}
```

### 1.10.4 切片的使用场景

- 提高效率：切片通过借用数据的一部分避免了数据的复制。
- 函数参数传递：切片常常用作函数参数，避免传递整个数组或字符串。
- 避免不必要的内存开销：切片通过对数据的一部分进行引用而不是复制，可以节省内存开销。
```
fn print_slice(slice: &[i32]) {
    for &item in slice {
        println!("{}", item);
    }
}
fn main() {
    let arr = [1, 2, 3, 4, 5];
    print_slice(&arr[1..4]); // 传递切片
}
```

### 1.10.5 切片的**边界注意事项**

- 字符边界：对于 String 和 &str，切片的开始和结束位置必须在有效字符边界上，否则会引发运行时错误（panic!）。
- 越界访问：在使用数组或 Vec 的切片时，若切片索引越界，Rust 会引发 panic!。

### 1.10.6 总结

- 切片是一种对数组、Vec 或 String 的引用，不会拥有数据，且可以是不可变或可变的。
- 使用切片可以避免复制数据，节省内存开销，且切片操作的语法简单。
- 处理字符串切片时要注意 Unicode 字符的边界，确保不会跨越字符的边界。

&ensp; &ensp; &ensp;切片是 Rust 中非常强大的工具，掌握它可以使得你在进行数组、字符串等数据处理时更加高效。

## 1.11 类型别名(type)

&ensp; &ensp; &ensp;与 C++ 中的 typedef 用法类似，可以使用 type 关键字来为现有类型声明一个新名称：

```
type Bytes = Vec<u8>;
//这里声明的类型 Bytes 就是这种特定 Vec 的简写形式。
fn decode(data: &Bytes) {
...
}
```
# 二.所有权机制

&ensp; &ensp; &ensp;所有的程序都必须和计算机内存打交道，如何从内存中申请空间来存放程序的运行内容，如何在不需要的时候释放这些空间，成了重中之重，也是所有编程语言设计的难点之一。在计算机语言不断演变过程中，出现了三种流派：

- **垃圾回收机制(GC)**，在程序运行时不断寻找不再使用的内存，典型代表：Java、Go
- **手动管理内存的分配和释放**, 在程序中，通过函数调用的方式来申请和释放内存，典型代表：C++
- **通过所有权来管理内存**，编译器在编译时会根据一系列规则进行检查。

&ensp; &ensp; &ensp;其中 Rust 选择了第三种，最妙的是，这种检查只发生在编译期，因此对于程序运行期，不会有任何性能上的损失。
## 2.1 所有权

&ensp; &ensp; &ensp;当你的代码调用一个函数时，传递给函数的参数（包括可能指向堆上数据的指针和函数的局部变量）依次被压入栈中，当函数调用结束时，这些值将被从栈中按照相反的顺序依次移除。

&ensp; &ensp; &ensp;因为堆上的数据缺乏组织，因此跟踪这些数据何时分配和释放是非常重要的，否则堆上的数据将产生内存泄漏 —— 这些数据将永远无法被回收。这就是 Rust 所有权系统为我们提供的强大保障。

&ensp; &ensp; &ensp;通过内存上的关系来进一步认识“所有权”：

![|575](image/{{所有权2.1}}-20241108.png)
```
fn print_padovan() {
    let mut padovan = vec![1,1,1];  // 在此分配
    for i in 3..10 {
        let next = padovan[i-3] + padovan[i-2];
        padovan.push(next);
    }
    println!("P(1..10) = {:?}", padovan);
}                                   // 在此丢弃
```
&ensp; &ensp; &ensp;请注意，保存 padovan 指针、容量和长度的字都直接位于print_padovan 函数的栈帧中，只有向量的缓冲区才分配在堆上。

![|675](image/{{所有权2.1}}-20241108-2.png)
```
struct Person { name: String, birth: i32 }
fn main(){
    let mut composers = Vec::new();
    
    composers.push(Person { name: "Palestrina".to_string(),birth: 1525 });
    composers.push(Person { name: "Dowland".to_string(), birth: 1563 });
    composers.push(Person { name: "Lully".to_string(), birth: 1632 });
    
    for composer in &composers {
        println!("{}, born {}", composer.name, composer.birth);
    }
}
```
&ensp; &ensp; &ensp;composers 拥有一个向量，向量拥有自己的元素，每个元素都是一个 Person 结构体，每个结构体都拥有自己的字段，并且字符串字段拥有自己的文本。当控制流离开声明 composers 的作用域时，程序会丢弃自己的值并将整棵所有权树一起丢弃。

&ensp; &ensp; &ensp;每个值都有一个唯一的拥有者，因此很容易决定何时丢弃它。Rust 的单一拥有者规则将禁止任何可能让它们排列得比树结构更复杂的可能性。Rust 程序中的每一个值都是某棵树的成员，树根是某个变量。

&ensp; &ensp; &ensp;在 Rust 中丢弃一个值的方式就是从所有权树中移除它：或者离开变量的作用域，或者从向量中删除一个元素，或者执行其他类似的操作。

&ensp; &ensp; &ensp;所有权的概念仍然过于严格，还处理不了某些场景。Rust 从几个方面扩展了这种简单粗暴的思想。

+ 可以将值从**一个拥有者转移给另一个拥有者（移动）**。这允许你构建、重新排列和拆除树形结构。
+ 像整数、浮点数和字符这样的非常简单的类型，不受所有权规则的约束。这些称为 **Copy 类型**。
 + 标准库提供了引用计数指针类型 **Rc 和 Arc**，它们允许值在某些限制下有多个拥有者。
+ 可以对值进行“**借用”（borrow）**，以获得值的引用。这种引用是非拥有型指针，有着受限的生命周期。

&ensp; &ensp; &ensp;每一个策略都为所有权模型带来了灵活性，但同时仍然坚持着 Rust 的那些承诺。接下来我们将依次解释这几种方式中所有权的变化（看标题）。
## 2.2 移动（Move）

&ensp; &ensp; &ensp;在 Rust 中，对大多数类型来说，像为变量赋值、将其传给函数或从函数返回这样的操作都不会复制值，而是会移动值。说到复制，在C++中有这样的两个词：浅拷贝、深拷贝，本身就学习过这两个词的含义，我想本节的内容手拿手掐。

```
fn main(){
    let s = vec!["udon".to_string(), "ramen".to_string(), "soba".to_string()];
    let t = s;
    let u = s;
}
```

![|650](image/{{所有权2.1}}-20241108-4.png)
&ensp; &ensp; &ensp;大多数类型的赋值会将值从源转移给目标，而源会回到**未初始化状态。**
![|600](image/{{所有权2.1}}-20241108-3.png)

&ensp; &ensp; &ensp;初始化语句 let t = s; 将向量的 3 个标头字段从 s 转移给了 t，现在 t 拥有此向量。向量的元素保持原样，字符串也没有任何变化。每个值依然只有一个拥有者，尽管其中一个已然易手。译器现在会认为 s 是未初始化状态。

&ensp; &ensp; &ensp;执行初始化语句 let u = s; 时会发生什么呢？这会将尚未初始化的
值 s 赋给 u。Rust 明智地禁止使用未初始化的值，因此编译器会拒绝此代码并报告。

&ensp; &ensp; &ensp;如果需要同时访问s，就必须**显式地要求复制**。如果想达到与 C++ 程序相同的状态（每个变量都保存一个独立的结构**副本**），就必须调用向量的 clone 方法，该方法会执行向量及其元素的**深拷贝**：
```
fn main(){
    let s = vec!["udon".to_string(), "ramen".to_string(), "soba".to_string()];
    let t = s.clone();
    let u = s.clone();
}
```

### 2.2.1 移动的发生

1. 初始化与赋值：(书上这部分内容有问题4.2.1章节，我觉得)

- 初始化：变量第一次赋值，赋予其初始值，使变量变为有效状态(没有经过初始化的变量在 Rust 中是无法使用的)。
- 赋值：对已初始化的变量重新赋值，覆盖原来的内容，且自动释放旧值的内存。

&ensp; &ensp; &ensp;在变量进入 let 语句的作用域时为它们提供值。**变量赋值**则与此略有不同，如果你将一个值转移给已初始化的变量，那么 Rust 就会丢弃该变量的先前值。

```
fn main(){
    let mut s = "Govinda".to_string();
    s = "Siddhartha".to_string(); // 在这里丢弃了值"Govinda"
}
```

![|725](image/{{所有权2.1}}-20241108-5.png)

&ensp; &ensp; &ensp;书中的这部分内容，个人觉得有问题。不丢弃不就内存泄漏了，那还玩什么？运行结果也显示这个地方会把原来的内容（“Govinda”）丢弃   这个就是覆盖赋值啊！

&ensp; &ensp; &ensp;这个地方需要注意，不要以为s的所有权转移后，你就用不了s了。那么什么情况下用不了s呢？-->**作用域的结束**

&ensp; &ensp; &ensp;Rust 还将“移动”的语义应用到了几乎所有对值的使用上。例如，将参数传给函数会将所有权转移给函数的参数、从函数返回一个值会将所有权转移给调用者、构建元组会将值转移给元组。
```
struct Person { name: String, birth: i32 }
fn main(){
    let mut composers = Vec::new();
    composers.push(Person { name: "Palestrina".to_string(),birth: 1525 }); 
}
```
&ensp; &ensp; &ensp;下面的分析基于此段代码。

2. 函数返回值

&ensp; &ensp; &ensp;Vec::new() 构造一个新向量并返回，返回的不是指向此向量的指针，而是向量本身：它的所有权从 Vec::new 转移给了变量 composers。同样，to_string 调用返回的是一个新的 String 实例。

3. 构造出新值

&ensp; &ensp; &ensp;新 Person 结构体的 name 字段是用 to_string 的返回值初始化的。该结构体拥有这个字符串的所有权。

4. 将值传给函数

&ensp; &ensp; &ensp;整个 Person 结构体（不是指向它的指针）被传给了向量的 push 方法，此方法会将该结构体移动到向量的末尾。向量接管了 Person 的所有权，因此也间接接手了name 这个 String 的所有权。

&ensp; &ensp; &ensp;移动的永远是值本身，而不是这些值拥有的堆存储。对于向量和字符串，值本身就是指单独的“三字标头”(对内存的地址，容量，当前长度)。
![|387](image/{{所有权2.1}}-20241108-8.png)

### 2.2.2 移动与控制流

&ensp; &ensp; &ensp;前面的例子中都有非常简单的控制流，那么该如何在更复杂的代码中移动呢？一般性原则是，如果一个变量的值有可能已经移走，并且从那以后尚未明确赋予其新值，那么它就可以被看作是未初始化状态。rust禁止不能直接使用未初始化的变量。

```
    let x = vec![10, 20, 30];
    if c {
        f(x); // ……可以在这里移动x
    } else {
        g(x); // ……也可以在这里移动x
    }
    h(x); // 错误：只要任何一条路径用过它，x在这里就是未初始化状态
```

&ensp; &ensp; &ensp;禁止在循环中进行变量移动:

```
let x = vec![10, 20, 30];
while f() {
    g(x); // 错误：x已经在第一次迭代中移动出去了，在第二次迭代中，它成了未初始化状态
}
```

&ensp; &ensp; &ensp;也就是说，除非在下一次迭代中明确赋予 x 一个新值，否则就会出错。
```
let mut x = vec![10, 20, 30];
while f() {
    g(x);           // 从x移动出去了
    x = h();        // 赋予x一个新值
}
e(x);
```

### 2.2.3 移动与索引内容

&ensp; &ensp; &ensp;移动会令其来源变成未初始化状态，因为目标将获得该值的所有权。但并非值的每种拥有者都能变成未初始化状态（拿不走所有权）。

```
// 构建一个由字符串"101"、"102"……"105"组成的向量
let mut v = Vec::new();
for i in 101 .. 106 {
    v.push(i.to_string());
}
// 从向量中随机抽取元素
let third = v[2]; // 错误：不能移动到Vec索引结构之外3
let fifth = v[4]; // 这里也一样
```

&ensp; &ensp; &ensp;为了解决这个问题，Rust 需要以某种方式记住向量的第三个元素和第五个元素是未初始化状态，用额外的额标记来表示未初始化状态吗？那开销可大了去了，不划算。

&ensp; &ensp; &ensp;编译器会建议使用引用，因为你可能只是想访问该元素而不是移动它，这确实通常确实是你想要做的。但是，如果真想将一个元素移出向量该怎么办呢？

&ensp; &ensp; &ensp;我们可以通过填充来解决：

```
fn main(){
    // 构建一个由字符串"101"、"102"……"105"组成的向量
    let mut v = Vec::new();
    for i in 101 .. 106 {
        v.push(i.to_string());
    }
    // 方法一：从向量的末尾弹出一个值：
    let fifth = v.pop().expect("vector empty!");
    assert_eq!(fifth, "105");
    
    // 方法二：将向量中指定索引处的值与最后一个值互换，并把前者移动出来：
    let second = v.swap_remove(1);
    assert_eq!(second, "102");
    
    // 方法三：把要取出的值和另一个值互换：
    let third = std::mem::replace(&mut v[2], "substitute".to_string());
    assert_eq!(third, "103");
    
    // 看看向量中还剩下什么
    assert_eq!(v, vec!["101", "104", "substitute"]);
}
```

&ensp; &ensp; &ensp;像 Vec 这样的集合类型通常也会提供在循环中消耗所有元素的方法：
```
let v = vec!["liberté".to_string(),
                 "égalité".to_string(),
                 "fraternité".to_string()];
    for mut s in v {
        s.push('!');
        println!("{}", s);
    }
```

&ensp; &ensp; &ensp;当我们将向量直接传给循环（如 for ... in v）时，会将向量从 v 中移动出去，让 v 变成未初始化状态。for 循环的内部机制会获取向量的所有权并将其分解为元素。在每次迭代中，循环都会将另一个元素转移给变量 s。 (for对vec说: 我全部拿走用了，一会全部还给你，但是你不能让别人在用了。）

&ensp; &ensp; &ensp;如果需要从拥有者中移出一个编译器无法跟踪的值，那么可以考虑将拥有者的类型更改为能动态跟踪自己是否有值的类型。

```
struct Person { name: Option<String>, birth: i32 }
let mut composers = Vec::new();
composers.push(Person { name: Some("Palestrina".to_string()),
                        birth: 1525 });
```

&ensp; &ensp; &ensp;不能这样做：`let first_name = composers[0].name;`

&ensp; &ensp; &ensp;这只会引发与前面一样的“无法移动到索引结构之外”错误。但是因为已将 name字段的类型从 String 改成了 Option\<String>，所以这意味着 None 也是该字段要保存的合法值。因此，可以replace：
```
let first_name = std::mem::replace(&mut composers[0].name, None);

assert_eq!(first_name, Some("Palestrina".to_string()));
assert_eq!(composers[0].name, None);
```

&ensp; &ensp; &ensp;replace 调用会移出 composers\[0].name 的值，将 None 留在原处，并将原始值的所有权转移给其调用者。事实上，这种使用 Option 的方式非常普遍，所以该类型专门为此提供了一个 take 方法，以便更清晰地写出上述操作

`let first_name = composers[0].name.take();`


## 2.3 Copy 

&ensp; &ensp; &ensp;移动能让这些类型的所有权清晰且赋值开销极低。但对于像整
数或字符这样的简单类型，如此谨小慎微的处理方式have必要?

&ensp; &ensp; &ensp;在Rust中String 进行赋值和用 i32 进行赋值时内存中有什么不同：
```
fn main(){
    let string1 = "somnambulance".to_string();
    let string2 = string1;
    
    let num1: i32 = 36;
    let num2 = num1;
}
```

![|650](image/{{所有权2.1}}-20241108-6.png)

&ensp; &ensp; &ensp;赋值会将 string1转移给string2，这样就不会出现两个字符串负责释放同一个缓冲区的情况。

&ensp; &ensp; &ensp;num1 和 num2 的情况有所不同。i32 只是内存中的几字节，它不拥有任何堆资源，也不会实际依赖除本身的字节之外的任何内存。当我们将它的每一位转移给 num2 时，其实已经为 num1 制作了一个完全独立的副本。

&ensp; &ensp; &ensp;大多数类型会被移动，现在该谈谈例外情况了，即那些被Rust 指定成 **Copy 类型**的类型。对 Copy 类型的值进行赋值会复制这个值，而不会移动它。赋值的源仍会保持已初始化和可用状态，并且具有与之前相同的值。把 Copy类型传给函数和构造器的行为也是如此。
### 2.3.1  实现Copy 特征的基本类型

&ensp; &ensp; &ensp;Rust 中的基本类型都实现了 Copy 特征，包括整数、浮点数、布尔值和字符。对于复合类型来说，如果包含的所有字段都是 Copy 的，那么这个元素也是 Copy 的。例如：(i32, i32) 、\[i32,i32]是 Copy 的，但 (i32, String) 、 \[i32, String]则不是。

&ensp; &ensp; &ensp;任何在丢弃值时需要做一些特殊操作的类型都不能是 Copy 类型：Vec 需要释放自身元素、File 需要关闭自身文件句柄、MutexGuard 需要解锁自身互斥锁，等等。

&ensp; &ensp; &ensp;对于 `String`、`Vec<T>` 这样的**堆分配类型**（不实现 `Copy`），只能使用 `.clone()` 进行与copy一样效果的拷贝。(一会再说这个Clone)

&ensp; &ensp; &ensp;所有实现了 `Copy` 的类型都必须实现 `Clone`。当你显式地调用 `clone` 方法时，Rust 会假定你知道自己在做什么，并且希望按位复制该值。

&ensp; &ensp; &ensp;那么对于自定义类型呢？**默认情况下**，struct 类型和 enum 类型不是 Copy 类型，你如果要用，就会发生**所有权转移**，后续在编写代码时发生该变量不可再用。但是结构体的所有字段本身都是 Copy 类型，那么也可以通过将属性`#[derive(Copy,Clone)]`放置在此定义之上来创建 Copy 类型，如下所示：
```
#[derive(Copy,Clone)]
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p1 = Point { x: 5, y: 10 };
    
    // 由于 `Point` 实现了 `Copy` 特性，赋值会自动复制
    let p2 = p1;        // 自动复制（按位复制）

    // 使用 `clone()` 方法显式复制
    let p3 = p1.clone(); // 显式复制（效果和自动复制相同）

    println!("p1: ({}, {}), p2: ({}, {}), p3: ({}, {})", p1.x, p1.y, p2.x, p2.y, p3.x, p3.y);
}
```

&ensp; &ensp; &ensp;经过此项更改，前面的代码可以顺利编译了。

&ensp; &ensp; &ensp;切记不要试图在一个字段不全是Copy 类型的结构体上这样做。
### 2.3.2 Clone
&ensp; &ensp; &ensp;说到Copy，那就不得提一提他的好兄弟Clone，这里做一简单介绍：

&ensp; &ensp; &ensp;与 `Copy` 不同， `Clone` 是一个普通的 trait，它包含一个方法：`clone`。允许你**显式**地复制类型的值。当一个类型实现了 `Clone` trait 时，你可以调用它的 `clone` 方法来创建一个新的副本。这对于那些不能按位复制的类型非常有用，例如包含指针或引用的类型。`Clone` trait 还允许你自定义复制行为。你可以在 `clone` 方法中添加任何逻辑，以便在复制时执行特定的操作。

&ensp; &ensp; &ensp;要实现 `Clone` trait，你需要在类型定义上添加 `#[derive(Clone)]` 属性或手动实现 `clone` 方法。

```
#[derive(Clone)]
struct Person {
    name: String,
    age: u8,
}

fn main() {
    let person1 = Person { name: String::from("Alice"), age: 30 };
    
    // let person2 = person1; // 这会转移所有权，person1 不再可用
    
    let person2 = person1.clone(); // 显式复制

    println!("person1: {}, {}", person1.name, person1.age);
    println!("person2: {}, {}", person2.name, person2.age);
}

```

```
struct Point {
    x: i32,
    y: String,
}

impl Clone for Point {
    fn clone(&self) -> Self {
        Self { x: self.x, y: self.y.clone() } // `y` 需要调用 `clone` 方法
    }
}

fn main() {
    let p1 = Point { x: 5, y: String::from("hello") };
    let p2 = p1.clone(); // 手动实现的 clone 方法
    println!("p1: ({}, {}), p2: ({}, {})", p1.x, p1.y, p2.x, p2.y);
}

```

&ensp; &ensp; &ensp;手动实现 `Clone` 允许对克隆过程进行更精细的控制，例如在克隆时执行特定逻辑或只克隆部分字段。只要你能够定义如何创建一个新的副本，你就可以实现 `Clone` trait。

## 2.4 Rc 与 Arc

&ensp; &ensp; &ensp;在 Rust 中，`Rc` 和 `Arc` 是用于引用计数的智能指针，分别适用于单线程和多线程环境。这些智能指针允许多个拥有者共享一个值，这对于需要多重所有权的场景非常有用，特别是当无法为每个值找到唯一拥有者时。Rust 提供了这两种类型来满足不同的并发需求：

- **`Rc<T>`（Reference Counted）**：
    
    - 适用于单线程场景。
    - 通过引用计数来管理共享数据的生命周期。当最后一个引用被丢弃时，数据会自动释放。
    - 不会导致数据竞争，但只能在单线程环境中使用。
- **`Arc<T>`（Atomic Reference Counted）**：
    
    - 适用于多线程场景，是 `Rc` 的线程安全版本。
    - 使用原子操作进行引用计数，因此开销比 `Rc` 稍高，但保证了线程安全。
    - 在多线程场景中，可以安全地在多个线程中共享数据。

```
use std::rc::Rc;

fn main() {
    let value = Rc::new(5);
    let a = Rc::clone(&value); // 增加引用计数
    let b = Rc::clone(&value);

    println!("a: {}, b: {}, value: {}", a, b, value);
    println!("引用计数: {}", Rc::strong_count(&value));   //3
}
```

```
use std::sync::Arc;
use std::thread;

fn main() {
    let value = Arc::new(5);
    let handles: Vec<_> = (0..3).map(|_| {
        let value = Arc::clone(&value);
        thread::spawn(move || {
            println!("线程中的值: {}", value);
        })
    }).collect();

    for handle in handles {
        handle.join().unwrap();
    }
}
```

&ensp; &ensp; &ensp;Rust 的 `Rc` 和 `Arc` 避免了手动管理引用计数的风险，确保引用计数的安全性和准确性。如果不需要在线程之间共享指针，则没有理由为 Arc 的性能损失“埋单”，因此应该使用Rc，Rust 能防止你无意间跨越线程边界传递它。这两种类型在其他方面都是等效的。

&ensp; &ensp; &ensp;克隆一个 Rc\<T> 值并不会复制 T，相反，它只会**创建另一个指向它的指针并递增引用计数**。

```
use std::rc::Rc;
// Rust能推断出所有这些类型，这里写出它们只是为了讲解时清晰
let s: Rc<String> = Rc::new("shirataki".to_string());
let t: Rc<String> = s.clone();
let u: Rc<String> = s.clone();
```

![|450](image/{{所有权2.1}}-20241108-9.png)

&ensp; &ensp; &ensp;这 3 个 Rc\<String> 指针指向了同一个内存块，其中包含引用计数和 String本身的空间。通常的所有权规则适用于 Rc 指针本身，当丢弃最后一个现有 Rc 时，
Rust 也会丢弃 String。

&ensp; &ensp; &ensp;可以直接在 Rc\<String> 上使用 String 的任何常用方法（仅是读的操作），如果你试图将一些文本添加到字符串的末尾：`s.push_str(" noodles")`那么 Rust 会拒绝。

&ensp; &ensp; &ensp;Rust 的内存和线程安全保证的基石是：确保不会有任何值是既共享又可变的。Rust 假定 Rc 指针的引用目标通常都可以共享，因此就不能是可变的。

&ensp; &ensp; &ensp;移动和引用计数指针是缓解所有权树严格性问题的两种途径。接下来我们将研究第三种途径：借用对值的引用。

# 三.引用

&ensp; &ensp; &ensp;迄今为止，我们看到的所有指针类型（无论是简单的 Box\<T> 堆指针，还是String 值和 Vec 值内部的指针）都是拥有型指针，这意味着当拥有者被丢弃时，它
的引用目标也会随之消失。Rust 还有一种名为引用（reference）的非拥有型指针，这
种指针对引用目标的生命周期毫无影响。

&ensp; &ensp; &ensp;任何引用的生命周期都不可能超出它指向的值。为了强调这一点，
Rust 把创建对某个值的引用的操作称为借用（borrow）那个值：凡是借用，终须归还。




















