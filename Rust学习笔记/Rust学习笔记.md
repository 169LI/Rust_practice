# 搭建开发环境
首先，需要安装最新版的 Rust 编译工具和 Visual Studio Code

Rust 编译工具：[安装 Rust - Rust 程序设计语言](https://www.rust-lang.org/zh-CN/tools/install)

Visual Studio Code：[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)

+ Rust 的编译工具依赖 C 语言的编译工具，这意味着你的电脑上至少已经存在一个 C 语言的编译环境。如果你使用的是 Linux 系统，往往已经具备了 GCC 或 clang。
+ 如果你使用的是 macOS，需要安装 Xcode。
+ 如果你是用的是 Windows 操作系统，你需要安装 Visual Studio 2013 或以上的环境（需要 C/C++ 支持）以使用 MSVC 或安装 MinGW + GCC 编译环境
## 1下载过vs2022 
（没下过也不建议你下了   还不如开虚拟机用linux系统）
![[Pasted image 20241105202526.png]]
## 2rust 编译工具
官方下载地址: [rust](https://www.rust-lang.org/learn/get-started)  选择64bit，下载后的文件名为rustup-init.exe
![[Pasted image 20241105202801.png]]
## 3运行rustup-init.exe
![[Pasted image 20241105203307.png]]
上图显示的是一个命令行安装向导。
如果你已经安装 MSVC （推荐），那么安装过程会非常的简单，输入 1 并回车，直接进入第二步。
![[Pasted image 20241105203332.png]]
 后面可能会使用GNU（没有安装MSVC或者后续准备使用GNU）
如果你安装的是 MinGW，那么你需要输入 2 （自定义安装），然后系统会询问你 Default host triple? ，请将上图中 default host triple 的 "msvc" 改为 "gnu" 再输入安装程序
![[Pasted image 20241105203348.png]]
设置完所有选项，会回到安装向导界面（第一张图），这是我们输入 1 并回车即可
## 4测试
```
rustc -V        # 注意的大写的 V
```
![[Pasted image 20241105203418.png]]
## 5Visual Studio Code 开发环境
analyzer 和 Native Debug 两个扩展   之后重启  选择一个新的文件夹
![[Pasted image 20241105203442.png]]
![[Pasted image 20241105203450.png]]
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
![[Pasted image 20241105203519.png]]
成功的构建了一个 Rust 命令行程序！
## 6 调试（debug）
自带的那个是真不好用     自己配的这个也没好到哪里！  Rust后面会调试应该可能可以学快点（学c++不会调试直接凉一半）
![[Pasted image 20241105203553.png]]直接粘贴就ok了
![[Pasted image 20241105203605.png]]
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
要卸载 Rust 和 rustup，在终端执行以下命令即可卸载：
`rustup self uninstall（不建议卸载）`
## 8本地文档
安装 Rust 的同时也会在本地安装一个文档服务，方便我们离线阅读：运行
```
 rustup doc
 cargo doc --help
```
 让浏览器打开本地文档。
## 9  .gitignore文件
 如果有上传github需求  建议加一个.gitignore文件  把不想上传的文件写进去。他的target（编译的文件都在里面放）一直需要上传 真的很烦。
```
target
.gitignore
```
# 一.数据类型
本章从简单的数值类型（如整数和浮点值）开始，后面转而介绍包含更多数据的类型：Box、元组（tuple）、数组和字符串。<span style="color:red">（此处需要后续补充后续详细章节链接）</span>

 **固定数值类型（整数+浮点数）**
Rust 中数值类型的名称都遵循着一种统一的模式，类型定义的形式统一为：有无符号 + 类型大小(位数)。
![[Pasted image 20241105203720.png]]
机器字是一个值，其大小等于运行此代码的机器上“地址”的大小，可能是 32 位，也可能是 64 位。

默认情况下，12.0 将表示 64 位浮点数 12表示有符号32位整数。

方法调用的优先级高于前缀运算符，因此在对负值进行方法调用时，请务必正确地加上圆括号。<span style="color:red">（代码补充）</span>
## 1.1整型（Integer）
整数型简称整型，按照比特位长度和有无符号分为以下种类
![[Pasted image 20241105203729.png]]
为了让长数值更易读，可以在数字之间任意插入下划线。
  ![[Pasted image 20241105203854.png]]

### 1.1.1 整型溢出
假设有一个 u8 ，它可以存放从 0 到 255 的值。那么当你将其修改为范围之外的值，比如 256，则会发生整型溢出。Rust 会检查整型溢出，若存在这些问题，则使程序在编译时 panic(崩溃,Rust 使用这个术语来表明程序因错误而退出)。在当使用release 参数进行 release 模式构建时，Rust 不检测溢出。相反，当检测到整型溢出时，Rust 会按照补码**循环溢出**（two’s complement wrapping）的规则处理。程序不会 panic，但是该变量的值可能不是你期望的值。依赖这种默认行为的代码都应该被认为是错误的代码。
### 1.1.2 溢出的处理
要显式处理可能的溢出，可以使用标准库针对原始数字类型提供的这些方法，以下是常用的几个:<span style="color:red">（代码补充）</span>
1. 加法
-  wrapping_add: 循环加法。
- checked_add: 溢出时返回 None。
- overflowing_add: 返回结果和溢出指示布尔值。
- saturating_add: 超过最大值时返回最大值。
2. 减法
- wrapping_mul: 循环乘法。
- checked_mul: 如果发生溢出返回 None。
- overflowing_mul: 返回计算结果和是否溢出的布尔值。
- saturating_mul: 结果不会超过最大值。
3. 乘法
- wrapping_mul: 循环乘法。
- checked_mul: 如果发生溢出返回 None。
- overflowing_mul: 返回计算结果和是否溢出的布尔值。
- saturating_mul: 结果不会超过最大值。
4. 除法
- wrapping_div: 循环除法（注意除以零会导致 panic）。
- checked_div: 如果发生除以零返回 None。
- overflowing_div: 返回计算结果和是否发生溢出的布尔值（通常不使用）
- saturating_div: 结果不会低于最小值（通常不使用）。
5. 取模
- wrapping_rem: 循环取模（注意除以零会导致 panic）。
- checked_rem: 如果发生除以零返回 None。
- overflowing_rem: 返回计算结果和是否发生溢出的布尔值（通常不使用）。
- saturating_rem: 结果不会低于最小值（通常不使用）。
每种运算都有不同的处理方式，可以根据具体需求选择适合的方法来处理溢出和边界情况。

|      |      |                                       |
| ---- | ---- | ------------------------------------- |
| 运算   | 名称后缀 | 例子                                    |
| 加法   | add  | 100_i8.checked_add(27) == Some(127)   |
| 减法   | sub  | 10_u8.checked_sub(11) == None         |
| 乘法   | mul  | 128_u8.saturating_mul(3) == 255       |
| 除法   | div  | 64_u16.wrapping_div(8) == 8           |
| 求余   | rem  | (-32768_i16).wrapping_rem(-1) == 0    |
| 取负   | neg  | (-128_i8).checked_neg() == None       |
| 绝对值  | abs  | (-32768_i16).wrapping_abs() == -32768 |
| 求幂   | pow  | 3_u8.checked_pow(4) == Some(81)       |
| 按位左移 | shl  | 10_u32.wrapping_shl(34) == 40         |
| 按位右移 | shr  | 40_u64.wrapping_shr(66) == 10         |

### 1.1.3 数字运算

上面提到了基本运算下面简单的来介绍一下数字运算。Rust 支持所有数字类型的基本数学运算：加法、减法、乘法、除法和求余运算。
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

    // 求余
    let remainder = 43 % 5;       
     
}
```
许多运算符号之后加上 = 号是自运算的意思，例如：sum += 1 等同于 sum = sum + 1。（涉及所有权问题需注意）<span style="color:red">（代码补充）</span>

**注意**：Rust 不支持 ++ 和 --，因为这两个运算符出现在变量的前后会影响代码可读性，减弱了开发者对变量改变的意识能力。

### 1.1.4 位运算
Rust 的位运算基本上和其他语言一样。

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

## 1.2浮点数型（Floating-Point）

Rust 提供了 IEEE 单精度浮点类型和 IEEE 双精度浮点类型。这些类型包括**正无穷大和负无穷大、不同的正零值和负零值，以及非数值**。

浮点类型数字是**带有小数点**的数字，在 Rust 中浮点类型数字也有两种基本类型： f32 和 f64，分别为 32 位和 64 位大小。**默认浮点类型是 f64**，在现代的 CPU 中它的速度与 f32 几乎相同，但精度更高。

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

对于**数学上未定义**的结果，例如对负数取平方根会产生一个特殊的结果：Rust 的浮点数类型使用 NaN (not a number) 来处理这些情况.出于防御性编程的考虑，可以使用 is_nan() 等方法，可以用来判断一个数值是否是 NaN ：

```
fn main() {
    let x = (-42.0_f32).sqrt();
    if x.is_nan() {
        println!("未定义的数学行为")
    }
}
```

### 1.2.2 浮点数陷阱

1. 浮点数往往是你想要数字的近似表达<span style="color:red">（代码补充）</span>

浮点数类型是基于二进制实现的，学过计组应该知道这里的问题了。例如 0.1 在二进制上并不存在精确的表达形式，但是在十进制上就存在。

2. 浮点数在某些特性上是反直觉的

例如大家都会觉得浮点数可以进行比较，对吧？

是的，它们确实可以使用 >，>= 等进行比较，f32 ， f64 上的比较运算实现的是std::cmp::PartialEq 特征，但是并没有实现 std::cmp::Eq 特征。

为了避免上面说的两个陷阱，你需要**遵守以下准则**：

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
![0](data:image/png;base64,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)

对 f32 类型做加法时，0.1 + 0.2 的结果是 3e99999a，0.3 也是 3e99999a，因此 f32 下的 0.1 + 0.2 == 0.3 通过测试。

f64 类型时，结果就不一样了，因为 f64 精度高很多，因此在小数点非常后面发生了一点微小的变化，0.1 + 0.2 以 4 结尾，但是 0.3 以3结尾，这个细微区别导致 f64 下的测试失败了，并且抛出了异常。

### 1.2.3 As 完成类型转换
**Rust 几乎不会执行任何隐式的数值转换**。如果函数需要 f64参数，则传入 i32 型参数是错误的。事实上，Rust 甚至不会隐式地将 i16 值转换为 i32 值，虽然每个 i16 值都必然在 i32 范围内。

不过，你随时可以用 as 运算符写出显式转换：i as f64 或 x as i32。隐式整数转换有着导致错误和安全漏洞的大量“前科”，特别是在用这种整数表示内存中某些内容的大小时，很可能发生意外溢出。根据以往的经验，Rust 这种要求明确写出数值类型转换的行为，会提醒我们注意到一些可能错过的问题。
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

Rust 中可以使用 As 来完成一个类型到另一个类型的转换，其最常用于将原始类型转换为其他原始类型，但是它也可以完成诸如将指针转换为地址、地址转换为指针以及将指针转换为其他指针等功能。<span style="color:red">（需要添加后续笔记链接）</span>
## 1.3 布尔类型(bool)

Rust 中的布尔类型值**只能**是：true 和 false，布尔值占用内存的大小为 1 个字节。

这个地方和C++语言有点不一样的地方： true能写成1,false能写成0吗？事实说话。

![[Pasted image 20241105203927.png]]
```
fn main() { 
	let t = true; 
	let f: bool = false; 
	// 使用类型标注,显式指定f的类型 if f { println!("这是段毫无意义的代码"); } }
```

使用布尔类型的场景**主要在于流程控制**，例如上述代码的中的 if 就是其中之一。

Rust 的 **as 运算符可以将 bool 值转换为整型：**

```
fn main(){
    assert_eq!(false as i32, 0);
    assert_eq!(true  as i32, 1);
}
```

但是，as **无法进行另一个方向（从数值类型到 bool）的转换**。相反，你必须显式地写出比较表达式。

## 1.4 字符类型(char)

Rust 的字符不仅仅是 ASCII，**所有的 Unicode 值都可以作为 Rust 字符**，包括单个的中文、日文、韩文、emoji 表情符号等等，都是合法的字符类型。

Unicode 值的范围从 U+0000 到 U+D7FF 和 U+E000 到 U+10FFFF （包括两端），char 永远不会是“半代用区”中的码点（0xD800 到 0xDFFF 范围内的码点， 它们不能单独使用）。

一般推荐使用字符串储存 UTF-8 文字（非英文字符尽可能地出现在字符串中）。在 Rust 中字符串和字符都必须使用 UTF-8 编码，否则编译器会报错。

字符的Unicode码点在 U+0000 到 U+007F 范围内（也就是说，如果它是从 ASCII 字 符集中提取的），就可以把字符写为 '\xHH'，其中 HH 是两个十六进制数。例 如，字符字面量 '*' 和 '\x2A' 是等效的。
（真写不下去了 后面关于Unicode码点的我是真看不懂 ！！！这个地方应该是不是学习重点）
```
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let g = '国';
    let heart_eyed_cat = '😻';
}
```

由于 Unicode 都是 4 个字节编码，因此**字符类型也是占用 4 个字节**。

**切记Rust 的字符只能用 '  ' 来表示， " " 是留给字符串的。====**

## 1.5 元组(Tuple)

元组是各种类型值的值对或三元组、四元组、五元组等（因此称为 n-元组或元 组）。

其实你可以把数组[ ]和元组叫做**复合类型**。因为可以包含不同种类的数据(这句话有毛病可以忽略)。但他俩还是有点不同的。

+ 定义：() 表示一个元组，可以包含多个不同类型的值。

	   - 用法：

	* 元组可以用来组合不同类型的值。
	* 元组的长度是固定的，且长度在编译时已知。

+ 示例：
```
fn main(){
    let tuple: (i32, f64, char) = (42, 3.14, 'a');  //不同类型是这个意思
    println!("Tuple values: {:?}", tuple);
}
```


这里和数组[ ]做一个简单对比 后面有对数组的详细介绍（加链接）

类型：

	元组可以包含不同类型的元素；
	
	数组只能包含相同类型的元素。

长度：

	元组的长度是固定的，但长度可以是不同的（不同的元组可以有不同数量的元素）；
	
	数组的长度在定义时确定，并且所有数组的长度都是相同的。

访问方式：

	元组可以通过位置来访问元素， tuple.0、tuple.1。
	
	数组可以通过索引来访问， array[0]。

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

还有常用的元组类型是零元组 ()。传统上，这叫作单元类型，因为此类型只有 一个值，写作 ()。当无法携带任何有意义的值但其上下文仍然要求传入某种类型时， Rust 就会使用单元类型。main 函数就返回这个单元类型 ()，你不能说 main 函数无返回值，因为没有返回值的函数在 Rust 中是有单独的定义的：发散函数( diverge function )，顾名思义，无法收敛的函数。

例如，不返回值的函数的返回类型为 ()。常见的 println!() 的返回值就是单元类型 ()。

Rust 始终允许在所有能用逗号的地方（函数参数、 数组、结构体和枚举定义，等等）添加额外的尾随逗号。 为了保持一致性，甚至有包含单个值的元组。字面量 ("lonely hearts",) 就 是一个包含单个字符串的元组，它的类型是 (&str,)。在这里，值后面的逗号是必需 的，以用于区分单值元组和简单的括号表达式。

### 1.5.1用模式匹配解构元组

```
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```

使用 let (x, y, z) = tup; 来完成一次模式匹配，因为元组是 (n1, n2, n3) 形式的，因此我们用一模一样的 (x, y, z) 形式来进行匹配，元组中对应的值会绑定到变量 x， y， z上。这就是解构：用同样的形式把一个复杂对象中的值匹配出来

### 1.5.2用 . 来访问元组

Rust 提供了 . 的访问方式：和其它语言的数组、字符串一样，元组的索引从 0 开始。

```
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

let hello = String::from("Hola"); 这行代码来说，Hola 的长度是 4 个字节，因为 "Hola" 中的每个字母在 UTF-8 编码中仅占用 1 个字节，但是对于下面的代码呢？

### 1.5.3元组的使用示例

元组在函数返回值场景很常用，例如下面的代码，可以使用元组返回多个值：
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

calculate_length 函数接收 s1 字符串的所有权，然后计算字符串的长度，接着把字符串所有权和字符串长度再返回给 s2 和 len 变量。

## 1.6 指针类型

Rust 有多种表示内存地址的类型，接下来将讨论 3 种指针类型：引用、Box 和不安全指针

### 1.6.1引用

最简单的方式是将引用视为 Rust 中的基本指针类型.

对 i32 的引 用是一个保存着 i32 地址的机器字，这个地址可能位于栈或堆中。表达式 &x 会生成 一个对 x 的引用，在 Rust 术语中，我们会说它借用了对 x 的引用。给定一个引用 r，表达式 *r 会引用 r 指向的值。

Rust 引用有两种形式：
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
+ &mut T
一个可变的、独占的引用。你可以读取和修改它指向的值，就像 C 中的 T* 一样。但是只要该引用还存在，就不能对该值有任何类型的其他引用。事实上，访问该值的唯一途径就是使用这个可变引用。

Rust 利用共享引用和可变引用之间的“二选一”机制（只有一个可变引用或者多个不可变引用）来强制执行“单个写入者或多个读取者”规则：你或者独占读写一个值，或者让任意数量的读取者共享，但二者只能选择其一。这种限制的好处就是使 Rust 在编译期就避免数据竞争，数据竞争可由以下行为造成：

- 两个或更多的指针同时访问同一数据
- 至少有一个指针被用来写入数据
- 没有同步数据访问的机制

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

来吧见识一下NLL吧！！（Rust 1.31 后）

对于这种编译器优化行为，Rust 专门起了一个名字 —— Non-Lexical Lifetimes(NLL)，专门用于找到某个引用在作用域(})结束前就不再被使用的代码位置。（Rust编译器,天才第一步）

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

