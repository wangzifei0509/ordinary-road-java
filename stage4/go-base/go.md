Go 基本语法
1. go项目目录结构
|—— bin
|—— pkg
|—— src
|—— |—— 域名
|—— |—— |—— 项目名or账号名
2. Helloworld.go
``` package main
import "fmt"
func main(){
 fmt.Println("hello world!")
}
```

3. 注释
```
// 这是一个单行注释
/*
这是一个多行注释 
*/
// 不用使用；显示结束，一行默认是一个语句，如果两个语句写在一行里，需要加；显性表示是两句
```
4. 标识符
```组成：字母、数字和_下划线，但是数字不能作为开头```
5. 声明变量
```
var a int = 10 //最完整的方式
var b = 10 //省略变量类型，根据值去猜测
var a int //给a设置的值是int类型的默认值
c : = 10 // 省略var,只能在函数体内使用
var { //全局变量，不能出现在函数体内
    a int,
    b string
}
a, b, c := 5, 7, "abc" //多个变量一起声明
a,_ := 1,7 //_匿名变量，接受但是不用
const LENGTH int = 5 //常量使用const声明
iota
```
6. ioat
是go语言中的常量计数器，只能在常量的表达式中使用，ioat在const关键字出现时将被重置为0，const中每新增一行常量声明ioat计数一次（ioat可理解为const的行索引）使用ioat能简化定义，定义枚举时有用。
所以常量这里有两个特殊之处，1 常量定义可以省略，默认继承上一行的定义。2.ioat是const的行索引值。
```
package main

import "fmt"

const pi = 3.14

const (
   a = 100
   b = 1000
   c
   d
)

const (
   e = iota
   f = iota * 2
   g
)

const (
   h = iota
   i = 100
   j = iota
   k
)

func main(){
   fmt.Println(pi) //3.14
   fmt.Println(a) //100
   fmt.Println(b)  //1000
   fmt.Println(c) //1000
   fmt.Println(d)  //1000
   fmt.Println(e)  //0
   fmt.Println(f)  //2
   fmt.Println(g) //4
   fmt.Println(h) //0
   fmt.Println(i) //100
   fmt.Println(j)  //2
   fmt.Println(k)  //3
}
```
7. 数据类型
布尔值：
  - 布尔类型变量的默认值为false。
  - Go 语言中不允许将整型强制转换为布尔型.
  - 布尔型无法参与数值运算，也无法与其他类型进行转换。
字符串：
  - “” 代表字符串，‘’ 代表字符，``代表多行文本原样输出
  - strings.工具类内置了一些常用的方法
  - rune是一个字，方便字符处理
  - 要修改字符串，需要先将其转换成[]rune或[]byte，完成后再转换为string。无论哪种转换，都会重新分配内存，并复制字节数组。
```
package main

import (
   "fmt"
   "strings"
)

func main() {
   str1 := "wang王"
   str2 := 'x'
   str3 := `this is a 
      raw string "原样输出"`
   fmt.Println(str1) //wang王
   fmt.Println(str2) //120
   fmt.Println(str3)
   /*this is a
   raw string "原样输出"
   */
   fmt.Println("-------------")
   fmt.Println(len(str1)) //7
   str_array := strings.Split(str1, "a")
   fmt.Println(str_array) //[w ng王]

   var r rune = '王'
   fmt.Println(strings.ContainsRune(str1, r))
   fmt.Println(strings.HasPrefix(str1, "w"))
   fmt.Println("-------------")

   b1 := strings.HasSuffix(str1, "王")
   var i2 int = strings.Index(str1, "a")
   var i3 int = strings.LastIndex(str1, "a")
   var str4 string = strings.Join(str_array, ",")

   fmt.Println(b1)
   fmt.Println(i2)
   fmt.Println(i3)
   fmt.Println(str4)
   fmt.Println("-------------")

   str6 := "hello world 王夏梅"

   for i := 0; i < len(str6); i++ {
      fmt.Printf("%v(%c)", str6[i], str6[i]) //%v代表的输出ASC码值
   }
   //104(h)101(e)108(l)108(l)111(o)32( )119(w)111(o)114(r)108(l)100(d)32( )231(ç)142()139()229(å)164(¤)143()230(æ)162(¢)133()
   fmt.Println("")
   for _, r = range str6 {
      fmt.Printf("%v(%c)", r, r)
   }
   //104(h)101(e)108(l)108(l)111(o)32( )119(w)111(o)114(r)108(l)100(d)32( )29579(王)22799(夏)26757(梅)

}
```
|数据类型|初始化默认值|
|---|---|
|int|0|
|float32|0|
|pointer|nil|
|string|“”|
|bool|fasle|
8. 运算符
`++`（自增）和`--`（自减）在Go语言中是单独的语句，并不是运算符。要单独占一行
9. 条件语句
  - go语言没有while，统一使用for
  - 支持goto、break、continue 
