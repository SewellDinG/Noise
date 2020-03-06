[对比学习：Golang VS Python3](https://juejin.im/post/5cd945d6e51d453d022cb65f)

Golang和Python都是目前在各自领域最流行的开发语言之一。

Golang其高效而又友好的语法，赢得了很多后端开发人员的青睐，最适用于高并发网络编程的语言之一。

Python不用说，TIOBE排行榜的前十常驻居民，现在已经稳定在前五了。在机器学习、AI、数据分析领域成为必学语言。

两门编程语言在语法上都有各自的特点，而且都**易学易用**。

本文对比这两门语言目的不是争谁优谁略，只是为了对比学习，适合掌握Python想学Go或者掌握Go想学Python的同学们参考。

Go和Python，一个是静态语言一个是动态语言，从各个方面来看，都有根本性的差异，所以，文中很多内容不进行深入的比较了，我们只从程序员最直观的语法面做对比。

**为了便于阅读，文中涉及代码都采用尽量简单的语句呈现**

## 字符编码

### Python

Python2中默认的编码格式是 ASCII 格式，程序文件中如果包含中文字符（包括注释部分）需要在文件开头加上 `# -*- coding: UTF-8 -*-` 或者 `#coding=utf-8` 就行了

Python3默认支持Unicode

### Golang

原生支持Unicode

## 保留字（关键字）

### Python

30个关键字

```
and	exec	not
assert	finally	or
break	for	pass
class	from	print
continue global	raise
def	if	return
del	import	try
elif	in	while
else	is	with
except	lambda	yield
```

### Golang

25个关键字

```
break	default	func	interface	select
case	defer	go	map	struct
chan	else	goto	package	switch
const	fallthrough	if	range	type
continue	for	import	return	var
```

## 注释

### Python

```
# 单行注释

'''
多行注释
多行注释
'''

"""
多行注释
多行注释
"""
```

### Golang

```
//单行注释

/*
多行注释
多行注释
*/
```

## 变量赋值

### Python

Python是动态语言，所以在定义变量的时候不需要申明类型，直接使用即可。 Python会根据值判断类型。

```
name = "Zeta" # 字符串变量
age = 38 # 整数
income = 1.23 # 浮点数
```

多变量赋值

```
a,b = 1,2 # a=1; b=2
c = d = 3 # c=3; d=3
```

### Golang

Go是静态语言，是强类型的，但是Go语言也允许在赋值变量时确定类型。

因此Go有多种申明变量的方式

```
// 1. 完整的申明并赋值
var a int
a = 1

// 2. 声明变量类型同时赋值
var a int = 1

// 3. 不声明类型，赋值时确定
var a = 1

// 4. 不用 var 关键字申明变量并赋值后确定类型
a := 1
```

注意，Go中的new关键字并不是声明变量，而是返回该类型的指针

```
a := new(int) //这时候a是一个*int指针变量
```

## 标准数据类型

### Python 的标准数据类型有：

- Boolean（布尔值）
- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

### Golang

- boolean（布尔值）
- numeric（数字）
- string（字符串）
- 数组（数组）
- slice（切片：不定长数组）
- map（字典）
- struct（结构体）
- pointer（指针）
- function（函数）
- interface（接口）
- channel（通道）

### 总结

Python中的**List列表**对应Go语言中的**Slice切片**

Python中的**Dictionary字典**对应Go语言中的**map**

有一些值得注意的地方：

- Go是支持函数编程的语言，所以在Go语言中函数是一个类型
- Go语言不是面向对象的语言，没有定义类的关键字Class，要实现OOP风格编程，是通过struct、interface类型实现的
- Python中的元组和集合在Go中都没有
- channel是Go里独有的类型，多线程之间的通信就靠它

## 数据类型转换

### Python

Python类型转换非常简单，用类型名作为函数名即可。

```
int(n)            # 将数字n转换为一个整数
float(n)          # 将数字n转换到一个浮点数
str(o)            # 将对象 obj 转换为字符串
tuple(s)          # 将序列 s 转换为一个元组
list(s)           # 将序列 s 转换为一个列表
set(s)            # 将序列 s 转换为一个集合
```

### Golang

Go语言的基础类型转换和Python差不多，也是用类型名作为函数名

```
i := 1024
f := float32(i)
i = float32(f)
```

另外，Python中可以直接转换数字字符串和数字：

```
s = "123"
i = 456
print(int(s), str(i))
```

**但是Go是不可以的。**

Go语言的字符串处理很不同，`string()`只能用于`[]byte`类型转换成字符串，其他基础类型的转换需要用`strconv`包，另外，其他类型转换成为`string`类型除了用`strconv`包，还可以用`fmt.Sprintf`函数：

```
package main

import (
    "fmt"
    "strconv"
)

func main() {
    s := "123"
    i, _ := strconv.Atoi(s)
    println(i)

    s2 := fmt.Sprintf("%d", 456)
    println(s2)
}
```

Go中的interface类型是不能直接转换成其他类型的，需要使用到**断言**

```
package main

func main() {
var itf interface{} = 1
i, ok := itf.(string)
println("值:", i, "; 断言结果", ok)

j, ok := itf.(int)
println("值:", j, "; 断言结果", ok)
}
```

输出为:

```
值:  ; 断言结果 false
值: 1 ; 断言结果 true
```

## 条件语句

### Python

Python传统的判断语句如下

```
if name == 'zeta':          # 判断变量是否为 zeta 
    print('Welcome boss')   # 并输出欢迎信息
else:
    print('Hi, ' + name)  
```

Python不支持三元表达式，但是可以用一种类似的替代办法

```
title = "boss"
name = "zeta" if title == "boss" else "chow"
print(name)
```

逻辑与用 `and` ，逻辑或用 `or`

### Golang

Go的`if`的语法类似Java，但是表达式不需要使用`()`

```
if a > b{
    println("a > b")
} else {
    println("a <= b")
}
```

Go同样没有三元表达式，并且也没有什么替代方法。

另外，Go允许在`if`的表达式里定义变量，定义并赋值的表达式与判断的表达式用`;`隔开，常见的情况是获取函数返回error，然后判断error是否为空：

```
if err := foo(); err != nil {
    println("发生一些错误")
} 
```

与Python不同，逻辑与用 `&&`， 逻辑或用`||`

## 循环语句

### Python

Python中有`while`和`for`两种循环，都可以使用`break`跳出循环和`continue`立即进入下一轮循环，另外，Python的循环语句还可以用`else`执行循环全部完毕后的代码，`break`跳出后不会执行`else`的代码

**while** 条件循环，

```
count = 0
while (count < 9):
    print('The count is:', count)
    count = count + 1
    if count == 5:
        break   # 可以比较以下break和不break的区别
        pass
else:
    print('loop over')
```

**for** 遍历循环，循环遍历所有序列对象的子项

```
names = ['zeta', 'chow',  'world']
for n in names:
    print('Hello, ' + n)
    if n == 'world':
        break
        pass
else:
    print('Good night!')
```

`for`循环中也可以用`else`，（注释掉代码中的`break`试试看。)