我以为这就完了，其实还有好多呢 ！！！！！ 这里只是简单介绍一下。 等待中（后面链接）

### 1.6.2Box

在堆中分配值的最简单方式是使用 Box::new。（这里需要对内存的栈和堆有一个简单的认识，后面学习依旧要用到，这里不在做笔记）Box 是一个智能指针，它在堆上分配内存并提供对该内存的安全访问。使用 Box 可以在运行时动态分配内存，并且可以存储大小在编译时未知的类型。

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

在所有权和移动时再详细深入介绍Box 等待补充链接

### 1.6.3不安全指针(裸指针)

Rust 也有裸指针类型 *mut T 和 *const T。裸指针实际上和 C++ 中的指针很像。使用裸指针是不安全的，因为Rust 不会跟踪它指向的内容。例如，裸指针可能为空，或者它们可能指向已释放的内存或现在包含不同类型的值。C++ 的所有经典指针错误都可能“借尸还魂”。

但是，你只能在 unsafe 块中对裸指针解引用（dereference）。unsafe 块是Rust 高级语言特性中的可选机制，其安全性取决于你自己。如果代码中没有 unsafe块（或者虽然有但编写正确），那么本书中强调的安全保证就仍然有效。（需要进一步的代码补充 后面遇到会补充）

## 1.7数组

