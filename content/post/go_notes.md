---
title: "Go_notes"
date: 2020-09-10T16:42:27+08:00
lastmod: 2020-09-10T16:42:27+08:00
draft: false
keywords: ["golang"]
description: "golang notes"
tags: ["golang"]
categories: ["golang", "notes"]
author: "ztf88"
---

# 基本结构和基本数据类型

## 文件名、关键字与标识符

- Go源文件命名，均以小写字母组成，多部分的文件名使用`_`连接，不包含空
  格及其他字符，示例：`scanner.go`,`scanner_test.go`
- Go语言内部普通变量使用小写字母（或`_`）开头，长变量名使用驼峰方式命
  名，需要外部引用的方法使用*大写*字母开头
- `_`也可以作为空字符，占位使用
- 关键字、保留字及数据类型无法作为变量

## Go程序的基本结构和要素

```go
package main

import "fmt"

func main() {
	fmt.Println("hello world")
}

```

包是结构化代码的一种方式：每个程序都由包的概念组成，可以使用自身的包或
其他包中导入内容。

每个程序至少包含一个`main`包及其他包，和`main`函数。

1. 声明包`package main`
2. 引入标准库或其他包`import "fmt"`
3. 主函数`func main() {}`
4. 大写字母的函数可以被其他包引入`fmt.Println()`
5. 单行注释`/**/`和多行注释`//`
6. `\`换行符

## 常量

常量用于存储不会改变的数据，声明关键字`const`

```go
const Pi = 3.14159

//显式声明
const a string = "abc"
//隐式声明
const b = "def"
```

`const`配合`iota`用作枚举；`iota`每被引用一次自动加一；再次遇到`const`自
动归零

```go
func main

import "fmt"

const (
	Sunday =iota
	Monday
	Tuesday
	wednesday
	Thursday
	Friday
	Saturday
)

func main() {
	fmt.Println(Friday)
}
```

## 变量

变量声明的几种形式

```go
//一般
var name string
name = "john"

var name string = "john"

//省略变量类型，go通过变量值来判断类型
var name = "john"

//省略变量值，go为没有值的声明变量赋予对应0值
var name string //name为空字符串""
var i int //i为整数型0值
var pointer *int //指针类型初始化值为nil
var f float //浮点数初始化为0.0
var t bool //布尔值初始化为false

//分组声明

var (
	a string
	b int
	c bool
	)
	
//变量的命名遵循驼峰命名法
var numShips int

//如果全局变量希望能够被外部包引用则以大写开头，同样函数希望在外部被引
用也需要大写字母开头
var UserId int