### Golang

Go语言只有一个循环语句`for`，但是根据不同的表达式，`for`有不同的表现

```
for 前置表达式; 条件表达式; 后置表达式 {
	//...
}
```

**前置表达式** 在每轮循环前运行，可以用于声明变量或调用函数返回； **条件表达式** 满足该表达式则执行下一轮循环，否则退出循环; **后置表达式** 在循环完成后执行

经典的用法：

```
for i := 0; i < 10; i++ {
    println(i)
}
```

我们可以忽略掉前置和后置表达式

```
sum := 1
for sum < 10 {
	sum += sum
}
```

设置可以忽略掉全部表达式，也就是无限循环

```
for {
    print(".")
}
```

Go的`for`循环同样可以使用 `break`退出循环和`continue`立即进行下一轮循环。

`for`除了配合表达式循环，同样也可以用于遍历循环，需要用到`range`关键字

```
names := []string{"zeta", "chow", "world"}
for i, n := range names {
    println(i,"Hello, " + n)
}
```

## 函数

### Python

用`def`关键字定义函数，并且在Python中，作为脚本语言，调用函数必须在定义函数之后。

```
def foo(name):
    print("hello, "+name)
    pass

foo("zeta")
```

**默认参数** Python定义函数参数时，可以设置默认值，调用时如果没有传递该参数，函数内将使用默认值，默认值参数必须放在无默认值参数后面。

```
def foo(name="zeta"):
    print("hello, "+name)
    pass

foo()
```

**关键字参数** 一般函数传递参数时，必须按照参数定于的顺序传递，但是Python中，允许使用关键字参数，这样通过指定参数明，可以不按照函数定义参数的顺序传递参数。

```
def foo(age, name="zeta"):
    print("hello, "+name+"; age="+str(age))
    pass

foo(name="chow", age=18)
```

**不定长参数**，Python支持不定长参数，用`*`定义参数名，调用时多个参数将作为一个元祖传递到函数内