### 1.7.1 数组的基本声明

在 Rust 中，数组的声明形式如下：

```
let lazy_caterer: [u32; 6] = [1, 2, 4, 7, 11, 16]; // 声明一个固定长度的数组
```

- \[u32; 6] 说明这是一个长度为 6 的数组，元素类型是 u32。
- 数组是固定大小的，在编译时长度就已经确定。

您还可以在数组中放入多个值：

```
let taxonomy = ["Animalia", "Arthropoda", "Insecta"];  // 声明一个字符串数组
assert_eq!(taxonomy.len(), 3);  // 数组长度是 3
assert_eq!(taxonomy[1], "Arthropoda");  
// 索引从 0 开始，第二个元素是 "Arthropoda"
```

1.7.2 使用 \[V; N] 语法创建固定大小的数组

Rust 允许使用 \[V; N] 的语法来创建一个元素都为 V 且长度为 N 的数组。

```
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
```
这里：

- 使用 \[true; 10000] 创建一个布尔值数组，所有值初始化为 true。
- 该算法是著名的埃拉托斯特尼筛法，用于筛选质数。

### 1.7.3 数组和切片

数组的一个重要特性是它可以作为切片来使用。切片是对数组（或向量）的引用，提供了一种更加灵活的访问方式，且切片的长度是可以变化的。