//包一级别的变量为全局变量，函数体内的变量为局部变量
//局部变量可以使用更为简洁的声明语句
name := "john"
```

调试

引入"fmt"包，打印信息

```go
fmt.Println("hello world")
//fmt.Printf(format string, list of values to be printed)
//格式化标志符号%s对应字符串
fmt.Printf("hello %s", name)
//%v代表使用类型的默认输出格式
fmt.Printf(hello %v", name)
//fmt.Print与fmt.Println会对内容自动格式化，添加空格
fmt.Print("hello", 23)
> hello 23
```

	*注意：* 不可对已经声明的变量重新声明
## 基本类型和运算符

- 布尔类型

```go
//布尔值只能是常量true和false
var b bool = true
var a bool = false
//布尔值之间可以用“==”或“!=”比较
//也可以使用“!”，“&&”，“||”逻辑运算符产生新的布尔值
```

- 数值类型

常用的数值类型就是整形和浮点类型

```go
//基于计算机架构的类型
//int（32位系统上均使用32位，4个字节；64位系统均使用64位，8个字节）、
uint和uintpr（一个指针的大小）

//go没有float类型，只有float32和float64

// 整数
//int8(-128->127,2^8)
//int16(-32768->32767,2^16)
//int32(-2147483648->2147483647)
//int64(-9223372036854775808-9223372036854775807)

// 无符号整数
//unit8(0->256)
//unit16(0->65536)
//unit32(0->4294967296)
//unit64(0->18446744073709551616)

// 浮点数
//float32
//float64

//int型是计算最快的一种类型
//整型的零值为0，浮点型的零值为0.0
//float32精确到小数点7位
//float64精确到小数点15位
//计算浮点数应尽量选择精确度高的float64

//%d用于格式化整数（%x和%X用于格式化16进制表示的数）
//%g用于格式化浮点型（%f输出浮点数，%e输出科学计数表示法）
//%0d用于输出定长的整数
//%n.mg用于表示数字n并精确到小数点后m位，g也可以替换成e或f

//go拥有复数类型
complex32
complex64

```

- 运算符

```go
//二元运算符


//一元运算符

// 逻辑运算附

// 算数运算符

// 随机数
package main
import (
	"fmt"
	"math/rand"
	"time"
	)

func main() {
	for i := 0; i < 10; i++ {
		a := rand.Int() //rand.Int() 伪随机数
		fmt.Printf("%d / ", a)
		
	for i := 0; i <5 ; i++ {
		r := rand.Int(8) //rand.Intn(n) 0-n之间伪随机数
		fmt.Printf("%d / ", r)
	}
	fmt.Println()
	timens := int64(time.Now().Nansecond())
	rand.Seed(timens) //为伪随机数提供种子
	for i :=0; i < 10; i++ {
	fmt.Printf("%2.2f / ", 100*rand.Float32())
	}
}

// 运算符与优先级

运算方向从左到右，由上至下，优先级由高至低

优先级     运算符
 7      ^ !
 6      * / % << >> & &^
 5      + - | ^
 4      == != < <= >= >
 3      <-
 2      &&
 1      ||


// 类型别名

为某一类型声明新的名称，避免冲突
type TZ int //将TZ（timezone）声明为int类型，区分与其他int类型的数据


// 字符类型

byte是uint8的别名

```


## 字符串

字符串是utf-8字符的一个序列

解释字符串

- `\n`换行
- `\r`回车
- `\t`tab键
- `\u`或`\U`unicode字符
- `\\`反斜杠本身

非解释性字符串

`\`反引号的字符串会被原样输出\``

字符串类数字，可以通过`len()`函数计算字符串字符数，并使用`s[m:n]`索引，
不能使用指针提取某字符`&s[1]`为非法

字符串可以通过“+”拼接，但是最好的方法是`strings.Join()`

## strings和strconv包

```go
import "strings"

//判断-前缀和后缀
strings.HasPrefix(s, prefix string) bool
strings.HasSuffix(s, suffix string) bool
//判断-包含关系
strings.Contains(s, sunstr string) bool
//判断-子字符串在父字符串中出现缩印的位置
strings.Index(s, str string) int
strings.LastIndex(s, str string) int //判断子字符串出现的最后的位置
strings.IndexRune(s string, r rune) int //如果是非ACSII码
//替换-字符串,n=-1,替换所有字符串
strings.Replace(str, old, new, n) string
//统计-字符串出现的次数
strings.Count(s, str string) int
//重复字符串
strings.Repeat(s, count int) string
//修改大小写
strings.ToLower(s) string
strings.ToUpper(s) string
//修剪字符串
strings.TrimSpace(s) //剔除开头结尾空白
strings.Trim(s, "cut") //剔除字符串s中的cut
//分割字符串
strings.Field(s) //利用空白作为分隔符将字符串分割
strings.Split(s, sep) //利用自定义的sep来将字符串分割
//拼接字符串
strings.Join(s1 []string, sep string) string

////
//字符串转换strconv
strconv.Itoa(i int) string //返回数字i所表示的字符串类型的十进制数
strconv.FormatFloat(f float64, fmt byte, pre int, bitSize int) //将64
位浮点型的数字转换为字符串

## 时间和日期

time包提供了一个数据类型time.Time以及显示和测量时间和日期的功能函数

```go
import (
	"fmt"
	"time"
	)
	
func main() {
	t := time.Now()
	fmt.Printf("%02d.%02d.%4d\n", t.Day(), t.Month(), t.Year())
}
```

## 指针

...
# 控制结构

## 简述

- 条件语句: if-else, switch, break, continue, select

- 循环语句: for, range

## if-else

```go
# base 1

if condition {
	// do something
}

# base 2

if condition {
	// do something
} else {
	// do something
}

# base 3

if condition1 {
	// do something
} else if condition2 {
	// do something
} else {
	// default something
}

# 4 if条件可以有一个初始化语句

if v := 4; v > max {
	// do something
}

```

## 测试多返回值函数的错误

## switch

应用于if-else对过多，可使用switch语句

```go
// switch v与case后变量对比
switch v {
	case 1:
		...
	case 2:
		...
	default:
		...
}

// 实例

switch i {
	case 0: //只有i == 0 才会进入该分支
	case 1：
		f() //当i == 1执行f()函数
}

// fallthrough

switch i {
	case 0: fallthrough
	case 1:
		f() //当i == 0函数f()也会执行
}

// 无条件switch，配合其他变量

var num = 3
switch {
	case num > 2:
		fmt.Println("num is bigger than 2")
	case num < 2:
		fmt.Println("num is smaller than2")
	default:
		// ...
}

// 带初始化语句的switch
switch initialzation {
	case v1:
		...
	case v2:
		...
	default:
		...
}

// 实例
switch t := time.Now(); {
	case t > 0:
		...
	case t < 0:
		...
	default:
		//
}

```



## for

```go
for 初始化语句；条件语句；修饰语句 {}

// case 1
for i, j := 0, N; i < j; i, j = i+1, j-1 {}

// case 2
for i:=0; i<5; i++ {
    for j:=0; j<10; j++ {
        println(j)
    }
}

// 基于条件判断的迭代，或者说没有初始化语句与修饰语句的判断
for i >= 0 {
	i = i -1
	fmt.Println("...")
	
// 无限循环

for {
	...
}

// for-range

for pos, char := range str {
	...
}

// 
```

## break and continue

break关键字阻断循环；continue关键字跳过本轮循环

```go
var i int = 5
for {
	i = i -1
	fmt.Printf("The variable i is now: %d\n", i)
	if i < 0 {
		break
	}
}


for i := 1; i < 5; i ++ {
	fmt.Println("i")
	if i == 3 {
		continue
	}
}

```

## 标签与goto

for, switch 或 select 语句都可以配合标签label形式的标识符使用

*标签的大小写是敏感的，一般使用大写字母*