```
//if 
if a > 20 {
  ....
}
//类似于while的用法
a :=0
for a <20 {
}
for{ //无限循环
}
```
10. 数组
  1. 数组是值复制，不会改变原始的值
  2. 数组支持 “==“、”!=” 操作符，因为内存总是被初始化过的。
  3. [n]*T表示指针数组，*[n]T表示数组指针 。
```
var array1 [3]int
var ptr_array [3]*int
var ptr *[3]int
```
11. 切片
  - 切片是对数组进行了一层封装，底层还是数组。
  - append()切片一般情况下是按照现有cap*2的规律扩容的，如果需要的cap大于double，那么使用需要的cap，扩容后的底层数组内存地址会变。如果容量还满足，那么底层数组就还是原来的数组。
```
make([]T, size, cap) //声明
var array []int //声明
append() //修改
copy() //深层复制
func main(){ //删除
   splice1 := []int{1,2,3,4,5}
   fmt.Printf("%v,%d,%d,%p\n", splice1, len(splice1), cap(splice1), splice1)

   splice1 = append(splice1[:2],splice1[3:]...)
   fmt.Printf("%v,%d,%d,%p\n", splice1, len(splice1), cap(splice1), splice1)
}

var array = [...]int{1,2,3} //数组
var splice = []int{1,2,3} //切片
```
12. Map
```
make(map[KeyType]ValueType, [cap]) 
value, ok := map[key]
for k, v := range scoreMap { fmt.Println(k, v) }
map[key] = value
delete(map,key)

func main() {
   //声明
   map1 := make(map[string]int, 4)
   map2 := map[string]int{
      "zhangsna": 8,
      "lisi":     6,
   }
   var map3 map[string]int
   fmt.Printf("%T,%v,%p,%d \n", map1, map1, map1, len(map1))
   fmt.Printf("%T,%v,%p,%d \n", map2, map2, map2, len(map2))
   fmt.Printf("%T,%v,%p,%d \n", map3, map3, map3, len(map3))
   //查询
   if value, ok := map2["lisi"]; ok {
      fmt.Printf("value:%v\n", value)
   }

   if value, ok := map1["liis"]; !ok {
      fmt.Printf("value is not contain!,%v\n", value)
   }
   for key, value := range map2 {
      fmt.Printf("key:%v,value:%d \n", key, value)
   }
   //删除
   delete(map2, "lisi")
   delete(map1, "lisi")
   //修改
   map2["lisi"] = 4
   map2["zhangsan"] = 9
   //按照指定的顺序打印map
   map4 := map[string]int{
      "zhagnsan": 6,
      "lisi":     9,
      "wanger":   0,
      "zhaosi":   3,
      "qian":     7,
      "sun":      5,
   }
   var valueArray []string
   for key, _ := range map4 {
      valueArray = append(valueArray, key)
   }
   sort.Strings(valueArray)
   for _, key := range valueArray {
      fmt.Printf("key:%s,value:%v \n", key, map4[key])
   }
   //map中有切片
   map5 := make(map[int][]int, 4)
   fmt.Printf("%T,%v,%p,%d \n", map5, map5, map5, len(map5))

   s1 := []int{1, 2, 3, 4}
   map5[0] = s1
   fmt.Printf("%T,%v,%p,%d \n", map5, map5, map5, len(map5))

   //切片中有map
   s2 := make([]map[string]string,2,4)
   s2[0] = make(map[string]string,4)
   fmt.Printf("%T,%v,%p,%d \n", s2, s2, s2, len(s2))
}
```
13. 函数
  - 返回值也可以命名，直接在函数体内赋值，然后return就可以啦
  - 函数在go语言中是一等公民，函数可以定义函数类型，声明，赋值变量，作为函数的返回值、参数等
  - 函数体内通常使用匿名函数，因为函数体内不能再声明函数啦 
  - 闭包=环境+匿名函数
  - defer 通常用来做异常处理，资源关闭、清理资源等操作。在函数确定返回值，并没有结束之前执行，按照栈的方式后进先出
  - defer注册要延迟执行的函数时该函数所有的参数都需要确定其值
  1. recover()必须搭配defer使用。
  2. defer一定要在可能引发panic的语句之前定义。