Rust 中的数组方法大多是通过切片来实现的，常见的切片方法包括 sort、iter、len 等。

```
let mut chaos = [3, 5, 4, 1, 2];
chaos.sort();  // 排序
assert_eq!(chaos, [1, 2, 3, 4, 5]);  // 排序后的数组是 [1, 2, 3, 4, 5]
```

这里：

- sort 方法是定义在切片上的，但它可以通过数组的引用来隐式地调用。
- Rust 会自动将数组 chaos 转换为 &mut [i32] 类型的切片引用，然后再调用 sort 方法。

### 1.7.4 数组的不可变和可变借用

数组是栈上的固定大小的集合，您可以借用它们，但必须遵守不可变或可变借用规则：

- 不可变借用：允许您以只读方式访问数组中的元素。
- 可变借用：允许修改数组中的元素。

例如：
```
let mut nums = [1, 2, 3];
let nums_ref = &mut nums;  // 可变借用
nums_ref[0] = 42;  // 修改 nums 的第一个元素
```

### 1.7.5 数组的大小是固定的

Rust 的数组长度在编译时是固定的，因此不能在运行时动态改变数组的大小。

```
let n = 5;
let arr = [0; n];  // 错误：`n` 需要是常量
```

为了处理大小动态的数组，Rust 提供了**向量（Vec）**类型，它在运行时可以动态增长或缩小。

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
## 1.8向量