```
def foo(*names):
    for n in names:
        print("hello, "+n)
    pass

foo("zeta", "chow", "world")
```

**return** 返回函数结果。

### Golang

Go用`func`定义函数，没有默认值参数、没有关键字参数，但是有很多其他特征。

```
func main() {
    println(foo(18, "zeta"))
}

func foo(age int, name string) (r string) {
    r = fmt.Sprintf("myname is %s , age %d", name, age)
    return 
}
```

函数的定义和调用没有顺序的限制。

Go的函数不仅可以定义函数返回值类型，还可以申明返回值变量，当定义了返回值变量时，函数内的`return`语句可以不需要带返回值，函数会默认使用返回值变量返回。

**可变参数**

使用`…类型`定义可变参数，函数内获得的参数实际是该`类型`的`slice`对象

```
func main() {
	println(foo(18, “zeta”, “chow”, “world”))
}

func foo(age int, names …string) (r string) {
	for _, n := range names {
		r += fmt.Sprintf(“myname is %s , age %d \n”, n, age)
	}

	return
}
```

**defer句**

`defer`语句后面指定一个函数，该函数会延迟到本函数return后再执行。

defer语句在Go语言中非常有用，详细可以查阅本专栏的另一篇文章《**Golang研学：如何掌握并用好defer（延迟执行）**》

```
func foo() {
	defer fmt.Println("defer run")
	fmt.Println("Hello world")
	return
}
```

运行结果：

```
Hello world
defer run
```

另外，在Go语言中**函数也是类型**，可以作为参数传递给别的函数

```
func main() {
	n := foo(func(i int, j int) int {
		return i + j
	})
	println(n)
}

func foo(af func(int, int) int) int {
	return af(1, 2)
}
```

上面这个例子直接在参数定义时使用函数类型，看上去有点混乱

再看来看一个清晰并完整的例子，说明全在注释里。

```
package main

type math func(int, int) int //定义一个函数类型，两个int参数，一个int返回值

//定义一个函数add，这个函数两个int参数一个int返回值，与math类型相符
func add(i int, j int) int {
	return i + j
}

//再定义一个multiply，这个函数同样符合math类型
func multiply(i, j int) int {
	return i * j
}

//foo函数，需要一个math类型的参数，用math类型的函数计算第2和第3个参数数字，并返回计算结果
//稍后在main中我们将add函数和multiply分别作为参数传递给它
func foo(m math, n1, n2 int) int {
	return m(1, 2)
}

func main() {
	//传递add函数和两个数字，计算相加结果
	n := foo(add, 1, 2)
	println(n)

	//传递multply和两个数字，计算相乘结果
	n = foo(multiply, 1, 2)
	println(n)
}
```

结果

```
3
2
```

## 模块

### Python

- 模块是一个.py文件
- 模块在第一次被导入时执行
- 一个下划线定义保护级变量和函数，两个下划线定义私有变量和函数
- 导入模块习惯性在脚本顶部，但是不强制

### Golang

- 与文件和文件名无关，每一个文件第一行用package定义包名，相同包名为一个包
- 包中的变量第一次引用时初始化，如果包中包含init函数，也会在第一次引用时执行（变量初始化后）
- 保重首写字母大写的函数和变量为共有，小写字母为私有，Golang不是面向对象的，所以不存在保护级。
- 导入模块必须写在package之后，其他代码之前。

## 导入包

### Python

在Python中，使用`import`导入模块。

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
# 导入模块
import support
 
support.print_func(“Runoob”)
```

还可以使用`from import`导入模块指定部分

```
from modname import name1[, name2[, ... nameN]]
```

为导入的包设置别名用 `as`关键字

```
import datetime as dt
```

### Golang

也是使用`import`导入包，导入包指定的是包的路径，包名默认为路径中的最后部分

```
import "net/url" //导入url包
```

多个包可以用`()`组合导入

```
import (
	"fmt"
	"net/url"
)
```

为导入的包设置别名, 直接在导入包时，直接在报名前面添加别名，用空格隔开

```
import (
	f "fmt"
  u "net/url"
)
```

## 错误和异常

### Python

Python中用经典的 `try/except` 捕获异常

```
try:
<语句>        #运行别的代码
except <异常名称>：
<语句>        #
except <异常名称>，<数据>:
<语句>        #如果引发了指定名称的异常，获得附加的数据
```

还提供了 **else** 和 **finally**

如果没发生异常的执行`else`语句块，`finally`块的代码无论是否捕获异常都会执行

Python内建了很全面的异常类型名称，同时能自定义异常类型

### Golang

Golang里没有用经典的 `try/except`捕获异常。

Golang提供两种错误处理方式

1. 函数返回`error`类型对象判断错误
2. `panic`异常

一般情况下在Go里只使用`error`类型判断错误，Go官方希望开发者能够很清楚的掌控所有的异常，在每一个可能出现异常的地方都返回或判断`error`是否存在。

`error`是一个内置的接口类型

```
type error interface {
	Error() string
}
```

通常，使用`error`异常处理类似这样：

```
package main