```
func 函数名(参数)(返回值){ 函数体 }

type cal func(int, int) int  // 声明函数类型

func add(a int, b int) int {
   return a + b
}

func sub(a int, b int) int {
   return a - b
}

func main() {

   fmt.Printf("%T,%p,%d\n", add, add, add(2, 3))
   fmt.Printf("%T,%p,%d\n", sub, sub, sub(2, 3))
   var c cal
   c = add //函数变量
   fmt.Printf("%T,%p,%d\n", c, c, c(2, 3))
   c = sub
   fmt.Printf("%T,%p,%d", c, c, c(2, 3))
 

}

-------- 类似多态

//函数作为返回值
func cal1(str string) func(int, int) int {
   switch str {

   case "+":
      return add1
   case "-":
      return sub1
   default:
      return nil
   }
}

func add1(a int,b int) int {
   return a+b
}
func sub1(a int,b int)int  {
   return a-b

}
//函数作为参数 类似多态
func op(a int,b int,f func(int,int)int){

   i := f(a, b)
   fmt.Println(i)
}
```
14. 指针

|运算符|描述|实例|
|---|---|---|
|&|返回变量存储地址|&a; 将给出变量的实际地址。|
|* |指针变量。|*a; 是一个指针变量|

  - go语言的指针是安全指针，不能进行位移和运算
  - 值类型因为声明的时候就能推算出内存空间，所以值类型不需要初始化
  - 引用类型。slice 、map、chan因为声明的时候不能推算内存空间，所以需要初始化
Make
```
func make(t Type, size ...IntegerType) Type
// 对引用类型初始化
```
New 
```
func new(Type) *Type
//对值类型初始化
```
15. 结构体
  1. 结构体是值引用
  2. 以下情况结构体实例的传递需要使用指针，1 结构体内容占用很大，复制很耗资源。2.需要改变结构体内的值 3. 结构体有一个方法使用指针，为了统一，最好都使用指针。
```
type structName struct{
    filedName string 
    int8
}
//构造函数 规范建议使用new结构体名作为函数名
func newStruct(filedName string,num int8) *struct {
    return &struct{
        "xxxx",
        12,
    }
} 
//结构体方法
func (p *persion) setAge(num int8){
        p.age = 20
}

type Person struct {
   Name string `json:"name" xml:"name"`
   Age  int8 `json:"age" xml:"age"`
   //Address Address `json:"address" xml:"address"` //普通属性
   Address //匿名属性 其他语言中的继承
}

type Address struct {
   City   string
   Street string
}

//构造函数
func newPerson(name string, age int8, city string, street string) *Person {
   return &Person{
      Name: name,
      Age:  age,
      Address: Address{
         City:   city,
         Street: street,
      },
   }
}

//方法
func (p Person) Run() {
   fmt.Printf("%s running!", p.Name)
}

//方法
func (a Address) Print() {
   fmt.Printf("%s printting!", a.City)
}

func main() {
   p1 := newPerson("wangxiamei", int8(18), "beijing", "wangjing")
   fmt.Printf("%T,%#v\n", p1, p1)
   fmt.Printf("%s\n", p1.Name)
   fmt.Printf("%s\n", p1.City)
   p1.Run()
   p1.Print()
   //序列化
   result, err := json.Marshal(p1)
   if err != nil {
      fmt.Println("json format fail", err)
      return
   }
   fmt.Println(string(result))
   //反序列化
   p2 := new(Person)
   str := "{\"Name\":\"zhier\",\"Age\":18,\"City\":\"beijing\",\"Street\":\"wangjing\"}"
   err1 :=json.Unmarshal([]byte(str),p2)
   if err1 != nil {
      fmt.Println("json un format fail!",err1)
      return
   }
   fmt.Printf("%#v\n",p2)
   fmt.Println(p2)


}
```
16. 包
  - 首字母大写包外可见；首字母小写包内可见；建议struct和属性的首字母都大写。
  - 一个包定义一组功能
  - init函数执行时间，该函数在import之后，处理完全局变量，main函数之前执行，所以链引用的话，最底层引用的init函数先执行