在 Rust 中，Vec 是一种非常重要的集合类型，代表一个可以动态增长和缩小的向量。它提供了一个灵活、可调整大小的数组，内存分配在堆上，使得我们可以在运行时动态地操作数据。

### 1.8.1 创建向量

+ 使用 vec! 宏    最简单的方式是使用 vec! 宏，它类似于数组字面量的语法，用于快速创建一个向量：

```
let mut primes = vec![2, 3, 5, 7];  // 创建一个包含质数的向量
assert_eq!(primes.iter().product::<i32>(), 210);  // 计算元素的乘积
```

 vec!\[2, 3, 5, 7] 创建一个包含指定元素的向量。

+ 动态添加元素    向量是动态可变的，我们可以使用 push 方法向向量添加元素：

```
primes.push(11);  // 向向量添加元素
primes.push(13);
assert_eq!(primes.iter().product::<i32>(), 30030);  // 更新后的元素乘积
```

+ 创建具有重复值的向量    可以通过指定元素和重复次数来创建一个具有重复值的向量：

```
fn new_pixel_buffer(rows: usize, cols: usize) -> Vec<u8> {
    vec![0; rows * cols]  // 创建一个大小为 rows * cols 的向量，每个元素都是 0
}
```

+ 使用 Vec::new 创建空向量

