### Go语言学习

alt+enter

ctrl+space

ctrl+shift+space

ctrl+alt+L

ctrl+alt+M重构

F2查看错误

alt+6查看问题

ctrl+shift+/

alt+F8 评估表达式

ctrl+F8 切换断点

环境搭建，编译之后生成可执行exe文件，就可以直接使用了

![image-20210725102106105](Go语言学习.assets/image-20210725102106105.png)

![image-20210725102139391](Go语言学习.assets/image-20210725102139391.png)

编译

使用 go build

1.在项目目录下执行go build

2.在其他路径下执行go build ，需要在后面加上项目的路径（项目路径从gopath/src后开始写起，编译之后的可执行文件就保存在当前目录下）

3.go build -o hello.exe



go run

像执行脚本文件一样执行go代码



go install

分为两步：

1.先编译得到一个可执行文件

2.将可执行文件拷贝到gopath的bin目录



交叉编译，可以跨平台跑程序

例如在windows平台编译一个能在linux平台上执行的可执行文件

**这个似乎要在源文件位置处使用cmd命令操作,并且要用大写!!!**

```shell
E:\project\GOproject\code.oldboyedu.com\day1>SET CGO_ENABLE=0

E:\project\GOproject\code.oldboyedu.com\day1>SET GOOS=linux

E:\project\GOproject\code.oldboyedu.com\day1>SET GOARCH=amd64

E:\project\GOproject\code.oldboyedu.com\day1>go build


```

![image-20210725103733683](Go语言学习.assets/image-20210725103733683.png)



go语言的基本结构

```go
package main

//导入的包
import "fmt"

//程序的入口函数
//函数外部只能放置标识符（变量、常量、函数、类型）的声明
func main() {
   fmt.Println("hello world")
}
```



变量和常量

go语言中的变量必须先声明后使用

var s1 string :声明一个保存字符串数据的变量

var name string 

var age int 

var isOk bool

```go
package main

import "fmt"

var name string
var age int
var isOk bool

//批量声明
var (
	name1 string
	age1 int
	isOk1 bool
)
func main() {
	fmt.Println(name1)
	fmt.Println(age1)
	fmt.Println(isOk1)

	name1 = "linjianshu"
	age1 = 16
	isOk1 = true

	//go语言中推荐使用驼峰命名
	//go语言中非全局变量声明必须使用，不用就编译不过去
	fmt.Println(name1)
	fmt.Println(age1)
	fmt.Println(isOk1)
	fmt.Printf("name:%s",name1)  //%s占位符，使用name1这个变量去替换这个占位符

	//声明变量同时赋值
	var studentName string = "ljs"
	//类型推导
	var studentName1  = "ljs"
	fmt.Println(studentName)
	fmt.Println(studentName1)
	//简短变量声明 :=  只能在函数里面使用
	studentName2 := "jwt"
	fmt.Println(studentName2)

	x,_ :=foo()
	fmt.Println(x)

	x1 := 0
	x1,_ =foo()
	fmt.Println(x1)

}

func foo() (int, string) {
	return 10,"ljs"
}
```

匿名变量 用_来接收，表示我不用这个变量，匿名变量不占用命名空间，不会分配内存，所以匿名变量不存在重复声明

注意：1.函数外的每个语句都必须以关键字开始2.同一个作用域{}中不能重复声明同名的变量



常量

iota

ioto是go语言的常量计数器，只能在常量表达式中使用

iota在const关键字出现的时候被重置为0. const中每新增一行常量声明将使iota计数一次iota可理解为const语句块中的行索引 使用iota能简化定义，在定义枚举时很有用

```go
package main

import "fmt"

//常量
const pi = 3.1415926
//常量定义了之后不能修改
//在程序运行期间不会改变

//批量声明常量时，如果某一行没有赋值，默认就和上一行一致
const (
	pi1 = pi
	pi2
	pi3
)

const (
	i1 = iota
	i2
	i3
)

const (
	n1 = iota
	n2
	_
	n3
)

//插队
const (
	k1 = iota
	k2 = 100
	k3
	k4 =iota
	k5
)

const (
	p1,p2 = iota+1,iota+2
	p3,p4 = iota+1,iota+2
)

//定义数量级
const (
	_ = iota
	KB = 1<<(10 * iota)
	MB = 1<<(10 * iota)
	GB = 1<<(10 * iota)
	TB = 1<<(10 * iota)
)

func main() {
	// 不可以 pi = 12.3
	fmt.Println("pi2:",pi2)

	fmt.Println("i1:",i1)
	fmt.Println("i2:",i2)
	fmt.Println("i3:",i3)

	fmt.Println("n1:",n1)
	fmt.Println("n2:",n2)
	fmt.Println("n3:",n3)

	fmt.Println("k1:",k1)
	fmt.Println("k2:",k2)
	fmt.Println("k3:",k3)
	fmt.Println("k4:",k4)
	fmt.Println("k5:",k5)

	fmt.Println("p1:",p1)
	fmt.Println("p2:",p2)
	fmt.Println("p3:",p3)
	fmt.Println("p4:",p4)

	fmt.Println("kb:",KB)
	fmt.Println("mb:",MB)
	fmt.Println("gb:",GB)
	fmt.Println("tb:",TB)
}
```



关键字和标识符

go语言有25个关键字

break default func interface select case defer go map struct chan else goto package switch const fallthrough if range type continue for import return var 



基本数据类型

整型

整型分为以下两大类：按长度分为：int8 , int16 , int32 ,int64 对应的无符号整型：uint8 , uint16 ,uint32

其中，uint8就是我们熟知的byte型，int16对应C语言中的short型，int64对应C语言中的long型

特殊整型

uint根据电脑位数来搞

int根据电脑位数来搞

uintptr无符号整数，用于存放一个指针

```go
package main

import "fmt"

func main() {
	 i1  := 10
	fmt.Printf("%d\n",i1)
	fmt.Printf("%o\n",i1)   //把十进制转成8进制
	fmt.Printf("%b\n",i1)   //把十进制转成2进制
	fmt.Printf("%x\n",i1)   //把十进制转成16进制

	 //八进制
	 i2 := 077
	 fmt.Printf("%d\n",i2)
	 //十六进制
	 i3:= 0x123
	 fmt.Printf("%d\n",i3)

	 fmt.Printf("%T\n",i1)

	 //声明一个int8类型的 要明确指定类型，都则就是int类型
	 i4:= int8(9)
	 fmt.Println(i4)
}
```

浮点型

```go
package main

import "fmt"

//float
func main() {
	//maxFloat32 := math.MaxFloat32 最大值
	f1:=1.23
	//默认go语言中的小数都是float64类型
	fmt.Printf("%T\n",f1)

	//显式声明float32类型
	f2:=float32(1.23)
	fmt.Printf("%T\n",f2)

	f1 = float64(f2) //不能隐式转换

}
```



布尔值

go语言中以bool类型进行声明，只有true和false

注意：

1. 布尔类型变量默认为false
2. go语言中不允许将整型强制转换为布尔型
3. 布尔型无法参与数值运算，也无法与其他类型进行转换

```go
package main

import "fmt"

func main() {
	//布尔值
	b:=true
	var b1 bool = false
	fmt.Printf("%v",b)
	fmt.Println()
	fmt.Printf("%v",b1)
	fmt.Println()
	fmt.Printf("Type:%T,Value:%v",b,b)
}

```



复习

```go
package main

import "fmt"

func main() {
	//fmt占位符 %s %d %x %o %b %T %v

	i :=2
	fmt.Printf("%T\t",i)
	fmt.Printf("%v\t",i)
	fmt.Printf("%b\t",i)
	fmt.Printf("%d\t",i)
	fmt.Printf("%o\t",i)
	fmt.Printf("%x\t",i)

	s:="linjianshu"
	fmt.Printf("%s\t",s)
	fmt.Printf("%v\t",s)
	fmt.Printf("%#v\t",s)
}
```



### 字符串

go语言中字符串是用双引号包裹的！

go语言中单引号包裹的是字符！！



```go
//字符串
s:="hello ljs"
//单独的字母、汉字、符号表示一个字符
c1 := 'h'
c2 := '1'
c3 := '啥'
//字节：1字节=8Bit（8个二进制位）
//一个字符 'A' = 1个字节
//一个utf8编码的汉字‘啥’ = 一般占3个字节
```



字符串转义符

Go语言的字符串常见转义符包含回车、换行、单双引号、制表符等

\r \n \t \' \\"  \\\ 

```go
package main

import "fmt"

func main() {
	//fmt占位符 %s %d %x %o %b %T %v

	i :=2
	fmt.Printf("%T\t",i)
	fmt.Printf("%v\t",i)
	fmt.Printf("%b\t",i)
	fmt.Printf("%d\t",i)
	fmt.Printf("%o\t",i)
	fmt.Printf("%x\t",i)

	s:="linjianshu"
	fmt.Printf("%s\t",s)
	fmt.Printf("%v\t",s)
	fmt.Printf("%#v\t",s)
}
```



多行字符串

go语言中要定义一个多行字符串时，就必须使用反引号 字符``

```go
s:= `
	a
	b
	c
`
```



字符串的常用操作

```go
len(str) 求长度
+或者fmt.Strintf  拼接字符串
strings.Split  分割
strings.contains  判断是否包含
strings.HasPrefix, strings.HasSuffx  前缀、后缀判断
strings.Index(), strings.LastIndex  子串出现的位置
strings.Join(a[] string , sep string)  join操作
```



```go
package main

import (
	fmt "fmt"
	"strings"
)

func main() {
	path := "\"C:\\Users\\Sweetie\\Desktop\\车间级MES\""
	fmt.Printf("%s\t" , path)

	s := `
	世情薄
	人情恶
	雨送黄昏花易落
`
	fmt.Printf("%s\r",s)
	s3:=`C:\Users\Sweetie\Desktop\车间级MES`
	fmt.Printf("%s\n",s3)

	//字符串相关操作
	fmt.Printf("%d\n",len(s3))

	//字符串拼接
	name := "ljs"
	world := "shuaibi"
	describtion := name+world
	fmt.Printf("%v\n",describtion)
	describtion1 := fmt.Sprintf("%s%s",name,world)
	fmt.Printf("%s\n",describtion1)

	//分割
	s1 := strings.Split(s3,"\\")
	fmt.Println(s1)
	for i := 0; i < len(s1); i++ {
		fmt.Println(s1[i])
	}

	//包含
	fmt.Println(strings.Contains(describtion, name))
	fmt.Printf(" '%s' Contains '%s' ? result:%v",describtion1,name,strings.Contains(describtion, name))
	fmt.Println()
	//前缀、后缀
	fmt.Println(strings.HasPrefix(describtion, "ljs"))
	fmt.Println(strings.HasSuffix(describtion, "shuaibi"))

	//索引 查找
	s4:="abcdeb"
	fmt.Println(strings.Index(s4,"b"))
	fmt.Println(strings.LastIndex(s4,"b"))

	//拼接
	var sJoin = strings.Join(s1,"+")
	fmt.Println(sJoin)
}
```



byte和rune类型

组成每个字符串的元素叫做‘字符’，可以通过遍历或者单个获取字符串元素获得字符。字符用单引号‘ 包裹起来，如：

var a:='中'

var b:='x'

Go语言的字符有以下两种：

1.uint8类型，或者叫byte型，代表了ascii码的一个字符

2.rune类型，代表一个utf-8字符

当需要处理中文、日文或者其他符合字符时，则需要用到rune类型。rune类型实际是一个int32



Go使用了特殊的rune类型来处理unicode，让基于unicode的文本处理更方便，也可以使用byte型进行默认字符串处理，性能和扩展性都有照顾

因为utf8编码下一个中文汉字由3-4个字节组成，所有我们不能简单的按照字节去遍历一个包含中文的字符串，否则就会出现上面输出中的第一行结果



字符串底层是一个byte数据，所以可以和[]byte 类型相互转换，字符串是不能修改的 字符是由byte字节组成，所以字符串的长度是byte字节的长度 rune类型用来表示utf8字符，一个rune字符由一个或多个byte组成



修改字符串

**要修改字符串，需要先将其转换成[]rune或 []byte ，完成后再转换为string ，都会重新分配内存，并复制字节数组**

注:rune是一个别名 实际上是类型int32 所以 '中'的类型是int32

byte是一个别名 实际上是类型uint8 所以'c'的类型是uint8



类型转换

Go语言中只有强制类型转换，没有隐式类型转换。该语法只能在两个类型之间支持相互转换的时候使用。

强制类型转换的基本语法如下：

T(表达式)

其中，T表示要转换的类型。表达式包括变量、复杂算子和函数返回值等

比如计算直角三角形的斜边长使用math包的sqrt()函数，该函数接收的是float64类型的参数，而变量a和b都是int类型，这个时候就将a和b强制类型转换为float64类型



总结：

go语言的基本类型： int8 int16 int32 int64 uint8 uint16 uint32 uint64 float32 float64 bool string



if语句

```go
package main

import (
	"fmt"
	"strings"
)

func main() {

	//if 条件判断
	age:=19
	if age>18 {
		fmt.Println("性感荷官在线发牌")
	}else {
		fmt.Println("好好学习，以后赌博")
	}

	if age >= 35 && age < 80 {
		fmt.Println("人到中年，不得不服")
	}else if age > 18 {
		fmt.Println("年轻力壮，不怕困难")
	}else {
		fmt.Println("好好学习，少吃点苦")
	}

	if name := "linjianshu"; strings.Contains(name, "lin") {
	fmt.Println("确实确实")
}else {
	fmt.Println("不敢不敢")
	}	
}
```



for range(键值循环)

go语言中可以使用for range 遍历数据、切片、字符串、map及通道channel 通过for range 遍历返回值有以下规律：

1. 数组、切片、字符串返回索引和值
2. map返回键和值
3. 通道channel 只返回通道内的值



### 内容回顾

go安装

gopath

go env

![image-20210726100638960](Go语言学习.assets/image-20210726100638960.png)

gopath/bin 添加到环境变量：go install 命名会把生成的二进制可执行文件拷贝到gopath/bin



#### go 命令

go build 编译go程序

go build -o "xxx.exe" 指定名称

go run main.go 像执行脚本一样执行mai.go

go install 先编译后拷贝

##### go语言文件基础语法

存放go源代码的文件后缀名 .go

文件第一行：package main 声明包名

如果要编译可执行文件，必须要有main包和main函数（入口函数）

单行注释和多行注释

go语言函数外的语句必须以关键字开头

函数内部定义的变量必须使用

##### 变量

3种声明方式：

1. var name string 
2. name:="ljs"
3. var name = "ljs" 函数内部专属

匿名变量（哑元变量）

当有些数据必须用变量接收但是又不使用它时，就可以用`_` 来接收这个值

##### 常量

`const` PI = 3.1415926

`const` UserNotExistErr  = 1000 

`iota` 实现枚举 实际上就是行索引

三个要点：

- const关键字出现时重置为0 
- 每新增一行常量声明，iota累加1

##### 流程控制

if

```go
if 条件 {
    
}
else if 条件{
    
}
else
{
    
}
```

for循环

1. 标准for循环
2. 变种没有i初始
3. 变种没有i限定
4. 变种没有i增量

```go
	for i := 0; i < 10; i++ {
		fmt.Println(i)
	}

	i:=5
	for ; i <10 ; i++ {
		fmt.Println(i)
	}
	fmt.Println(i)

	var i1 = 3
	for i1<10  {
		fmt.Println(i1)
		i1++
	}

	for	{
		fmt.Println("hello world")
		break
	}

	for i, v := range "hello world" {
		fmt.Printf("index:%d\t,value:%c\n",i,v)
	}

	s:="hello world"
	for i, _ := range s {
		fmt.Printf("index:%d\t,value:%c\n",i,s[i])
	}

	//哑元变量，不想用到的都直接给_
	for _, v := range s {
		fmt.Printf("%c\n",v)
	}

	for i := 1; i <10 ; i++ {
		for j := 1; j <=10-i ; j++ {
			fmt.Printf("%d x %d = %d\t" , i , j , i*j)
		}
		fmt.Println()
	}

	for i := 1; i < 10; i++ {
		for j := i; j >0; j-- {
			fmt.Printf("%d x %d = %d\t" , i,j,i*j)
		}
		fmt.Println()
	}
```



### 基本数据类型

整型

​	无符号整型：`uint8` `uint16` `uint32` `uint64`

​	有符号整型：`int8` `int16` `int32` `int64`

​	`uint` `int` 具体是32位还是64位看操作系统

​	`uintptr` 表示指针	

其他进制数

go语言中没办法直接定义二进制数

八进制数 %o

二进制数 %b

十六进制数 %x



浮点型 `float32` `float64` 默认64位，转成32需要强制转换

布尔型 true&false 不能和其他的类型做转换

字符串型 

常用方法

字符串不能修改

复数

complex128和complex64

byte和rune类型

是类型别名 

##### 字符串、字符、字节都是什么

字符串：双引号包裹的是字符串

字符：单引号包裹的是字符，单个字母、日文、韩文、中文、单个符号

字节： 1byte = 8bit

go语言中字符串都是UTF8编码，UTF8编码中一个常用汉字一般占用3个字节 



##### switch 表达式

switch还可以使用表达式，这时候switch语句后买呢不需要再跟判断变量。例如

`fallthrough` 语法可以执行满足条件的case的下一个case，是为了兼容c语言中的case设计的

```go
package main

import (
	"fmt"
)

func main() {
	score:=68
	switch score {
	case 68:
		fmt.Println("及格")
	default:
		fmt.Println("未知")
	}

	//简化代码 作用域问题
	switch  i:=3 ;i{
	case 1:
		fmt.Println("wumingzhi")
	case 2:
		fmt.Println("zhongzhi")
	case 3:
		fmt.Println("damuzhi")
	}

	//同时声明几种情况
	switch i:=10;i{
	case 1, 3, 5, 7, 9:
		fmt.Println("this is 奇数")
	case 2, 4, 6, 8, 10:
		fmt.Println("this is 偶数")
	}

	score1:=68
	switch  {
	case score1>60&&score1<=100:
		fmt.Println("及格")
	case score1<60:
		fmt.Println("挂了呀")
	}
}
```



##### goto表达式

break只能退出当前for语句的循环

```go
package main

import "fmt"

func main() {
	flag:=false
	for i := 0; i < 10; i++ {
		for j := 0; j < 10; j++ {
			if j==2 {
				flag = true
				break
			}
			fmt.Printf("%d-%d\n",i,j)
		}
		if flag {
			break
		}
	}


	//for i := 0; i < 10; i++ {
	//	for j := 0; j < 10; j++ {
	//		if j == 2 {
	//			goto breakTag
	//		}
	//		fmt.Printf("%v-%v\n",i,j)
	//	}
	//}
	//return

	//breakTag:
	//	fmt.Println("结束for循环")
}
```



##### 运算符

go语言内置的运算符有：

1. 算术运算符+ - * / %
2. 关系运算符 
3. 逻辑运算符
4. 位运算符
5. 赋值运算符

##### 关系运算符

==、！= 、> 、 >= 、< 、 <=

##### 逻辑运算符

&& || !

##### 位运算

位运算符对整数在内存中的二进制位进行操作。

& 参与运算的两数各对应的二进制位相与

| 参与运算的两位各对应的二进制位相或

^ 参与运算的两数各对应的二进制位相异或，当两对应的二进制位相异时，结果为1

<< 左移n位就是乘以2的n次方  高位丢弃，低位补0

》》右移n位就是除以2的n次方 a>>b就是a右移b位

```go
package main

import "fmt"

func main() {

	//运算符
	var(
		a=5
		b=2
	)

	//算术运算符
	fmt.Println(a+b)
	fmt.Println(a-b)
	fmt.Println(a*b)
	fmt.Println(a/b)
	fmt.Println(a%b)
	a++ //单独的语句，不能放在=的右边赋值
	b++


	//关系运算符
	fmt.Println(a==b) //go语言是强类型，相同类型的变量才能比较
	fmt.Println(a!=b)
	fmt.Println(a>b)
	fmt.Println(a<b)

	age:=22
	if age > 18 && age < 60 {
		fmt.Println("上班族")
	}else {
		fmt.Println("不用上班")
	}

	if age > 60 || age < 18 {
		fmt.Println("不用上班")
	}else  {
		fmt.Println("上班族")
	}


	//not取反
	b2:=true
	fmt.Println(!b2)

	//位运算：针对的是二进制数
	//5的二进制表示 101
	//2的二进制表示 010
	//按位与
	fmt.Println(101&010)
	fmt.Println(5&2)
	//按位或
	fmt.Println(101|10)
	fmt.Println(5|2)
	//^按位异或
	fmt.Println(101^010)  //这个有点奇怪 这个是109答案？？？
	fmt.Println(5^2)

	//左移右移运算 *2 和 \2
	fmt.Println(5<<2)  //101=>10100
	fmt.Println(1<<10)
	fmt.Println(5>>1) //101=>10

	//注意别溢出了
	m:=int8(1)
	fmt.Println(m<<10)
	fmt.Println(1<<2+1)

	//192.168.1.1
	//权限 文件操作会将位运算实际的应用
	//0644
	//赋值运算符，用来给变量赋值的
	var x int
	x = 10
	fmt.Println(x)
	x+=1
	fmt.Println(x)
	x-=1
	fmt.Println(x)
	x*=2
	fmt.Println(x)
	x/=2
	fmt.Println(x)
	x<<=2
	fmt.Println(x)
	x>>=2
	fmt.Println(x)
	fmt.Printf("%b",x)
	fmt.Println()
	x&=2
	fmt.Println(x)
	fmt.Printf("%b",x)
	x|=2
	x<<=2
	x>>=2
	x^=2
}
```

##### 数组

array数组

数组是同一种数据类型元素的集合。在go语言中，数组从声明时就确定，使用时可以修改数组成员，但是数组大小不可变化。基本语法：

```go
package main

import "fmt"

func main() {
	//数组
	//存放元素的容器
	//必须指定存放的元素的类型和容量（长度）
	//数组的长度是数组类型的一部分 也就是尽管类型一致但是长度不一致也不是同一个数组类型
	var a1 [3]bool
	var a2 [4]bool
	fmt.Printf("a1:type%T, a2:type%T",a1,a2)
	fmt.Println()

	//数组的初始化
	//如果不初始化：默认元素都是零值(布尔值就是false，整型和浮点型都是0，字符串就是“”)
	fmt.Println(a1,a2)
	//1.初始化方式1
	b1 :=[3]bool{true,true,true}
	fmt.Println(b1)
	//2.初始化方式2 根据初始值自动推断数组的长度是多少
	b2 :=[...]int{1,3,4,2,6,2,73,12}
	fmt.Println(b2)
	fmt.Println(len(b2))
	//3.初始化方式3 根据索引初始化
	b3:=[5]int{1,2}
	fmt.Println(b3)
	b3=[5]int{0:1,4:2}
	fmt.Println(b3)

	//数组的遍历
	citys :=[...]string{"北京","上海","深圳"}
	//1.for range
	for _, v := range citys {
		fmt.Println(v)
	}

	for i, _ := range citys {
		fmt.Println(citys[i])
	}

	//2.根据索引遍历
	for i := 0; i < len(citys); i++ {
		fmt.Println(citys[i])
	}

	//多维数组
	c1:=[3][2]int{0:[2]int{2,3},1:[2]int{4,5}}
	fmt.Println(c1)
	c2:=[3][2]int {{1,2},{3,4}}
	fmt.Println(c2)

	//多维数组的遍历
	//var b11:=[2][3]string{{"a","b","c"},{"d","e","f"}}
	//可以这么记 go语言中 实际数组展示使用空格来区分的，但是声明的时候需要用逗号隔开
	for _, v := range c1 {
		fmt.Println(v)
		for _, v1 := range v {
			fmt.Printf("%d ",v1)
		}
		fmt.Println()
	}

	for i := 0; i < len(c2); i++ {
		fmt.Println(c2[i])
		for j := 0; j < len(c2[j]); j++ {
			fmt.Printf("%d ",c2[i][j])
		}
		fmt.Println()
	}

	//数组是值类型
	d1:=[...]int{1,2,3}
	d2:=d1
	d2[0]=100
	fmt.Println(d1)
	fmt.Println(d2)

	//练习
	e:=[...]int{1,3,5,7,8}
	sum:=0
	for _, v := range e {
		sum+=v
	}
	fmt.Println(sum)

	for i, _ := range e {
		for j := i+1; j < len(e); j++ {
			if e[i]+e[j] == 8 {
				fmt.Printf("(%d %d)",i,j)
				break
			}
		}
		fmt.Println()
	}
}
```

数组定义 var 数组变量名 [元素数量]T

[5]int 和 [10]int 是不同的类型

##### 切片

切片slice是一个拥有相同类型元素的可变长度的序列。他是基于数组类型做的一层封装。他非常灵活，支持自动扩容。切片是一个引用类型，他的内部结构包含`地址` 、 `长度` 和 `容量` 。切片一般用于快速地操作一块数据集合。

切片的定义

声明切片类型的基本语法如下：

```go
var name []T 
```

其中，name是变量名字， T是元素类型

##### 切片的容量和长度

切片拥有自己的长度和容量，我们可以通过使用内置的len函数求长度，使用内置的cap函数求切片的容量

##### 基于数组定义切片

由于切片的底层就是一个数组，所以我们可以基于数组定义切片

还支持如下方式

```go
package main

import "fmt"

func main() {
	//切片的定义
	var s1 []int //定义一个存放int类型元素的切片
	var s2 []string
	fmt.Println(s1,s2)
	fmt.Println(s1==nil)
	fmt.Println(s2==nil)
	//初始化
	s1 = []int{1,2,3}
	s2 = []string{"沙河","张江","平山村"}
	fmt.Println(s1,s2)
	fmt.Println(s1==nil)
	fmt.Println(s2==nil)
	//长度和容量
	fmt.Printf("len:%d,cap:%d\n", len(s1), cap(s1))
	fmt.Printf("len:%d,cap:%d\n", len(s2), cap(s2))

	//2.由数组定义切片
	a :=[]int{1,3,5,7,9,11,13}
	fmt.Println(cap(a))
	b :=a[1:4]  //[3 5 7] 左闭右开 基于一个数组进行切割
	fmt.Println(b)
	b1 :=a[:4]  //0-4
	fmt.Println(b1)
	b2 :=a[2:]  //
	fmt.Println(b2)
	b3 :=a[:]
	fmt.Println(b3)

	//切片的长度就是元素的个数，切片的容量就是底层数组从切片第一个元素到最后一个元素的数量
	fmt.Println(len(b),cap(b))
	//3.切片再切片
	b4:=b[1:2] //[5 7] 但是b的容量已经是6了 这时候切的b从第一位切起 那么容量应该是5
	fmt.Println(b4, len(b4), cap(b4))
	fmt.Println(b)
	a[2] = 10
	//这里说明了切片是引用类型，都指向了底层的数组，修改了底层数组，那么上层的切片值肯定会变化
	fmt.Println(b)
	fmt.Println(b4)
}
```

切片指向了一个底层的数组

切片的长度就是它元素的个数

切片的容量是底层数组从切片的第一个元素到最后一个元素的数量

![image-20210729000908993](Go语言学习.assets/image-20210729000908993.png)

![image-20210729000949711](Go语言学习.assets/image-20210729000949711.png)

##### 使用make函数构造切片

我们上面都是基于数组来创建的切片，如果需要动态的创建一个切片，我们就需要使用内置的make函数

```go
make([]T , size ,cap)
```

其中：T：切片的元素类型 size：切片中元素的数量 cap：切片的容量

上面的代码中a的内部存储空间已经分配cap个，但是实际上只是使用了len个，容量并不会影响当前元素的个数，所以len返回使用了几个，cap返回切片的容量

##### 切片的本质

切片就是一个框，框住了一块连续的内存。属于引用类型，真正的数据都是保存在底层数组里的。

##### 切片不能直接比较

切片之间是不能比较的，我们不能使用==操作符来判断两个切片是否含有全部相等元素。切片唯一合法的比较操作是和nil比较。一个nil值的切片并没有底层数组，一个nil值的切片的长度和容量都是0.但是我们不能说一个长度和容量都是0的切片一定是nil

```go
package main

import "fmt"

func main() {
	//make函数创造切片
	s1:=make([]int,3,10)
	fmt.Printf("s1=%v,len(s1)=%d,cap(s1)=%d,s1==nil?:%v\n",s1,len(s1),cap(s1),s1==nil)

	var s2 []int
	fmt.Printf("s2=%v,len(s2)=%d,cap(s2)=%d,s2==nil?:%v\n",s2,len(s2),cap(s2),s2==nil)

	s3:=[]int{}
	fmt.Printf("s3=%v,len(s3)=%d,cap(s3)=%d,s3==nil?:%v\n",s3,len(s3),cap(s3),s3==nil)

	s4:=make([]int,0)
	fmt.Printf("s4=%v,len(s4)=%d,cap(s4)=%d,s4==nil?:%v\n",s4,len(s4),cap(s4),s4==nil)

	//切片的赋值
	s5:=[]int {1,3,5,7}
	s6:=s5 //s5 和 s6都指向了同一个底层数组
	fmt.Println(s5,s6)
	s5[0]=100
	fmt.Println(s5,s6)

	//切片的遍历
	//1.索引遍历
	for i := 0; i < len(s5); i++ {
		fmt.Printf("%d ",s5[i])
	}
	fmt.Println()
	//2.forrange遍历
	for _, v := range s5 {
		fmt.Printf("%d ",v)
	}
}
```

所以要判断一个切片是否是空的，要使用len(s)==0来判断

##### append方法为切片添加元素

go语言的内置函数append可以为切片动态添加元素，每个切片会指向一个底层数组，这个数组能容纳一定数量的元素。当底层数组不能容纳新增的元素时，切片就会自动按照一定的策略进行扩容，此时该切片指向的底层数组就会更换。扩容操作往往发生在append函数调用时。

切片的扩容策略就不说了

```go
package main

import "fmt"

func main() {
	//append 为切片追加元素
	s1:=[]string{"北京","上海","深圳"}
	fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n",s1,len(s1),cap(s1))
	//s1[3] = "广州" //错误的写法 会导致编译错误：索引越界

	//调用append函数必须使用原来的切片变量接收返回值
	s1= append(s1, "广州") //append追加元素 原来的底层数组放不下的时候 go底层就会把底层数组换一个
	//必须用变量接收append的返回值
	fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n",s1,len(s1),cap(s1))
	s1 = append(s1,"杭州","成都")
	fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n",s1, len(s1), cap(s1))
	s2:=[]string{"武汉","西安","苏州"}
	s1 = append(s1,s2...) //...表示拆开
	fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n",s1, len(s1), cap(s1))
}
```



##### 使用copy复制切片

由于切片是引用类型，a和b其实是指向了同一块内存地址，所以如果单纯的赋值的话，修改了b的值的同时a的值也会发生变化

go语言内建的copy函数可以迅速地将一个切片的数据复制到另一个切片空间

```go
copy (destSlice , srcSlice[] T)
```

##### 从切片中删除元素