17. 接口
  - 接口内的方法都实现啦 就代表实现这个接口啦 
  - 接口是定义了一组特征一组定义，只要实现啦这些方法你就是什么 鸭子模型
```
//定义一组特征
type Animal interface {
   say()
   move()
}

type Dog struct {
   Name string
}

type Cat struct {
   Name string
}

func (d Dog) say(){
   fmt.Println(d.Name,"say...")
}

func (c Cat) say(){
   fmt.Println(c.Name,"say....")
}

func (d Dog) move()  {
   fmt.Println(d.Name,"move....")

}
func (c Cat )move(){
   fmt.Println(c.Name,"move.....")
}
func main()  {
   var a Animal
   a = Dog{
      "lajiao",
   }
   a.move()
   a.say()
   a = Cat{
      "boluo",
   }
   a.move()
   a.say()
}
```

18. 单元测试 
  - 函数测试
    - 与被测试函数同文件夹下（Split）
    - 以被测试函数_test.go（Split_test.go）文件命名
    - 测试函数的签名必须是Test被测试函数名(t *testing.T) {...}
    - go test -v #查看详情 -run="Split" #制定测试哪一个函数
    - split_test.go
```
func TestSplit(t *testing.T) {
   type TestArray struct {
      str  string
      sep  string
      want []string
   }
   mapTest := map[string]TestArray{
      "chinese": TestArray{"我爱你", "爱", []string{"我", "你"}},
      "simple":  TestArray{"a:b:f:g", ":", []string{"a", "b", "f", "g"}},
      "some":    TestArray{"arbcdbcg", "bc", []string{"ar", "d", "g"}},
   }

   for key, value := range mapTest {
      t.Run(key, func(t *testing.T) {
         got := Split(value.str, value.sep)
         if !reflect.DeepEqual(got, value.want) {
            t.Errorf("split error ,got:%v,want:%v", got, value.want)
         }
      })
   }
}

  - 基准测试
    - split_test.go
func BenchmarkSplit(b *testing.B) {
   for i := 0; i < b.N; i++ {
      Split("沙河有沙又有河", "沙")
   }
}
```
  - 示例测试

19. fmt包常用函数
fmt.Print/fmt.Scan
fmt.Printf
fmt.Println
fmt.Fprint


fmt.Sprint


fmt.Errorf



20. time包
  - go语言time格式化的模板是go的诞生时间2006年01月02日 15:04:05 
  - 