另外，也可以通过 Vec::new() 来创建一个空的向量，然后逐个添加元素：

```
let mut pal = Vec::new();
pal.push("step");
pal.push("on");
pal.push("no");
pal.push("pets");
assert_eq!(pal, vec!["step", "on", "no", "pets"]);
```

从迭代器创建向量

也可以从迭代器生成一个向量：

```
let v: Vec<i32> = (0..5).collect();  // 使用 collect 将迭代器生成的值收集成向量
assert_eq!(v, [0, 1, 2, 3, 4]);
```

- collect 方法根据上下文的类型推断，默认将结果收集为向量，但也可以指定其他类型的集合。

### 1.8.2 与数组的相似性

虽然数组和向量在 Rust 中都是集合类型，数组的大小在编译时确定，而向量的大小在运行时动态变化。向量支持与切片类似的方法，比如 sort()、reverse() 等：

```
let mut palindrome = vec!["a man", "a plan", "a canal", "panama"];
palindrome.reverse();  // 反转向量
assert_eq!(palindrome, vec!["panama", "a canal", "a plan", "a man"]);
```

### 1.8.3 向量的容量管理

向量在堆上分配内存，并且随着元素的添加，向量会自动扩展。Vec 由 3 个部分组成：指向堆中元素的指针、缓冲区能存储的元素数量、以及当前实际包含的元素数量。

+ Vec::with_capacity

如果知道向量的初始大小，可以使用 Vec::with_capacity 来避免不必要的内存分配：
```
let mut v = Vec::with_capacity(2);
assert_eq!(v.len(), 0);
assert_eq!(v.capacity(), 2);

v.push(1);
v.push(2);
assert_eq!(v.len(), 2);
assert_eq!(v.capacity(), 2);  // 容量保持 2

v.push(3);
println!("capacity is now {}", v.capacity());  // 容量通常会扩展为 4
```

 - capacity() 返回当前向量能够容纳的最大元素数，而不需要进行内存重新分配。
 - 当向量超过容量时，它会自动增加容量。

### 1.8.4 向量的修改操作

+ 插入元素

可以在任意位置插入元素：

```
let mut v = vec![10, 20, 30, 40, 50];
v.insert(3, 35);  // 在索引为 3 的位置插入 35
assert_eq!(v, [10, 20, 30, 35, 40, 50]);
```

+  删除元素

可以通过索引删除元素：

```
v.remove(1);  // 移除索引为 1 的元素
assert_eq!(v, [10, 30, 35, 40, 50]);
```

+ 弹出元素

可以使用 pop 方法从向量中移除最后一个元素，并返回一个 Option：

```
let mut v = vec!["Snow Puff", "Glass Gem"];
assert_eq!(v.pop(), Some("Glass Gem"));  // 弹出 "Glass Gem"
assert_eq!(v.pop(), Some("Snow Puff"));  // 弹出 "Snow Puff"
assert_eq!(v.pop(), None);  // 向量为空，返回 None
```

### 1.8.5 遍历向量

可以使用 for 循环遍历向量：
```
let languages: Vec<String> = std::env::args().skip(1).collect();
for l in languages {
    println!("{}: {}", l,
             if l.len() % 2 == 0 {
                 "functional"
             } else {
                 "imperative"
             });
}
```

这段代码展示了如何将命令行参数收集为向量，并根据字符串的长度判断其是函数式语言还是命令式语言。

### 1.8.6 总结

- Vec 是一个可动态增长的集合，适用于需要动态调整大小的场景。
- 通过 vec! 宏、Vec::new、Vec::with_capacity 和迭代器等方法可以创建和初始化向量。
- 向量可以通过切片方法进行操作（如 sort()、reverse()），也支持修改操作（如 push()、insert()、remove()）。
- 向量的内存管理会自动扩展，Vec::capacity() 和 Vec::with_capacity 提供了更高效的容量管理。
- 向量与数组的区别在于，向量的大小在运行时是动态的，而数组的大小在编译时是固定的。