go语言中并没有删除切片元素的专用方法，我们可以使用切片 本身的特性来删除元素。

```go
package main

import (
	"fmt"
)

func main() {
	a1:=[]int {1,3,5}
	a2:=a1
	var a3=[]int{}  //这样声明没办法复制进去
	var a4 []int	//这样声明也没办法复制进去
	var a5=make([]int,len(a1), cap(a1))
	copy(a3,a1)
	copy(a4,a1)
	copy(a5,a1)
	fmt.Println(a1,a2,a3,a4,a5)

	a1[0] = 100
	fmt.Println(a1,a2,a3,a4,a5)

	//删除第二个元素
	a5 = append(a5[:1],a5[2:]...)
	fmt.Println(a5)
	fmt.Println(cap(a5))


	//验证
	//1.切片不保存具体的值
	//2.切片对应一个底层数组
	//3.底层数组都是占用一块连续的内存
	x1:=[...]int{1,3,5}  //数组
	x2:=x1[:]   //切片 切片指向底层数组
	fmt.Println(x2,len(x2),cap(x2))
	fmt.Printf("%p\n",&x1[0])
	x2 = append(x1[:1],x1[2:]...) //切片截取底层数组 重新定义了底层数组的索引的值
	fmt.Printf("%p\n",&x2[0]) //说明指向的底层数组地址没变 变了的是地址里的值
	fmt.Println(x2)  //切片的索引的值
	fmt.Println(x1)  //被修改后的底层数组的索引和值
}
```

练习

```go
package main

import "fmt"

func main() {
	a1:=[...]int{1,3,5,7,9,11,13,15,17}
	a2:=a1[:]

	a2=append(a1[:1],a1[2:]...)
	fmt.Println(a2)
	fmt.Println(a1)
}
```

#### 指针

go语言中不存在指针操作，只需要记住两个符号

1. `&` 取地址
2. `*` 根据地址取值

go语言中的指针不能进行偏移和运算，是安全指针。

要搞明白go语言中的指针需要先知道3个概念，指针地址，指针类型和指针取值

go语言中的函数传参都是值拷贝，当我们想要修改某个变量的时候，我们可以创建一个指向该变量地址的指针变量。传递数据使用指针，而无需拷贝数据。类型指针不能进行偏移和运算。go语言中的指针操作非常简单，只需要记住两个符号：& 取地址 *根据地址取值

##### 指针地址和指针类型

每个变量在运行时都拥有一个地址，这个地址代表变量在内存中的位置。go语言中使用&字符放在变量前面对变量进行取地址操作。go语言中的值类型int / float / bool / string / array / struct 都有对应的指针类型 *int / *int64 / *string 

总结：取地址操作符& 和取值操作符*是一对互补操作，&取出地址， *根据地址取出地址指向的值，变量、指针地址、指针变量、取地址、取值的相互关系如下

- 对变量进行取地址&操作，可以获得这个变量的指针变量
- 指针变量的值是指针地址
- 对指针变量进行取值*操作，可以获得指针变量指向的原变量的值

```go
package main

import "fmt"

func main() {
   //1.&取地址
   //2.*根据地址取值
   n:=18
   fmt.Println(&n)
   p:=&n
   fmt.Printf("%T\n",p)  //*int表示int类型的指针
   m:=*p
   fmt.Printf("%v\n",m)
   fmt.Printf("%T\n",m)

   var a *int
   fmt.Println(a)  //nil 赋值会报错 空指针异常
   var a1 = new(int)  //使用new关键字会分配内存块 不会造成空指针
   fmt.Println(a1)
   fmt.Println(*a1)
   *a1 = 100
   fmt.Println(*a1)
}
```

##### make

make也是用于内存分配的，区别于new，它只用于slice、map以及chan的内存创建，而且它返回的类型就是这三个类型本身，而不是她们的指针类型，因为这三种类型就是引用类型，没有必要返回她们的指针了。make函数的函数签名

```go
func make (t Type,size ... IntergerType) Type
```

make函数是无可替代的，我们在使用slice、map以及channel的时候，都需要使用make进行初始化，然后才可以对她们进行操作。这个我们在上一章中都有说明，关于channel我们会在后续的章节中详细说明

##### make和new的区别

1. make和new都是用来申请内存的
2. new很少用，一般用来给基本数据类型申请内存，string / int 返回的是对应类型的指针，例如*string . *int。
3. make是用来给slice  、 map 、 chan申请内存的，make函数返回的是对应的这三个类型本身

#### map

go语言中提供的映射关系容器为map，其内部使用散列表hash实现

map是一种无序的基于key-value的数据结构，go语言中的map是引用类型，必须初始化才能使用

```go
map[KeyType]valueType
```

map类型的变量默认初始值为nil，需要使用make函数来分配内存

```go
make(map[keyType] valueType,[cap])
```

#####  判断某个键是否存在

特殊写法

```go
value,ok:=map[key] 
```

遍历map 使用for range即可

##### 使用delete函数删除键值对

类型为map的切片

值的类型为切片的map

```go
package main
import "fmt"

func main() {
	//map和slice的组合
	a:=[]map[string]int{}
	//元素类型为map的切片
	var a1 = make([]map[string]int,10,10)
	//没有对内部的map做初始化
	a1[0] = make(map[string]int,10)
	a1[0]["ljs"] = 9
	a1[0]["jwt"] = 8
	fmt.Println(a)
	fmt.Println(a1)

	//值为切片类型的map
	var a2 = make(map[string][]string,10)
	a2["ljs"] = make([]string,10,10)
	a2["ljs"] = []string{"giegie"}
	fmt.Println(a2)
	a2["ljs"] = append(a2["ljs"],[]string{"jiejie","didi"}...)
	fmt.Println(a2)
}
```

#### 内容回顾

##### 运算符

算术运算符

逻辑运算符

赋值运算符+= -= *= /= &= |= ^=

位运算符 >> << | & ^

比较运算符

##### 数组array

[...]int{3,5} 数组包含元素的类型和元素的个数 数组的长度属于数组类型的一部分

数组是值类型

多维数组

```go
package main

import "fmt"

func main() {
	var name string
	name = "ljs"
	fmt.Println(name)
	var ages [30]int
	ages[0] = 1
	ages = [30]int{2,3,5}
	fmt.Println(ages)
	ages1:=[...]int{2,3,6,8,9}
	fmt.Println(ages1)
	ages2:=[...]int{1:1,99:99}
	fmt.Println(ages2)

	//二维数组
	a:=[3][2]string{}
	a[0][1] = "ljs"
	a[0][0] = "jwt"
	fmt.Println(a)

	//多维数组是值类型
	a1:=[3][2]string{{"ljs","jwt"},{"fyz","lje"}}
	fmt.Println(a1)

	var a2 =[3][2]int{[2]int{1,2},[2]int{3,4}}
	fmt.Println(a2)

	//数组是值类型
	a3:=[3]int{1,2,3}
	fmt.Println(a3)
	f1(a3)
	fmt.Println(a3)

	a4:=[]int{1,2,3}
	fmt.Println(a4)
	f2(a4)
	fmt.Println(a4)
}
func f1(a [3]int)  {
	//go语言中函数传递的都是值 ctrl+c ctrl+v 
	a[1] = 100
}

func f2(a []int) {
	a[1] =100
}
```

##### 切片

切片不存值，像一个框，在底层的数组里取值

切片的定义：指针、长度、容量

var name []T 

切片的扩容策略

1. 如果申请的容量大于原来的2倍，那就直接扩容至新申请的容量
2. 如果小于1024，那么就直接两倍
3. 如果大于1024，就按照1.25倍去扩容
4. 具体存储的值类型不同，扩容策略也有一定的不同

```go
	a4:=[]int{1,2,3}
	fmt.Println(a4)
	f2(a4)
	fmt.Println(a4)

	//切片
	a5:=[]int{}
	fmt.Println(a5)
	fmt.Println(a5==nil)
	//没有分配内存 零切片声明 nil
	var a6 []int
	fmt.Println(a6)
	fmt.Println(a6==nil)
	//make初始化 分配内存
	a7 := make([]int, 5, 5)
	fmt.Println(a7)
	fmt.Println(a7==nil)

	s1 :=[]int{1,2,3}
	s2:=s1
	fmt.Println(s1)
	s2[1] = 100
	fmt.Println(s2)
	fmt.Println(s1) //切片不存值 指向同一个数组

	var s3 []int
	//append将自动初始化分配内存+扩容
	s3 = append(s3,1)
	fmt.Println(s3)

	var s4 []int
	s4 = make([]int,1,1)
	copy(s4,s3) //copy函数必须先将dest切片声明好并且初始化好分配好内存和长度
	fmt.Println(s4)
```

#####  指针

```go
	//指针
	//go里面的指针只能读不能修改
	addr:="沙河"
	addrpointer:=&addr
	fmt.Println(addrpointer)
	fmt.Printf("%T\n",addrpointer)
	fmt.Printf(*addrpointer)
```

##### map

map存储的是键值对的数据。他也是需要申请内存的

```go
//map
	var m map[string]int
	m = make(map[string]int,5)
	m["ljs"] = 99
	m["jwt"] = 98
	fmt.Println(m)
	fmt.Println(m["jiwuming"]) //如果不存在key ，返回的将是value类型的默认值
	score,ok:=m["jiwuming"]
	if ok {
		println(score)
	}else{
		println("查无此人")
	}

	delete(m,"lalala")  //如果没有的话，什么都不干，不报错
	delete(m, "jwt")
	fmt.Println(m)
```

##### 复习

```go
package main

import (
	"fmt"
	"strings"
	"unicode"
)

func main() {
	s1:="hello沙河"
	sum:=0
	for _, v := range s1 {
		//if v >= 128 {
		//	sum++
		//}

		if unicode.In(v, unicode.Han) {
			sum++
		}
	}
	fmt.Println(sum)

	s2:="how do you do"
	s3:= strings.Split(s2," ")
	fmt.Println(s3)

	m:= make(map[string]int, 5)
	for _, v := range s3 {
		//if m[v] == 0 {
		//	m[v] =1
		//}	else {
		//	m[v] ++
		//}
		if _,ok := m[v];!ok{
			m[v]=1
		}else {
			m[v]++
		}
	}
	fmt.Println(m)

	//回文判断
	//字符串从左往右读和从右往左读是一样的，就是回文
	//黄山落叶松叶落山黄
	s4:="黄山落叶松叶落山黄"
	s5:= make([]string, len(s4))
	for i, v:= range s4 {
		s5[len(s4)-i-1]=string(v)
		//fmt.Println(i, string(v))
		fmt.Println(s5)
	}
	var s6 string
	s6 = strings.Join(s5,"")
	fmt.Println(s6)
	fmt.Println(s6==s4)

	runes:= make([]rune, 0, len(s4))
	for _, rune := range s4 {
		runes =append(runes, rune)
	}
	fmt.Println("rune[] :",runes)
	for i := 0; i < len(runes)/2; i++ {
		if runes[i]!=runes[len(runes)-i-1] {
			return
		}
	}
	println("回文")
}
```

##### 函数func

```go
package main

import "fmt"

func main() {
   println(f4(1, 2, 3, 4))
}

func f1() {
   fmt.Println("hello 沙河")
}

func f2(name string) {
   fmt.Println("hello",name)
}

func f3(x, y int) int {
   return x+y  //y是一个可变长度的切片类型
}

func f4(x int, y ...int) int {
   sum:=x
   for _, v := range y {
      sum+=v
   }
   return sum
}

func f5(x, y int) (sum int) {
   sum = x+y
   return 
}

func f6(x, y int) (x1, y1 int) {
   x1=x
   y1=y
   return
}
```

##### defer语句

go语言中的defer语句会将其后面跟随的语句进行延迟处理，在defer归属的函数即将返回时，将延迟处理的语句按照defer定义的逆序进行执行，也就是说先被defer的语句最后被执行，后被defer的语句最先被执行

##### defer执行时机

在go语言的函数中，return语句在底层并不是原子性操作，他分为给返回值赋值和ret指令两步。而defer语句执行的实际就是在返回值赋值操作后，ret指令执行前，具体如图

![image-20210731151015069](Go语言学习.assets/image-20210731151015069.png)

```go
package main

import "fmt"

//go语言中的函数的return不是原子操作，在底层是分为两步来执行
//第一步：返回值赋值
//第二步：真正的return返回
//函数中如果存在defer，那么defer执行的时机是在第一步和第二步之间
func main() {
	fmt.Println(f1())  //5
	fmt.Println(f2())  //6
	fmt.Println(f3())  //5
	fmt.Println(f3_1())  //[100 2]
}

func f1() int {
	x :=5
	defer func() {
		x++  //修改的是x不是返回值
	}()
	return x
}

func f2() (x int) {
	defer func() {
		x++
	}()
	return 5  //返回值是x x又++了 所以返回6
}

func f3() (y int) {
	x:=5
	defer func() {
		x++  //是因为int是值类型 所以y是拷贝值而不是拷贝地址的原因吗
	}()
	return x
}

func f3_1() (y []int) {
	x:=[]int{1,2}
	defer func() {
		x[0]=100   //因为[]int 切片是引用类型 所以y拷贝的是地址而不是值
	}()
	return x
}

func f4() (x int) {
	defer func(x int) {
		x++  //改变的是函数的副本
	}(x)  //(x)代表的是传入参数
	return 5
}
```

### 变量

##### 全局变量

##### 局部变量

局部变量又分为两种，函数内定义的变量无法在该函数外使用

如果局部变量和全局变量重名，优先访问局部变量

##### 语句块作用域

#### 函数类型和变量

我们可以使用type关键字来定义一个函数类型

```go
type calculation func(int,int) int
```

定义了一个函数类型，这种函数接收两个int类型的参数并且返回一个int类型的返回值

```go
package main

import "fmt"

func main() {
	fmt.Printf("%T \n",f1)
	fmt.Printf("%T \n",f2)
	fmt.Printf("%T \n",f3)
	f3(f2)

	a := f4(f2)
	fmt.Printf("%T\n",a)
}

func f1() {
	fmt.Println("hello 沙河")
}

func f2() int {
	return 5
}
//函数也可以作为参数的类型
func f3(x func() int) {
	fmt.Println(x())
}

//函数还可以作为返回值的类型
func f4(x func() int)  func(int,int) int {
	return f5
}

func f5(x, y int) int {
	return x+y
}
```

### 今日内容

#### 函数

##### 函数的定义

##### 基本格式

参数的格式

有参数的函数

参数类型简写

可变参数

##### 返回值的格式

有返回值

无返回值

命名返回值

##### 变量的作用域

1. 全局作用域
2. 函数作用域
   1. 先在函数内部找变量，找不到往外层找
   2. 函数内部的变量，外部访问不到
3. 代码块作用域

##### 高阶函数

函数也是一种类型，它可以作为一种参数，也可以作为返回值

##### 匿名函数

没有名字的函数

```go
package main

import "fmt"

func main() {
   println(a(10))
   //但是通常匿名函数不是这么用的 通常是由于函数内部不允许定义函数，所以使用匿名函数现写现用
   a:= func(x,y int) int {
      return x+y
   }
   println(a(10, 20))
   //如果只是调用一次的函数，还可以简写成立即执行函数
   i := func(x, y int) int {
      return x * y
   }(10, 20)
   fmt.Println(i)
}

var a = func (x int) int {
   return x
}
```

##### 闭包

```go
package main

import "fmt"

func main() {
	f1(f3(1,2))
	f1(f4(1, 2))
	f1(f5(f2,1,2))
}

func f1(f func()) {
	fmt.Println("this is f1")
	f()
}

func f2(x, y int) {
	fmt.Println("this is f2")
	fmt.Println(x+y)
}

//如何让f1调用的时候执行f2 也就是两个同事写的代码相互兼容
//由于f1的形参是一个无形参无返回值的函数类型，因此需要构造一个函数，让其返回值是无形参无返回值的函数类型f3
//当然为了兼容f2，f3的形参需要和f2的形参相匹配，这样一来在执行f3的时候，内部调用了f2，并且返回类型满足f1所需
func f3(x,y int) func() {
	 func(x,y int)  {
		 f2(x,y)
	}(x,y)
	return func() {
	}
}

func f4(x, y int) func() {
	return func() {
		f2(x,y)
	}
}

func f5(f func(int, int), x, y int) func() {
	//把原来需要传递两个int类型的参数包装成一个不需要传参的函数
	return func() {
		f(x,y)
	}
}
```

闭包=函数 + 外部变量的引用

```go
package main

import "fmt"

func main() {
	//闭包是什么
	//闭包是一个函数，这个函数包含了他外部作用域的一个变量
	//底层
	//1.函数可以作为返回值
	//2.函数内部查找变量的顺序，先在自己内部找，找不到往外层找
	ret := adder(100)
	i:= ret(200)
	fmt.Println(i)
}

func adder(x int) func(int) int {
	return func(y int) int {
		x +=y
		return x
	}
}
```

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	suffixFunc:= makeSuffixFunc(".jpg")
	f := makeSuffixFunc(".txt")
	fmt.Println(suffixFunc("text"))
	fmt.Println(f("text"))
}

func makeSuffixFunc(suffix string) func(string2 string) string{
	return func(name string) string {
		if !strings.HasSuffix(name, suffix) {
			return name+suffix
		}
		return name
	}
}
```

```go
package main

import "fmt"

func main() {
	f, f2 := calc(10)
	fmt.Println(f(1),f2(2))   //11 9
	fmt.Println(f(3),f2(4))	  //12 8
	fmt.Println(f(5),f2(6))	  //13 7

}

func calc(base int) (func(int)int ,func(int)int) {
	add :=func(i int)int{
		base+=i
		return base
	}
	sub := func(i int)int{
		base-=i
		return base
	}
	return add,sub

}
```

##### defer进阶

```go
package main

import (
	"fmt"
)

func main() {
	a:=1
	b:=2
	defer calc("1",a,calc("10",a,b))
	a=0
	defer calc("2",a,calc("20",a,b))
	b=1
	//defer会先把预定的值先算出来等着最后执行函数
	//defer calc("1",1,calc("10",1,2))
	//输出 "10" 1 2 3
	//defer calc("1",1,3)
	//a=0
	//defer calc("2",1,calc("20",0,2))
	//输出 "20" 0 2 2
	//defer calc("2",0,2)
	//b=1
	//程序退出
	//执行 defer calc("2",0,2)
	//输出 "2" 0 2 2
	//执行 defer calc("1",1,3)
	//输出 "1" 1 3 4
}

func calc(index string, a, b int) int {
	ret :=a+b
	fmt.Println(index,a,b,ret)
	return ret
}
```

##### 内置函数介绍

close 主要用来关闭channel

len 用来求长度 string array slice map channel

new 用来分配内存，主要用来分配值类型，比如int struct 返回的是指针

make 用来分配内存，主要用来分配引用类型，比如chan map slice 

append 用来追加元素到数组 slice中

panic和recover 用来做错误处理

##### panic/recover

go语言中目前是没有异常机制的，但是使用panic/recover模式来处理错误。panic可以在任何地方引发，但recover只有在defer调用的函数中有效。



程序运行期间funcB如果引发了panic导致的程序崩溃，异常退出了。这个时候我们就可以通过recover将程序恢复回来，继续往后执行。

```go
package main

import "fmt"

func main() {
	A()
	B()
	C()
}

func A() {
	fmt.Println("A")
}
func B() {
	//假设此时打开了个数据库连接
	defer func() {
		error := recover()
		fmt.Println(error)
		fmt.Println("要尝试在出错的时候释放数据库连接...")
	}()
	panic("fatal error!")  //程序奔溃退出
	fmt.Println("B")
}
func C() {
	fmt.Println("C")
}
```

注意：

1. recover必须搭配defer使用
2. defer一定要在可能引发panic的语句之前定义



#### go语言fmt.printf使用指南

##### fmt

fmt包实现了类似C语言printf和scanf的格式化I/O 主要分为向外输出内容和获取输入内容两大部分

##### 向外输出

print 直接输出

println输出带换行符

printf格式化输出

| 占位符 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| %v     | 值的默认格式                                                 |
| %+v    | 类似%v,但输出结构体时会添加字段名                            |
| %#v    | 值的go语法表示                                               |
| %T     | 打印值的类型                                                 |
| %%     | 百分号                                                       |
| %t     | 布尔值                                                       |
| %b     | 对于整型而言，是二进制数，对于浮点数而言，是二进制指数的科学计数法 |
| %c     |                                                              |
| %d     |                                                              |
| %o     |                                                              |
| %x     |                                                              |
| %X     |                                                              |
| %U     |                                                              |
| %q     |                                                              |
| %e     | 科学计数法                                                   |
| %E     | 科学计数法                                                   |
| %f     |                                                              |
| %F     |                                                              |
| %g     | 根据实际情况采用%e或%f格式（以获得更简洁、准确的输出）       |
| %G     |                                                              |
| %s     |                                                              |
| %q     |                                                              |
| %x     | 每个字节用两字符十六进制数表示                               |
| %9f    | 宽度9，默认精度                                              |
| %9.2f  | 宽度9，精度2                                                 |
| %5.2s  | 一共5个 保留2个                                              |
| %-5s   | 有空格补在前面                                               |

##### 获取输入

fmt.scan fmt.scanf fmt.scanln

- scan从标准输入扫描文本，读取由空白符分割的值保存到传递给本函数的参数中，换行符视为空白符
- 本函数返回成功扫描的数据个数和遇到的任何错误，如果读取的数据个数比提供的参数少，会返回一个错误报告原因

sprint

sprint系列函数会把传入的数据生成并返回一个字符串

```go
package main

import "fmt"

func main() {
	fmt.Print("hello world")
	fmt.Println("hello world")
	fmt.Printf("%p","helloworld")

	//%d 十进制
	//%v 值
	//%o 八进制
	//%x 十六进制
	//%T 类型
	//%s 字符串
	//%p 指针
	//%b 二进制
	//%c 字符s
	//%f 浮点数
	//%t 布尔值
	fmt.Println()
	var m map[string]int
	m= make(map[string]int)
	m["ljs"]=98
	fmt.Printf("%v\n",m)
	fmt.Printf("%#v\n",m)

	fmt.Printf("%q\n",65)
	printfPersentage(98)
	fmt.Printf("%b\n",5.6)

	n:=12.34
	fmt.Printf("%f\n",n)
	fmt.Printf("%9f\n",n)
	fmt.Printf("%.2f\n",n)
	fmt.Printf("%9.2f\n",n)
	fmt.Printf("%9.f\n",n)

	s:="小王子"
	fmt.Printf("%s\n",s)
	fmt.Printf("%5s\n",s)
	fmt.Printf("%-5s\n",s)
	fmt.Printf("%5.7s\n",s)
	fmt.Printf("%-5.7s\n",s)
	//一共5个 只留2个
	fmt.Printf("%5.2s\n",s)
	fmt.Printf("%05s\n",s)

	var s1 string
	fmt.Scan(&s1)
	fmt.Println(s1)

	var (
		name string
		age int
		class string
	)
	//fmt.Scanf("%s %d %s\n",&name,&age,&class)
	fmt.Printf("%s %d %s\n",name,age,class)
	fmt.Scanln(&name,&age,&class)
	fmt.Printf("%s %d %s\n",name,age,class)

}

func printfPersentage(a int) {
	fmt.Printf("%d%%\n",a)
}
```

##### 今日难点

1. 函数的定义
2. 高阶函数
3. 函数类型
4. 闭包
5. defer
6. panic/recover

![image-20210802002337782](Go语言学习.assets/image-20210802002337782.png)

#### 结构体 struct

方法

实际上类似于类

#### 内容回顾

函数的定义

func name () 返回值 {}

函数进阶

- ​	高阶函数：函数可以作为参数，也可以作为返回值


- ​	闭包：函数和其外部变量的引用


- ​	defer：延迟调用 多用于处理资源释放


- ​	内置函数：
  - ​		panic/recover

##### 递归

```go
package main

import "fmt"

func main() {
	//递归:自己调用自己
	//递归适合处理那种问题相同但是规模越来越小的场景
	//递归一定要有一个明确的退出条件
	println(Factorial(7))

	fmt.Println(taijie(4))
}

func Factorial(n int) (result int) {
	if n == 1 {
		return 1
	} else{
		result =n * Factorial(n-1)
		return
	}
}

//上台阶面试题
//n个台阶 一次可以走1步 一次可以走2步 有多少种走法
func taijie(n int) (result int) {
	if n == 1 {
		result =1  //如果只有1个台阶就一种走法
		return
	}else if n == 2 {
		return 2
	}
	return taijie(n-1)+taijie(n-2)
}
```

##### 自定义类型和类型别名

在go语言中有一些基本的数据类型，如string bool int float等数据类型，go语言中可以使用type关键字来定义自定义类型

自定义类型是定义了一个全新的类型。我们可以基于内置的基本类型定义，也可以通过struct定义



类型别名规定typealias只是type的别名，本质上是一个类型，这些名字都指向一个类型



区别 ： 自定义类型编译后类型是自定义的 类型别名只会在代码中存在，编译完成只会有原类型

![image-20210806225811170](Go语言学习.assets/image-20210806225811170.png)

```go
package main

import "fmt"

//type后面跟的是类型
type myInt int //自定义类型
type yourInt = int //类型别名

func main() {
	//自定义类型和类型别名
	var n myInt
	n = 100
	fmt.Println(n)
	fmt.Printf("%T\n",n)

	var m yourInt
	m = 100
	fmt.Println(m)
	fmt.Printf("%T\n",m)

	var r rune
	r = '中'
	fmt.Printf("%c\n",r)
	fmt.Printf("%T\n",r)
}
```



#### 结构体

go语言中没有类的概念，也不支持类的继承等面向对象的概念。go语言中通过结构体的内嵌再配合接口比面向对象具有更高的扩展性和灵活性。

go语言中的基础数据类型可以表示一些事务的基本属性，但是当我们想表达一个事务的全部或者部分属性时，这时候再用一些基本数据类型明显就无法满足需求了，go语言提供了一种自定义数据类型，可以封装多个基本数据类型，这种数据类型叫结构体，英文名称struct 也就是我们可以通过struct来定义自己的类型

go语言中通过struct来实现面向对象



##### 结构体的定义

使用type和struct关键字来定义结构体

```go
package main

import "fmt"

//结构体

type person struct {
	name string
	age int
	hobby []string
	gender string
}
func main() {
	//声明一个person类型的变量
	var f person
	//通过字段赋值
	f.gender = "男"
	f.hobby = make([]string,10)
	f.hobby[0] ="football"
	f.hobby[1] ="basketball"
	f.age = 18
	f.name = "ljs"
	fmt.Println(f)
	fmt.Printf("%T\n",f)
	fmt.Println(f.hobby)

	var f1 person
	f1.name = "jwt"
	fmt.Println(f1)
}

	//匿名结构体  多用于临时场景
	s := struct {
		name string
		age  int
	}{age: 18,name: "fyz"}
	fmt.Println(s)

	var s1 = struct {
		name string
		sex  int
	}{sex : 1,name:"lje"}
	fmt.Println(s1)
```

结构体是值类型

##### 在Go语言中只存在值传递（要么是该值的副本，要么是指针的副本），不存在引用传递。之所以对于引用类型的传递可以修改原内容数据，是因为在底层默认使用该引用类型的指针进行传递，但是也是使用指针的副本，依旧是值传递。

![image-20210807001149451](Go语言学习.assets/image-20210807001149451.png)

- 创建指针类型结构体
- 取结构体地址实例化
- 结构体初始化
  - 使用键值对初始化
  - 使用值的列表初始化

```go
package main

import (
	"fmt"
)

type person struct {
	name string
	sex string
}
func main() {
	//结构体是值类型
	p :=person{
		name: "ljs",
		sex: "男",
	}
	fmt.Println(p)

	var p1 person
	p1.name ="lje"
	p1.sex = "nan"

	var p2 person
	p2 = p1
	p2.name ="fyz"
	fmt.Println(p2)
	fmt.Println(p1)

	func(x person){
			x.sex = "女"  //传的是值
	}(p2)
	fmt.Println(p2)

	func(x *person){
		(*x).sex = "nv"  //传的是地址
		//x.sex = "nv"  //语法糖 一样的同上
	}(&p2)
	fmt.Println(p2)

	//创建一个指针类型的person
	var p3 = new (person)   //new 返回的是指针地址 这个类型
	p3.sex = "nan"
	(*p3).name = "www"  //语法糖 一样的同上
	fmt.Println(p3)
	fmt.Printf("%T\n",p3)
	fmt.Printf("%p\n",p3)  //返回的是这个指针的值 p3保存的值就是一个内存地址
	fmt.Printf("%v\n",p3)
	fmt.Printf("%T\n",&p3)
	fmt.Printf("%p\n",&p3)  //返回的是这个指针类型的值的地址


	//key value 初始化
	var p4 =&person{
		name: "lll",
	}
	fmt.Println(p4)

	//使用值 列表的形式初始化 顺序保持一致
	p5:=person{
		 "nv",
		 "slkdjf",
	}
	fmt.Println(p5)
}
```



```go
package main

import "fmt"

func main() {
	var a int
	a = 100
	b := &a
	fmt.Printf("%T %p\n",&a,&a)
	fmt.Printf("%T %p\n",b,b)  //b的值
	fmt.Printf("%T %v\n",b,b)  //b的值
	fmt.Printf("%T %p\n",&b,&b)  //b的内存地址
}
```

##### 结构体的内存布局

占用连续内存

```go
package main

import "fmt"

type x struct {
	a ,b ,c int8
}
func main() {
	//结构体占用一块连续的内存空间
	x :=x{
		a: 10,
		b: 20,
		c: 30,
	}

	fmt.Printf("%p\n",&(x.a))
	fmt.Printf("%p\n",&(x.b))
	fmt.Printf("%p\n",&(x.c))
}
```

结构体是值类型 赋值的时候是拷贝

构造函数：返回一个结构体变量的函数



构造函数和方法

##### 方法和接收者

go语言中的方法method是一种作用于特定类型变量的函数。这种特定类型变量叫做接收者receiver 接收者的概念就类似于其他语言中的this或者self

```go
func (接收者变量 接收者类型) 方法名(参数列表) (返回参数)
{
    函数体
}
```



```go
package main

import "fmt"

//标识符：变量名、函数名、类型名、方法铭
//go语言中如果标识符首字母是大写的，就表示对外部包可见（暴露的，公有的）

//Dog 这是一个狗的结构体注释
type Dog struct {
	name string
}

func newDog(name string) Dog {
	return Dog{
		name: name,
	}
}

type person struct {
	name string
	age int
}

func newPerson(name string, age int) person {
	return person{
		name: name,
		age: age,
	}
}

//方法是作用于特定类型的函数
//接受者表示的是调用该方法的具体类型变量，多用类型变量首字母小写表示
func (d Dog) wangwang() {
	fmt.Println(d.name+"汪汪汪")
}

//使用值接收者：传拷贝进去
func (p person) guonian() {
	p.age++
}