import "fmt"

func foo(i int, j int) (r int, err error) {
    if j == 0 {
        err = fmt.Errorf("参数2不能为 %d", j) //给err变量赋值一个error对象
        return //返回r和err，因为定义了返回值变量名，所以不需要在这里写返回变量
    }

    return i / j, err //如果没有赋值error给err变量，err是nil
}

func main() {
    //传递add函数和两个数字，计算相加结果
    n, err := foo(100, 0)
    if err != nil { //判断返回的err变量是否为nil，如果不是，说明函数调用出错，打印错误内容
        println(err.Error())
    } else {
        println(n)
    }
}
```

`panic`可以手工调用，但是Golang官方建议尽量不要使用`panic`，每一个异常都应该用error对象捕获。

Go语言在一些情况下会触发内建的`panic`，例如 0 除、数组越界等，修改一下上面的例子，我们让函数引起0除`panic`

```
package main

func foo(i int, j int) (r int) {
	return i / j
}

func main() {
	//传递add函数和两个数字，计算相加结果
	n := foo(100, 0)
	println(n)
}
```

运行后会出现

```
panic: runtime error: integer divide by zero
goroutine 1 [running]:
main.foo(...)
        /lang.go:4
main.main()
        /lang.go:9 +0x12
exit status 2
```

手工`panic`可以这样:

```
func foo(i int, j int) (r int) {
	if j == 0 {
		panic("panic说明: j为0")
	}
	return i / j
}
```

运行后，可以看到，错误消息的第一句:

```
panic: panic说明: j为0
```

## 面向对象

### Python

Python完全支持面向对象的。

### Golang

尽管Go语言允许面向对象的风格编程，但是本身并不是面向对象的

官方FAQ原文

**Is Go an object-oriented language?**

> Yes and no. Although Go has types and methods and allows an object-oriented style of programming, there is no type hierarchy. The concept of “interface” in Go provides a different approach that we believe is easy to use and in some ways more general. There are also ways to embed types in other types to provide something analogous—but not identical—to subclassing. Moreover, methods in Go are more general than in C++ or Java: they can be defined for any sort of data, even built-in types such as plain, “unboxed” integers. They are not restricted to structs (classes).

## 多线程

### Python

1. 使用`thread`模块中的`start_new_thread()`函数
2. 使用`threading`模块创建线程

### Golang

用关键 `go`创建协程`goroutine`

在`go`关键字后指定函数，将会开启一个协程运行该函数。

```
package main

import (
    "fmt"
    "time"
)

func foo() {
    for i := 0; i < 5; i++ {
        fmt.Println("loop in foo:", i)
        time.Sleep(1 * time.Second)
    }
}

func main() {
    go foo()

    for i := 0; i < 5; i++ {
        fmt.Println("loop in main:", i)
        time.Sleep(1 * time.Second)
    }
    time.Sleep(6 * time.Second)
}
```

Go语言中，协程之间的通信是通过`channel`实现的：

```
package main

import (
    "fmt"
    "time"
)

//接受一个chan类型的参数c
func foo(c chan int) { 
    time.Sleep(1 * time.Second) //等待1秒
    c <- 1024                   //向c中写入数字
}

func main() {
    c := make(chan int) //创建chan变量c
    go foo(c)           //在子写成中运行函数foo，并传递变量c
    fmt.Println("wait chan 'c' for 1 second")
    fmt.Println(<-c) //取出chan 'c'的值（取值时，如果c中无值，主县城会阻塞等待）
}
```

## 总结

Python和Go分别在动态语言和静态语言中都是最易学易用的编程语言之一。

它们并不存在取代关系，而是各自在其领域发挥自己的作用。

Python的语法简单直观，除了程序员爱不释手外也非常适合于其他领域从业者使用。

Go兼具语法简单和运行高效的有点，在多线程处理方面很优秀，非常适合已经掌握一定编程基础和一门主流语言的同学学习，不过，Go是不支持面向对象的，对于大多数支持面向对象语言的使用者在学习Go语言的时候，需要谨记并且转换编程思路。