Rust 中的 Vec 类型非常灵活，适合用于处理需要动态增长的列表，几乎可以在任何需要动态集合的场景中使用。

## 1.9字符串类型

在 Rust 中，字符串的处理方式与 C++ 和其他编程语言有一些相似之处，但也有独特的设计。Rust 提供了多种方式来处理字符串，包括字符串字面量、字节串和动态字符串类型（String）。Rust 中的字符是 Unicode 类型，因此每个字符占据 4 个字节内存空间，但是在字符串中不一样，字符串是 UTF-8 编码，也就是字符串中的字符所占的字节数是变化的(1 - 4)，这样有助于大幅降低字符串所占用的内存空间。

Rust 在语言级别，只有一种字符串类型： str，它通常是以引用类型出现 &str，也就是上文提到的字符串切片。虽然语言级别只有上述的 str 类型，但是在标准库里，还有多种不同用途的字符串类型，其中使用最广的即是 String 类型。

str 类型是硬编码进可执行文件，也无法被修改，但是 String 则是一个可增长、可改变且具有所有权的 UTF-8 编码字符串，当 Rust 用户提到字符串时，往往指的就是 String 类型和 &str 字符串切片类型，这两个类型都是 UTF-8 编码。

除了 String 类型的字符串，Rust 的标准库还提供了其他类型的字符串，例如 OsString， OsStr， CsString 和 CsStr 等

### 1.9.1 字符串字面量

字符串字面量是在代码中直接书写的字符串，它们以双引号包围。可以使用转义序列来处理特殊字符，如换行符、双引号等。

- 基本的字符串字面量

```
let speech = "\"Ouch!\" said the well.\n";
```

在这个例子中，\" 转义了双引号，\n 表示换行符。

- 多行字符串 Rust 支持跨多行的字符串字面量，自动包含换行符和空格：

println!("In the room the women come and go, Singing of Mount Abora");

这里字符串包含换行符，甚至在第二行的开头有空格。

- 行连接 可以用反斜杠 \ 来连接多行字符串，连接时会丢弃换行符和多余的空格：

```
println!("In the room the women come and go,
Singing of Mount Abora");
```

输出会是单行文本，注意反斜杠前的空格仍然会保留。

- 原始字符串 原始字符串用 r 前缀标记，允许字符串直接包含反斜杠而不进行转义，非常适合处理文件路径或正则表达式。

```
let default_win_install_path = r"C:\Program Files\Gorillas";
let pattern = Regex::new(r"\d+(\.\d+)*");
```
为了处理包含双引号的字符串，可以使用 r###"..."### 语法：
```
println!(r###"
This raw string started with 'r###"'.
Therefore it does not end until we reach a quote mark ('"')
followed immediately by three pound signs ('###'):
"###);
```
### 1.9.2 字节串（Byte String）

字节串以 b 前缀标记，用于表示由字节（u8）构成的字符串，而不是 Unicode 字符。它们通常用于处理原始二进制数据。

- 字节串的定义

```
let method = b"GET";
assert_eq!(method, &[b'G', b'E', b'T']);
```

- 字节串的多行表示

与普通字符串类似，字节串也可以跨多行，并且可以使用反斜杠连接行：

```
let pattern = br"\d+(\.\d+)*";
```

字节串的类型是 &\[u8]，它只支持 ASCII 字符和少数的 \xHH 转义序列。

### 1.9.3 内存中的字符串

Rust 中的字符串是 UTF-8 编码的，这意味着它们可以高效地存储多种语言的字符。

- String和 &str：

	- String 是一个动态增长的字符串类型，存储在堆上，支持添加、修改等操作。
	- &str 是一个指向已有 UTF-8 字符数据的不可变引用，通常表示字符串字面量。

- String 和 &str 的内存布局：

	- String 存储在堆上，可以动态增长。
	- &str 是一个胖指针，包含指向数据的地址和长度。

示例代码：

```
let noodles = "noodles".to_string();  // 创建 String
let oodles = &noodles[1..];           // 创建 &str 切片
let poodles = "ಠ_ಠ";                 // 字符串字面量
```

字符串的底层的数据存储格式实际上是\[ u8 ]，一个字节数组。对于

```
let hello = String::from("中国人");
```