```
package main

import (
   "fmt"
   "time"
)

func main() {
   t := time.Now()
   fmt.Printf("%T,%v\n", t, t)
   fmt.Printf("%d-%02d-%02d %02d:%02d:%02d\n", t.Year(), t.Month(), t.Day(), t.Hour(), t.Minute(), t.Second())
   fmt.Printf("%d,%d\n", t.Unix(), t.UnixNano())
   t1 := time.Unix(1623912349, 0)
   fmt.Printf("%T,%v\n", t1, t1)
   fmt.Printf("%d-%02d-%02d %02d:%02d:%02d\n", t1.Year(), t1.Month(), t1.Day(), t1.Hour(), t1.Minute(), t1.Second())
   sub1 := t1.Unix() - t.Unix() //seconds
   fmt.Printf("%T,%v\n", sub1, sub1)
   t2 := t.Add(time.Second)
   fmt.Printf("%T,%v\n", t2, t2)
   fmt.Printf("%d-%02d-%02d %02d:%02d:%02d\n", t2.Year(), t2.Month(), t2.Day(), t2.Hour(), t2.Minute(), t2.Second())
   t3 := t.Sub(t2) //Duration as an int64 nanosecond count
   fmt.Printf("%T,%v\n", t3, t3)

   fmt.Println("------------")
   t4 := time.Now()
   t5 := t4.UTC()
   fmt.Printf("%T,%v\n", t4, t4)
   fmt.Printf("%T,%v\n", t5, t5)
   fmt.Println(t4.Equal(t5))

   t6 := time.Now()
   t7 := t6.Add(time.Second)
   fmt.Println(t6.After(t7))
   fmt.Println(t6.Before(t7))
   fmt.Println("---------")
   //time->string
   t8 := time.Now()
   fmt.Println(t8.Format("2006/01/02 15:04"))
   fmt.Println(t8.Format("2006-01-02 15:04:05"))
   //string-time
   loc,_ := time.LoadLocation("Asia/Shanghai")
   t9,_ := time.ParseInLocation("2006-01-02 15:04:05","2021-01-08 23:00:01",loc)
   fmt.Printf("%v,%T",t9,t9)
}
```
## Go 总结
变量 全局变量 函数内变量  匿名变量 常量
函数 全局函数  函数内函数 匿名函数
数组 var array [5]int 
切片
Map 
指针 * & 
结构体
Interface
Error
Goruntime  go chan 
#### Go 常用的fmt
```
%v //默认方式输出
%d //数字
%f //浮点
%c //字符
%s //字符串
%p //内存地址
%T //变量类型
```
#### Go 数据类型分类
```
int bool string float32 rune array  struct ...//值类型
slice map chan//引用数据类型
// 引用数据类型使用时要注意，复制一份副本再使用
//引用类型range循环的时候使用的是将值分配到一个固定的内存上去，所以循环体中无法改变值的内容，除非使用指针
```
#### Go 常用的内置函数
```
len(v) //用来求长度，比如string、array、slice、map、channel

int(v) //类型强转
float32(v) 

make(T,size,cap) //用来分配内存，主要用来分配引用类型，比如chan、map、slice
new(T)        //用来分配内存，主要用来分配值类型，比如int、struct。返回的是指针
append(v,v...) //append(slice1,1,1,1,1)   用来追加元素到数组、slice中
copy(destV,srcV)
delete(map2, "lisi")
close(chan)       //主要用来关闭channel
panic("")          //阻断程序 抛出错误
recover()        //处理panic，让程序继续运行
```

#### Go常用的内置工具类
```
strings.HasSuffix("") //string的工具类
errors.New("") //错误的工具类
```

#### Go 命令
```
Go run filename.go


Go build filename.go


go run：编译并运行 Go 程序
go build：编译并打包 Go 程序
go get：安装依赖
go test：运行测试
```


go语言特性
特性	优点	缺点
语法简单	提升开发效率，节省时间	难以处理一些复杂的工程问题
天然支持并发	极大减少异步编程的难度，提高开发效率	不熟悉通道和协程的开发者会有一些学习成本
类型系统	Go 语言是静态类型，相对于动态类型语言更稳定和可预测IOP 鸭子类型比严格的 OOP 语言更简洁	没有继承、抽象、静态、动态等特性缺少泛型，导致灵活性降低难以快速构建复杂通用的框架或工具
错误处理	强制约束错误管理，避免 “try/catch 一把梭”	啰嗦的错误处理代码，充斥着 if err := ...
编译迅速	这绝对是一个优点	怎么可能是缺点？
非常规依赖管理	可以直接引用发布到 Github 上的仓库作为模块依赖引用，省去了依赖托管的官方网站可以随时在 Github 上发布 Go 语言编写的第三方模块自由的依赖发布意味着 Golang 的生态发展将不受官方依赖托管网站的限制	严重依赖 Github，在 Github 上搜索 Go 语言模块相对不精准
非常规日期格式	按照 6-1-2-3-4-5（2006-01-02 15:04:05），相对来说比较好记	对于已经习惯了 yyyy-MM-dd HH:mm:ss 格式的开发者来说非常不习惯
## 参考文档
[首页 - Go语言中文网 - Golang中文社区](https://books.studygolang.com/)
[【置顶】Go语言学习之路/Go语言教程 - 李文周的博客](https://www.liwenzhou.com/posts/Go/golang-menu/)