//操作指针 指针接收者：传地址进去
func (p *person) guonian1() {
	(*p).age++
}
func main() {
	newDog("jwt").wangwang()

	p := newPerson("ljs", 18)
	fmt.Println(p.age)
	p.guonian()
	fmt.Println(p.age)

	p1:=newPerson("jwt",19)
	fmt.Println(p1.age)
	p1.guonian1()
	fmt.Println(p1.age)

}
```

##### 什么时候应该使用指针类型接收者

1. 需要修改接收者中的值
2. 接收者是拷贝代价比较大的大对象
3. 保证一致性，如果有某个方法使用了指针接收者，那么其他的方法也应该使用指针接收者

##### 任意类型添加方法

```go
package main

import "fmt"

//给自定义类型添加方法
//不能给别的包里面的类型添加方法，只能给自己的包里的类型添加方法
type myInt  int

func (i myInt) hello()  {
	fmt.Println("this is a int"+(string(i)))
}
func main() {
	var i myInt
	i= 10
	i.hello()

}
```

##### 结构体的匿名字段

```go
package main

import "fmt"

//匿名字段
type person struct {
	string
	int
}
func main() {
	a:=person{
		"ljs",
		10,
	}
	fmt.Println(a.string)
	fmt.Println(a.int)
}
```

##### 结构体嵌套

实际上就是包含关系或者继承嘛感觉

##### 匿名嵌套结构体

匿名嵌套结构体的字段冲突

```go
package main

import "fmt"

type person struct {
   name string
   age int
   addr address
}

type company struct {
   name string
   address  //匿名嵌套结构体 可以直接拿到匿名结构体里面的字段
}

type address struct {
   province string
   city string
}
func main() {
   p1:=person{
      name: "ljs",
      age: 18,
      addr: address{city: "fuzhou",province: "fujian"},
   }
   fmt.Println(p1.addr.province)

   c1:=company{
      name:    "alibaba",
      address: address{province: "zhejiang",city: "hangzhou"},
   }
   fmt.Println(c1.city) //先在自己结构体找这个字段 找不到就去匿名嵌套的结构体中查找该字段
}
```

##### 结构体的“继承”

go语言中使用结构体也可以实现其他编程语言中面向对象的继承

 ```go
 package main
 
 import "fmt"
 
 type animal struct {
 	name string
 }
 
 func (a animal) move() {
 	fmt.Println(string(a.name)+"会动")
 }
 
 type dog struct {
 	feet byte
 	animal
 }
 
 func (d dog) wang() {
 	fmt.Println(d.name+"wangwangwang")
 }
 
 func newDog(a animal, feet byte) dog {
 	return dog{
 		feet,a,
 	}
 }
 
 func newAnimal(name string) animal {
 	return animal{name:name}
 }
 func main() {
 	//结构体模拟实现其他语言中的继承
 	newDog(newAnimal("jwt"),4).wang()
 
 	d1:=dog{
 		 4, animal{name: "ljs"},
 	}
 	d1.move()  //只能匿名嵌套结构体才能实现类似于继承的效果 如果有名字好像就调用不了
 
 
 }
 ```

##### 结构体与json

```go
package main

import (
   "encoding/json"
   "fmt"
)

func main() {
   //结构体与json
   //1.序列化 把go语言中的结构体变量 --> json格式的字符串
   //2.反序列化 把json格式的字符串  --> go语言中能够识别的结构体变量

   p1:=person{
      Name: "ljs",
      Age: 18,
   }

   //序列化
   v,err:=json.Marshal(p1)
   if err != nil {
      fmt.Println("marshal fail ")
      fmt.Println(err)
      fmt.Printf("%v  %T\n",err,err)
      return
   }
   fmt.Println(v)
   fmt.Printf("%v  %T\n",string(v),v)

   //反序列化  传指针进去
   var v1 person
   err1 := json.Unmarshal(v, &v1)
   if err1 != nil {
      fmt.Println(err1)
      return
   }
   fmt.Println(v1)
   fmt.Println(v1.Age)
   fmt.Println(v1.Name)

   s:=`{"name":"ljs","age":18}`
   var v2 person    //传指针进去
   json.Unmarshal([]byte(s),&v2)
   fmt.Printf("%#v\n",v2)

}

type person struct {
   Name string `json:"name" db:"dbname"`
   Age int `json:"age"`
}
```

#### day05内容回顾

##### 自定义类型和类型别名

```go
type myInt int 自定义类型 
type myInt1 = int 类型别名 在编译过程中
```

类型别名只在代码编写过程中有效，编译完之后就不存在，内置的byte和rune都属于类型别名

##### 结构体

基本数据类型 ：表示现实中的物体有局限性

结构体是一种数据类型，一种我们可以自己造的可以保存多个维度的类型

```go
type person struct{
    name string 
    age int 
    addr address
}
```

##### 匿名结构体

多用于了临时场景

##### 结构体的初始化

##### 构造函数

##### 方法和接收者

方法是有接收者的函数，接收者指的是哪个类型的变量可以调用这个函数

##### 接收者可以是指针

结构体是值类型

##### 结构体的嵌套

##### 结构体的匿名字段

##### JSON序列化与反序列化

经常出现的问题

1. 结构体内部的字段要大写 不然别人是访问不到的
2. 反序列化时要传递指针

```go
package main

import (
   "encoding/json"
   "fmt"
)

type temp struct {
   X int `json:"x"`
   Y int `json:"y"`
}
func main() {
   var a = struct {
      x int
      y int
   }{x:2,y: 1}
   fmt.Println(a)

   var a1 temp
   a1.X = 1
   a1.Y = 2

   a2:=temp{
      X: 0,
      Y: 0,
   }
   fmt.Println(a2)

   //调用构造函数
   a3:=newTemp(1,2)
   fmt.Println(a3)

   a3.dream()
   a3.exchange()
   fmt.Println(a3)

   marshal, err := json.Marshal(a3)
   if err != nil {
      fmt.Println(err)
   }
   fmt.Println(string(marshal))

   s1:=`{"x":2,"y":4}`
   var a4 temp
   err1 := json.Unmarshal([]byte(s1), &a4)
   if err1 != nil {
      fmt.Println(err1)
   }
   fmt.Println(a4)
}

//构造函数 返回值是对应的结构体类型
func newTemp(x, y int) temp {
   return temp{
      X: x,
      Y: y,
   }
}

//接收者是用对应类型的首字母小写
//指定接收者之后 只有该类型的变量才有资格调用
func (t temp) dream() {
   fmt.Println("temp也有梦想")
   fmt.Println(t.X+t.Y)
}

//指针接收者
//1.需要修改结构体变量的值时需要使用指针接收者
//2.结构体本身比较大，拷贝的内存开销比较大时也要使用指针接收者
//3.保持一致性：如果有一个方法使用了指针接收者，其他的方法为了统一也要使用指针接收者
func (t *temp) exchange() {
   temp:=t.X
   t.X = t.Y
   t.Y = temp
}

type addr struct {
   city , province string
}

type student struct {
   name string
    addr  //匿名嵌套结构体，就是用类型名字作为名称
}
```

##### 接口interface

接口是一种类型，是一种特殊的类型，他规定了变量有哪些方法

在编程中会遇到一下场景

我不关心一个变量是什么类型，我只关心能调用他的什么方法

```go
package main

import "fmt"

//引出接口的实例

type cat struct {

}

type dog struct {

}

func (c cat) speak() {
   fmt.Println("miaomiaomiao~")
}

func (d dog) speak() {
   fmt.Println("wangwangwang~")
}

type speaker interface {
   speak()  //只要实现了speak方法的变量都是speaker类型
}

func fuck(a speaker) {
   a.speak()
}

func main() {
   c:=cat{}
   d:=dog{}
   fuck(c)
   fuck(d)

   var ss1 speaker  //定义一个接口类型 ：speaker的变量
   ss1=d
   ss1.speak()

   ss:=speaker(c)
   ss.speak()
}
```

##### 接口的定义

```go
type name interface{
    methodname(参数1，参数2) (返回值1，返回值2)
    ...
}
```

用来给变量/参数/返回值 等设置类型

##### 接口的实现

一个变量如果实现了接口中规定的所有的方法，那么这个变量就实现了这个接口，可以理解称为接口类型的变量。 

![image-20210808151410287](Go语言学习.assets/image-20210808151410287.png)

![image-20210808151514714](Go语言学习.assets/image-20210808151514714.png)

##### 接口类型的变量

接口类型变量能够存储所有实现了该接口的实例

##### 值接收者和指针接收者实现接口的区别

前者可以传值，也可以传指针

后者只能传指针

```go
package main

import (
   "fmt"
)

//使用值接收者和指针接收者的区别
type animal interface {
   move()
   eat(string)
}

type cat struct {
   name string
   feet int
}

////使用值接收者实现了接口的所有方法
//func (c cat) move() {
// fmt.Println("走猫步")
//}
//
//func (c cat) eat(a string) {
// fmt.Println("猫吃"+a)
//}

//使用指针接收者实现了接口的所有方法
func (c *cat) move() {
   fmt.Println("走猫步")
}

func (c *cat) eat(a string) {
   fmt.Println("猫吃"+a)
}

func main() {
   var a1 animal
   c1:=cat{
      name: "tom",
      feet: 4,
   }
   c2:=&cat{
      name: "假老练",
      feet: 4,
   }

   a1=&c1
   fmt.Println(a1)
   a1.eat("bianbian")

   a1=c2
   fmt.Println(a1)
   a1.eat("大便便")

}
```

##### 类型与接口的关系

多个类型可以实现同一个接口

一个类型可以实现多个接口

接口可以嵌套接口

```go
package main

import "fmt"


//接口还可以嵌套
type animal interface {
   mover
   eater
}

//同一个结构体可以实现多个接口
type mover interface {
   move()
}

type eater interface {
   eat(string)
}

type cat struct {
   name string
   feet byte
}

//一个结构体可以实现多个接口
func (c *cat) move() {
   fmt.Println(c.name+" is moving")
}

func (c *cat) eat(something string) {
   fmt.Println(c.name+" is eating "+something)
}
func main() {
   c1:=cat{
      name: "tom",
      feet: 4,
   }
   mover.move(&c1)
   eater.eat(&c1,"猫粮")
}
```

##### 空接口

```go
type xxx interface{
    
}
```

```go
interface{}  //既然是空接口 那就不需要名字了
```

所有的类型都实现了空接口这种类型，也就是任意类型的变量都能保存到空接口中。

空接口的应用

- 作为函数的参数
- 作为map的值

```go
package main

import "fmt"

//空接口
func main() {
   m1 := make(map[interface{}]interface{},10)
   m1[1]="hello world"
   m1["hello world"] = 1
   m1[false] =[...]string{"1","2","3"}
   m1[[...]int{1,2}]=[]bool{true,false}
   fmt.Println(m1)

   show(m1)
}

func show(a interface{}) {
   fmt.Printf("%T  %v\n",a,a)
}
```

##### 类型断言

```go
package main

import (
   "fmt"
)

//类型断言
func main() {
   assert("100")
   assert(float32(32.1))
}

func assert(a interface{}) {
   fmt.Printf("%T %v\n",a,a)
   s,ok := a.(string)  //类型断言
   if !ok {
      fmt.Println("error ")
      return
   }
   fmt.Println(s)

   switch i:=a.(type) {
   case string:
      fmt.Printf("this is a string %T %v\n",i,i)
   case int:
      fmt.Printf("this is a int %T %v\n",i,i)
   case bool:
      fmt.Printf("this is a bool %T %v\n",i,i)
   case float64,float32:
      fmt.Printf("this is a float %T %v\n",i,i)

   }
}
```

##### 接口的注意事项

只有当有两个或两个以上的具体类型必须以相同的方式进行处理时才需要定义接口。不要为了接口而写接口，那样只会增加不必要的抽象，导致不必要的运行时消耗

##### 包package

包是多个go源码的集合，是一种高级的代码复用方案，go语言为我们提供了很多内置包，如fmt、os、io等

定义包

```go
package 包名
```

注意：

- 一个文件夹下只能有一个包，同样一个包的文件不能在多个文件夹下
- 包名可以不和文件夹的名字一样，包名不能包含符号 - 
- 包名为main的包为程序的入口包，编译时不包含main包的源代码是不会得到可执行文件的



##### 包的导入

- import导入语句通常放在文件开头包声明语句的下面
- 导入的包名需要使用双引号包裹起来
- 包名是从 $gopath/src/后开始计算的 ， 使用 / 路径进行分割
- go语言禁止循环导入包

单行导入 、 多行导入、自定义导入、匿名导入包 _

##### init()初始化函数

在go语言程序执行时导入包语句会自动触发包内部init（）函数的调用 

init()函数没有参数也咩有返回值 init()函数在程序运行时自动被调用执行 不能在代码中主动调用它

![image-20210808175802083](Go语言学习.assets/image-20210808175802083.png)

![image-20210808175917585](Go语言学习.assets/image-20210808175917585.png)

##### 文件操作

自己写一个日志库

接口：用处？日志可以输出到终端，可以输出到文件，输出到卡夫卡

文件操作



##### 打开和关闭文件

os.Open函数能够打开一个文件 返回一个*File 和一个err ，对得到的文件实例调用close()方法能够关闭文件

为了防止文件忘记关闭 我们通常使用defer注册文件关闭语句

##### file.Read()

##### bufio读取文件

##### ioutil读取整个文件

##### 文件写入操作

os.openfile()函数能够以指定模式打开文件，从而实现文件写入相关功能

```go
func OpenFile(name string , flag int , perm FileMode) (*File,error){
    
}
```

flag是文件打开的模式

- os.O_WRONLY
- os.O_CREATE
- os.O_RDONLY
- os.O_RDWR
- os.O_TURNC
- os.O_APPEND

perm：文件权限，一个八进制数。r读 o4 w写 o2 x执行 o1

file.write

file.writestring

```go
writer:= bufio.NewWriter(file)
```

```
ioutil.WriteFile
```

```go
package main

import (
	"bufio"
	"fmt"
	"io"
	"io/ioutil"
	"os"
)

func readFromFile1() {
	fileObj,err:=os.Open("./main.go")
	if err != nil {
		fmt.Println("open file failed...")
		return
	}

	//记得关闭文件
	defer fileObj.Close()
	var b =make([]byte,128)
	for {
		n,err:=fileObj.Read(b)
		if err == io.EOF {
			fmt.Println("读完了")
			return
		}
		if err != nil {
			fmt.Println("read from file failed , error")
			return
		}
		fmt.Println(n)
		fmt.Println(string(b))
		if n <128 {
			return
		}
	}
}

//利用bufio这个包读取文件
func readFromFileByBufio()  {
	fileObjFile,err :=os.Open("./main.go")
	if err != nil {
		fmt.Printf("err, %v",err)
		return
	}
	defer fileObjFile.Close()

	reader:=bufio.NewReader(fileObjFile)
	for {
		string,err:=reader.ReadString('\n')
		if err==io.EOF {
			return
		}
		if err != nil {
			fmt.Printf("read line failed , err : %v",err)
			return
		}
		fmt.Print(string)
	}
}

func readFromFileByIoutil() {
	file, err := ioutil.ReadFile("./main.go")
	if err != nil {
		fmt.Printf("err , cause: %v\n",err)
	}
	fmt.Println(string(file))
}


//打开文件
func main() {
	//readFromFile1()
	//readFromFileByBufio()
	readFromFileByIoutil()
}
```



```go
package main

import (
	"bufio"
	"fmt"
	"io/ioutil"
	"os"
)

func write() {
	fileObj , err :=os.OpenFile("./xx.txt",os.O_WRONLY|os.O_CREATE|os.O_TRUNC,0644)
	if err != nil {
		fmt.Printf("err cause: %v\n",err)
		return
	}

	//write
	fileObj.Write([]byte{97,98,99})
	fileObj.Write([]byte("this is a b c "))
	fileObj.WriteString("hello world!")
	defer fileObj.Close()
}

func writeByBufIo() {
	file, err := os.OpenFile("./xx.txt", os.O_WRONLY|os.O_CREATE|os.O_TRUNC, 0644)
	if err != nil {
		fmt.Printf("err cause : %v\n",err)
		return
	}

	writer:= bufio.NewWriter(file)
	writer.WriteString("comeon baby!")   //bufio是做了一个缓存
	writer.Flush()
	defer file.Close()
}

func writeByIoutil()  {
	str:="hello 北京"
	err := ioutil.WriteFile("./xx.txt", []byte(str), 0666)
	if err != nil {
		fmt.Printf("error cause : %v\n",err)
		return
	}
}
func main() {
	//write()
	//writeByBufIo()
	writeByIoutil()
	
}
```

拷贝文件 可以借助io.copy()实现一个拷贝文件函数

```go
package main

import (
	"io/ioutil"
)

func main() {
	copyFile("./xxcopy.txt","./xx.txt")
}

func copyFile(dstName,srcName string) (written int64,err error) {
	//以读的方式打开文件
	//file, err := os.OpenFile(srcName, os.O_RDONLY, 0644)
	//if err != nil {
	//	return 0, err
	//}
	//reader:= bufio.NewReader(file)
	readFile, err := ioutil.ReadFile(srcName)
	if err != nil {
		return 0, err
	}

	err1 := ioutil.WriteFile(dstName, readFile, 0644)
	if err1 != nil {
		return 0, err1
	}

	return 1,nil

}
```

通过文件操作获取终端输入

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	//useScan()
	ioscan()
}

func useScan() {
	fmt.Println("请输入内容！")
	var s string
	fmt.Scanln(&s)
	fmt.Printf("你输入的内容是 %v\n",s)
}

func ioscan() {
	fmt.Println("请输入内容！")
	var s string
	reader := bufio.NewReader(os.Stdin)
	s,_=reader.ReadString('\n')
	fmt.Println(s)
}
```

##### 日志库作业

需求：

1. 可以往不同的输出位置记录日志
2. 日志可以分为五种级别

#### 内容回顾

##### 包

包的定义 package，包名通常是和目录名一致，不能包含-

- 一个文件夹就是一个包
- 文件夹里面放的都是.go文件

包的导入 import

- ​	单行导入 和 多行导入
- ​    包导入路径是从gopath\src后面的路径开始写起
- ​    给导入的包起别名
- 匿名导入 ---> sql包导入时会讲
- 不支持循环导入

包中标识符(变量名、函数名、结构体、接口、常量...) 可见性 标识符首字母大写

`init()` 

- 包导入的时候会自动执行
- 一个包里只有一个init()
- init()没有参数也没有返回值也不能调用他
- 多个包的init执行顺序
- 一般用于初始化操作...

##### 接口

接口是一种类型，一种抽象的类型

接口就是你要实现的方法的清单

##### 接口的定义

```go
type mover interface{
    方法签名(参数)(返回值)
}
```

##### 接口的实现

实现了接口的所有方法就实现了这个接口

实现了接口就可以当成这个接口类型的变量

##### 接口的变量

实现了一个变量，可以保存所有实现了我这个接口类型的值

通常作为函数的参数出现

##### 空接口

接口中没有定义任何方法，也就是所任意类型都实现了空接口==>任何类型的变量都可以存到这个空接口变量中 

```go
interface {}
```

作为函数参数fmt.println()

map[string]interface{}

##### 接口底层

- 动态类型
- 动态值

##### 类型断言

做类型断言的前提是 一定要是一个接口类型的变量

x.(T)

使用switch来做类型断言

##### 文件操作

##### 打开文件和关闭文件

![image-20210810185410507](Go语言学习.assets/image-20210810185410507.png)

缓冲区

![image-20210810185806983](Go语言学习.assets/image-20210810185806983.png)

read

bufio

ioutil

##### 写文件

os.openfile()

write 和 writestring

bufio.newwriter

ioutil

在文件中插入东东

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	//OpenFile()
	InsertFile()
}

func InsertFile() {
	//打开文件
	file, err := os.OpenFile("./sb.txt", os.O_RDWR, 0644)
	if err != nil {
		fmt.Printf("err cause : %v\n",file)
		return
	}
	defer file.Close()

	//读首两个字节
	var b = [2]byte{}
	n, _ := file.Read(b[:])

	//创建文件 写首两个字节
	openFile, _ := os.OpenFile("./sbinsert.txt", os.O_CREATE|os.O_WRONLY, 0644)
	openFile.Write(b[:n])
	defer openFile.Close()

	//尝试移动光标
	_, err1 := file.Seek(2, 0)  //光标移动
	if err1 != nil {
		return
	}

	//尝试写要插入的数据
	openFile.Write([]byte{'c'})

	//尝试读光标下一个字节的数据
	var a [128]byte
	read, err2 := file.Read(a[:])
	if err2 != nil {
		return
	}

	fmt.Println(string(a[:read]))

	openFile.Write(a[:read])

	os.Rename("./sbinsert.txt","./sb.txt")
	//writer := bufio.NewWriter(file)
	//writer.WriteString("c")
	//writer.Flush()

}
func OpenFile() {
	open, err := os.Open("./xx.txt")
	if err != nil {
		fmt.Printf("err cause: %v\n",open)
		return
	}
	defer open.Close()
	var b [128]byte
	for {
		read, err1 := open.Read(b[:])
		if err1 != nil {
			fmt.Printf("read err cause: %v\n",err1)
			return
		}
		fmt.Println(string(b[:]))
		if read <128 {
			return
		}
	}


}
```

#### 今日内容

##### time标准库

时间类型

time.time类型表示时间 我们可以通过time.now() 函数获取当前的时间对象 然后获取时间对象的年月日时分秒等信息。示例代码如下：

##### 时间戳



##### 时间间隔

##### add

##### sub

##### equal

##### before

##### after

##### 定时器time.tick

##### 时间格式化

时间类型有一个自带的方法Format进行格式化，需要注意的是go语言中格式化时间模版不是常见的y-m-d h:/m:/s 而是使用go诞生的时间2006 1 2 3 4

补充：如果想要格式化为12小时方式，需要指定PM

```go
package main

import (
   "fmt"
   "time"
)

func main() {
   f2()
}

func f1() {
   now := time.Now()
   fmt.Printf("%v \n",now)
   fmt.Printf("%v \n",now.Year())
   fmt.Printf("%v \n",now.Month())
   fmt.Printf("%v \n",now.Day())
   fmt.Printf("%v \n",now.Hour())
   fmt.Printf("%v \n",now.Minute())
   fmt.Printf("%v \n",now.Second())
   fmt.Println(now.Date())

   //时间戳
   fmt.Println(now.Unix())
   fmt.Println(now.UnixNano())
   //time.Unix()
   unix:= time.Unix(now.Unix(), 0)
   fmt.Println(unix)
   //时间间隔
   fmt.Println(time.Second)
   //now +24 hours
   fmt.Println(time.Now().Add(time.Hour*24))
   //定时器
   //tick := time.Tick(time.Second)
   //for  i := range tick {
   // fmt.Println(i)
   //}

   //格式化时间 把语言中时间对象 转换成字符串类型的时间
   //2021/08/10
   fmt.Println(time.Now().Format("2006/01/02"))
   fmt.Println(time.Now().Format("2006-1-2 15:04:05"))
   fmt.Println(time.Now().Format("2006-1-2 03:04:05"))
   fmt.Println(time.Now().Format("2006-1-2 15:04:05 PM"))
   fmt.Println(time.Now().Format("2006:01:02 15:04:05.000 PM"))

   //按照对应的格式 解析字符串类型的时间
   value, err := time.Parse("2006-01-02", "2019-05-20")
   if err != nil {
      fmt.Println( " err ",err)
      return
   }
   fmt.Println(value)

   fmt.Println(time.Now().Sub(time.Now().Add(-time.Hour)))

   fmt.Println("beginning")
   //sleep
   time.Sleep(time.Second*2)
   fmt.Println("ending...")
}

func f2() {
   now:= time.Now()
   //获取的是当前时区的时间
   fmt.Println(now)
   //按照东八区的时区和格式解析一个字符串格式的时间
   time.Parse("2006-01-02 15:04:05", "2021-08-11 21:33:05")
   //根据字符加载时区
   location, err := time.LoadLocation("Asia/Shanghai")
   if err!=nil {
      fmt.Printf("load loc failed , err :%v\n",err)
      return
   }
   //按照指定时区解析时间
   parseInLocation, err := time.ParseInLocation("2006-01-02 15:05:05", "2021-08-11 21:33:05", location)

   fmt.Println(time.Now().Sub(parseInLocation))

}
```

##### 日志库

需求分析

1. 支持往不同的地方输出日志
2. 分级别输出
   1. debug
   2. info
   3. warning
   4. error
   5. fatal
3. 日志要支持开关控制，比如说开发的时候什么级别的日志都能输出，但是上线之后只有INFO级别往下才能输出
4. 完整的日志记录要包含日志要有时间、行号、文件名、日志级别、日志信息
5. 日志文件要切割

   1. 按文件大小切割
      1. 每次记录日志之前都判断一下当前写的这个文件的文件大小
   2. 按日期切割
      1. 在日志结构体中设置一个字段记录上一次切割的小时数
      2. 在写日志之前检查一下当前时间的小时数和之前保存的是否一致，不一致就要切割

```go
package main

import (
	"fmt"
	"os"
	"path"
	"runtime"
	"strconv"
	"time"
)

func main() {
	consoleLogger := NewConsoleLogger(ERROR)
	Logger.Debug(consoleLogger,"hello world")
	Logger.Info(consoleLogger,"hello world")
	Logger.Warning(consoleLogger,"hello world")
	Logger.Error(consoleLogger,"hello world%d",10)
	Logger.Fatal(consoleLogger,"hello world")

	fileLogger := NewFileLogger(ERROR, ".", "logdemo.txt", "logdemoerr.txt", 128)
	Logger(fileLogger).Debug("hello world %d",10)
	Logger(fileLogger).Error("fatal error %v","某树被榨干了...")
}

type Logger interface {
	Debug(string,...interface{})
	Info(string,...interface{})
	Warning(string,...interface{})
	Error(string,...interface{})
	Fatal(string,...interface{})
}

type ConsoleLogger struct {
	LogLevel MODE
}

type MODE = int

const (
	DEBUG MODE =iota
	INFO
	WARNING
	ERROR
	FATAL
)

func NewConsoleLogger(logLevel MODE) ConsoleLogger {
	return ConsoleLogger{
		LogLevel: logLevel,
	}
}