如果问你该字符串多长，你可能会说 3，但是实际上是 9 个字节的长度，因为大部分常用汉字在 UTF-8 中的长度是 3 个字节，因此这种情况下对 hello 进行索引，访问 &hello[0] 没有任何意义，因为你取不到 中 这个字符，而是取到了这个字符三个字节中的第一个字节.(补充代码)

### 1.9.4 String 类型

String 是一个可变的、在堆上分配内存的字符串类型。它与 Vec 类似，但会保证其中的内容是有效的 UTF-8。
+ 创建 String：
     - 使用 .to_string() 方法将 &str 转换为 String：
	 - 使用  format! 宏生成新的 String：
	 - 连接多个字符串：
```
let error_message = "too many pets".to_string();
let formatted_string = format!("{}°{:02}′{:02}″N", 24, 5, 23);
let bits = vec!["veni", "vidi", "vici"];
assert_eq!(bits.concat(), "venividivici");
assert_eq!(bits.join(", "), "veni, vidi, vici");
```

那么如何将 String 类型转为 &str 类型呢？答案很简单，取引用即可：

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

实际上这种灵活用法是因为 deref 隐式强制转换.

### 1.9.5 使用字符串

Rust 字符串类型支持许多操作，包括比较、查找、替换和拆分 追加、插入、替换、删除、连接等。

字符串比较

- 使用 == 和 != 进行字符串的比较：

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

push(): 向字符串尾部追加一个字符（char）。

- push_str(): 向字符串尾部追加一个字符串字面量（&str）。
- 这两个方法会直接修改原有字符串，因此需要使用 mut 修饰字符串变量。

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

Rust 提供了多种类似字符串的类型，处理不同的场景，特别是当与非 UTF-8 数据或系统进行互操作时：
- PathBuf 和 Path：用于处理文件路径。
- Vec 和 &[u8]：用于处理二进制数据。
- OsString 和 &OsStr：用于处理操作系统特有的字符串（如环境变量名、命令行参数）。
- CString 和 &CStr：用于与 C 语言的 null 结尾字符串进行互操作。

### 1.9.7 总结

Rust 提供了灵活且强大的字符串处理方式，允许程序员高效地处理 UTF-8 字符串、字节串及其他格式的数据。在处理字符串时，&str 是不可变的引用类型，而 String 则是可变的、在堆上分配内存的类型。理解这些类型的区别，以及如何选择它们，将帮助你在 Rust 中更加高效地处理字符串。

## 1.10切片(slice)

在 Rust 中，切片（slices）是对数组或字符串的一部分的引用，允许你借用数据的一部分而不需要复制它。切片可以应用于数组、Vec 和 String 类型。

### 1.10.1 数组和 Vec 的切片

+ 切片的基本语法

切片是对数组或 Vec 的引用，它没有所有权，并且是不可变的或可变的。切片的语法如下：
```let arr = [1, 2, 3, 4, 5];
let slice = &arr[1..4];  // 切片从索引1到3（不包括4），即 [2, 3, 4]
```
+ 数组切片示例
```fn main() {
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

对于 String 和字符串字面量（&str），切片操作类似，但由于字符串的字符是 Unicode 编码的，所以切片的起止位置必须是有效的字符边界。可以使用 get() 方法避免索引越界。

+ 字符串切片示例

```
fn main() {
    let s = String::from("Hello, Rust!");
    let slice = &s[7..11]; // 字符串从第 7 到第 10 个字节
    println!("{}", slice); // 输出: Rust
}
```

+ 使用 get() 方法

get() 方法返回一个 Option<&str>，可以避免越界错误：

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

可变切片示例

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

传递切片给函数

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

### 1.10.5 切片的边界注意事项

- 字符边界：对于 String 和 &str，切片的开始和结束位置必须在有效字符边界上，否则会引发运行时错误（panic!）。
- 越界访问：在使用数组或 Vec 的切片时，若切片索引越界，Rust 会引发 panic!。

### 1.10.6 总结

- 切片是一种对数组、Vec 或 String 的引用，不会拥有数据，且可以是不可变或可变的。
- 使用切片可以避免复制数据，节省内存开销，且切片操作的语法简单。
- 处理字符串切片时要注意 Unicode 字符的边界，确保不会跨越字符的边界。

切片是 Rust 中非常强大的工具，掌握它可以使得你在进行数组、字符串等数据处理时更加高效。

## 1.11类型别名(type)

与 C++ 中的 typedef 用法类似，可以使用 type 关键字来为现有类型声明一个新名称：

```
type Bytes = Vec<u8>;
//这里声明的类型 Bytes 就是这种特定 Vec 的简写形式。
fn decode(data: &Bytes) {
...
}
```