func (m ConsoleLogger) Debug(s string,a...interface{}) {
	if m.LogLevel>=DEBUG {
		var msg string
		if a == nil {
			msg=s
		} else {
			msg=fmt.Sprintf(s,a)
		}
		fmt.Printf("[%v] [DEBUG] this is a debug log, value :%v\n",time.Now().Format("2006-01-02 15-04-05"),msg)
		fmt.Println(getInfo(2))
	}
}
func (m ConsoleLogger) Info(s string,a ...interface{}) {
	if m.LogLevel>=INFO {
		var msg string
		if a == nil {
			msg=s
		} else {
			msg=fmt.Sprintf(s,a)
		}
		fmt.Printf("[%v] [INFO] this is a info log, value :%v\n", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Println(getInfo(2))
	}
}
func (m ConsoleLogger) Warning(s string , a ...interface{}) {
	if m.LogLevel>=WARNING {
		var msg string
		if a == nil {
			msg=s
		} else {
			msg=fmt.Sprintf(s,a)
		}
		fmt.Printf("[%v] [WARNING] this is a warning log, value :%v\n", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Println(getInfo(2))
	}
}
func (m ConsoleLogger) Error(s string,a ...interface{}) {
	if m.LogLevel>=ERROR {
		var msg string
		if a == nil {
			msg=s
		} else {
			msg=fmt.Sprintf(s,a)
		}
		fmt.Printf("[%v] [ERROR] this is a error log, value :%v \n", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Println(getInfo(2))
	}
}
func (m ConsoleLogger) Fatal(s string,a...interface{}) {
	if m.LogLevel>=FATAL {
		var msg string
		if a == nil {
			msg=s
		} else {
			msg=fmt.Sprintf(s,a)
		}
		fmt.Printf("[%v] [FATAL] this is a fatal log, value :%v\n", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Println(getInfo(2))
	}
}

func getInfo(n int) string {
	caller, file, line, ok := runtime.Caller(n)
	if !ok {
		return "error"
	}
	name:= runtime.FuncForPC(caller).Name()
	return "fileLocation: "+path.Base(file)+", method: "+name+", line: "+strconv.Itoa(line)
}

type FileLogger struct {
	LogLevel MODE
	fileName string  //日志文件的名称
	filePath string	 //日志文件的路径
	errFileName string 	//错误日志单独记录
	maxFileSize int64
	fileObj *os.File
	errFileObj *os.File
}

func NewFileLogger(logLevel MODE,filePath, fileName , errFileName string , maxFileSize int64)*FileLogger  {
	file, err := os.OpenFile(path.Join(filePath,fileName), os.O_CREATE|os.O_APPEND|os.O_WRONLY, 0644)
	if err != nil {
		fmt.Println(err)
		return nil
	}

	errfile, err := os.OpenFile(path.Join(filePath,errFileName),os.O_CREATE|os.O_APPEND|os.O_WRONLY,0644)
	if err != nil {
		return nil
	}
	return &FileLogger{
		LogLevel: logLevel,
		fileName:    fileName,
		filePath:    filePath,
		errFileName: errFileName,
		maxFileSize: maxFileSize,
		fileObj: file,
		errFileObj: errfile ,
	}
}
func (f *FileLogger) Close()  {
	f.fileObj.Close()
	f.errFileObj.Close()
}

func (f *FileLogger) checkSize(fileObj *os.File) bool {
	stat, err := fileObj.Stat()
	if err != nil {
		return false
	}
	if stat.Size() > f.maxFileSize {
		return true
	}else{
		return false
	}
}
func (f *FileLogger)SplitLogFile() {
	//需要切割文件
	//1.关闭当前文件
	f.fileObj.Close()
	//2.rename 备份一下 xx.log -> xx.log.bak201908031709
	nowStr:=time.Now().Format("20060102150405000")
	bakFilePath := path.Join(f.filePath, f.fileName)+".bak"+nowStr
	err := os.Rename(path.Join(f.filePath, f.fileName), bakFilePath)
	if err != nil {
		return
	}
	//3.打开一个新的日志文件
	newFile, err := os.OpenFile(path.Join(f.filePath, f.fileName), os.O_CREATE|os.O_APPEND|os.O_WRONLY, 0644)
	if err != nil {
		return
	}
	//4.将打开的新日志文件对象赋值给 f.fileObj
	f.fileObj = newFile

}
func (f *FileLogger) Debug(s string, a ...interface{}) {
	if f.LogLevel>=DEBUG {
		if f.checkSize(f.fileObj) {
			f.SplitLogFile()
		}
		msg := fmt.Sprintf(s, a)
		msg = fmt.Sprintf("[%v] [DEBUG] this is a debug log, value :%v", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Fprintln(f.fileObj)
		fmt.Fprintln(f.fileObj,msg)
		fmt.Fprintln(f.fileObj,getInfo(2))
		f.Close()
	}
}

func (f *FileLogger) Info(s string, a ...interface{}) {
	if f.LogLevel>=INFO {

		msg := fmt.Sprintf(s, a)
		msg = fmt.Sprintf("[%v] [INFO] this is a info log, value :%v", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Fprintln(f.fileObj)
		fmt.Fprintln(f.fileObj,msg)
		fmt.Fprintln(f.fileObj,getInfo(2))
		f.Close()
	}
}
func (f *FileLogger) Warning(s string, a ...interface{}) {
	if f.LogLevel>=WARNING {

		msg := fmt.Sprintf(s, a)
		msg = fmt.Sprintf("[%v] [WARNING] this is a warning log, value :%v", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Fprintln(f.fileObj)
		fmt.Fprintln(f.fileObj,msg)
		fmt.Fprintln(f.fileObj,getInfo(2))
		f.Close()
	}
}
func (f *FileLogger) Error(s string, a ...interface{}) {
	if f.LogLevel>=ERROR {

		msg := fmt.Sprintf(s, a)
		msg = fmt.Sprintf("[%v] [ERROR] this is a error log, value :%v", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Fprintln(f.fileObj)
		fmt.Fprintln(f.fileObj,msg)
		fmt.Fprintln(f.fileObj,getInfo(2))

		fmt.Fprintln(f.errFileObj)
		fmt.Fprintln(f.errFileObj,msg)
		fmt.Fprintln(f.errFileObj,getInfo(2))
		f.Close()
	}
}
func (f *FileLogger) Fatal(s string, a ...interface{}) {
	if f.LogLevel>=FATAL {

		msg := fmt.Sprintf(s, a)
		msg = fmt.Sprintf("[%v] [FATAL] this is a Fatal log, value :%v", time.Now().Format("2006-01-02 15-04-05"), msg)
		fmt.Fprintln(f.fileObj)
		fmt.Fprintln(f.fileObj,msg)
		fmt.Fprintln(f.fileObj,getInfo(2))

		fmt.Fprintln(f.errFileObj)
		fmt.Fprintln(f.errFileObj,msg)
		fmt.Fprintln(f.errFileObj,getInfo(2))
		f.Close()
	}
}
```

##### 反射

反射是指在程序运行期间对程序本身进行访问和修改的能力。程序在编译时，变量被转换为内存地址，变量名不会被编译器写入到可执行部分。在运行程序时，程序无法获取自身的信息。

支持反射的语言可以在程序编译期将变量的反射信息，如字段名称、类型名称、结构体信息等整合到可执行文件中，并给程序提供接口访问反射信息，这样就可以在程序运行期获取类型的反射信息，并且有能力修改她们。



go程序在运行期使用reflect包访问程序的反射信息。

空接口可以存储任意类型的变量，那么我们如何知道空接口保存的数据是什么呢？反射就是在运行时动态的获取一个变量的类型信息和值信息。



##### reflect包

在go语言的反射机制中，任何接口值都是由一个具体类型和具体类型的值两部分组成的。在go语言中反射的相关功能有内置的reflect包提供，任意接口值在反射中都可以理解为有reflect.Type 和 reflect.Value 两部分组成，并且reflect包提供了reflect.TypeOf 和 reflect.ValueOf两个函数来获取任意对象的value和type

typeof

valueof

##### type name 和 type kind

在反射中关于类型还划分为两种：类型type和种类kind 在go语言中我们可以使用type关键字构造很多种自定义类I型那个，而种类kind就是指底层的类型，但在反射中，当需要区分指针、结构体等大品种的类型时，就会用到种类kind

##### valueof

```go
package main

import (
   "fmt"
   "reflect"
)

func main() {
   reflectType(int64(8))
   reflectType(int32(8))
   reflectType("hello world")
   reflectType(map[interface{}]interface{}{1:"hello" , "hello world":[]bool{true}})
   reflectType(cat{name: "tomcat"})

   reflectValue(int64(8))

   b:=int64(20)
   //reflectSetValue1(b)  //这样不行会引发panic错误
   reflectSetValue2(&b)
   fmt.Println(b)

   var a *int
   fmt.Println(reflect.ValueOf(a).IsNil())
   fmt.Println(reflect.ValueOf(a).IsValid())
   c := cat{name: "tomcat"}
   fmt.Println(reflect.ValueOf(c).FieldByName("name"))
   fmt.Println(reflect.ValueOf(c).MethodByName("name").IsValid())

   m:=map[string]int{"娜扎":1}
   fmt.Println(reflect.ValueOf(m).MapIndex(reflect.ValueOf("娜扎")).IsValid())

}
func reflectType(a interface{}) {
   v := reflect.TypeOf(a)
   fmt.Printf("%T %v\n",v,v)
   fmt.Printf("type %v  kind %v \n",v.Name(),v.Kind())
}
func reflectValue(a interface{})  {
   v:=reflect.ValueOf(a)
   kind := v.Kind()
   switch kind {
   case reflect.Int64:
      fmt.Printf("type is int64,value is %d\n",int64(v.Int()))
   case reflect.Float32:
      fmt.Printf("type is float32, value is %f\n",float32(v.Float()))
   }

}
func reflectSetValue1(x interface{}) {
   value := reflect.ValueOf(x)
   if value.Kind() == reflect.Int64 {
      value.SetInt(200)  //修改的是副本 reflect包会引发panic
   }
}
func reflectSetValue2(x interface{}) {
   value :=reflect.ValueOf(x)
   if value.Elem().Kind() == reflect.Int64 {
      value.Elem().SetInt(200)
   }
}
type cat struct {
   name string
}
```

##### 通过反射设置变量的值

想要在函数中通过反射修改变量的值，需要注意函数参数传递的是值拷贝，必须传递变量地址才能修改变量值。而反射中使用专有的elem()方法来获取指针对应的值

##### isNil和isValid

报告持有的值是否为nil，持有的值的分类必须是通道、函数、接口、映射、指针、切片之一，否则会导致panic

isvalid返回v是否持有一个值，如果v是value的零值就会返回假，如果v除了isvalid、string、kind之外的方法都会导致panic

##### 区别

isnil常被用于判断指针是否为空，isvalid常被用于判定返回值是否有效

```go
package main

import (
   json2 "encoding/json"
   "fmt"
   "reflect"
)

func main() {
   s:=student{
      Name:  "xwz",
      Score: "90",
   }
//最终要得到 {"name":"xwz","score":90}
   typeof := reflect.TypeOf(s)
   json:=`{`
   for i := 0; i < typeof.NumField(); i++ {
      fmt.Println(typeof.FieldByIndex([]int{i}).Name)
      //fmt.Println(typeof.Field(i).Name)
      fmt.Println(typeof.FieldByIndex([]int{i}).Tag.Get("json"))
      json+="\""+typeof.Field(i).Tag.Get("json")+"\""+":"
      structField, b := typeof.FieldByName(typeof.Field(i).Name)
      fmt.Println(structField.Name)
      fmt.Println(structField.Type)
      fmt.Println(structField.Index)
      valueof:= reflect.ValueOf(s)
      fmt.Println(valueof.Field(i))
      sprint := fmt.Sprint(valueof.Field(i))
      if b {
         json+="\""+sprint+"\""+","
      }
   }
   s2 := json[:len(json)-1]
   json = s2
   json+="}"
   fmt.Println(json)

   var s1 student
   json2.Unmarshal([]byte(json),&s1)
   fmt.Println(s1)
   //反序列化实例
}

type student struct {
   Name string `json:"name"`
   Score string `json:"score"`
}
```

##### 内容回顾

##### time

##### 时间类型

- time.Time : Time.Now()
- 时间戳: 
  - time.Now().Unix()
  - time.Now().UnixNano():1971.1.1到现在的纳秒数

##### 时间间隔类型

- time.Duration ：时间间隔类型
  - time.Second
  - time.Hour
  - time.Minute

##### 时间操作

时间对象+-一个时间间隔对象

after 、 before

##### 时间格式化

format

##### 定时器

```go
//定时器
//tick := time.Tick(time.Second)
//for  i := range tick {
// fmt.Println(i)
//}
```

##### 解析字符串格式的时间（时区）

```go
now:= time.Now()
//获取的是当前时区的时间
fmt.Println(now)
//按照东八区的时区和格式解析一个字符串格式的时间
time.Parse("2006-01-02 15:04:05", "2021-08-11 21:33:05")
//根据字符加载时区
location, err := time.LoadLocation("Asia/Shanghai")
if err!=nil {
   fmt.Printf("load loc failed , err :%v\n",err)
   return
}
//按照指定时区解析时间
parseInLocation, err := time.ParseInLocation("2006-01-02 15:05:05", "2021-08-11 21:33:05", location)

fmt.Println(time.Now().Sub(parseInLocation))
```

##### 日志库

time

文件操作

runtime.caller()

##### 反射

接口类型的变量分为两部分，动态类型和动态值。

反射的应用：json等数据解析 ORM等工具...

##### 反射的两个方法：

- reflect.Typeof()
- reflect.Valueof()

#### 今日内容

##### strconv标准库介绍

```go
package main

import (
   "fmt"
   "strconv"
)

func main() {
   str:="1000"
   parseInt, err := strconv.ParseInt(str, 10, 64) //10进制 int64
   if err != nil {
      return
   }
   fmt.Printf("%T %v\n",parseInt,parseInt)

   parseInt1, err := strconv.ParseInt(str,10,0)
   if err != nil {
      return
   }
   fmt.Printf("%T %v\n",parseInt1,parseInt1)

   atoi,_:=strconv.Atoi("1000")//go语言继承c语言而来的 a是array 因为string底层实际上是array的byte数组 i是int
   fmt.Println(atoi)

   i :=97
   fmt.Println(string(i))  //a
   sprint := fmt.Sprint(i) //97

   //字符串中解析出bool值
   s2:="true"
   parseBool, _ := strconv.ParseBool(s2)
   fmt.Println(parseBool)

   fmt.Println(strconv.ParseFloat("2.14",32))

   fmt.Println(sprint)

}
```

##### 并发

并发是编程里面一个非常重要的概念，go语言在语言层面天生支持并发，这也是go语言流行的一个很重要的原因。

##### go语言的并发编程

##### 并发与并行

并发：同一时间段内执行多个任务

并行：同一时刻执行多个任务

go语言的并发通过goroutine实现。goroutine类似于线程，属于用户态的线程.我们可以根据需要创建成千上万个goroutine个并发工作。goroutine由go语言的运行时runtime调度完成，而线程是由操作系统调度完成的。

go语言还提供channel在多个goroutine间进行通信。goroutine和channel是go语言秉承CSP communication sequential  process 并发模式的重要实现基础.

##### goutine

在java和c++中我们要实现并发编程的时候,我们通常要自己维护一个线程池,并且需要自己去包装一个又一个任务,同时需要自己去调度线程执行任务并维护上下文切换,这一切通常会耗费程序员大量的心智.那么能不能有一种机制,程序员只需要定义很多个任务,让系统去帮助我们吧这些任务分配到CPU上实现并发执行呢?

go语言中的goroutine就是这样一种机制,goroutine的概念类似于线程,但goroutine是由go的运行时runtime调度和管理的.go程序会智能地将goroutine中的任务合理的分配给每个cpu.go语言之所以被成为现代化的编程语言,就是因为他在语言层面已经内置了调度和上下文切换的机制.

在go语言变成中你不需要自己去写进线程/线程/协程,你的技能包里只有一个技能 ---- goroutine,当你需要让某个任务并发执行的时候,你只需要把这个任务包装成一个函数,开启一个goroutine去执行这个函数就可以了,就是这么简单粗暴.

##### 使用goroutine

go语言中使用goroutine非常简单,只需要在调用函数的时候在前面加上go关键字,就可以为一个函数创建一个goroutine

一个goroutine必定对应一个函数,可以创建多个goroutine去执行相同的函数

```go
package main

import (
   "fmt"
   "time"
)

//程序启动之后会创建一个主goroutine去执行
func main() {
   for i := 0; i < 10; i++ {
      //go hello(i)  //开启一个单独的goroutine去执行hello函数（任务）

      //匿名
      //go func() {
      // fmt.Println(i)
      //}()  //闭包 会出现i外层是1 内部输出1 外部这时候已经跑到10了 那么这时候内部就输出10

      //
      go func(i int) {
         fmt.Println(i)  //用的是函数参数的那个i ， 不再是外面的那个i了
      }(i)


   }
   fmt.Println("main")
   //main函数结束了 由main函数启动的goroutine也都结束了
   time.Sleep(time.Second)
}

func hello(i int)  {
   fmt.Println("hello",i)
}
```

##### goroutine什么时候结束

goroutine对应的函数执行结束 goroutine就结束了

```go
package main

import (
   "fmt"
   "math/rand"
   "sync"
   "time"
)

func main() {
   //waitGroup
   //f1()
   for i := 0; i <10 ; i++ {
      wg.Add(1)
      go f2(i)
   }

   //如何知道这10个goroutine都结束了
   wg.Wait()  //等待wg的计数器减为0
}

var wg sync.WaitGroup

func f1() {
   rand.Seed(time.Now().UnixNano())
   for i := 0; i < 5; i++ {
      i1 := rand.Int()
      i2 := rand.Intn(10)  //左开右闭
      fmt.Println(i1,i2)
   }
}

func f2(i int) {
   time.Sleep(time.Millisecond*time.Duration(rand.Intn(300)))
   fmt.Println(i)
   defer wg.Done()
}
```

##### rand

```go
func f1() {
   rand.Seed(time.Now().UnixNano())
   for i := 0; i < 5; i++ {
      i1 := rand.Int()
      i2 := rand.Intn(10)  //左开右闭
      fmt.Println(i1,i2)

   }
}
```

#### goroutine与线程

##### 可增长的栈

OS线程（操作系统线程）一般都有固定的栈内存（通常为2MB），一个goroutine的栈在其生命周期开始时只有很小的栈（典型情况下2KB），goroutine的栈不是固定的，他可以按需增大和减小，goroutine的栈大小限制可以达到1GB，虽然极少会用到这么大，所以在go语言中一次创建10w左右的goroutine也是可以的。

##### goroutine调度

GMP是go语言运行时runtime层面的实现，是go语言自己实现的一套调度系统。区别与操作系统调度OS线程。

- G很好理解，就是个goroutine的，里面除了存放goroutine信息外 还有与所在P的绑定等信息
- M machine是Go运行时runtine对操作系统内核线程的虚拟，M与内核线程一般是一一映射的关系，一个goroutine最终是要放到M上执行的
- P管理着一组goroutine队列，P里面会存储当前goroutine运行的上下文环境（函数指针、堆栈地址及地址边界），P会对自己管理的goroutine队列做一些调度（比如把占用CPU时间较长的goroutine暂停、运行后续的goroutine等等）当自己的队列消费完了就去全局队列里取，如果全局队列里也消费完了会去其他P的队列里抢任务。

P与M一般也是一一对应的。她们关系是：P管理着一组G挂载在M上运行。当一个G长久的阻塞在一个M上时，runtime会新建一个M，阻塞G所在的P会把其他的G挂载在新建的M上。当旧的G阻塞完成或者认为其已经死掉时，回收掉旧的M

P的个数是通过runtime.GOMAXPROCS设定的，最大为256 go1.5版本之后默认为物理线程数。在并发量大的时候会增加一些P和M，但不会太多，切换太频繁的话会得不偿失

单从线程调度讲，Go语言相比起来其他语言的优势在于OS线程是有OS内核来调度的。goroutine则是由Go运行时 runtime自己的调度器调度的。这个调度器使用一个成为m：n调度技术（复用/调度m个goroutine到n个OS线程）其一大特点是goroutine的调度是在用户态下完成的，不涉及内核态与用户态之间的频繁切换，包括内存的分配与释放都是在用户态维护着一大块的内存池，不直接调用系统的malloc函数（除非内存池需要改变），成本比调度OS线程低很多。另一方面充分利用了多核的硬件资源，近似的吧若干goroutine均分在物理线程上，再加上本身goroutine的超轻量，以上种种保证了go调度方面的性能。

##### GOMAXPROCS

go运行时的调度使用gomaxprocs参数来确定需要使用多少个OS线程来同时执行go代码。默认值是机器上的CPU核心数。例如在一个8核心的机器上，调度器会把go代码同时调度到8个OS线程上(GOMAXPROCS是m：n调度中的n)

go语言中可以通过runtime.gomaxprocs()函数来设定当前程序并发时占用的CPU逻辑核心数

go1.5版本之前，默认使用的是单核心执行。go1.5版本之后，默认使用全部的CPU逻辑核心数

```go
package main

import (
   "fmt"
   "runtime"
   "sync"
)
var wg sync.WaitGroup

func main() {
   runtime.GOMAXPROCS(2)  //默认CPU的逻辑核心数，默认跑满整个CPU
   fmt.Println(runtime.NumCPU())
   wg.Add(2)
   go a()
   go b()
   wg.Wait()
}

func a() {
   for i := 0; i < 10; i++ {
      fmt.Printf("A:%d\n",i)
   }
   defer wg.Done()
}

func b() {
   for i := 0; i < 10; i++ {
      fmt.Printf("B:%d\n",i)
   }
   defer wg.Done()
}
```

##### go语言中的操作系统线程和goroutine的关系

1. 一个操作系统线程对应用户态多个goroutine
2. go程序可以同时使用多个操作系统线程 
3. goroutine和OS线程是多对多的关系，即m:n

##### goroutine调度模型

GMP

m：n

goroutine初始栈的大小是2k

##### channel

单纯地将函数并发执行是没有意义的。函数与函数间需要交换数据才能体现并发执行的意义

虽然可以使用共享内存进行数据交换，但是共享内存在不同的goroutine中容易发生竞态问题。为了保证数据交换的正确性，必须使用互斥量对内存进行加锁，但这种做法势必造成性能问题。

go语言的并发模型是CSP communication sequential processes 提倡通过通信共享内存而不是通过共享内存而实现通信

如果说goroutine是go程序并发的执行体，channel就是他们之间的连接。channel是可以让一个goroutine发送特定值到另一个goroutine的通信机制

go语言中的通道channel是一种特殊的类型。通道像一个传送带或者队列，总是遵循先入先出fifo的规则，保证收发数据的顺序。每一个通道都是具体类型的导管，也就是声明channel的时候需要为其指定元素类型。

##### channel类型

```go
var 变量 chan 元素类型
```

通道必须使用make函数初始化才能使用

##### 发送

将一个值发送到通道中

```go
ch <- 10 //把10发送到ch
```

##### 接收

从一个通道接收值

```go
x := <- ch  //从ch中接收值并赋值
<- ch //从ch中接收值，忽略结果
```

##### 关闭

我们通过调用内置的close函数来关闭通道

```go
close(ch)
```

关于关闭通道需要注意的事情是，只有在通知接收方goroutine所有的数据都发送完毕的时候才需要关闭通道。通道是可以被垃圾回收机制回收的，他和关闭文件不一样，在结束操作之后关闭文件是必须要做的，但关闭通道不是必须的。

关闭后的通道有以下特点：

1. 对一个关闭的通道再发送值就会导致panic
2. 对一个关闭的通道进行接收就会一直获取直到通道为空
3. 对一个关闭的并且没有值的通道执行接收操作会得到对应类型的零值
4. 关闭一个已经关闭的通道会导致panic

##### 无缓冲通道

无缓冲的通道又称为阻塞的通道。无缓冲的通道只在有人接收值的时候才能发送值。无缓冲通道上的发送操作会阻塞，直到另一个goroutine在该通道上执行接收操作，这个值才能发送成功，两个goroutine将继续执行。相反，如果接收操作先执行，接收方的goroutine将阻塞，直到另一个goroutine在该通道上发送一个值。使用无缓冲通道进行通信将导致发送和接收的goroutine同步化。因此，无缓冲通道也被成为同步通道

##### 有缓冲通道

在使用make初始化的时候为其指定通道的容量

只要通道的容量大于零，那么该通道就是有缓冲的通道，通道的容量表示通道中能存放元素的数量。

我们可以使用内置的len函数获取通道内元素的数量，使用cap函数获取通道的容量

##### 如何优雅的从通道循环取值

当通过通道发送有限的数据时，我们可以通过close函数关闭通道来告知从该通道接收值的goroutine停止等待。当通道被关闭时，往该通道发送值会引发panic，从该通道里接收的值一直都是类型的零值。那么如何判断一个通道是否被关闭了呢？

##### 单向通道

有的时候我们会将通道作为参数在多个任务函数间传递，很多时候我们在不同的任务函数中使用通道都会对其进行限制，比如只能发送或只能接收。go语言中提供了单向通道来处理这种情况。

```go
var ch1 <-chan //只能取值
var ch2 chan<- //只能存值
```

![image-20210813220847452](Go语言学习.assets/image-20210813220847452.png)

##### worker pool （goroutine池）

编写代码实现一个计算随机数的每个位置数字之和的程序。要求使用goroutine和channel构建生产者和消费者模式，可以指定启动的goroutine数量-worker pool模式

在工作中我们通常会用worker pool模式，控制goroutine数量，防止goroutine泄漏和暴涨

```go
package main

import (
   "fmt"
   "time"
)

var jobs chan int
var results chan int
func main() {
   jobs = make(chan int , 100)
   results = make(chan int , 100)
   for i := 1; i <= 3; i++ {
      go worker(i,jobs,results)
   }
   for i := 1; i <= 5; i++ {
      jobs<-i
   }
   for i := 0; i < 5; i++ {
      <-results
   }
   //for result := range results {
   // fmt.Println(result)
   //}
}

func worker(id int, jobs <-chan int, results chan<- int) {
   for j := range jobs {
      fmt.Println("worker ",id," start job ",j)
      time.Sleep(time.Second)
      results<-2*j
      fmt.Println("worker ",id," end job" , j)
   }
}
```

##### 练习

##### select多路复用

在某些场景下我们需要同时从多个通道接收数据。通道在接收数据时，如果没有数据可以接收将会发生阻塞。你也许会写出如下代码使用遍历的方式来实现

![image-20210813232439809](Go语言学习.assets/image-20210813232439809.png)

这种方式虽然可以实现从多个通道接收值的要求，但是运行性能会差很多。为了应对这种场景，go内置了select关键字，可以同时响应多个通道的操作。select的使用类似于switch语句，他有一些case分支和一个默认的分支。每个case会对应一个通道的通信（接收或发送）过程。select会一直等待，直到某个case的通信操作完成时，就会执行case分支对应的语句。

![image-20210813232707904](Go语言学习.assets/image-20210813232707904.png)

使用select语句能提高可读性

- 可处理一个或多个channel的发送/接收操作
- 如果有多个case同时满足，select会随机选择一个
- 对于没有case的select{}会一直等待，可用于阻塞main函数

```go
package main

import "fmt"

func main() {
   ch:=make(chan int , 1)
   for i := 0; i < 10; i++ {
      select {
      case x:=<-ch:
         fmt.Println(x)
      case ch<-i:
      default:
         fmt.Println("hiahiahia")
      }
   }

}
```

##### 并发安全和锁

##### 作业

1. 日志库中channel怎么用
2.  什么时候起后台的goroutine去写日志到文件中

#### day08

##### 今日内容

##### 并发のgoroutine

并发和并行的区别

goroutine的启动  `go`

将并发执行的任务包装成一个函数，调用函数的时候前面加上go关键字，就能够开启一个goroutine去执行该函数

goroutine对应的函数执行完，该goroutine就结束了

程序启动的时候会自动的创建一个goroutine去执行main函数，main函数结束了那么程序就结束了所有开启的goroutine也都结束了

sync.waitGroup 等待组

```go
var wg waitGroup
wg.add(1):计数器+1
wg.done()：计数器-1
wg.wait()：等待
```

##### goroutine的本质

goroutine的调度模型GMP

m：n 把m个goroutine分配给n个操作系统的线程

##### goroutine与操作系统线程（OS）的区别

goroutine是用户态的线程，比内核态的线程更轻量级一点，初始值2Kb

##### runtime.GOMAXPROCS()

go1.5之后模式就是操作系统的逻辑核心数,默认跑满cpu

runtime.GOMAXPROCS(1)只占用一个核心

##### work pool 模式

开启一定数据的goroutine去干活。

##### channel为什么需要

想通过channel实现多个goroutine的通信

CSP ：通过通信来共享内存

channel是一种类型，一种引用类型。make函数初始化才能使用（slice  / map /channel）

channel的声明 var ch chan int

channel的初始化 make(chan 元素类型，[缓冲区大小])

channel的操作：

- 发送<-

- 接收<-

- 关闭close

带缓冲区的通道和无缓冲区的通道

##### 单向通道

通常是用做函数的参数，只读和只写

##### select

同一时刻有多个通道要操作的场景，使用select



#### sync包

##### 互斥锁

互斥锁是一种常用的控制共享资源访问的方法，他能够保证同时只有一个goroutine可以访问资源，go语言中使用sync包的mutex类型来实现互斥锁。使用互斥锁来修复上面的代码

使用互斥锁能够保证同一时间有且只有一个goroutine进入临界区，其他的goroutine则在等待锁，当互斥锁释放后，等待的goroutine才可以获取锁进入临界区，多个goroutine同时等待一个锁时，唤醒的策略是随机的

##### 读写互斥锁

互斥锁是完全互斥的，但是很多实际场景下是读多写少的，当我们并发的去读取一个资源不涉及资源修改的时候是没有必要加锁的，这种场景下使用读写锁是更好的一种选择。读写锁在go语言中使用sync包中的rwmutex类型。

读写锁分为两种：读锁和写锁。当一个goroutine获取读锁之后，其他的goroutine如果是获取读锁会继续获取锁，如果是获取写锁就会等待；当一个goroutine获取写锁之后，其他的goroutine无论是获取读锁还是写锁都会等待。

##### sync.waitgroup

在代码中生硬的使用time.sleep肯定是不合适的，go语言中可以使用sync.waitgroup来实现并发任务的同步

wg.add

wg.done

wg.wait

sync.waitgroup内部维护着一个计数器，计数器的值可以增加和减少。当我们启动了n个并发任务，就将计数器增加n，每个任务完成时通过调用done方法将计数器减一，通过调用wait来等待并发任务执行完，当计数器为0时，表示所有并发任务已经完成。

##### sync.once

在编程的很多场景下我们需要确保某些操作在高并发的场景下只执行一次，例如只加载一次配置文件、只关闭一次通道等

go语言中的sync包中提供了一个针对只执行一次场景的解决方案--sync.once 

sync.once只有一个do方法

```go
func (o *Once) Do (f func()) {}
```

备注：如果要执行的函数f需要传递参数就需要搭配闭包来使用

##### sync.map

map并发多了之后执行就会报fatal error: concurrent map writes 错误

像这种场景下就需要为map加锁来保证并发的安全性了，go语言的sunc包中提供了一个开箱即用的并发安全版map----sync.map 开箱即用表示不用向内置map一样使用make函数初始化就能直接使用。同时sync.map内置了诸如store 、 load 、 loadorstore 、 delete 、 range等操作方案

```go
package main

import (
   "fmt"
   "strconv"
   "sync"
)

var wg = sync.WaitGroup{}
var m = sync.Map{}

func main() {
   for i := 0; i < 20; i++ {
      wg.Add(1)
      go func(i int) {
         key:=strconv.Itoa(i)
         set(key,i)    //必须使用sync.map内置的store方法设置键值对
         fmt.Printf("k=%v v=%v\n",key,get(key)) //必须使用sync.map内置的load方法根据key取值
         wg.Done()
      }(i)
   }
   wg.Wait()
}

func set(key string , value int) {
   m.Store(key,value)
}

func get(key string) interface{} {
    value,_:=m.Load(key)
    return value
}
```

##### atomic包

func loadint32

func storeint32

func addint32

func swapint32

func compareandswapint32

#### 网络编程

如何才能让我们的程序通过网络互相通信呢？本文只是演示了如何使用net包进行tcp和udp通信。

##### 互联网协议介绍

互联网的核心是一系列协议，总称为互联网协议internet protocol suite ， 正是这些协议规定了电脑如何连接和组网。我们理解了这些协议，就理解了互联网的原理。由于这些协议太过复杂和庞大，只能介绍日常开发中接触较多的几个协议

##### 互联网分层模型

互联网的逻辑实现被分为好几层。每一层都有自己的功能。互联网按照不同的模型划分会有不同的分层，但是不论是按照什么模型去划分，越往上的层越靠近用户，越往下的层越靠经硬件。在软件开发中我们使用最多的是将互联网划分为五个分层的模型。

![image-20210815154839385](Go语言学习.assets/image-20210815154839385.png)

##### 物理层

我们的电脑要与外界互联网通信，需要先把电脑连接网络，我们可以用双绞线、光纤、 无线电波等方式。这就叫做“实物理层”，他就是把电脑连接起来的物理手段。他主要规定了网络的一些电气特性，作用是负责传送0和1的电信号。

##### 数据链路层

单纯的0和1没有任何意义，所以我们使用者会为其赋予一些特定的含义，规定解读电信号的方式：多少个电信号算一组？每个信号为有何意义？这就是数据链路层的功能，他在物理层的上方，确定了物理层传输0和1的分组方式及代表的意义。早起的时候，每家公司都有自己的电信号分组方式。逐渐的，一种叫做以太网ethernet的协议占据了主导地位。

以太网规定，一组电信号构成一个数据包，叫做帧frame。每一帧分为两部分：标头head和数据data。其中表头包含数据包的一些说明项，比如发送者、接收者、数据类型等等。数据则是数据包的具体内容。标头的长度固定为18字节。数据的长度最短为46字节，最长为1600字节。因此，整个帧最短为64字节，最长为1518字节。如果数据很长，就必须分割成多个帧进行发送。

那么，发送者和接收者是如何标识的呢？以太网规定，连入网络的所有设备都必须具有网卡接口。数据包必须是从一块网卡，传送到另一块网卡。网卡的地址，就是数据包的发送地址和接收地址，这叫做MAC地址。每块网卡出厂的时候，都有一个全世界独一无二的MAC地址，长度是48个二进制位，通常用12个十六进制数来表示。前6个十六进制是厂商编号，后6个是该厂商的网卡流水号。有了MAC地址，就可以定位网卡和数据包的路径了。

我们会通过ARP协议来获取接收方的MAC地址，有了MAC地址之后，如何把数据准确的发送给接收方呢？ 其实这里以太网采用了一种很原始的方式，他不是把数据准确的送到接收方，而是向本网络内所有的计算机都发送，让每台计算机读取这个包的标头，找到接收方的MAC地址，然后与自身的MAC地址相比较，如果两者相同，就接受这个包，做进一步处理，否则就丢弃这个包。这种发送方式就叫做广播broadcast

##### 网络层

按照以太网协议的规则我们可以依靠MAC 地址来向外发送数据。理论上依靠MAC地址，你电脑的网卡就可以找到身在师姐另一个儿角落的某台电脑的网卡了，但是这种做法有一个重大缺陷就是以太网采用广播方式发送数据包，所有成员人手一包，不仅效率低，而且发送的数据只能局限在发送者所在的子网络。也就是说如果两台计算机不在同一个子网络，广播是传不过去的。这种设计是合理且必要的，因为如果互联网上每一台计算机都会收到互联网上收发的所有数据包，那是不现实的。

因此，必须找到一种方法区分那些MAC地址属于同一个子网络，那些不是。如果是同一个子网络，就采用广播方式发送，否则就采用路由方式发送。这就导致了网络层的诞生。他的作用是引进一套新的地址，使得我们能够区分不同计算机是否属于同一个子网络。这套地址就叫做网络地址，简称网址

网络层出现以后，每台计算机有了两种地址，一种是MAC地址，另一种是网址。两种地址之间没有任何联系，MAC地址是绑定在网卡上的，网络地址则是网络管理员分配的。网络地址帮助我们确定计算机所在的子网络,MAC地址则将数据包发送到该子网络中的目标网卡上。因此，从逻辑上可以推断，必定是先处理网络地址，然后在处理MAC地址。

规定网络地址的协议，叫做IP协议。它所定义的地址，就被称为IP地址。目前，广泛采用的是IP协议第四版，简称IPv4.IPv4这个版本规定，网络地址由32个二进制为组成，我们通常习惯用分成四段的十进制数表示IP地址，从0.0.0.0一直到255.255.255.255

根据IP协议发送的数据，就叫做IP数据包。IP数据包也分为标头和数据两个部分：标头部分主要包括版本、长度、IP地址等信息，数据部分则是IP数据包的具体内容，IP数据包的标头部分的长度为20到60字节，整个数据包的总长度最大为65535字节。

##### 传输层

有了MAC地址和IP地址，我们已经可以在互联网上任意两台主机上建立通信。但问题是同一台主机会有许多程序都需要用网络收发数据，比如QQ和浏览器这两个程序都需要连接互联网并收发数据，我们如何区分某个数据包到底是归哪个程序呢？也就是说，我们还需要一个参数，表示这个数据包到底供哪个程序（进程）使用。这个参数就叫做端口port，他其实是每一个使用网卡的程序的编号。每个数据包都发到主机的特定端口，所以不同的程序就能取到自己所需要的数据。

端口是0到65535之间的整数，正好是16个二进制位。0到1023的端口被系统占用，用户只能选用大于1023的端口。 有了IP和端口我们就能实现唯一确定互联网上的一个程序，进而实现网络间的程序通信。

我们必须在数据包中加入端口信息，这就是需要新的协议。最简单的实现叫做UDP协议，他的格式几乎就是在数据的前面，加上端口号。UDP数据包，也就是由标头和数据两部分组成：标头部分主要定义了发出端口和接收端口，数据部分就是具体的内容。UDP数据包非常简单，标头部分一共只有8个字节，总长度不超过65535字节，正好放进一个IP数据包。

UDP协议的优点是比较简单，容易实现，但是缺点是可靠性较差，一旦数据包发出，无法知道对方是否收到。为了解决这种问题，提高网络可靠性，TCP协议就诞生了。TCP协议能够确保数据不会遗失。他的缺点是过程复杂、实现困难、消耗较多的资源、TCP数据包没有长度限制，理论上可以无限长，但是为了保证网络的效率，通常TCP数据包的长度不会超过IP数据包的长度，以确保单个TCP数据包不必再分割。

##### 应用层

应用程序收到传输层的数据，接下来就要对数据进行解包。由于互联网是开放架构，数据来源五花八门，必须事先规定好通信的数据格式，否则接收方根本无法获得真正发送的数据内容。应用层的作用就是规定应用程序使用的数据格式，例如我们TCP协议之上常见的Email、HTTP、FTP等协议，这些协议就组成了互联网协议的应用层。

如图，发送方的HTTP数据经过互联网的传输过程中会依次添加各层协议的标头信息，接收方收到数据包之后再依次根据协议解包得到数据。![image-20210815163841064](Go语言学习.assets/image-20210815163841064.png)

#### socket编程

socket是BSD UNIX的进程通信机制，通常也称为套接字，用于描述IP地址和端口，是一个通信链的句柄。socket可以理解为TCP/IP网络的API，它定义了许多函数或例程，程序员可以用它们来开发TCP/IP网络上的应用程序。电脑上运行的应用程序通常通过套接字向网络发出请求或者应答网络的请求。

##### socket图解

socket是应用层与TCP/IP协议族通信的中间软件抽象层。在设计模式中，socket其实就是一个门面模式，他把复杂的TCP/IP协议族隐藏在socket后面，对用户来说只需要调用socket规定的相关函数，让socket去组织符合指定的协议数据然后进行通信。

![image-20210815165946914](Go语言学习.assets/image-20210815165946914.png)

#### go语言实现TCP通信

##### TCP协议

TCP/IP transmission control protocol 、 internet protocol即传输控制协议/网间协议，是一种面向连接（连接导向）的、可靠的、基于字节流的传输层（Transport layer）通信协议，因为是面向连接的协议，数据就像水流一样传输，会存在粘包问题。

##### TCP服务端

一个TCP服务端可以同时连接很多个客户端，例如世界各地的用户使用自己电脑上的浏览器访问淘宝网。因为go语言中创建多个goroutine实现并发非常方便和高效，所以我们可以每建立一次链接就创建一个goroutine去处理。

TCP服务端程序的处理流程：

1. 监听端口
2. 接收客户端请求建立链接
3. 创建goroutine处理连接

```go
package main

import (
   "fmt"
   "net"
)

//tcp server端
func main() {
   //1.本地端口启动服务
   listen, err := net.Listen("tcp", "127.0.0.1:20000")
   if err != nil {
      fmt.Println("start server on 127.0.0.1:20000 failed , err : ",err)
      return
   }

   for {
      //2.等待别人来跟我连接
      accept, err := listen.Accept()
      if err != nil {
         fmt.Println("build connect failed , err : ",err)
         return
      }

      go func(conn net.Conn) {
         for {
            //3.与客户端通信
            var temp [128]byte
            read, err := conn.Read(temp[:])
            if err != nil {
               fmt.Println("attemp read failed , err : ",err)
               return
            }
            fmt.Println(string(temp[:read]))
         }
      }(accept)

   }

}
```

client

```go
package main

import (
   "bufio"
   "fmt"
   "net"
   "os"
)

//tcp client
func main() {
   //1.与server建立连接
   dial, err := net.Dial("tcp", "127.0.0.1:20000")
   if err != nil {
      fmt.Println("dial 127.0.0.1:20000 failed , err : ",err)
      return
   }
   //2.发送数据
   //var write1 = make([]byte,100)
   //if len(os.Args)<2 {
   // write1 = []byte("hello world")
   //}else {
   // write1 = []byte(os.Args[1])
   //}

   for {
      reader := bufio.NewReader(os.Stdin)
      //dial.Write(write1)
      line, _ := reader.ReadString('\n')
      if string(line)=="exit" {
         break
      }
      dial.Write([]byte(line))
   }

   dial.Close()
}
```

##### TCP黏包

黏包可发生在发送端也可发生在接收端：

1. 由Nagle算法造成的发送端的黏包：nagle算法是一种改善网络传输效率的算法。简单来说就是当我们提交一段数据给TCP发送时，TCP并不立刻发送此段数据，而是等待一小段时间看看在等待期间是否还有要发送的数据，如有会一次把这两段数据发送出去。
2. 接收端接收不及时造成的接收端黏包：TCP会把接收到的数据存在自己的缓冲区中，然后通知应用层取数据。当应用层由于某些原因不能及时的把TCP的数据取出来，就会造成TCP缓冲区中存放了几段数据。 ![image-20210816200320281](Go语言学习.assets/image-20210816200320281.png)

server

```go
package main

import (
   "fmt"
   "net"
)

func main() {
   dial, err := net.Dial("tcp", "127.0.0.1:30000")
   if err != nil {
      fmt.Println("dial failed , error : ",err)
      return
   }
   defer dial.Close()

   for i := 0; i < 20; i++ {
      dial.Write([]byte("how are you , hello !"))
   }
}
```

server

```go
package main

import (
   "fmt"
   "io"
   "net"
)

func main() {
   listen, err := net.Listen("tcp", "127.0.0.1:30000")
   if err != nil {
      fmt.Println("listen port failed , err : ",err)
      return
   }
   defer listen.Close()

   for {
      accept, err := listen.Accept()
      if err != nil {
         fmt.Println("connect accept failed , err :", err)
         return
      }

      go func(conn net.Conn) {
         defer conn.Close()
         for  {
            var b  [1024]byte
            read, err := conn.Read(b[:])
            if err == io.EOF {
               break
            }
            if err != nil {
               fmt.Println("try to read failed , err : ",err)
               return
            }
            fmt.Println("received data : ",string(b[:read]))
         }

      }(accept)

   }
}
```

##### 解决方法

出现黏包的关键在于接收方不确定将要传输的数据包的大小，因此我们可以对数据包进行封包和拆包的操作。

封包：封包就是给一段数据加上包头，这样一来数据包就分为包头和包体两部分内容了（过滤非法包时封包会加入”包尾“内容）。包头部分的长度是固定的，并且他存储了包体的长度，根据包头长度固定以及包头中含有包体长度的变量就能正确的拆分出一个完整的数据包。

我们可以自己定义一个协议，比如数据包的前四个字节为包头，里面存储的是发送的数据的长度。

大端小端模式

```go
package main

import (
   "fmt"
   "net"
   "src/code.oldboyedu.com/day8/11nianbao_jiejue/protocol"
)

func main() {
   dial, err := net.Dial("tcp", "127.0.0.1:30000")
   if err != nil {
      fmt.Println("dial failed , error : ",err)
      return
   }
   defer dial.Close()

   for i := 0; i < 20; i++ {
      encode, err := protocol.Encode("how are you , hello!")
      if err != nil {
         return
      }
      dial.Write(encode)
      //dial.Write([]byte("how are you , hello !"))
   }
}
```

protocol

```go
package protocol

import (
   "bufio"
   "bytes"
   "encoding/binary"
)

//Encode 将消息编码
func Encode(message string )([]byte,error) {
   //读取消息的长度，转换为int32
   length := int32(len(message))
   pkg := new(bytes.Buffer)
   //写入消息头
   err := binary.Write(pkg, binary.LittleEndian, length)
   if err != nil {
      return nil, err
   }
   //写入消息体
   err1 := binary.Write(pkg, binary.LittleEndian, []byte(message))
   if err1 != nil {
      return nil, err1
   }
   return pkg.Bytes(),err
}

//Decode 解码消息
func Decode(reader *bufio.Reader) (string, error) {
   //读取消息的长度
   peek, err := reader.Peek(4)
   if err != nil {
      return "", err
   } //读取前四个字节的数据
   buffer := bytes.NewBuffer(peek)
   var length int32
   err1 := binary.Read(buffer, binary.LittleEndian, &length)
   if err1 != nil {
      return "", err1
   }
   //Buffered 返回缓冲区中现有的可读取的字节数
   if int32(reader.Buffered()) < length+4 {
      return "" , err
   }
   //读取真正的消息数据
   pack:=make([]byte,int(4+length))
   _,err2:=reader.Read(pack)
   if err2!=nil {
      return "",err2
   }

   return string(pack[4:]),nil


}
```

server

```go
package main

import (
   "bufio"
   "fmt"
   "net"
   "src/code.oldboyedu.com/day8/11nianbao_jiejue/protocol"
)

func main() {
   listen, err := net.Listen("tcp", "127.0.0.1:30000")
   if err != nil {
      fmt.Println("listen port failed , err : ",err)
      return
   }
   defer listen.Close()

   for {
      accept, err := listen.Accept()
      if err != nil {
         fmt.Println("connect accept failed , err :", err)
         return
      }

      go func(conn net.Conn) {
         defer conn.Close()
         for  {
            reader := bufio.NewReader(conn)
            decode, err := protocol.Decode(reader)
            if err != nil {
               return
            }
            fmt.Println("received data : ",decode)
         }

      }(accept)

   }
}
```

##### UDP协议

UDP协议 user datagram protocol中文名称是用户数据报协议，是OSI open system interconnection ， 开放式系统互联，参考模型中一种无连接的传输层协议，不需要建立连接就能直接进行数据发送和接收，属于不可靠的，没有时序的通信，但是UDP协议的实时性比较好，通常用于视频直播相关领域

##### UDP服务端

server

```go
package main

import (
   "fmt"
   "net"
   "strings"
)

func main() {
   udp, err := net.ListenUDP("udp",&net.UDPAddr{
      IP:   net.IPv4(127,0,0,1),
      Port: 40000,
   })
   if err != nil {
      fmt.Println("listen failed , error : ",err)
      return 
   }
   //不需要建立链接，直接收发数据
   var b [1024]byte
   defer udp.Close()
   for  {
      n, addr, err := udp.ReadFromUDP(b[:])
      if err != nil {
         fmt.Println("read from udp failed , err: " , err)
         return
      }

      fmt.Println(b[:n])
      reply:=strings.ToUpper(string(b[:n]))
      //发送数据
      udp.WriteToUDP([]byte(reply),addr)
   }

}
```

client

```go
package main

import (
   "bufio"
   "fmt"
   "net"
   "os"
)

func main() {
   //UDP client
   socket, err := net.DialUDP("udp",nil,&net.UDPAddr{
      IP:   net.IPv4(127, 0, 0, 1),
      Port: 40000,
   })
   if err != nil {
      fmt.Println("dial failed , error : ",err)
      return
   }

   defer  socket.Close()
   reader := bufio.NewReader(os.Stdin)
   var reply [1024]byte
   for {
      readString, err := reader.ReadString('\n')
      if err != nil {
         return
      }
      socket.Write([]byte(readString))
      //收回复的数据
      n, adder, err := socket.ReadFromUDP(reply[:])
      if err != nil {
         return
      }
      fmt.Println("received data: ,addr :    ",string(reply[:n]),adder)
   }

}
```

#### day09

日志收集项目

gin框架和微服务

docker和k8s

#### 今日分享

注释/日志/单元测试

#### 今日内容

context

单元测试

pprof调试工具

#### 内容回顾

##### 互斥锁

sync.mutex

是一个结构体 是值类型 。给函数传参数的时候要传指针

lock 和 unlock

##### 为什么要用锁

防止同一时刻多个goroutine操作同一资源

##### 读写互斥锁

适用于读多写少的场景下,才能提高程序的执行效率

特点:

1. 如果是读的人来获取的是读锁,后续的goroutine能读不能写
2. 如果是写的goroutine来了,获取的是写锁,后续的goroutine不管是读还是写,都要等待获取锁

rwlock.rlock()

rwlock.wlock()

rwlock.lock()

rwlock.unlock()

##### 等待组

sync.waitgroup

用来等goroutine执行完再继续

是一个结构体,是值类型,给函数传参数的时候要传指针

wg.add()

wg.done()

wg.wait()

##### sync.Once

使用场景

某些函数只需要执行一次的时候，就可以使用sync.once

once.Do(func ( ) )

接收无参数无返回值的函数参数

##### sync.Map

使用场景

并发操作一个map的时候，内置的map不是并发安全的

使用，是一个开箱即用的(不需要make）并发安全的map

var map sync.Map

load() 

store()

loadorstore()

delete()

range()

##### 原子操作

go语言内置了一些针对内置的基本数据类型的一些并发安全的操作

```go
var i int64 =10
atomic.addint64(&i,1)
```

##### 网络编程

##### 互联网协议

OIS七层模型

应用层 表示层  会话层 传输层 网络层 数据链路层 物理层

#### HTTP客户端和服务端

go语言内置的net/http包提供了http客户端和服务端的实现

##### HTTP协议

超文本传输协议HTTP hypertext transfer protocol 是互联网上应用最为广泛的一种网络传输协议，所有www文件都必须遵守这个标准。设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。

##### HTTP客户端

使用net / http 包编写一个简单的发送HTTP请求的client端

![image-20210817000221229](Go语言学习.assets/image-20210817000221229.png)

HTTP：超文本传输协议

规定了：浏览器和网站服务器之间通信的规则

HTML：超文本标记语言

学的就是标记的符号、标签

CSS：层叠样式表

规定了HTML中标签的具体样式（颜色、背景、大小、位置、浮动...）

JS：一种跑在浏览器上的编程语言

http_server

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

//net / http server
func main() {
	http.HandleFunc("/posts/go/15_socket/",f1)
	http.HandleFunc("/xxx/",f2)
	http.ListenAndServe("127.0.0.1:9090",nil)
}

func f2(writer http.ResponseWriter, request *http.Request) {
	//对于get请求 参数都放在URL上 （query param）请求体中是没有数据的
	fmt.Println(request.URL)
	fmt.Println(request.Method)
	fmt.Println(ioutil.ReadAll(request.Body))
	writer.Write([]byte("ok!"))

	queryParam :=request.URL.Query()
	fmt.Println(queryParam)
	name:=queryParam.Get("name")
	fmt.Println(name)
	age:=queryParam.Get("age")
	fmt.Println(age)
}
func f1(w http.ResponseWriter, r *http.Request) {
	file, err := ioutil.ReadFile("./xx.txt")
	if err != nil {
		w.Write([]byte(fmt.Sprintf("%v",err)))
		return
	}
	w.Write(file)
}
```

http_client

```go
package main

import (
   "fmt"
   "io/ioutil"
   "net/http"
   "net/url"
)

//net/http client
func main() {
   f1()
   f2()
   f3()
}

//构造一个client
var client= http.Client{ Transport: &http.Transport{
            DisableKeepAlives:false}}

func f3() {
   //构造参数
   urlparams := url.Values{}
   urlparams.Add("name","ljs")
   urlparams.Add("score","100")
   //构造头部
   urlParse, _ := url.ParseRequestURI("http://127.0.0.1:9090/xxx")
   //拼接url
   urlParse.RawQuery = urlparams.Encode()
   //构造一个请求 request
   request, _ := http.NewRequest("get", urlParse.String(), nil)
   response, _ := client.Do(request)
   defer response.Body.Close()
   ioutil.ReadAll(response.Body)
}

func f2() {
   //构造请求
   uri, _ := url.ParseRequestURI("http://127.0.0.1:9090/xxx")
   data:=url.Values{}
   data.Set("name","林の树")
   data.Set("age","18")
   urlStr := data.Encode()
   fmt.Println(urlStr)
   uri.RawQuery=urlStr
   fmt.Println(uri)
   request, err := http.NewRequest("Get", uri.String(), nil)
   if err != nil {
      fmt.Println("request failed ,error : ",err)
      return
   }
   //发请求
   response, err := http.DefaultClient.Do(request)
   if err != nil {
      return
   }

   defer response.Body.Close()  //一定要记得关闭resp.body
   all, err := ioutil.ReadAll(response.Body)
   if err != nil {
      return
   }
   fmt.Println(string(all))

}

func f1() {
   response, err := http.Get("http://127.0.0.1:9090/xxx?name=ljs&age=18")
   if err != nil {
      fmt.Println("get failed , error : ",err)
      return
   }
   //从response中吧服务端返回的数据读出来
   read, err := ioutil.ReadAll(response.Body)
   if err != nil {
      fmt.Println("read failed , error : ",err )
      return
   }

   fmt.Println(string(read))
}
```

http.get

http.post

http.postform

##### 单元测试

开发自己给自己的代码写测试

go语言中的测试依赖go test命令。编写测试代码和编写普通的go代码过程是类似的，并不需要学习新的语法、规则或工具。

go test命令是一个按照一定约定和组织的测试代码的驱动程序。在包目录内，所有以_test.go为后缀名的源代码文件都是go test测试的一部分，不会被go build 编译到最终的可执行文件中。

在*_test.go文件中有三种类型的函数，单元测试函数、基准测试函数和示例函数。

| 类型     | 格式                  | 作用                           |
| -------- | --------------------- | ------------------------------ |
| 测试函数 | 函数名前缀为test      | 测试程序的一些逻辑行为是否正确 |
| 基准函数 | 函数名前缀为benchmark | 测试函数的性能                 |
| 示例函数 | 函数名前缀为example   | 为文档提供实力文档             |

go test命令会遍历所有的*_test.go文件中符合上述命名规则的函数，然后生成一个临时的main包用于调用相应的测试函数，然后构建并运行、报告测试结果，最后清理测试中生成的临时文件

##### 测试函数

测试函数的格式 每个测试函数必须导入testing包，基本格式如下：

```go
func TestName (t *testing.T)
{
    
}
//testing.T拥有的方法如下
Error
Errorf
Fail
FailNow
Failed
Fatal
Fatalf
Log
Logf
Name
Parallel
Run
Skip
SkipNow
Skipf
Skipped
```

##### 测试用例和测试组和子测试

```go
package main

import (
   "fmt"
   "strings"
)
var m = make([]string,4)

//Split 切割字符串 a b c => [a c]
func Split(str ,sep string) []string {
      i:=0
      judge(str,sep,i)
      return m
}

func judge(s string,sep string,i int)  {
   if !strings.Contains(s,sep){
      return
   }

   index:=strings.Index(s,sep)
   if s[:index] != "" {
      m[i] = s[:index]
   }else {
      m[i]=s[index+1:]
   }
   if s[index+1:]!="" {
      m[i+1] = s[index+1:]
   }
   judge(m[i+1],sep,i+1)
}

func main() {
   got:=Split("abcb","b")
   fmt.Println(got)
}
```

测试用例写

```go
package main

import (
   "fmt"
   "reflect"
   "testing"
)

func TestSplit(t *testing.T) {
   got:=Split("abcb","b")
   want:=[]string{"a","c"," "}
   if !reflect.DeepEqual(got, want) {
      fmt.Println("测试用例失败")
      t.Errorf("want %v but got %v\n",want,got)
   }
}

func TestSplit2(t *testing.T) {
   got:=Split("a:b:c",":")
   want:=[]string{"a","b","c"}
   if !reflect.DeepEqual(got, want) {
      t.Errorf("want %v but got %v\n",want,got)
   }
}

//测试组
func TestSplitGroup(t *testing.T) {
   type TestCase struct {
      str string
      sep string
      got string
      want []string
   }
   testCase :=[]TestCase{
      {
         str:  "abcb",
         sep:  "b",
         want: []string{"a","c",""},
      },
      {
         str:"a:b:c",
         sep: ":",
         want:[]string{"a","b","c"},
      },
   }
   for _, v := range testCase {
      if !reflect.DeepEqual(Split(v.str,v.sep),v.want){
         t.Errorf("want %v but got %v\n",v.want,Split(v.str,v.sep))
      }
   }
}

func TestSingle(t *testing.T) {
   type TestCase struct {
      str string
      sep string
      got string
      want []string
   }
   testCase:=map[string]TestCase{
      "case1":{
         str:  "abcb",
         sep:  "b",
         want: []string{"a","c",""},
      },
      "case2":{
         str:"a:b:c",
         sep: ":",
         want:[]string{"a","b","c"},
      },
   }

   for name, v := range testCase {
      t.Run(name, func(t *testing.T) {
         got:=Split(v.str,v.sep)
         if !reflect.DeepEqual(got, v.want) {
            t.Errorf("want %v but got %v\n",v.want,got)
         }
      })
   }
}
```

```shell
尝试新的跨平台 PowerShell https://aka.ms/pscore6

PS E:\project\GOproject\src\code.oldboyedu.com\day9\02splitString> go test -run=TestSingle/case2
--- FAIL: TestSingle (0.00s)
    --- FAIL: TestSingle/case2 (0.00s)
        split_test.go:77: want [a b c] but got [a b c ]
FAIL
exit status 1
FAIL    src/code.oldboyedu.com/day9/02splitString       0.240s
```

##### 测试覆盖率

go test -cover

函数覆盖率100%

代码覆盖率60%

##### 基准测试

基准测试就是在一定的工作负载之下检测程序性能的一种方法。基准测试的基本格式如下：

func BenchName(b *testing.B)

![image-20210818211645228](Go语言学习.assets/image-20210818211645228.png)

##### 性能比较测试

默认情况下每个基准测试至少运行1s，如果在benchmark函数 返回时没有到1s，则b.N的值会按1,2,5,50...增加,并且函数再次运行

可以指定benchtime

##### 重置时间

b.ResetTimer之前的处理不会放到执行时间里，也不会输出到报告中，所以可以在之前做一些不计划作为测试报告的操作。

##### 并行测试

runparallel会以并行的方式执行给定的基准测试

可以调用setparallelism来确定cpu核数

##### setUp和teardown

测试程序有时需要在测试之前进行额外的设置setup或者在测试之后进行拆卸teardown

##### 示例函数

ExampleName

#####  prof调试工具

go语言项目中的性能优化主要有以下几个方面：

- CPU profile：报告程序的CPU使用情况，按照一定频率去采集应用程序在CPU和寄存器上面的数据
- Memory Profile (Heap Profile) :报告程序的内存使用情况
- Block Profiling: 报告goroutines不在运行状态的情况，可以用来分析和查找死锁等性能瓶颈
- Goroutine Profiling:报告goroutines的使用情况，有那些goroutine，她们的调用关系是怎么样的

##### 采集性能数据

go语言内置了获取程序的运行数据的工具，包括一下两个标准库

- runtime/pprof:采集工具型应用运行数据进行分析
- net/http/pprof:采集服务型应用运行时数据进行分析

pprof开机后，每个一段时间10ms就会收集当前的堆栈信息，获取各个函数占用的cpu以及内存资源；最后通过对这些采样数据进行分析，形成一个性能分析报告。

注意，我们只应该在性能测试的时候才在代码中引入pprof

##### CPU性能分析

pprof.StartCPUProfile(w io.Writer)

pprof.stopCPUPorfile()

应用执行结束后，就会生成一个文件，保存了我们的CPUprofiling数据。得到采样数据之后，使用go tool pprof工具进行CPU性能分析

等待30s

##### 内存性能优化

pprof.WriteHeapProfile(w io.Writer)

```go
package main

import (
   "flag"
   "fmt"
   "os"
   "runtime/pprof"
   "time"
)

func main() {
   var isCPUPprof bool  //是否开启cpuprofile标志位
   var isMemPprof bool    //是否开启内存profile标志位

   flag.BoolVar(&isCPUPprof,"cpu",false,"turn cpu pprof on")
   flag.BoolVar(&isMemPprof,"mem",false,"turn mem pprof on")
   flag.Parse()

   if isCPUPprof {
      create, err := os.Create("./cpu.pprof")
      if err != nil {
         fmt.Println("create file failed , error : ",err)
         return
      }
      pprof.StartCPUProfile(create)  //往文件中记录cpu profile信息
      defer create.Close()
      defer pprof.StopCPUProfile()
   }

   for i := 0; i < 6; i++ {
      go logicCode()
   }

   time.Sleep(20*time.Second)
   if isMemPprof{
      create, err := os.Create("./mem.pprof")
      if err != nil {
         fmt.Println("create file failed , error : ",err)
         return
      }
      pprof.WriteHeapProfile(create)
      defer create.Close()
   }
}

func logicCode() {
   var c chan int //nil
   for {
      select {
         case v:=<-c: //阻塞
            fmt.Printf("received from chan , value : %v\n",v)
      default:
            time.Sleep(time.Millisecond*500)
      }
   }
}
```

##### 命令行交互界面

使用go工具链里的pprof来分析一下

##### 服务型应用

##### flag

通过flag.string or flag.stringvar 定义好命令行flag参数后，需要通过调用flag.parse()来对命令行参数进行解析

支持的命令行参数格式有以下几种

- -flage xxx
- --flag xxx
- -flag=xxx
- --flag=xxx

其中，布尔类型的参数必须使用等号方式指定

flag解析在第一个非flag参数之前停止 或者在终止符-之后停止

```go
package main

import (
   "flag"
   "fmt"
   "time"
)

//flag 获取命令行参数
func main() {
   //创建一个标志位参数flag
   name :=flag.String("name","ljs","请输入名字")
   age :=flag.Int("age",100,"请输入年龄")
   married :=flag.Bool("married",false,"结婚了么")
   cTime:=flag.Duration("duration",time.Second,"有多快")
   //使用flag
   //flag.Parse()
   fmt.Println(*name)
   fmt.Println(*age)
   fmt.Println(*married)
   fmt.Println(*cTime)

   var name1 string
   flag.StringVar(&name1,"name1","name1","请输入name1")
   flag.Parse()
   fmt.Println(name1)

   fmt.Println(flag.NArg())  //返回除了规定的参数之外的命令行参数有几个
   fmt.Println(flag.NFlag())  //返回规定的flag命令行参数有几个
   fmt.Println(flag.Args())   //返回除了规定的参数之外的命令行参数具体是

}
```

##### 面试题

![image-20210819001237778](Go语言学习.assets/image-20210819001237778.png)



##### 本周复习

两个面试题

leetcode刷题每天一道题

数据结构和算法很重要，要找机会抓紧补上

##### 内容回顾

##### net/http包的用法

如何发请求

当需要频繁发送请求的时候（每5s从阿里云接口同步数据）：定义一个全局的client，后续发请求的操作都使用这个全局的client

##### 单元测试

xxx/ccc.go

单元测试的文件名必须是xxx/ccc_test.go

go内置的单元测试工具：

```go
go test
```

单元测试函数

```go
//Test开头后接函数名
func TestSplit(t *testing.T)
{
    
}
```

##### 性能测试/基准测试

函数格式

```go
func BenchmarkSplit(b *testing.B)
{
    //b.N:被测试函数执行的次数
}
```

执行命令：

```go
go test -bench=Split -v
```

##### 并行测试

##### setup和teardown

##### pprof

记录cpu和内存的快照信息

##### flag标准库

os.Args

flag.stringvar()返回的是一个指针变量

必须调用flag.parse()

```bash
./xxx -name = "lsj" -age=90
```

flag.args

flag.nargs

flag.nflag

#### 今日内容

Mysql：主流的关系型数据库 类似的还有postgreSQL

redis：kv数据库

nsq:go语言开发的分布式消息队列

包的依赖管理go module     go1.1之后官方出的依赖管理工具

##### MySql

数据库

常见的数据库：oracle sqlite文件数据库 mysql sqlserver

关系型数据库：用表来存一类数据

表结构设计的三大范式《漫画数据库》 

mysql知识点

sql语句：结构化查询语言

##### 存储引擎

mysql支持插件式的存储引擎

常见的存储引擎：myisam、innodb

myisam：

- 查询速度快
- 只支持表锁
- 不支持事务

innodb：

- 整体速度快
- 支持表锁和行锁
- 支持事务

事务：把多个操作当成一个整体

事务的特点：

ACID

- 原子性：事务要么成功，要么失败，没有中间状态
- 一致性：数据库的完整性没有被破坏
- 持久性：事务操作的结果是不会被丢失的
- 隔离性：事务之间是相互隔离的
  - 隔离级别
    - 读未提交
    - 读提交
    - 可重复读
    - 串行化

##### 索引

索引的原理是：B树和B+树

索引类型：

索引的命中

分库分表

SQL注入

SQL慢查询优化

Mysql主从：binlog

Mysql读写分离

##### Go操作MySql

##### 连接

go语言中的database/sql包提供了保证SQL或类SQL数据库的泛用接口，并不提供具体的数据库驱动。使用database/sql包时必须注入至少一个数据库驱动。

我们常用的数据库基本上都有完整的第三方实现。

##### database/sql

原生支持连接池，是并发安全的

这个标准库没有具体实现，只是列出了一些需要第三方库实现的具体内容。

##### 下载依赖

go get -u github.com/go-sql-driver/mysql

##### 使用Mysql驱动

func Open(driverName , dataSourceName string)(*DB , error)

open一个drivername指定的数据库，datasourcename指定数据源，一般包至少包括

![image-20210820105514841](Go语言学习.assets/image-20210820105514841.png)

go get包的路径就是下载第三方的依赖

将第三方的依赖默认保存在$gopath/src/

##### 使用驱动

```go
package main

import (
   "database/sql"
   "fmt"
   _ "github.com/go-sql-driver/mysql"
   "log"
)

func main() {
   //go连接mysql实例
   //数据库源信息
   dsn:="root:123456@tcp(127.0.0.1:3306)/tset"
   //连接数据库
   db, err := sql.Open("mysql", dsn) //不会校验用户名和密码是否正确
   if err != nil {
      log.Printf("dsn %s invalid , err : %v\n",dsn,db)
      return
   }
   err = db.Ping()
   if err != nil {
      log.Printf("open %s failed , err : %v\n",dsn , err)
      return 
   }
   fmt.Println(db,"连接数据库成功!")

}
```

github上的mysql驱动如何关联到database/sql这个包里呢？

![image-20210820123021805](Go语言学习.assets/image-20210820123021805.png)

##### 单行查询

单行查询db.queryrow()执行一次查询，并期望返回最多一行结果row。queryrow总是返回非nil值，直到返回值的scan方法被调用时，才会返回被延迟的错误（如未找到）

##### setmaxopenconns方法

设置与数据库连接池的最大连接数

##### setmaxidleconns方法

setmaxidleconnes设置连接池中的最大闲置连接数。如果n大于最大开启连接数，则新的最大闲置连接数会减小到匹配最大开启连接数的限制。如果n<=0 不会保留闲置连接

##### 多行查询

多行查询db.query()执行一次查询，返回多行结果（rows），一般用于执行select命令。参数args表示query中的占位参数

##### 插入数据

插入、更新和删除操作都使用方法 Exec

删除也是一样的

##### MySQL预处理

##### 什么是预处理

普通sql语句执行过程:

1. 客户端对SQL语句进行占位符替换得到完整的SQL语句
2. 客户端发送完整的SQL语句到MySQL服务端
3. mysql服务端执行完整的sql语句并将结果返回给客户端

预处理执行过程:

1. 把sql语句分成两部分,命令部分与数据部分
2. 先把命令部分发送给mysql服务端,mysql服务端进行sql预处理
3. 然后吧数据部分发送给mysql服务端,mysql服务端对sql语句进行占位符替换
4. mysql服务端执行完整的sql语句并将结果返回给客户端

##### 为什么要预处理

1.优化mysql服务器重复执行sql的方法,可以提升服务器性能,提前让服务器编译,一次编译多次执行,节省后续编译的成本

2.避免sql注入的问题

##### go实现mysql预处理

prepare方法会先将sql语句发送给mysql服务端,返回一个准备好的状态用于之后的查询和命令.返回值可以同时执行多个查询和命令

```go
package main

import (
   "database/sql"
   "fmt"
   _ "github.com/go-sql-driver/mysql"
   "log"
)

type student struct {
   sno ,sname,ssex string
   sage int
}
var db *sql.DB //是一个连接池对象
func main() {

   initDB()
   //queryOne("2016210867")
   //queryMany()
   //insert()
   //update()
   prepareSelect()
}
func initDB() (err error) {
   dsn:="root:123456@tcp(127.0.0.1:3306)/tset"
   db,err =sql.Open("mysql",dsn)
   if err != nil {
      log.Printf("dsn %s is invalid , error : %v\n",dsn,err)
   }

   err = db.Ping()
   if err != nil {
      log.Printf("open %s failed , err : %v\n",dsn,err)
      return err
   }
   //设置数据库连接池最大连接数  如果超过了就会阻塞等待其他的程序
   db.SetMaxOpenConns(10)
   //最大空闲连接数
   db.SetMaxIdleConns(5)
   return nil
}
func queryOne(sno string) {
   var s student
   //查找
   row := db.QueryRow("select * from student where sno = ?",sno) //从连接池中拿一个连接出来去数据库查询单挑记录
   //扫描+释放连接  必须对rowobj调用scan方法
   row.Scan(&s.sno,&s.sname,&s.ssex,&s.sage)

   var sname string
   db.QueryRow("select sname from student where sno = ?",sno).Scan(&sname)
   fmt.Printf("student: %v \n",s)
   fmt.Println(sname)
}
func queryMany()  {
   rows, err := db.Query("select sno , sname , ssex , sage from student ")
   if err != nil {
      fmt.Println("db query failed , error : %v\n",err)
      return
   }
   //非常重要 一定要关闭rows
   defer rows.Close()
   //循环取值
   for rows.Next(){
      var s student
      rows.Scan(&s.sno,&s.sname,&s.ssex,&s.sage)
      fmt.Println(s)
   }

}

func insert() {
   sql:="insert into student values ('2020170281','ljs','man',23)"
   exec, err := db.Exec(sql)
   if err != nil {
      fmt.Println("exec insert %s failed , err : %v\n",sql,err)
      return
   }
   //如果是插入数据的操作,能够拿到插入数据的id
   id, err := exec.LastInsertId()
   if err != nil {
      fmt.Println("get id failed ,err : %v\n", err)
      return
   }
   fmt.Println("id:",id)
}

func update() {
   exec, err := db.Exec("update student set sname = 'ljsnew' where sno='2020170281' ")
   if err != nil {
      fmt.Println(err)
      return
   }
   fmt.Println(exec.RowsAffected())
}

//预处理方式select多条数据
func prepareSelect() {
   prepare, err := db.Prepare("select * from student where sno like ? ")//吧sql语句先发给mysql预处理一下
   if err != nil {
      return
   }

   rows, err := prepare.Query("%2016%") //后续只需要传值就行了
   if err != nil {
      return
   }

   defer prepare.Close()
   defer rows.Close()
   for rows.Next
    () {
      var s student
      rows.Scan(&s.sno,&s.sname,&s.ssex,&s.sage)
      fmt.Println(s)
   }
}
```

##### go语言实现mysql事务

事务相关方法:begin / commit /  rollback

##### sqlx使用

第三方库 sqlx 能够简化操作,提高开发效率

安装 go get github.com/jmoiron/sqlx

##### 注意事项

##### SQL中的占位符

不同数据库中,SQL语句使用的占位符语法不尽相同

| 数据库     | 占位符语法 |
| ---------- | ---------- |
| Mysql      | ?          |
| postgresql | $1,$2      |
| sqlite     | ?和$1      |
| oracle     | :name      |

##### sql注入

我们任何时候都不应该自己拼接sql语句

```go
package main

import (
   "fmt"
   _"github.com/go-sql-driver/mysql"
   "github.com/jmoiron/sqlx"
)

func main() {
   sqlInjectDemo("xxx'or 1=1#")
   sqlInjectDemo("xxx' union select * from student #")
}
var db *sqlx.DB
type student struct {
   SNO , SNAME , SSEX string
   SAGE int
}
func sqlInjectDemo(name string) {
   //自己拼接sql语句
   sqlStr:=fmt.Sprintf("select * from student where sname ='%s'",name)
   fmt.Println(sqlStr)

   var err error
   db, err = sqlx.Connect("mysql", "root:123456@tcp(127.0.0.1:3306)/tset")
   if err != nil {
      fmt.Println(err)
      return
   }

   err = db.Ping()
   if err != nil {
      fmt.Println(err)
      return
   }

   var s []student
   err = db.Select(&s, sqlStr)
   if err != nil {
      fmt.Println(err)
      return
   }

   fmt.Println(s)
}
```

![image-20210820163242826](Go语言学习.assets/image-20210820163242826.png)

##### redis

kv数据库

redis的用处

1. cache缓存
2. 简单的队列
3. 排行榜

redis是一个开源的内存数据库,redis提供了多种不同类型的数据结构,很多业务场景下的问题都可以很自然地映射到这些数据结构上.除此之外,通过复制/持久化和客户端分片等特性,我们可以很方便的将redis扩展成为一个能够包含数百GB数据/每秒处理上百万次请求的系统

##### redis支持的数据结构

redis支持诸如字符串strings 哈希hashes 列表lists 集合sets 带范围查询的排序集合 sorted sets 位图bitmaps hyperloglogs 带半径查询和流的地理空间索引等数据结构 geospatial indexes

##### redis应用场景

- 缓存系统,减轻主数据库mysql的压力
- 计数场景,比如微博/抖音中的关注数和粉丝数
- 热门排行榜,需要排序的场景特别适合使用zset
- 利用list可以实现队列的功能

##### redis与memcached比较

memcache中的值只支持简单的字符串,redis支持更丰富的5种数据结构类型.redis的性能比memcache好很多.redis支持rdb持久化和aof持久化.redis支持master/slave模式

##### 安装

go语言中使用第三方库连接redis数据库并进行操作.使用以下命令下载并安装

go get -u github.com/go-redis/redis

##### get和set

##### zset

```go
package main

import (
   "fmt"
   "github.com/go-redis/redis"
)

var redisDb *redis.Client
func main() {
   err := initRedis()
   if err != nil {
      fmt.Println(err)
      return
   }

   fmt.Println("连接redis成功")

   redisExample()
   redisExample2()
}

func initRedis() (err error) {
   redisDb = redis.NewClient(&redis.Options{
      Addr:     "127.0.0.1:6379",
      Password: "",
      DB:       0,
   })

   result, err := redisDb.Ping().Result()
   if err != nil {
      return err
   }

   fmt.Println(result)
   return
}

func redisExample() {
   err := redisDb.Set("score", 100, 0).Err()
   if err != nil {
      fmt.Println(err)
      return
   }

   val1, err := redisDb.Get("score").Result()
   if err != nil {
      return
   }

   fmt.Println("scoer",val1)

   val2, err := redisDb.Get("name").Result()
   if err == redis.Nil {
      fmt.Println("name does not exist")
   } else if err != nil {
      fmt.Println(err)
      return 
   }else {
      fmt.Println(val2)
   }
}

func redisExample2() {
   //zset
   key:="rank"
   items:=[]redis.Z{
      redis.Z{
         Score:  99,
         Member: "php",
      },
      redis.Z{
         Score:  96,
         Member: "golang",
      },
      redis.Z{
         Score: 97,
         Member: "python",
      },
      redis.Z{
         Score:  99,
         Member: "java",
      },
   }
   fmt.Println(items)
   //把元素都追加到key中
   num, err := redisDb.ZAdd(key,items...).Result()
   if err != nil {
      return
   }
   fmt.Println(num)

   //加分数
   newScore, err := redisDb.ZIncrBy(key, -1, "java").Result()
   if err != nil {
      return
   }
   fmt.Println(newScore)


   //取分数最高的
   scoreList, err := redisDb.ZRevRangeWithScores(key,0,3).Result()
   if err != nil {
      return
   }
   for _, z := range scoreList {
      fmt.Println(z.Member,z.Score)
   }

   //取95到100分的
   option := &redis.ZRangeBy{
      Min: "95",
      Max: "100",
   }
   ret, err := redisDb.ZRangeByScoreWithScores(key,*option).Result()
   if err != nil {
      return 
   }
   for _, z := range ret {
      fmt.Println(z.Member,z.Score)
   }
}
```

##### NSQ

NSQ是目前比较流行的一个分布式的消息队列,本文主要介绍了NSQ及go语言如何操作NSQ

##### NSQ介绍

NSQ是go语言编写的一个开源的实时分布式内存消息队列,其性能十分优异.NSQ的优势有:

1. NSQ提倡分布式和分散的拓扑,没有单点故障,支持容错和高可用性,并提供可靠的消息交付保证
2. NSQ支持横向扩展,没有任何集中式代理
3. NSQ易于配置和部署,并且内置了管理界面

##### NSQ的应用场景

通常来说,消息队列都适用于以下场景

##### 异步处理

利用消息队列把业务流程中的非关键流程异步化,从而显著降低业务请求的响应时间

![image-20210820235216910](Go语言学习.assets/image-20210820235216910.png)

##### 应用解耦

通过使用消息队列将不同的业务逻辑解耦,降低系统间的耦合,提高系统的健壮性.后续有其他业务要使用订单数据可直接订阅消息队列,提高系统的灵活性

![image-20210820235428939](Go语言学习.assets/image-20210820235428939.png)

##### 流量削峰

类似秒杀等场景下,某一时间可能会产生大量的请求,使用消息队列能够为后端处理请求提供一定的缓冲区,保证后端服务的稳定性

![image-20210820235659875](Go语言学习.assets/image-20210820235659875.png)

##### NSQ组件

##### nsqd

nsqd是一个守护进程,它接收/排队并向客户端发送消息

启动nsqd,指定-broadcast-address=127.0.0.1来配置广播地址

如果是在搭配nsqdlookupd使用的模式下还需要指定nsqdlookupd地址

如果是部署了多个nsqlookupd节点的集群,那还可以指定多个-lookupd-tcp-address

##### nsqlookupd

nsqlookupd是维护所有nsqd状态/提供服务发现的守护进程.他能为消费者查找特定topic下的nsqd提供了运行时的自动发现服务.他不是维持持久状态,也不需要与任何其他的nsqdlookupd实例协调以满足查询.因此根据系统的冗余要求尽可能多地部署nsqlookupd节点.她们消耗的资源很少,可以与其他服务共存,我们的建议是为每个数据中心运行至少三个集群

nsqadmin

一个实时监控集群状态/执行各种管理任务的web管理平台,启动nsqdadmin,指定nsqlookupd地址

我们可以使用浏览器打开http://127.0.0.1:4171访问管理界面

![image-20210821104437565](Go语言学习.assets/image-20210821104437565.png)

##### topic和channel

每个nsqd实例旨在一次处理多个数据流.这些数据流成为topics,一个topic具有一个或者多个channels,每个channel都会收到topic所有消息的副本,实际上上下游的服务是通过对应的channel来消费topic消息

topic和channel不是预先设置的.topic在首次使用时创建,方法是将其发布到指定topic,或者订阅指定topic上的channel. channel是通过订阅指定的channel在第一次使用时创建的

topic和channel都互相独立地缓冲数据,防止缓慢的消费者导致其他channel的积压(同样适用于topic级别)

channel可以并且通常会连接多个客户端.假设所有连接的客户端都处于准备接收消息的状态,则每条消息将被传递到随机客户端

总而言之,消息是从topic->channel(每个channel接收该topic的所有消息的副本) 多播的,但是从channel->consumers均匀分布(每个消费者接收到该channel的一部分消息)

![image-20210821105522944](Go语言学习.assets/image-20210821105522944.png)

![image-20210821105528935](Go语言学习.assets/image-20210821105528935.png)

##### NSQ特性

- 消息默认不持久化,可以配置成持久化模式. nsq采用的方式是内存+硬盘的模式,当内存达到一定程度时就会将数据持久化到硬盘上.
  -  如果将 --mem-queue-size 设置为0
  - 服务器重启时也会将当时在内存中的消息持久化
- 每条消息至少传递一次
- 消息不保证有序

##### go操作nsq



##### day11课上笔记

##### 今日内容

##### 依赖管理go module

##### context

##### 服务端agent开发

##### 日志项目架构设计

##### kafka和zookeeper

##### tailf介绍



##### 为什么需要依赖管理 

最早的时候,go所依赖的所有第三方库 放在gopath这个目录下面.这就导致了同一个库只能保存一个版本的代码.如果不同的项目依赖同一个第三方的库的不同版本,应该怎么解决

##### godep

go语言从v1.5开始引入vendor模式,如果项目目录下有vendor目录,那么go工具链会优先使用vendor内的包进行编译/测试 等等

godep是一个通过vendor模式实现的go语言的第三方依赖管理工具,类似的还有由社区维护准官方包管理工具dep

##### go module

go1.11之后退出的官方版本管理工具,从go1.13版本开始,go module将是go语言默认的依赖管理工具

go111module

要启用go module 支持首先要设置环境变量 go111module,通过他可以开启和关闭模块支持,他可以有三个可选值:

off on auto 默认值是auto

off就是禁用模块支持,编译时会从gopath和vendor文件夹中查找包

on就是启用模块支持,编译时会忽略gopath和vendor文件夹,只根据go.mod下载依赖

auto就是当gopath外有go.mod文件时,开启模块支持

简单来说,设置on之后就可以使用go module了

使用go module管理依赖后会在项目根目录下生成两个文件go.mod和go.sum

##### goproxy

go1.11之后设置goproxy命令,由于国内无法访问,所以建议设置goproxy

##### go mod命令

```go
go mod download
go mod edit
go mod graph 
go mod init
go mod tidy
go mod vendor
go mod verify
go mod why
```

##### go.mod

go.mod文件记录了项目所有的依赖信息,其结构大致如下

其中:

- module用来定义包名
- require用来定义依赖包及版本
- indirect表示简介引用

##### go.sum

详细包和版本信息

##### go get

下载依赖包,并且还可以指定下载的版本 

##### go mod edit

因为我们可以手动修改go.mod文件,所以有时候需要格式化该文件/添加依赖项/移除依赖项

##### 在项目中使用go module

##### 既有项目

如果需要对一个已经存在的项目启用go module,可以按照以下步骤

1. 在项目目录下执行go mod init , 生成一个go.mod文件
2. 执行go get , 查找并记录当前项目的依赖,同时生成一个go. sum记录每个依赖库的版本和哈希值

##### 新项目

1. 执行go mod init 项目名 , 在当前项目文件夹下创建一个go.mod文件
2. 手动编辑go.mod中的require依赖项或执行go get自动发现/维护依赖

##### context

非常重要!!!

如何优雅的控制子goroutine退出

在go http包的server中,每一个请求在都有一个对应的goroutine去处理,请求处理函数通常会启动额外的goroutine用来访问后端服务,比如数据库和rpc服务.用来处理一个请求的goroutine,通常需要访问一些与请求特定的数据,比如终端用户的身份认证信息/验证相关的token/请求的截止时间.当一个请求被取消或超时时,所有用来处理该请求的goroutine都应该迅速退出,然后系统才能释放这些goroutine占用的资源

##### 使用全局变量

```go
package main

import (
   "fmt"
   "sync"
   "time"
)
//第一种就是通过全局变量 来控制goroutine退出
var notify bool
var wg sync.WaitGroup
//为什么需要context
func main() {
   wg.Add(1)
   go f()
   //如何通知子goroutine退出
   time.Sleep(time.Second)
   notify=true
   wg.Wait()
}

func f() {
   defer wg.Done()
   for !notify {
      fmt.Println("ljs")
      time.Sleep(time.Millisecond*500)
   }

}
```

##### 使用通道

```go
package main

import (
   "fmt"
   "sync"
   "time"
)
var i  = make(chan bool,1)
var wg sync.WaitGroup
//为什么需要context
func main() {
   wg.Add(1)
   go f()
   //如何通知子goroutine退出
   time.Sleep(time.Second)
   i<-true
   wg.Wait()
}

func f() {
   defer wg.Done()
   LOOP:
   for {
      fmt.Println("ljs")
      time.Sleep(time.Millisecond*500)
      select {
         case <-i:
            break LOOP
      default:

      }
   }
}
```

##### 使用context

```go
package main

import (
   "context"
   "fmt"
   "sync"
   "time"
)
var wg sync.WaitGroup

func main() {

   ctx, cancel := context.WithCancel(context.Background())
   wg.Add(2)
   go f(ctx)
   //如何通知子goroutine退出
   time.Sleep(time.Second)
   //通知子goroutine退出
   cancel()
   wg.Wait()

}

func f(ctx context.Context) {
   defer wg.Done()
   go f2(ctx)
   LOOP:
   for  {
      fmt.Println("ljs")
      time.Sleep(time.Millisecond*500)
      select {
         case <-ctx.Done():
            break LOOP
      default:
      }
   }
}

func f2(ctx context.Context) {
   defer wg.Done()
   LOOP:
   for {
      fmt.Println("jwt")
      time.Sleep(time.Millisecond*250)
      select {
         case<-ctx.Done():
            break LOOP
      default:
      }
   }
}
```

##### context初识

go1.7加入了一个新的标准库context,他定义了context类型,专门用来简化对于处理单个请求的多个goroutine之间与请求域的数据/取消信号/截止时间等相关操作,这些操作可能涉及多个api调用

对服务器传入的请求应该创建上下文,而对服务器的传出调用应该接受上下文.她们之间的函数调用链必须传递上下文,或者可以使用withcancle/withdeadline/withtimeout或withvalue创建的派生上下文,当一个上下文被取消时,他派生的所有上下文也被取消

其中:

- deadline方法需要返回当前context被取消的时间,也就是完成工作的截至时间(deadline)
- done方法需要返回一个channel,这个channel会在当前工作完成或者上下文被取消之后关闭,多次调用done方法会返回同一个channel
- err方法会返回当前context结束的原因,他只会在done返回的channel被关闭时才会返回非空的值
  - 如果当前context被取消就会返回canceled错误
  - 如果当前context超市就会返回deadlineexceeded
- value方法会从context中返回键对应的值,对于同一个上下文来说,多次调用value并传入相同的key会返回相同的结果,该方法仅用于传递跨api和进程间跟请求域的数据

##### background和todo

go内置两个函数:background和todo,这两个函数分别返回了一个实现了context接口的background和todo.我们代码中最开始都是以这两个内置的上下文对象作为最顶层的parent context,衍生出更多的子上下文对象

background主要用于main函数/初始化以及测试代码中,作为context这个树结构的最顶层的context,也就是根的context

todo,它目前还不知道具体的使用场景,如果我们不知道该使用什么context的时候,可以使用这个

background和todo本质上都是emptyctx结构体类型,是一个不可取消,没有设置截止时间,没有携带任何值的context

##### with系列函数

##### withcancel

```go
func withcancel (parent context) (ctx context , cancel cancelFunc)
```

withcancel返回带有新done通道的父节点的副本.当调用返回的cancel函数或当关闭父上下文的done通道时,将关闭返回上下文的done通道,无论先发生什么情况.

取消此上下文将释放与其关联的资源

##### withdeadline

```go
func withdeadline(parent context , deadline time.time) (context , cancelfunc)
```

返回父上下文的副本,并将deadline调整为不迟于d.如果父上下文的deadline已经早于d,则withdeadline(parent,d)在语义上等同于父上下文,当截止日过期时,当调用返回的cancel函数时,或者当父上下文的done通道关闭时,返回上下文的done通道将被关闭,以最先发生的情况为准

取消此上下文将释放与其关联的资源,因此代码应该在此上下文中运行的操作完成后立即调用cancel

##### withtimeout

withtimeout的函数签名如下

```go
func WithTimeout (parent context ,timeout time.Duration) (context , cancelfunc)
```

withtimeout返回withdeadline(parent,time.now().add(timeout))

取消此上下文将释放与其相关的资源,因此代码应该在此上下文中运行的操作完成后立即调用cancel,通常用于数据库或者网络连接的超时控制

##### withvalue

withvalue函数能够将请求作用域的数据与context对象建立关系

```go
func WithValue(parent context , key , val interface{}) context
```

withvalue 返回父节点的副本,其中与key关联的值为val

仅对api和进程间传递请求域的数据使用上下文值,而不是使用他来传递可选参数给函数

所提供的键必须是可比较的,并且不应该是string类型或任何其他内置类型,以避免使用上下文在包之间发生冲突.withvalue的用户应该为键自己定义自己的类型.为了避免在分配给interface{}时进行分配,上下文键通常使用具体类型struct{}.或者导出的上下文关键变量的静态类型应该是指针或接口

#####  go.sum文件

详细的包名和版本信息

##### 常见的命令

```go
go mod init //初始化项目
go mod tidy //检查代码里的依赖去更新go.mod文件中的依赖
go get 
go mod download
```



##### 日志收集项目

![image-20210823155422863](Go语言学习.assets/image-20210823155422863.png)

![image-20210823155631862](Go语言学习.assets/image-20210823155631862.png)

##### 组件介绍：

logagent：日志收集客户端，用来收集服务器上的日志

kafka：高吞吐量的分布式队列（linkin开发，apache顶级开源项目）

ElasticSearch：开源的搜索引擎，提供基于http restful 的web接口

kibana：开源的ES数据分析和可视化工具

hadoop：分布式计算框架，能够对大量数据进行分布式处理的平台

storm：一个免费并开源的分布式实时计算系统

##### 消息队列的通信模式

##### 点对点模式queue

消息生产者生产消息发送到queue中，然后消息消费者从queue中取出并消费消息。一条消息被消费以后，queue中就没有了，不存在重复消费。

##### 发布/订阅topic

消息生产者（发布）将消息发布到topic中，同时 有多个消息消费者（订阅）消费该消息。和点对点模式不同，发布到topic的消息会被所有订阅者消费（类似于关注了微信公众号的人都能收到推送的文章）

补充：发布订阅模式下，当发布者消息量很大时，显然单个订阅者的处理能力是不足的。实际上现实场景中是多个订阅者节点组成一个订阅组负载均衡消费topic消息即分组订阅，这样订阅者很容易实现消费能力的线性扩展。可以看成是一个topic下有多个queue，每个queue是点对点的方式，queue之间是发布订阅方式

##### kafka

apache kafka最初用来设计解决海量日志传输等问题。kafka使用scala编写。是一个分布式数据流平台，可以运行在单台服务器上，也可以在多台服务器上部署形成集群。它提供了发布和订阅功能，使用者可以发送数据到kafka中，也可以从kafka中读取数据（以便进行后续的处理）。kafka具有高吞吐量、低延迟、高容错等特点。

![image-20210823161642535](Go语言学习.assets/image-20210823161642535.png)

![image-20210823161731945](Go语言学习.assets/image-20210823161731945.png)

![image-20210823161916638](Go语言学习.assets/image-20210823161916638.png)

![image-20210823162018291](Go语言学习.assets/image-20210823162018291.png)

![image-20210823162112407](Go语言学习.assets/image-20210823162112407.png)

![image-20210823162150526](Go语言学习.assets/image-20210823162150526.png)

![image-20210823162256871](Go语言学习.assets/image-20210823162256871.png)

##### kafka

1. kafka集群的架构
   1. broker
   2. topic
   3. partition分区，把同一个topic分成不同的分区，提高负载
      1. leader：分区的主节点，boss
      2. flower：分区的从节点
   4. consumer group
2. 生产者往kafka发送数据的流程
   1. 获取集群的leader
   2. 生产者发送给leader
   3. leader落盘
   4. follower从leader拉取
   5. follower落盘回复ack
   6. leader回复生产者
3. kafka选择分区的模式
   1. 指定往哪个分区写
   2. 指定key，kafka根据key做hash然后决定写哪个分区
   3. 轮询
4. 生产者往kafka发送数据的模式
   1. 0 把数据发给leader就成功，效率最高、安全性最低
   2. 1 把数据发给leader，等待leader回ack
   3. all 把数据发给leader，follower拉取后回ack，leader再回ack，安全性最高
5. 为什么快？ 落盘的时候不是随机的而是顺序的

![image-20210823163451045](Go语言学习.assets/image-20210823163451045.png)

![image-20210823163547230](Go语言学习.assets/image-20210823163547230.png)

![image-20210823163621907](Go语言学习.assets/image-20210823163621907.png)

![image-20210823163708974](Go语言学习.assets/image-20210823163708974.png)

![image-20210823163926776](Go语言学习.assets/image-20210823163926776.png)

![image-20210823164008727](Go语言学习.assets/image-20210823164008727.png)

![image-20210823164021727](Go语言学习.assets/image-20210823164021727.png)



##### 启动zookeeper

1. 下载kafka 

2. kafka内置zookeeper

3. 修改config下zookeeper.properties配置文件![image-20210823191107893](Go语言学习.assets/image-20210823191107893.png)

4. 命令行启动zookeeper 

   ```bash
   D:\Softwares\kafka_2.12-2.8.0>bin\windows\zookeeper-server-start.bat config\zookeeper.properties
   ```

5. 修改config下kafka.properties配置文件![image-20210823192529505](Go语言学习.assets/image-20210823192529505.png)

6. 命令行启动kafka

   ```go
   D:\Softwares\kafka_2.12-2.8.0>bin\windows\kafka-server-start.bat config\server.properties
   ```

   **要用管理员身份打开命令行**



##### zookeeper

![image-20210823192857710](Go语言学习.assets/image-20210823192857710.png)

类似于consul 服务注册与发现



##### tail第三方日志库demo

tail作用 尝试读取某个log日志文件

```go
package main

import (
   "fmt"
   "github.com/nxadm/tail"
   "time"
)
func main() {
   //tail用法
   fileName:="./my.log"
   config:=tail.Config{
      Location:    &tail.SeekInfo{Offset: 0,Whence: 2}, //从文件的那个地方开始读
      ReOpen:      true, //重新打开
      MustExist:   false,    //文件不存在不报错
      Poll:        true,
      Pipe:        false,
      Follow:      true, //是否跟随
      MaxLineSize: 0,
      RateLimiter: nil,
      Logger:      nil,
   }
   tails, err := tail.TailFile(fileName, config)
   if err != nil {
      fmt.Println("tail file failed , err: ",err)
      return
   }
   var (
      line *tail.Line
      ok bool
   )

   for {
      line, ok =<-tails.Lines
      if !ok {
         fmt.Printf("tail file close reopen , filename :%s\n",tails.Filename)
         time.Sleep(time.Second)
         continue
      }
      fmt.Println("msg: ",line.Text)
   }

}
```

##### sarama第三方库demo

作用:向kafka发送消息

```go
package main

import (
   "fmt"
   "github.com/Shopify/sarama"
)
func main() {
   config := sarama.NewConfig()
   //tailf包使用
   config.Producer.RequiredAcks= sarama.WaitForAll  //发送完数据需要 leader 和 follower 都确认
   config.Producer.Partitioner = sarama.NewRandomPartitioner  //新选出一个 partitioner
   config.Producer.Return.Successes = true //成功交付的消息将在success channel 返回
   //构造一个消息
   msg:= &sarama.ProducerMessage{}
   msg.Topic = "web_log"
   msg.Value = sarama.StringEncoder("this is a test blog")
   //连接kafka
   client, err := sarama.NewSyncProducer([]string{"127.0.0.1:9092"}, config)
   if err != nil {
      fmt.Println("producer closed, err : ", err)
      return
   }
   defer client.Close()
   //发送消息
   pid, offSet, err := client.SendMessage(msg)
   if err != nil {
      fmt.Println("send msg failed , err : ", err)
      return
   }
   fmt.Printf("pid:%v offSet:%v\n",pid,offSet)

}
```

![image-20210823202230801](Go语言学习.assets/image-20210823202230801.png)

![image-20210823202240537](Go语言学习.assets/image-20210823202240537.png)

索引



##### 接下来就是日志收集项目

- 初始化sarama 让他连接上kafka 以便给kafka发送消息
- 初始化tail 让他能够读取日志文件
- 使用初始化好的sarama 将tail读取到的东西发送给kafka

kafka模块代码

```go
package kafka

import (
   "fmt"
   "github.com/Shopify/sarama"
)
//专门往kafka写日志的模块
var (
   client sarama.SyncProducer  //声明一个全局的连接kafka的生产者client
)

//Init 初始化client
func Init(address []string)(err error) {
   config := sarama.NewConfig()
   //tailf包使用
   config.Producer.RequiredAcks= sarama.WaitForAll  //发送完数据需要 leader 和 follower 都确认
   config.Producer.Partitioner = sarama.NewRandomPartitioner  //新选出一个 partitioner
   config.Producer.Return.Successes = true //成功交付的消息将在success channel 返回
   //连接kafka
   client, err = sarama.NewSyncProducer(address, config)
   if err != nil {
      fmt.Println("producer closed, err : ", err)
      return
   }
   return
}

func SendToKafka(topic, msg string) {
   //构造一个消息
   saramaMsg:= &sarama.ProducerMessage{}
   saramaMsg.Topic = topic
   saramaMsg.Value = sarama.StringEncoder(msg)
   //发送消息
   pid, offSet, err := client.SendMessage(saramaMsg)
   if err != nil {
      fmt.Println("send msg failed , err : ", err)
      return
   }
   fmt.Printf("pid:%v offSet:%v\n",pid,offSet)
}
```

tail模块代码

```go
package tail

import (
   "fmt"
   "github.com/nxadm/tail"
)
var tails *tail.Tail
//Init 专门收集日志
func Init(address string) (err error){
   //tail用法
   fileName:=address
   config:=tail.Config{
      Location:    &tail.SeekInfo{Offset: 0,Whence: 2}, //从文件的那个地方开始读
      ReOpen:      true, //重新打开
      MustExist:   false,    //文件不存在不报错
      Poll:        true,
      Pipe:        false,
      Follow:      true, //是否跟随
      MaxLineSize: 0,
      RateLimiter: nil,
      Logger:      nil,
   }
   tails, err = tail.TailFile(fileName, config)
   if err != nil {
      fmt.Println("tail file failed , err: ",err)
      return
   }
   return
}
func ReadLog() <-chan *tail.Line {
      return tails.Lines
}
```

main模块代码

```go
package main

import (
   "fmt"
   "src/code.oldboyedu.com/logAgent/kafka"
   tail "src/code.oldboyedu.com/logAgent/tail_log"
   "time"
)

func main() {

   //1.初始化kafka连接
   err := kafka.Init([]string{"127.0.0.1:9092"})
   if err != nil {
      fmt.Println("init kafka failed, err : " ,err)
      return
   }
   fmt.Println("init kafka success!")
   //2.打开日志文件准备收集日志
   err = tail.Init("./my.log")
   if err != nil {
      fmt.Println("init taillog failed, err : ",err)
      return
   }
   fmt.Println("init tail success!")

   run()

}

func run() {
   //1.收集日志
   for  {
      select {
      case line:=<-tail.ReadLog():
         //2.发送给kafka
         kafka.SendToKafka("web_log",line.Text)
      default:
         time.Sleep(time.Second)
      }
   }

}
```

定义消费者

```bash
bin\windows\kafka-console-consumer.bat --bootstrap-server=127.0.0.1:9092 --topic=web_log --from-beginning
```

![image-20210823210549292](Go语言学习.assets/image-20210823210549292.png)



优化版配置文件中读取

```go
package main

import (
   "fmt"
   "gopkg.in/ini.v1"
   "src/code.oldboyedu.com/logAgent/kafka"
   tail "src/code.oldboyedu.com/logAgent/tail_log"
   "time"
)

type appConf struct {
   KafkaConf `ini:"Kafka"`
   TailLogConf `ini:"Taillog"`
}
type KafkaConf struct {
   Address string `ini:"Address"`
   Topic string `ini:"Topic"`
}

type TailLogConf struct {
   FileName string `ini:"Filename"`
}

var appCfg =new(appConf)

func main() {
   //0.加载配置文件 获取ip:端口 日志文件 发送的topic
   err := ini.MapTo(appCfg, "./config.ini")
   if err != nil {
      fmt.Println("config init failed, err : ",err)
      return
   }

   //1.初始化kafka连接
   fmt.Println(appCfg.KafkaConf.Address)
   fmt.Println(appCfg.KafkaConf.Topic)
   fmt.Println(appCfg.TailLogConf.FileName)
   err = kafka.Init([]string{appCfg.KafkaConf.Address})
   if err != nil {
      fmt.Println("init kafka failed, err : " ,err)
      return
   }
   fmt.Println("init kafka success!")
   //2.打开日志文件准备收集日志
   err = tail.Init(appCfg.TailLogConf.FileName)
   if err != nil {
      fmt.Println("init taillog failed, err : ",err)
      return
   }
   fmt.Println("init tail success!")

   run()

}


func run() {
   //1.收集日志
   for  {
      select {
      case line:=<-tail.ReadLog():
         //2.发送给kafka
         kafka.SendToKafka(appCfg.KafkaConf.Topic,line.Text)
      default:
         time.Sleep(time.Second)
      }
   }

}
```

##### 内容复习

##### go module

依赖管理工具

##### context

goroutine管理

`context.Context`

两个根节点 context.todo context.background

四个方法 context.withTimeout() context.withCancel() context.withdeadline() context.withvalue()

##### 日志收集项目

ELK:部署的时候麻烦,每一个filebeat都需要配置一个配置文件

使用etcd来管理被收集的日志项

##### 项目的架构

![image-20210824195131980](Go语言学习.assets/image-20210824195131980.png)

##### 上节课项目进度

1. kafka:消息队列
2. tailf:从文件里读日志
3. sarama:向kafka发送数据
4. go-ini:解析配置文件

##### 今日内容

##### etcd

##### 使用etcd优化日志收集项目

![image-20210824195924259](Go语言学习.assets/image-20210824195924259.png)



raft协议

- 选举
- 日志复制机制
- 异常处理

zookeeper的zad协议和raft协议的区别

![image-20210824201151410](Go语言学习.assets/image-20210824201151410.png)

![image-20210824201255712](Go语言学习.assets/image-20210824201255712.png)



![image-20210824201531623](Go语言学习.assets/image-20210824201531623.png)

![image-20210824201641847](Go语言学习.assets/image-20210824201641847.png)

![image-20210824201859917](Go语言学习.assets/image-20210824201859917.png)

![image-20210824201921279](Go语言学习.assets/image-20210824201921279.png)

![image-20210824202013396](Go语言学习.assets/image-20210824202013396.png)

![image-20210824202041613](Go语言学习.assets/image-20210824202041613.png)

![image-20210824202051395](Go语言学习.assets/image-20210824202051395.png)

![image-20210824202203749](Go语言学习.assets/image-20210824202203749.png)

![image-20210824202403398](Go语言学习.assets/image-20210824202403398.png)





清华学神尹成

![image-20210826231049867](Go语言学习.assets/image-20210826231049867.png)



![image-20210826231828312](Go语言学习.assets/image-20210826231828312.png)

 

#### LogTransfer

从kafka里面把日志取出来,写入ES

##### Elastic Search

ES是一个基于lucene构建的开源的/分布式/restful接口的全文搜索引擎.elastic search还是一个分布式文档数据库,其中每个字段均可被索引,而且每个字段的数据均可被搜索,ES能够横向扩展至数以百计的服务器存储以及处理PB级的数据.可以在极短的时间内存储/搜索和分析大量的数据.通常作为具有复杂搜索场景情况下的核心发动机.

##### ElasticSearch能做什么

1. 当你经营一家网上商店,你可以让你的客户搜索你卖的商品.在这种情况下,你可以使用Elastic search来存储你的整个产品目录和库存信息,为客户提供精准搜索,可以为客户推荐相关商品.
2. 当你想收集日志或者交易数据的时候,需要分析和挖掘这些数据,寻找趋势,进行统计,总结,或者发现异常.在这种情况下,你可以使用logstash或者其他工具来进行收集数据,当这引起数据存储到elastic search中.你可以搜索和汇总这些数据,找到任何你感兴趣的信息
3. 对于程序员来说,比较有名的案例是github.github的搜索是基于elasticsearch构建的,在github.com/search页面,你可以搜索项目,用户/issue/pull request,还有代码.公有40-50个索引库,分别用于索引网站需要跟踪的各种数据,虽然只索引项目的主分支master,但这个数据量依然巨大,包括20亿个索引文档,30TB的索引文件.



##### ElasticSearch基本概念

##### near realtime 几乎实时

elasticsearch是一个几乎实时的搜索凭条,意思是,从索引一个文档到这个文档可以被搜索只需要一点点的延迟,这个时间一半为毫秒级

##### cluster集群

集群是一个或者多个节点服务器的集合,这些节点共同保存整个数据,并在所有节点上提供联合索引和搜索功能.一个集群由一个唯一集群ID确定,并指定一个集群名(默认为elasticsearch).该集群名非常重要,因为节点可以通过这个集群名加入集群,一个节点只能是集群的一部分.

确保在不同的环境中不要使用相同的集群名称,否则可能会导致连接错误的集群节点,例如你可以使用logging--dev/ logging-stage/ logging-prod 分别为开发/阶段产品/生产集群做记录.

##### node节点

节点是单个服务器实例

##### index索引

索引是具有相似特性的文档集合

##### type类型

 在索引中,可以定义一个或者多个类型,类型是索引的逻辑类别/分区,其语义完全取决于你.

##### document文档 

文档是可以被索引的信息的基本单位.例如,你可以为单个客户提供一个文档,单个产品提供另一个文档,以及单个订单提供另一个文档.

##### shards&replicas分片与副本

##### ES基本概念与关系型数据库的比较

| ES概念                                    | 关系型数据库   |
| ----------------------------------------- | -------------- |
| index索引支持全文检索                     | database数据库 |
| type类型                                  | table表        |
| document文档,不同文档可以有不同的字段集合 | row数据行      |
| field字段                                 | column数据列   |
| mapping映射                               | schema模式     |

##### ES API

 下载安装

![image-20210902001925922](Go语言学习.assets/image-20210902001925922.png)

查看

![image-20210902001948107](Go语言学习.assets/image-20210902001948107.png)

查看心跳

![image-20210902002107349](Go语言学习.assets/image-20210902002107349.png)

查询当前es集群中所有的indices

curl -X get 127.0.0.1:9200/_cat/indices?v

![image-20210902002202915](Go语言学习.assets/image-20210902002202915.png)



#### gin学习

hello world demo

```go
package main

import (
   "github.com/gin-gonic/gin"
   "net/http"
)

func main() {
   //1.创建路由
   engine := gin.Default()
   //2.绑定路由规则,执行的函数
   //gin.context , 封装了request和response
   engine.GET("/", func(c *gin.Context) {
      c.String(http.StatusOK,"hello world!!!")
   })
   //3.监听端口 默认在8080端口
   engine.Run(":8000")
}
```



#### gin路由

##### 基本路由

- gin框架中采用的路由库是基于tprouter做的
- 地址为:https://github.com/julienschmidt/httprouter

##### restful风格的API

- gin支持restful风格的API
- 即representational state transfer 的缩写 直接翻译是表现层状态转化,是一种互联网应用程序的api设计理念,url定位资源,用http描述操作

获取文章 /blog/getxxx   get blog/xxx

添加 /blog/addxxx		post blog/xxx

修改 /blog/updatexxx  put  blog/xxx

删除 /blog/delxxx  		delete blog/xxx

##### API参数

- 可以通过context的param方法来获取api参数
- localhost:8000/xxx/zhangsan

[localhost:8000/user/zhangsan/lisi](http://localhost:8000/user/zhangsan/lisi)

##### URL参数

- URL参数可以通过defaultquery()或者query()方法来取
- defaultquery()若参数不存在,返回默认值 query()若参数不存在,返回空字符串

[localhost:8000/welcome?name=yourtreedad](http://localhost:8000/welcome?name=yourtreedad)

##### 表单参数

- 表单传输为post请求,http常见的传输格式化为四种
  - application/json  json传参
  - application/x-www-urlencoded  表单传参
  - application/xml  xml传参
  - multipart/form-data  表单上传文件
- 表单参数可以通过postform()方法获取,该方法默认解析的是x-www-form-urlencoded 或 from-data格式的参数

##### 上传单个文件

- multipart/form-data格式用于文件上传
- gin 文件上传与原生的net/http 方法类似,不同在于gin把原生的request封装到了c.Request中

##### 上传多个文件

 MultipartForm使用这个方法获得所有文件的

使用multipartForm.File["files"]来取所有文件指针

遍历, 然后存着就行了

##### routes Group

- routes Group  是为了管理一些相同的URL

##### 路由原理

- httprouter 会将所有路由规则构造成一个前缀树

命令行也可以尝试传post和get指令

![image-20210828214026568](Go语言学习.assets/image-20210828214026568.png)



```go
package main

import (
   "fmt"
   "github.com/gin-gonic/gin"
   "log"
   "net/http"
)



func main() {
   //1.创建路由
   //默认使用了2个中间件 Logger(), Recovery()
   engine := gin.Default()
   //engine:=gin.New()也可以的
   //2.绑定路由规则,执行的函数
   //gin.context , 封装了request和response

   //路由组 实际上就是便于管理 少写点东西
   routerGroup := engine.Group("/Get")
   routerGroup.GET("/v1", func(context *gin.Context) {
      query := context.DefaultQuery("name", "getParam")
      context.String(http.StatusOK,query)

   })

   group := engine.Group("/Post")
   group.POST("/v1", func(context *gin.Context) {
      postParam := context.DefaultPostForm("name", "postParam")
      context.String(http.StatusOK,postParam)
   })

   //index 界面
   engine.GET("/", func(c *gin.Context) {
      c.String(http.StatusOK,"hello world!!!")
   })

   //api参数 用 : 来取
   engine.GET("/user/:name/*action", func(context *gin.Context) {
      //
      name:= context.Param("name")
      action := context.Param("action")
      context.String(http.StatusOK,name+" is "+action)
   })

   //url参数 ?name="xxx"
   engine.GET("/welcome", func(context *gin.Context) {
      query := context.DefaultQuery("name", "Jack")
      context.String(http.StatusOK,fmt.Sprintf("Hello %s !",query))
   })

   //form表单传参
   engine.POST("/PostForm", PostFormParams)
   //from上传单个文件
   engine.POST("/Upload",UploadFile)
   //限制表单上传大小 8mb,默认值为32mb
   engine.MaxMultipartMemory = 8<<20
   //form上传多个文件
   engine.POST("UploadFiles",UploadFiles)
   engine.PUT("/xxxput")
   //3.监听端口 默认在8080端口
   engine.Run(":8000")
}

func UploadFiles(context *gin.Context) {
   multipartForm, err := context.MultipartForm()
   if err != nil {
      fmt.Println("received multiple files failed , err :",err)
       context.String(http.StatusBadRequest,fmt.Sprintf("get err %s ",err.Error()))
      return
   }

   //获取所有文件
   files := multipartForm.File["files"]
   //遍历所有files
   for _, file := range files {
      //逐个存
      err := context.SaveUploadedFile(file, file.Filename)
      if err != nil {
         context.String(http.StatusBadRequest,fmt.Sprintf("upload err %s ",err.Error()))
         return
      }
   }

   context.String(200,fmt.Sprintf("upload ok %d files!", len(files)))
}

func UploadFile(context *gin.Context) {
   //从表单中取文件
   file, err := context.FormFile("file")
   if err != nil {
      fmt.Println("receive file error, cause : ",err)
      return
   }
   log.Println(file.Filename)
   //传到项目的根目录, 名字就用本身的就好
   err = context.SaveUploadedFile(file, file.Filename)
   if err != nil {
      fmt.Println("file save failed , error : ",err)
      return
   }

   //打印信息
   context.String(200,fmt.Sprintf("'%s' has already uploaded!",file.Filename))
}

func PostFormParams(context *gin.Context) {
   //表单参数 设置默认值
   type1 := context.DefaultPostForm("type", "alert")
   //接收其他的
   userName := context.PostForm("username")
   password := context.PostForm("password")
   //多选框
   hobbys := context.PostFormArray("hobby")

   context.String(http.StatusOK,fmt.Sprintf("type is %s, username is %s, password is %s , hobbys is %v",type1,userName,password,hobbys))
}
```

html前端界面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登陆</title>
</head>
<body>
<form action="http://127.0.0.1:8000/PostForm" method="post" enctype="application/x-www-form-urlencoded">
    用户名:<input type="text" name="username">
    <br>
    密&nbsp&nbsp码: <input type="password" name="password">
    <br>
    兴&nbsp&nbsp趣:
    <input type="checkbox" value="run" name="hobby">跑步
    <input type="checkbox" value="game" name="hobby">游戏
    <input type="checkbox" value="money" name="hobby">金钱
    <br>
    <input type="submit" value="登陆">
</form>

<br>
<br>
<br>


<form action="http://127.0.0.1:8000/Upload" method="post" enctype="multipart/form-data">
    头像:
    <input type="file" name="file">
    <br>
    <input type="submit" value="提交">
</form>

<form action="http://127.0.0.1:8000/UploadFiles" method="post" enctype="multipart/form-data">
    上传多个文件:
    <input type="file" name="files" multiple>
    <br>
    <input type="submit" value="提交">
</form>
    
</body>
</html>
```

#### gin数据解析和绑定

##### json数据解析和绑定

- 客户端传参,后端接收并解析到结构体

使用ShouldBindJSON来解析到结构体

```go
engine.GET("loginJSON", func(context *gin.Context) {
   //声明接收的变量
   var json Login
   //将request的body中的数据,自动按照json格式解析到结构体
   err := context.ShouldBindJSON(&json)
   if err != nil {
      //返回错误信息
      //gin.H 封装了生成json数据的工具
      context.JSON(http.StatusBadRequest,gin.H{"error ":err.Error()})
      return
   }

   //判断用户名密码是否正确
   if json.User!="2020170281"||json.Password!="lalala123" {
      context.JSON(http.StatusBadRequest,gin.H{"status":"304"})
      return
   }

   context.JSON(http.StatusOK,gin.H{"status":"200"})
})
```

![image-20210828224803650](Go语言学习.assets/image-20210828224803650.png)

##### 表单数据解析和绑定

使用Bind来解析结构体

```go
engine.GET("loginForm", func(context *gin.Context) {
   var form Login
   //bind()默认解析并绑定form格式
   //根据请求头中的content-type自动推断
   err := context.Bind(&form)
   if err != nil {
      context.JSON(http.StatusBadRequest,gin.H{"error":err.Error()})
      return
   }
   if form.User!="2020170281"||form.Password!="lalala123"{
      context.JSON(http.StatusBadRequest,gin.H{"status":"304"})
      return
   }

   context.JSON(http.StatusOK,gin.H{"status":"200"})
})
```

html界面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登陆</title>
</head>
<body>
<form action="http://127.0.0.1:8000/loginForm" method="get" enctype="application/x-www-form-urlencoded">
    用户名:<input type="text" name="username">
    <br>
    密&nbsp&nbsp码: <input type="password" name="password">
    <br>
    <input type="submit" value="登陆">
</form>

<br>
<br>

</body>
</html>
```

##### URI数据解析和绑定

 使用shouldbinduri方法

```go
engine.GET("loginURI/:user/:password", func(context *gin.Context) {
   var URI Login
   err := context.ShouldBindUri(&URI)
   if err != nil {
      context.JSON(http.StatusBadRequest,gin.H{"error":err.Error()})
      return
   }

   if URI.User!="2020170281"||URI.Password!="lalala123" {
      context.JSON(http.StatusBadRequest,gin.H{"status":304})
      return
   }
   context.JSON(http.StatusOK,gin.H{"status":200})
})
```

![image-20210828231200951](Go语言学习.assets/image-20210828231200951.png)



##### 响应类型

- xml
- json
- protobuf
- yaml

```go'
package main

import (
   "github.com/gin-gonic/gin"
   "github.com/gin-gonic/gin/testdata/protoexample"
   "net/http"
)

//多种响应方式
func main() {
   //1.创建路由
   //2.默认使用了2个中间件logger recovery
   engine := gin.Default()


   //1.json
   engine.GET("/someJson", func(context *gin.Context) {
      context.JSON(http.StatusOK,gin.H{"message":"someJson","Status":200})
   })

   //2.结构体响应
   engine.GET("someStruct", func(context *gin.Context) {
      context.JSON(http.StatusOK, struct {
         Name , Message string
         Number int
      }{"root","message",123})
   })

   //3.XML响应
   engine.GET("/someXML", func(context *gin.Context) {
      context.XML(http.StatusOK,gin.H{"message":"xml"})
   })

   //4.yaml响应
   engine.GET("/someYaml", func(context *gin.Context) {
      context.YAML(http.StatusOK,gin.H{"name":"YAML"})
   })

   //5.protobuf格式 副歌开发的高校存储读取的工具
   engine.GET("/someProtoBuf", func(context *gin.Context) {
       reps:=[]int64{1,2}
       //定义返回数据
       label:="protobuf"
       data:=&protoexample.Test{
          Label: &label,
          Reps: reps,
       }
       context.ProtoBuf(http.StatusOK,data)
   })

   engine.Run(":8000")
}
```

##### HTML 模版渲染

- gin支持加载html模版,然后根据模版参数进行配置并返回相应的数据,本质上就是字符串的替换
- loadhtmlglob()方法可以加载模版文件

```go
func main() {
   engine:= gin.Default()

   //加载模版文件
   engine.LoadHTMLGlob("templates/*")
   //以下这种方式也可以啦
   //engine.LoadHTMLFiles("templates/index.tmpl")
   engine.GET("/index", func(context *gin.Context) {
      //根据文件名渲染
      //最终json将title替换
      context.HTML(http.StatusOK,"index.tmpl",gin.H{"title":"我的标题"})
   })
   engine.Run(":8000")
}
```

![image-20210828234359001](Go语言学习.assets/image-20210828234359001.png)

##### 重定向

```go
func main() {
   engine := gin.Default()
   engine.GET("/redirect", func(context *gin.Context) {
      //支持内部和外部的重定向
      context.Redirect(http.StatusMovedPermanently,"http://www.baidu.com")
   })

   engine.Run(":8000")
}

```

##### 同步异步

-  goroutine机制可以方便地实现异步处理
- 另外,在启动新的goroutine时,**不应该使用原始上下文,必须使用他的只读副本**

```go
unc main() {
   engine := gin.Default()
   //1.异步
   engine.GET("/long_async", func(context *gin.Context) {
      //需要搞一个只读的副本
      copyContext := context.Copy()
      //模仿异步处理
      go func() {
         time.Sleep(3 *time.Second)
         log.Println("异步执行..."+copyContext.Request.URL.Path)
      }()
   })

   //2.同步
   engine.GET("/long_sync", func(context *gin.Context) {
      time.Sleep(3*time.Second)
      log.Println("同步执行..."+context.Request.URL.Path)
   })
   engine.Run(":8000")
}
```

#### gin中间件

![image-20210828235642323](Go语言学习.assets/image-20210828235642323.png)

- gin可以构建中间件,但它只对注册过的路由函数起作用
- 对于分组路由,嵌套使用中间件,可以限定中间件的作用范围
- 中间件分为全局中间件,单个路由中间件和群组中间件
- gin中间件必须是一个gin.handlerfunc类型

##### 全局中间件

- 所有请求都经过此中间件

```go
package main

import (
   "fmt"
   "github.com/gin-gonic/gin"
   "net/http"
   "time"
)

//定义全局中间件
func MiddleWare() gin.HandlerFunc {
   return func(context *gin.Context) {
      t:=time.Now()
      fmt.Println("中间件开始执行了...")
      //设置变量到context的key中,可以通过get取
      context.Set("request","中间件")
      //执行函数
      context.Next()
      //中间件执行完后续的一些事情
      status := context.Writer.Status()
      fmt.Println("中间件执行完毕",status)
      fmt.Println("用时 : ",time.Now().Sub(t))
   }
}
func main() {
   engine:= gin.Default()

   //注册中间件
   engine.Use(MiddleWare())
   {
      engine.GET("/middleware", func(context *gin.Context) {
         //取值
         request, _ := context.Get("request")
         fmt.Println(request)
         //页面接收
         context.JSON(http.StatusOK,gin.H{"request":request})
      })
   }
   engine.Run(":8000")
}
```

#####  next()方法

看原码 实际上就是遍历了注册的所有中间件的个数,

##### 局部中间件

```go
//如此就是在这个路由之下定义了新的中间件,可以视为单个中间件
engine.GET("/middlewareDouble",MiddleWare(), func(context *gin.Context) {
   //取值
   request, _ := context.Get("request")
   fmt.Println(request)
   //页面接收
   context.JSON(http.StatusOK,gin.H{"request":request})
})
```

#####  练习

```go
package main

import (
   "fmt"
   "github.com/gin-gonic/gin"
   "time"
)

func middleTimer() gin.HandlerFunc {
   return func(context *gin.Context) {
      now := time.Now()
      context.Next()
      fmt.Println("用时: ",time.Now().Sub(now))
   }
}
func main() {
   engine := gin.Default()
   engine.Use(middleTimer())
   group := engine.Group("/timer")
   group.GET("/countTimer", func(context *gin.Context) {
      time.Sleep(3*time.Second)
   })
   group.GET("/counTimer1", func(context *gin.Context) {
      time.Sleep(5*time.Second)
   })
   engine.Run(":8000")
}
```

#### 会话控制

##### cookie是什么

- http是无状态协议,服务器不能记录里浏览器的访问状态,也就是说服务器不能区分两次请求是否是由同一个客户端发出的
- cookie就是解决http协议无状态的方案之一,中文是小甜饼的意思
- cookie实际上就是服务器保存在浏览器上的一段信息,浏览器有了cookie之后,每次向服务器发送请求时都会同时将该信息发送给服务器,服务器收到请求后,就可以根据该信息处理请求
- cookie由服务器创建,并发送给浏览器,最终由浏览器保存

##### cookie用途

- 保持登陆状态
- 京东购物车

##### cookie的使用

- 服务端发送cookieid

##### cookie练习

- 模拟实现权限验证中间件
  - 有两个路由,login用来设置cookie
  - home用来访问

```go
package main

import (
   "github.com/gin-gonic/gin"
   "net/http"
)

func MiddleWareAuth() gin.HandlerFunc {
   return func(context *gin.Context) {
      cookie, err := context.Cookie("loginToken")
      if err != nil {
         //返回错误
         context.JSON(http.StatusOK, gin.H{"error": "StatusUnauthorized"})
         context.Abort()
         return
      }
      if cookie == "true" {
         context.Next()
      }
   }
}
func main() {
   engine := gin.Default()

   engine.GET("/login", func(context *gin.Context) {
      http.SetCookie(context.Writer, &http.Cookie{
         Name:  "loginToken",
         Value: "true",
      })
      context.String(http.StatusOK, "Login successful")
   })

   engine.GET("/home", MiddleWareAuth(), func(context *gin.Context) {
      context.JSON(http.StatusOK, gin.H{"data": "home"})
   })
   engine.Run(":8000")
}
```

##### cookie的缺点

- 不安全 明文
- 增加带宽消耗
- 可以被禁用
- cookie有上限

##### session是什么

- session可以弥补cookie的不足,session必须依赖于cookie才能使用,生成一个sessionid放在cookie里传给客户端就可以了

![image-20210829104620811](Go语言学习.assets/image-20210829104620811.png)



![image-20210829104914310](Go语言学习.assets/image-20210829104914310.png)

session存在服务端中

##### session中间件开发

- 设计一个通用的session服务,支持内存存储和redis存储

- session模块设计
  - 本质上是k-v系统,通过key来进行增删改查
  - session可以存储在内存或者redis(2个版本)

![image-20210829105225472](Go语言学习.assets/image-20210829105225472.png)

- session接口设计
  - set
  - get
  - del
  - save   session存储,redis的实现延迟加载
- sessionmgr接口设计
  - init 初始化 加载redis地址
  - createsession 创建一个新的session
  - getsession 通过sessionid获取对应的session对象
- memorysession设计
  - 定义memorysession对象 字段sessionid  存kv的map 读写锁
  - 构造函数 为了获取对象
- sessionmgr设计
  -  定义memorysessionmgr对象 字段存放所有的session的map,读写锁
  - 构造函数
  - init
  - cretesession
  - getsession
- redisression设计
  - 定义redissession对象 ssionid字段 存kv的map 读写锁 redis连接池 记录内存中map否被修改的标记
  - 构造函数
  - set将session存到内存中的map
  - get取数据实现延迟加载
  - del
  - save 将session存到redis
- redissessionmgr设计
  - 定义redissessionmgr对象

![image-20210829110208079](Go语言学习.assets/image-20210829110208079.png)

 



这里还是要重申一下 http传参啊

首先 传参可以分为网址传参和表单传参

网址传参又分为api传参和url传参

api传参使用/book/:name

```go
name:= context.Param("name")
```

url传参使用/book

```go
query := context.Query("name")
```

表单传参

分为get和post  get的话我们发现 get的method最终会变成url

```go
query := context.Query("searchThing")
```

post就使用

```go
searchThing, ok := context.GetPostForm("searchThing")
form := context.PostForm("searchThing")
```



#### Elastic Search

![image-20210903210305686](Go语言学习.assets/image-20210903210305686.png)



##### 查看健康

curl -X GET127.0.0.1:9200/_cat/health?v

##### 创建索引

curl -X PUT 127.0.0.1:9200/www

##### 删除索引

curl -X DELETE 127.0.0.1:9200/www

##### 插入数据

![image-20210903210614663](Go语言学习.assets/image-20210903210614663.png)

##### 检索数据

![image-20210903211123288](Go语言学习.assets/image-20210903211123288.png)

##### go操作ES



#### 微服务

##### 注册中心选型

consul / zookeeper / etcd / euerka



##### 选项设计模式

```go
package main

import "fmt"

func main() {
   newOptions("str1", "str2", "str3", 1, 2, 3)
   newOptionsNew(WithStrOption("str1"))
}

type OptionsNew struct {
   strOption1 string
   strOption2 string
   strOption3 string
   intOption1 int
   intOption2 int
   intOption3 int
}

// Option 先声明一个函数类型,用于传参
type Option func(option *OptionsNew)

// WithStrOption 定义具体给某个字段赋值的方法 返回一个方法 通过这个方法给结构体赋值
func WithStrOption(str string) Option {
   return func(option *OptionsNew) {
      option.strOption1 = str
   }
}
//初始化结构体
func newOptionsNew(otions ...Option) {
   options :=&OptionsNew{}
   //遍历otions,得到每一个函数
   for _, fun:= range otions {
      //调用函数, 在函数里,给传进去的对象赋值
      fun(options)
   }
   fmt.Printf("init options %#v\n",options)
}

type Options struct {
   strOption1 string
   strOption2 string
   strOption3 string
   intOption1 int
   intOption2 int
   intOption3 int
}

func newOptions(strOption1, strOption2, strOption3 string, intOption1, intOption2, intOption3 int) {
   options := Options{
      strOption1: strOption1,
      strOption2: strOption2,
      strOption3: strOption3,
      intOption1: intOption1,
      intOption2: intOption2,
      intOption3: intOption3,
   }

   fmt.Printf("init option %#v\n", options)
}
```

##### 注册组件接口开发

- 目标
  - 支持多注册中心,既支持consul又支持etcd
  - 支持可扩展
  - 提供基于名字的插件管理函数,用来注册插件

![image-20210903224236637](Go语言学习.assets/image-20210903224236637.png)



#####  流行RPC框架的对比

dubbo / motan / thrift / grpc

##### gRPC简介

- pc语言中立/平台中立/开源的远程过程调用系统
- grpc由客户端和服务端可以在多种环境中运行和交互,例如写一个java服务端,可以用go语言写客户端调用

##### grpc与protobuf介绍

-  微服务架构中,由于每个服务对应的代码库是独立运行的,无法直接调用,彼此间的通信就是个大问题
- grpc可以实现微服务,将大的项目拆分为多个小且独立的业务模块,也就是服务,各服务之间使用高校的protobuf协议进行rpc调用,grpc默认使用protocol buffers,这个google开源的一套成熟的结构数据序列化机制(当然也可以使用其他数据格式如json)
- 可以用proto files 创建grpc服务,用message类型来定义方法参数和返回类型

##### 安装grpc和protubuf

git clone https://github.com/grpc/grpc-go.git $GOPATH/src/google.golang.org/grpc 

git clone https://github.com/golang/net.git $GOPATH/src/golang.org/x/net 

git clone https://github.com/golang/text.git $GOPATH/src/golang.org/x/text 

go get -u github.com/golang/protobuf/{proto,protoc-gen-go} 

git clone https://github.com/google/go-genproto.git $GOPATH/src/google.golang.org/genproto

##### 进入src,并install

cd $GOPATH/src/ 

go install google.golang.org/grpc



##### protobuf语法

##### 基本规范

- 文件以.proto作为文件后缀,除结构定义外的语句以分号结尾
- 结构定义可以包含 message  / service / enum
- rpc方法定义结尾的分号可有可无
- message命名采用采用驼峰命名方式, 字段命名采用小写字母加下划线分隔方式
- enums类型名采用驼峰命名方式,字段命名采用大写字母加下划线分隔方式
- service与rpc方法名同意采用驼峰命名

##### 字段规则

- 字段格式:限定修饰符 | 数据类型 | 字段名称 | = |字段编码值| [字段默认值]
- 限定修饰符包含 requeired / optional / repeated 
  - requierd 表示是一个必须字段,必须相对于发送方,在发送消息之前必须设置该字段的值,对于接收方,必须能够识别该字段的意思.发送之前咩有设置required字段或者无法识别requered字段都会引发编解码异常,导致消息被丢弃
  - optional: 表示是一个可选字段,可选对于发送方,在发送消息时,可以有选择性的设置或者不设置该字段的值.对于接收方,如果能够识别可选字段就进行响应的处理,如果无法识别,则忽略该字段,消息中的其他字段正常处理.--因为option字段的特性,很多接口在升级版本中把后来添加的字段都统一设置为optional字段,这样老的版本无序升级程序也可以正常的与新的软件进行通信.只不过新的字段无法识别而已,因为并不是每个节点都需要新的功能,因此可以做到按需升级和平滑过渡
  - peated 表示该字段可以包含0-N个元素.其特性和optional一样,但是每一次可以包含多个值.可以看做是在传递一个数组的值
- 数据类型
  - protobuf以了一套基本数据类型.几乎都可以映射到c++/java等语言的基础数据类型
  - N表示打包的字节并不是固定的.而是根据数据的大小或者长度决定
  - 关于fixed32和int32的区别.fixed32的打包效率比int32的效率高,但是使用的空间一般比int32多.因此一个属于时间效率高,一个属于空间效率高
- 字段名称
  - 字段名称的命名与c / c++ / java等语言的便令命名方式几乎相同
  - protobuf建议字段的命名采用以下划线分隔的驼峰式.例如first_name而不是firstName
- 字段编码值
  -  有了该值,通信双方才能互相识别对方的字段,相同的编码值,其限定修饰符和数据类型必须相同,编码值的取值范围为1-2的32次方
  - 其中1-15的编码时间和空间效率都是最高的,编码值越大,其编码的时间和空间效率就越低,所以建议把经常要传递的值把其字段编码设置为1-15之间的值
  - 1900-2000编码值为google protobuf系统内部保留值,建议不要在自己的项目中使用
- 字段默认值
  -  当在传递数据时,对于required数据类型,如果用户没有设置值,则使用默认值传递到端

##### service如何定义

- 如果想要将消息类型用在rpc系统中,可以在.proto文件中定义一个rpc服务接口,protocol buffer编译器会根据所选择的不同语言生成服务接口代码
- 例如,想要定义一个rpc服务并具有一个方法,该方法接收searchrequest并返回一个searchresponse,此时可以在.proto文件中进行定义

```go
service SearchService{
    rpc Search (SearchRequest) returns (SearchResponse){}
}
```

- 生成的接口代码作为客户端与服务端的约定,服务端必须实现定义的所有接口方法,客户端直接调用同名方法向服务端发起请求,比较麻烦的是,即便业务上不需要的参数也必须指定一个请求消息,一般会定义一个空的message

##### message如何定义

-  一个message类型定义描述了一个请求或响应的消息格式,可以包含多种类型字段
- 例如定一个搜索请求的消息格式,每个请求包含查询字符串,页码,每页数目
- 字段名用小写,转为go后自动变为大写,message就相当于结构体

```go
syntax = "proto3" ; 

message SearchRequest{
  string query =1 ; 
  int32 page_number = 2 ; 
  int32 result_per_page = 3 ; 
  
}
```

- 首行声明使用的protobuf版本为protobuf3
- searchrequest定义了三个字段,每个字段声明以分号结尾,.proto文件支持双斜线注释

##### 添加更多message类型

##### 如何使用其他message

- message支持嵌套使用,作为另一message中的字段类型

##### proto3的map类型

-  proto3支持map类型声明

##### .proto文件编译

-  通过定义好的.proto文件生成java / python / c++ / go / rubu / javanano / oc / C# 代码,需要安装编译器protoc
- 当使用protocol buffer编译器运行.proto文件时,编译器将生成所选语言的代码,用于使用在.proto文件中定义的消息类型/ 服务接口约定等.不同语言生成的代码格式不同
  - go:生成一个.pb.go文件, 每个消息类型对应一个结构体

##### 写proto文件

```go
//版本号
syntax = "proto3";

//指定包名
package proto;
//指定生成的go文件在哪里
option  go_package="./";

//定义结构体
message UserRequest{
    //定义用户名
    string name = 1 ;
}

//响应结构体
message UserResponse{
     int32  id = 1 ;
     string name = 2 ;
     int32 age = 3 ;
     //repeated 修饰符 是可变数组 , go转切片
     repeated  string hobby =4 ;
}

//service定义方法
service UserInfoService{
    rpc GetUserInfo(UserRequest) returns (UserResponse){}
}
```

##### 生成.go文件

-  goland中打开命令行,输入命令生成接口文件
- protoc -I . --go_out=plugins=grpc:. ./user.proto

##### 编写服务端,实现接口

```go
package main

import (
   "context"
   "fmt"
   "google.golang.org/grpc"
   "net"
   pb "src/code.oldboyedu.com/gRPC/proto"
)
func main() {
   //1.需要监听
   addr:="127.0.0.1:8082"
   listen, err := net.Listen("tcp", addr)
   if err != nil {
      return
   }

   fmt.Println("监听正常")
   //2.需要实例化grpc
   server := grpc.NewServer()
   //3.在grpc注册微服务
   pb.RegisterUserInfoServiceServer(server,&u)
   //4.启动服务端
   server.Serve(listen)

}

// UserInfoService 定义空接口
type UserInfoService struct {

}

var u = UserInfoService{}

// GetUserInfo 实现方法
func (u *UserInfoService) GetUserInfo(ctx context.Context,req *pb.UserRequest) (res *pb.UserResponse,err error){
   //通过用户名查询用户信息
   name := req.Name
   //数据库里查询用户信息
   if name == "zs" {
      res = &pb.UserResponse{
         Id:    1,
         Name:  name,
         Age:   22,
         Hobby: []string{"singing","run"},
      }
   }
   return
}
```

##### 编写客户端,调用服务端方法

```go
package main

import (
   "context"
   "fmt"
   "google.golang.org/grpc"
   pb "src/code.oldboyedu.com/gRPC/proto"
)

func main() {

   //1.连接服务器
   dial, err := grpc.Dial("127.0.0.1:8082", grpc.WithInsecure())
   if err != nil {
      fmt.Printf("连接异常 , %s \n",err)
   }
   defer dial.Close()
   //2.实例grpc客户端
   client := pb.NewUserInfoServiceClient(dial)
   //3.调用接口
   request := pb.UserRequest{Name: "zs"}
   response, err := client.GetUserInfo(context.Background(), &request)
   if err != nil {
      fmt.Println("响应异常 %s\n",err)
      return
   }
   fmt.Printf("响应结果: %v\n",response)
}
```



#### go-micro简介

- go micro 是一个插件化的基础框架,基于此可以构建微服务,micro的设计哲学是可插拔的插件化架构
- 在架构之外,它默认实现了consul作为服务发现,2019年默认使用mdns,通过http进行通信,通过protobuf和json进行编码

##### go-micro的主要功能

- 服务发现:自动服务注册和名称解析.服务发现是微服务开发的核心.当服务A需要与服务B通话时,它需要该服务的位置.默认发现机制是多播DNS的一种零配置系统.您可以选择使用swim协议作为p2p网络设置八卦,或者为弹性云原生设置consul
- 负载均衡:基于服务发现构建的客户端的负载均衡.一旦我们发现了服务的任意数量的实例地址,我们现在需要一种方法来决定要路由到哪个节点.我们使用随机散列负载均衡来提供跨服务的均匀分布,并在出现问题时重试不同的节点.
- 消息编码:基于内容类型的动态消息编码.客户端和服务器将使用编解码器和内容类型为您无缝编码和解码go类型.可以编码任何种类的消息并从不同的客户端发送.客户端和服务器默认处理此问题,这包括默认的protobuf和json
- 请求/响应:基于rpc的请求/响应,支持双向流.我们提供了同步通信的抽象,对服务的请求将自动解决,负载均衡,拨号和流式传输.启用tls时,默认传输为http/1.1或http2
- async message :pubsub是异步通信和事件驱动架构的一流公民.时间通知是微服务开发的核心模式.启用tls时,默认消息是点对点http /1.1 或http2
- 可插拔接口:go micro为每个分布式系统抽象使用go接口,因此这些接口是可插拔的,并允许go micro与运行时无关,可以插入任何基础技术
  - 插件地址 https://github.com/micro/go-plugins

##### go-micro通信流程

- server监听客户端的调用,和broker推送过来的信息进行处理.并且server端需要向register注册自己的存在或消亡,这样client才能知道自己的状态
- register服务的注册和发现,client端从register中得到server的信息,然后每次调用都根据算法选择一个server进行通信,当然通信是要经过编解码的,选择传输协议等一系列过程的
- 如果有需要通知所有的server端可以使用broker进行信息的推送,broker信息队列进行信息的接收和发布



#### GORM

https://gorm.io/zh_CN/docs/

##### ORM优缺点

优点:

- 提高开发效率

缺点:

- 牺牲执行性能
- 牺牲灵活性
- 弱化SQL能力

##### 安装

go get -u github.com/jinzhu/gorm

##### 连接数据库

连接不同的数据库都需要导入对应数据的驱动程序,gorm已经贴心为我们包装了一些驱动程序,只需要按照如下方式导入需要的数据库驱动即可

```go
import _"github.com/jinzhu/gorm/dialects/mysql"
import _"github.com/jinzhu/gorm/dialects/postgres"
import _"github.com/jinzhu/gorm/dialects/sqlite"
import _"github.com/jinzhu/gorm/dialects/mssql"
```

##### 连接mysql

```go
package main

import (
   "fmt"
   "github.com/jinzhu/gorm"
   _ "github.com/jinzhu/gorm/dialects/mssql"
   "time"
)

type Student struct {
   Sno       string
   Sname     string
   Ssex      string
   Sbirthday time.Time
   Class     string
   Reserve1  string
   Reserve2  string
   Image     []byte
}

type Score struct {
   Sno string
   Cno string
   Degree1 string
}

func main() {
   //db, err := gorm.Open("mssql", "sqlserver://sa:123456@localhost:1433?database=Test")
   db, err := gorm.Open("mssql", "sqlserver://sa:123456@localhost?database=Test&connection+timeout=30")
   if err != nil {
      fmt.Println("open mssql failed . error : ", err)
      return
   }
   defer db.Close()

   //db.AutoMigrate(&Student{})
   var student Student
   db.First(&student)
   fmt.Println(student)


   var score Score
   first := db.First(&score)
   fmt.Println(first.RowsAffected)
   fmt.Println(score)
}
```

**生成结构体 利用xorm的逆向生成工具来生成go的结构体类型**



##### Gorm Model定义

在使用orm工具时,我们通常需要在代码中定义模型models 与数据库中的数据表进行映射,在gorm中模型models通常是正常定义的结构体,基本的go类型或者是她们的指针,同时也支持sql.scanner 以及 driver.valuer接口interface

```go
package main

import (
   "database/sql"
   "fmt"
   "github.com/jinzhu/gorm"
   _ "github.com/jinzhu/gorm/dialects/mysql"
   "time"
)

// User 定义模型
type User struct {
   gorm.Model
   Name string
   Age sql.NullInt64 `gorm:"column:user_age"`
   Birthday *time.Time
   Email string `gorm:"type:varchar(100);unique_index"`
   Role string `gorm:"size:255"`
   MemberNumber string `gorm:"unique;not null"` //唯一且非空
   Num int `gorm:"AUTO_INCREMENT"` //自增
   Address string `gorm:"index:add"` //创建名为addr的索引
   IgnoreMe   int    `gorm:"-"` //忽略本字段
}

type Animal struct{
   AnimalID int64 `gorm:"primary_key"`  //手动
}

func (a Animal) TableName() string {
   return "qimi"
}

func main() {
   gorm.DefaultTableNameHandler = func(db *gorm.DB, defaultTableName string) string {
      return "XXX_"+defaultTableName
   }
   //连接mysql数据库
   db, err := gorm.Open("mysql", "root:123456@(127.0.0.1:3306)/tset?charset=utf8mb4&parseTime=True&loc=Local")
   if err != nil {
      fmt.Println("open mysql failed , error: ", err)
      return
   }
   defer db.Close()


   db.SingularTable(true) //禁用复数
   db.AutoMigrate(&User{})
   db.AutoMigrate(&Animal{})

   //使用user结构体来创建名叫useruseruser的表
   //db.Table("useruseruser").CreateTable(&User{})
}
```

##### gorm.model

为了方便模型定义,gorm内置了一个gorm.model结构体 gorm.model是一个包含了ID . createAt UpdateAt DeleteAt 四个字段的golang结构体

你可以将它嵌入到你自己的模型中:

当然你也可以完全自己定义模型

##### 结构体标记

##### 关联相关标记

##### 主键 表名 约定

gorm默认会使用名为ID的字段作为表的主键

```go
type User struct{
    ID string //默认
}

type Animal struct{
    AnimalID int64 `gorm:"primary_key"`  //手动
}
```

 表名默认就是结构体的复数

字段默认会将结构体AnimalBoy=>Animal_boy

##### 时间戳跟踪

##### createdAt

如果模型有该字段,该字段的值将回事初次创建记录的时间

```go
db.Create(&user) //将会是当前时间

//可以使用update方法来改变createat的值
db.Model(&user).Update("CreatedAt",time.Now())
```

##### updateAt

如果模型有该字段,该字段的值将会是每次更新记录的时间

```go
db.save(&user)  //updateAt将会是当前的时间

db.Model(&user).Update("name","jinzhu")  //updateAt 将会是当前时间
```

##### deleteAt

如果模型有该字段,调用删除记录时,将会设置deletedAt字段为当前时间,而不是直接将记录从数据库中删除



##### CRUD

##### 创建

**注意:	** 改过tag定义字段的默认值,在创建记录时候生成的sql语句会排除没有值或值为零值的字段.在将记录插入到数据库后,gorm会从数据库加载那些字段的默认值.如果你想避免这种情况,可以考虑使用指针或实现scanner/valuer接口

##### 使用指针方式将零值存入数据库

```go
package main

import (
   "database/sql"
   "fmt"
   "github.com/jinzhu/gorm"
   _ "github.com/jinzhu/gorm/dialects/mysql"
)

// Employee 1.定义模型 使用指针
type Employee struct {
   ID   int64
   Name *string `gorm:"default:'小王子'"`
   Age  int64
}

// Employee1 1.使用scanner/valuer
type Employee1 struct {
   ID   int64
   Name sql.NullString `gorm:"default:'小王子'"`
   Age  int64
}

// TableName 定义已存在表和结构体的映射关系
func (e Employee1) TableName() string {
   return "employees"
}

func main() {

   db, err := gorm.Open("mysql", "root:123456@(127.0.0.1:3306)/tset?charset=utf8mb4&parseTime=True&loc=Local")
   if err != nil {
      fmt.Println("open mysql failed , error: ", err)
      return
   }

   defer db.Close()

   //2.把模型与数据库中的表对应起来
   db.AutoMigrate(&Employee{})

   //a:="ljs"
   //3.创建
   //employee := Employee{
   // Age:  38,
   // Name:  new(string),
   //}
   //
   //employee1 := Employee{
   // Age:  48,
   // Name:  &a,
   //}

   db.CreateTable()
   employee2 := Employee1{
      Age:  58,
      Name: sql.NullString{
         String: "",
         Valid:  true,
      },
   }
   //db.NewRecord(&employee) //判断主键是否为空
   //db.Debug().Create(&employee)
   //db.Debug().Create(&employee1)
   db.Debug().Create(&employee2)
   //fmt.Println(db.NewRecord(&employee))


}
```



##### 查询

##### 简单查询

##### 普通sql查询

##### struct&map查询

**提示:	**当通过结构体进行查询时,gorm将会只通过非零值字段查询,这意味这如果你的字段值为0,'',false或者其他零值时,将不会被用于构建查询条件

**你可以使用指针或者scanner/valuer来实现**

##### Not查询

#####  内联条件

作用与where查询类似,当内联条件与多个立即执行方法一起使用时,内联条件不会传递给后面的立即执行方法

#####  FirstOrInit

获取匹配的第一条记录,否则根据给定的条件初始化一个新的对象(仅仅支持struct 和 map 条件)

##### attrs

如果记录未找到,将使用参数初始化struct

##### assign

不管记录是否找到,都将参数赋值给struct

##### FirstOrCreate

获取匹配的第一条记录,否则根据给定的条件创建一个新的记录(仅支持struct和map条件)

##### 排序

order , 指定从数据库总检索出记录的顺序,设置第二个参数reorder为true,可以覆盖前面定义的排序条件

##### count

count必须是链式查询的最后一个操作,因为它会覆盖前面的select,但如果里面使用了count时不会覆盖

##### group&having

##### Join

##### 链式查询

##### Scope

scope是建立在链式操作的基础上的,基于此可以抽取通用逻辑,写出更多可重用的函数库

```go
package main

import (
   "fmt"
   "github.com/jinzhu/gorm"
   _ "github.com/jinzhu/gorm/dialects/mysql"
   "time"
)

type User struct {
   gorm.Model  // id createat update at deleteat
   Name string
   Age int64
}

func (u User) TableName() string {
   return "SelectUser"
}

func main() {
   db, err := gorm.Open("mysql", "root:123456@(127.0.0.1:3306)/tset?charset=utf8mb4&parseTime=True&loc=Local")
   if err != nil {
      fmt.Println("mysql open failed ,error : ",err)
      return
   }
   defer db.Close()

   //自动迁移 或者对应
   db.AutoMigrate(&User{})

   ////创建
   //db.Create(&User{Age: 18,Name: "ljs"})
   //
   //user := User{Age: 28, Name: "jwt"}
   //db.Create(&user)

   //查询 根据主键查询第一条
   user:=User{}
   db.First(&user)
   //select * from users order by id limit 1
   fmt.Println(user)

   //随机获取一条
   u := new(User)
   db.Take(u)
   fmt.Println(*u)


   //根据主键查询最后一条记录
   u2 := new(User)
   db.Last(u2)
   fmt.Println(*u2)

   //查询所有的记录
   var users []User
   db.Debug().Find(&users)
   fmt.Println(users)

   //查询特定某条记录 (仅当主键为整型的时候可用)
   u3 := new(User)
   db.Find(&u3,2)

   //普通sql查询
   //get first
   db.Where("name=?","ljs").First(&user)
   fmt.Println(user)

   db.Where("name like ?","%%%").Find(&users)
   fmt.Println(users)

   db.Where("updated_at < ?",time.Now()).Find(&users)
   fmt.Println(users)


   //struct && map 查询
   db.Where(&User{Name: "ljs",Age: 18}).First(&user)
   fmt.Println(user)

   //map
   db.Where(map[string]interface{}{"name":"ljs","age":18}).Find(&user)
   fmt.Println(user)

   //主键的切片
   db.Where([]int{1,2}).Find(&users)
   fmt.Println(users)

   //not查询
   db.Not("name","jinzhu").First(&user)
   fmt.Println(user,"notnot")

   //not in
   db.Not("name",[]string{"linjianshu","jwt"}).Find(&user)
   fmt.Println(user)

   //not in primary
   u4 := new(User)
   db.Debug().Not([]int64{1}).Find(u4)
   fmt.Println(u4 , "not in primary")

   //plain sql
   // = 和 ? 之间一定要有空格
   u5 := new(User)
   db.Debug().Not("name = ?","ljs").First(u5)
   fmt.Println(*u5)

   //struct
   u6 := new(User)
   u6.Name="ljs"
   u6.Age = 18
   u7 := new(User)
   db.Debug().Not(&u6).First(&u7)
   fmt.Println(u7 ," not in struct ")

   //or条件
   i := new([]User)
   db.Where("name = ?","ljs").Or("name = ?","jwt").Find(i)
   fmt.Println(i , " or condition ")

   //struct or
   i2 := new([]User)
   db.Where(User{Name: "ljs"}).Or(User{Age: 28}).Find(i2)
   fmt.Println(i2, "or struct")

   //map
   i3 := new([]User)
   db.Where(map[string]interface{}{"name":"ljs"}).Or(map[string]interface{}{"age":18}).Find(i3)
   fmt.Println(i3  , " or map ")

   //内联条件
   u8 := new(User)
   db.Debug().First(u8,2)
   fmt.Println(u8)

   //plan sql
   u9 := new(User)
   db.Find(u9,"name = ?","ljs")
   fmt.Println(u9)

   //struct map ...

   //firstOrInit
   //未找到
   u10 := new(User)
   db.FirstOrInit(u10,User{Name: "fuck no existing"})
   fmt.Println(u10)

   //attr
   db.Attrs(User{Age: 100}).FirstOrInit(u10,User{Name: "fuck no existing"})
   fmt.Println(u10)

   //assign
   u11:= new(User)
   db.Assign(User{Age: 1000}).Where(User{Name: "jwt"}).FirstOrInit(u11)
   fmt.Println(u11)

   //order
   i4 := new([]User)
   db.Order("age desc , name").Find(i4)
   fmt.Println(i4)

   i5 := new([]User)
   db.Order("age desc").Order("name").Find(i5)
   fmt.Println(i5)

   //覆盖了
   i6 := new([]User)
   db.Order("age desc").Find(i6).Order("age",true).Find(i6)
   fmt.Println(i6)

   //数量
   u12 := new(User)
   db.Limit(1).Find(u12)
   //-1 取消limit条件
   //i7 := new([]User)
   //db.Limit(2).Find(i7).Limit(-1).Find()

   //offset 偏移 也就是takeWhile
   u13 := new(User)
   db.Offset(1).First(u13)
   fmt.Println(u13)

   //count
   i7 := new(int)
   println(db.Table("selectuser").Count(i7))
   fmt.Println(*i7)



}
```

##### 更新

##### 更新所有字段

save()默认会更新该对象的所有字段,即使你没有赋值

##### 更新修改字段

如果你只希望更新指定字段,可以使用update或者updates

##### 更新选定字段

过你想更新或者忽略某些字段,你可以使用select omit

##### 无hooks更新

上面的更新操作会自动运行model的beforeupdate , afterupdate方法,更新updateat时间戳,在更新时保存其association,如果你不想调用这些方法,你可以使用updatecolumn,updatecolumns

##### 批量更新

批量更新时hook函数不会执行

使用struct更新时,只会更新非零值字段,若想更新所有字段,请使用map[string]interface{}

使用rowsaffected 获取更新记录总数

##### 使用sql表达式更新

```go
package main

import (
   "fmt"
   "github.com/jinzhu/gorm"
   _ "github.com/jinzhu/gorm/dialects/mysql"
)

type User struct {
   gorm.Model
   Name   string
   Age    int
   Active bool
}

func (u User) TableName() string {
   return "UpdateUser"
}

func main() {
   db, err := gorm.Open("mysql", "root:123456@(127.0.0.1:3306)/tset?charset=utf8mb4&parseTime=True&loc=Local")
   if err != nil {
      fmt.Println("mysql open failed ,error : ", err)
      return
   }
   defer db.Close()

   db.AutoMigrate(&User{})

   //db.Create(&User{Name: "qimi", Age: 18, Active: true})
   //db.Create(&User{Name: "jinzhu", Age: 20, Active: false})


   //var user = User{}
   //db.First(&user)
   //fmt.Println(user)
   //
   ////更新
   //user.Name ="林建树"
   //user.Age=99
   ////save 默认修改所有字段
   //db.Debug().Save(&user)
   //
   //db.Debug().Model(&user).Update("name","xwz")
   //
   //i := new([]User)
   //db.Debug().Where("name = ?","xwz").Or("active = ?",false).Find(i)
   //fmt.Println(i)
   //
   ////更新单个属性
   //db.Model(&i).Where("age = ?",99).Update("name","hello")
   ////更新完后还是不会变化的 原来查到的 i
   //fmt.Println(i)
   //
   ////使用map更新多个属性 , 只会更新其中有变化的属性
   //i2 := new([]User)
   //db.Find(i2)
   //fmt.Println(i2)
   //
   //db.Debug().Model(i2).Where(User{Age: 99}).Updates(map[string]interface{}{"age":100,"active":false})
   //
   ////使用struct更新多个属性,只会更新其中有变化且非零值的字段
   //i3 := new([]User)
   //db.Debug().Model(i3).Updates(User{Active: true})
   //
   ////警告：当使用struct更新时，gorm只会更新那些非零值的字段
   ////对于下面的操作，不会发生任何更新，因为false都是那些非零值的指端
   //db.Debug().Model(i3).Updates(User{Active: false})
   //
   ////更新选定字段 select
   //i4 := new(User)
   ////只适合于传入的参数是user 而不是 []user
   //db.Debug().Model(i4).Select("active").Updates(map[string]interface{}{"name":"hello1","active":false})
   //
   ////omit 忽略
   //i5 := new(User)
   ////只适合于传入的参数是user 而不是 []user
   //db.Debug().Model(i5).Omit("name").Updates(map[string]interface{}{"name":"hello","active":true})
   //
   ////无hook更新  不会更新update_at
   //u := new(User)
   ////db.Debug().Where("age= ?",100).First(u)
   ////db.Debug().Where(map[string]interface{}{"age":100}).First(u)
   //db.Debug().Where(User{Age: 100}).First(u)
   //fmt.Println(u)
   //db.Debug().Model(u).UpdateColumn("name","ljs")
   //
   //i6 := new([]User)
   //db.Debug().Where(map[string]interface{}{"active":true}).Find(i6)
   ////model在这里的作用并不能限制固定的数量 只能起到映射的作用
   //println(db.Debug().Model(i6).UpdateColumns(User{Active: true, Age: 18}).RowsAffected)

   //批量更新

   //使用sql表达式更新
   i7 := new([]User)
   db.Debug().Model(User{}).Where("active = ?",true).Find(&i7)
   //model不能作为限制输入参数的条件
   db.Debug().Model(i7).Update("age",gorm.Expr("age * ? + ?",1,1))

   db.Debug().Model(User{}).Where("active = ?",true).Update("age",gorm.Expr("age * ? + ?",1,1))

   
}
```

##### 删除

**警告:**删除记录时,请确保主键字段有值,gorm会通过主键去删除记录,如果主键为空,gorm会删除改model的所有记录

##### 批量删除

删除全部匹配的

##### 软删除

如果一个model有deleteat字段,他将自动获得软删除的功能,当调用delete方法的时候,记录不会真正从数据库中被删除,只会将deleteat字段的值会被设置为当前时间

##### 物理删除

```go
package main

import (
   "fmt"
   "github.com/jinzhu/gorm"
   _"github.com/jinzhu/gorm/dialects/mysql"
)
type User struct {
   gorm.Model
   Name   string
   Age    int
   Active bool
}

func (u User) TableName() string {
   return "DeleteUser"
}
func main() {
   db, err := gorm.Open("mysql", "root:123456@(127.0.0.1:3306)/tset?charset=utf8mb4&parseTime=True&loc=Local")
   if err != nil {
      fmt.Println("mysql open failed ,error : ", err)
      return
   }
   defer db.Close()

   db.AutoMigrate(&User{})

   //db.Debug().Create(&User{
   // Name:   "jwt",
   // Age:    20,
   // Active: false,
   //})
   //db.Debug().Create(&User{
   // Name:   "lje",
   // Age:    18,
   // Active: false,
   //})

   //删除
   //没有主键的时候很可怕 会删除所有的
   //user :=User{}
   ////user.ID  = 1
   //user.Name ="qimi"
   //db.Debug().Delete(&user)


   ////选择性批量删除
   //i := new([]User)
   ////使用结构体的时候 传入的参数如果是零值的话 不会作为筛选条件
   //db.Debug().Where(User{Active: false}).Find(i)
   //fmt.Println(i)
   ////delete i 不会将i作为批量删除的筛选条件
   ////db.Debug().Delete(i)
   //
   //db.Debug().Where(map[string]interface{}{"active":false}).Find(i)
   //fmt.Println(i)
   //
   ////这样删除才可以 有条件删除
   //db.Debug().Where(map[string]interface{}{"active":false}).Find(i).Delete(User{})
   //
   //i2 := new(int)
   //fmt.Println(db.Debug().Model(User{}).Count(i2))

   //sql删除
   //db.Debug().Delete(User{},"active like 1")

   //就想查到被软删除的内容
   //i := new([]User)
   //db.Unscoped().Debug().Where("deleted_at is not null").Find(i)
   //db.Unscoped().Debug().Where("deleted_at is not null").Find(i).UpdateColumn("deleted_at",nil)

   //db.Debug().Where("deleted_at is not null").Find(i)

   //物理删除 硬删除
   db.Debug().Unscoped().Where("name = 'lje'").Delete(User{})
}
```

