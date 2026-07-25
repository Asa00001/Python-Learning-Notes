# 核心语法-数据储存与运算

## 1.字面量

字面量是在代码里直接写出来的固定值。

常见的Python字面量：

1）整数字面量
类型为int，即integer，整数，如100、0、-10等。

2）浮点数字面量
类型为float，即小数，如3.14、0.5、-2.17等。

3）字符串字面量
如"Hello"、"Asa"等，单双引号均可。

4）布尔字面量
True、False，注意Python中首字母要大写。

5）空值字面量
None，表示什么也没有，类似于Java中的null。

==Note. （1）字面量可直接参与运算     （2）用 type() 可以查看字面量类型

## 2.变量

变量可以理解为程序中用来储存单个数据的容器。

定义格式：变量名 = 变量的值      
	等号代表赋值行为

==Note. Python变量不需要声明类型，且程序运行过程中变量可以更换类型。

变量命名规则：
	1）Python变量可以包含字母、数字、下划线，但是不能以数字开头
	2）通常会用snake_case蛇形命名

==Note. 用 type() 可以查看变量类型
isinstance(变量， 类型)可以判定变量是否是指定类型
	例：age = 18
	    print(isinstance(age, int))
	输出为True

Python中print时字符串与变量拼接：

1）加号 +， "Hello" + name
此时需要name类型为str，否则要先用 str() 转换变量类型。

2）format()
"Hello{}".format(name) 老式写法，现在不常用。

3）f-string 推荐写法
print(f"Hello{name}")

==Note. 临时测试时，也可以用逗号链接，打印时可以一次打印，从而实现拼接。

## 案例：变量交换

不同于Java的显式temp交换，Python可以用更简易的方法。

a = 10
b = 20
a, b = b, a
print(a, b)

可以直接交换。

## 3. 字符串定义

### 1）单引号/双引号定义

最基础的定义方式，效果相同

例如：name = "Asa"
       cat = '小星'

==Note. 如果在同一种引号中写引号，则需要转义符 \

例如：text = "他说：\"你好\""

### 2）三引号字符串

三引号字符串可以保留换行，适合写多行文本，单双引号均可。

例如：
text = """这是第一行
这是第二行
这是第三行"""

### 3）字符串格式化：格式说明符（f-string)

基本语法： f"{变量}"
	例如：
	name = "Asa"
	print(f"你好，{name}")
	输出：你好，Asa

### 4）常见格式说明符：

格式说明符语法：f"{变量:格式说明符}"

（1）保留两位小数
	pi = 3.1415926
	print(f"{pi:.2f}")
	输出：3.14

（2）百分比显示
	rate = 0.1234
	print(f"{rate:.2%}")
	输出：12.34%

==Note. %会自动乘一百并添加百分号%

（3）千分位分隔
	money = 1234567
	print(f"{money:,}")
	输出：1,234,567

（4）指定总宽度
	num = 42
	print(f"{num:5d}")
	输出：   42

==Note. 5d表示总宽度5位，整数（decimal)，不足部分补空格。

（5）前面补0
	num = 42
	print(f"{num:05d}")
	输出：00042

## 4. 输入与输出

1）输出（output）
可以直接用 print() 输出

2）输入（input）
使用 input(提示信息) 获取键盘输入。

例如：
name = input()
print(name)
输出：Asa

==Note. input() 获取的信息类型为str（字符串），
需使用int()、float()等转换成对应类型。
	例如：age = int(input())

## 5.Python运算符

### 1）算术运算符

加法：+     减法：-     乘法：*
除法：
	/ 单斜杠无论如何都会得到float
	// 双斜杠为整除

### 2）进阶运算符

取余：%
幂运算：**

### 3）赋值运算符

普通赋值：=     
加等于：+=     减等于：-=     乘等于：* =     除等于：/=

### 4）比较运算符

等于：==     不等于：!=       
大于：>     大于等于：>=
小于：<     小于等于：<=

### 5）逻辑运算符

不同于Java中的 && 、||、!，
Python中为and、or、not。

### 6）成员运算符（Python特色）

（1）判断是否存在（in）
	name = "Asa"
	print("A" in name)
	输出True
（2）判断不存在（not in）
	print("z" not in name)
	输出True

==Note. Python中，字符串可以直接比较。
如Java中，String a = "Asa";  String b = "Asa";
此时，a == b 的判断有对象引用的问题，需使用 a.equals(b) 判断二者内容是否相同。
但Python中，== ==可以直接比较内容而非地址。
此外，字符串也可以进行大小比较，
从第一位开始，将对应位置的字符依次比较。

# 核心语法-流程控制语句

## 1. if语法

### 1）最简单的if语法

if 条件:
    执行代码

==Note. （1）没有括号     （2）条件后需要冒号

![[Pasted image 20260531193559.png]]

==Note. 在Python中，缩进非常重要，不能多也不能少。
如果缩进没写或多写，会出现SyntaxError。
![[Pasted image 20260531193741.png]]
执行顺序：
if成立
↓
打印已成年
↓
打印程序结束

### 2）if - else

if 条件：
	代码块A
else：
	代码块B

### 3）else if

不同于Java，Python中使用elif引导分支条件。

## 2. match模式匹配

match是Python中的模式匹配语句，可以理解为Python版switch。

它适合处理一个变量有多个**固定取值**，然后根据不同取值执行不同代码。

### 1）基本语法
![[Pasted image 20260601153915.png]]
==Note. （1）case_相当于Java中的default     （2）Python不需要写break

### 2）case可以匹配多个值

如果多个值执行同一段代码，可以用 |：
![[Pasted image 20260601154231.png]]

这里的 case 1 | 2 | 3 | 4 | 5: 
指的是，只要 day 是 1、2、3、4、5 中任意一个，就匹配成功。

## 3. while循环

while循环的核心逻辑：只要条件成立，就一直重复执行。

### 1）基本语法

![[Pasted image 20260601160355.png]]
例子：
count = 1

while count <= 5:
    print(count)
    count += 1

输出：
1
2
3
4
5

### 2）while的执行流程

判断条件
↓
如果 True，执行循环体
↓
执行完后回到 while 再判断
↓
如果还是 True，继续执行
↓
直到条件变成 False，循环结束

==Note. 循环中必须改变条件，否则while检测到的条件始终为True，则会出现死循环。

### 3）break 结束循环

在循环中，如果运行到 break， 则立刻跳出当前循环。
![[Pasted image 20260601160932.png]]
运行时，虽然为while True，但只要执行到break，就会退出循环。

### 4）continue 跳过本轮循环

![[Pasted image 20260601161136.png]]
输出：
1
2
4
5

运行到 num == 3 时，continue会跳过后面的 `print(num)`，直接回到 while 条件判断。

## 4. for循环

for循环可以理解为，将一组东西，一个一个拿出来处理。

### 1）基本语法
![[Pasted image 20260601163008.png]]
例如：
for i in range(5):
    print(i)
输出：
0
1
2
3
4

==Note. range(5)是从0到4，不包含5。

### 2）range()的使用

range(n) 可以生成一串数字，从0开始，到n - 1。

（1）指定起点和终点
![[Pasted image 20260601163623.png]]

含义为： range(起点, 终点)

其中，遍历区间为左闭又开区间，包含起点，不包含终点。

（2）指定步长
![[Pasted image 20260601163801.png]]
格式为：range(起点, 终点, 步长)

## 3）for遍历字符串
![[Pasted image 20260601163922.png]]
输出：
A
s
a

该过程会把字符串中的每个字符，一个一个拿出来。

## 5. 嵌套循环

“嵌套”通常是指，一个结构里再放一个结构。

例如：
if 里面放 if
while 里面放 while
for 里面放 for
循环里面放 if

例如，嵌套if：
![[Pasted image 20260602112921.png]]

==Note. 其中，第二层判断依赖第一层判断。

嵌套for：
![[Pasted image 20260602113014.png]]

==Note. 核心规律：外层循环执行一次，内层循环完整执行一轮。

### 经典例子1：打印矩形

![[Pasted image 20260602113623.png]]

输出：
``` text
*****
*****
*****
```

### 经典例子2: 打印等腰三角形

![[Pasted image 20260602120334.png]]

输出结果：
```text
     *
    ***
   *****
  *******
 *********
```

==Note. 在同一行内，先打印空格，后打印星号

### 经典例子3: 打印乘法口诀表

![[Pasted image 20260602120932.png]]

输出l类似：
1 * 1 = 1
2 * 1 = 2       2 * 2 = 4
3 * 1 = 3       3 * 2 = 6       3 * 3 = 9
4 * 1 = 4       4 * 2 = 8       4 * 3 = 12      4 * 4 = 16
5 * 1 = 5       5 * 2 = 10      5 * 3 = 15      5 * 4 = 20      5 * 5 = 25
……

==Note. 注意边界值，乘法表需要从1开始循环。

### 关于print（）

通过 end =  "" ，可以控制print打印后的结尾字符。
![[Pasted image 20260602121422.png]]


# 核心语法-数据容器

数据容器指一种可以容纳多份数据类型的容器，容纳的每一份数据称为一个元素，每一个元素都可以是任意类型的数据。

## 1.列表list

列表是一个可以装很多数据的容器。

### 1）列表的定义
![[Pasted image 20260603081021.png]]

列表用方括号定义：[]
里面的元素用逗号分隔：,

列表中元素有序、可重复、可修改

==Note. Python中列表中元素的类型可以不同。

### 2）通过下标取元素
![[Pasted image 20260603081253.png]]

==Note. 下标从 **0** 开始，这点和 Java 数组 / ArrayList 一样。

**反向索引**：Python中支持反向索引，最后一位为 -1，从后往前依次缩小。
![[Pasted image 20260603081542.png|697]]

==Note. 此外，知道元素内容时，也可以使用index()反向查找元素位置
![[Pasted image 20260603095522.png]]

### 3）修改元素

列表元素可以通过索引获取并重新定义来修改。
![[Pasted image 20260603081840.png]]
输出：
['admin', 'lisi', 'taoge']

### 4)添加元素

（1）末尾添加
	names.append("wangwu")

（2）插入到指定位置
	names.insert(1, "lisi")

区别为，append()放在最后，而insert(index, value)放在指定下标位置。

（3）extend()
	可以将另一个列表拼接进来，将元素一个一个加进来
	![[Pasted image 20260603095015.png]]
	输出：[1, 2, 3, 4, 5, 6]

### 5）删除元素

（1）用del删除
	按下标删除，不返回元素，是Python关键字
	del names[1]

（2）remove() 
	按值删除
	names.remove("admin")

（3）pop()
	按下标删除，并返回删除的元素
	removed = names.pop(1)

（4）清空列表
	names.clear()

### 6）遍历列表

![[Pasted image 20260603084135.png]]
输出：
admin
zhangsan
taoge

==Note. Python可以不使用下标直接遍历数组。

### 7）获取长度
![[Pasted image 20260603084314.png]]
输出：3

Python中使用 len(数组名) 获取数组长度，类似于Java中的list.size()

Python中数组元素求和，使用 sum(nums)

### 8）判断元素是否存在
![[Pasted image 20260603084504.png]]
输出：
True
False

==此外，通过 count() 可以统计元素出现次数
![[Pasted image 20260603095709.png]]
输出为：3

### 9）排序

使用 sort() 可以给list排序
![[Pasted image 20260603100146.png]]
输出：[1,2,3,5]

排序时默认升序排列，想要设置降序，则需要
	nums.sort(reverse=True)
==列表中，使用max(nums)，min(nums)可以直接获取最大、最小值。

### 10）切片

切片就是从列表/字符串里截取一部分。

基本语法： 列表[start:end]
意思是：从 start 开始取，取到 end 之前，不包含 end
	也就是一个左闭又开区间

==Note. （1）省略start，则表示从开头取到end前     （2）省略end，则表示从start取到列表最后

（1）使用：列表[ : ] ，可以得到一个新的列表副本，如
	![[Pasted image 20260603085334.png]]输出：[10, 20, 30, 40, 50]

（2）加步长 step
	完整语法为：列表[start:end:step]
	![[Pasted image 20260603085605.png]]
	输出：[10, 30, 50]
	意思是，从下标0到下标6之前，每隔2个取一次
	==Note. 使用反向索引同样可以操作

**step < 0时**，指从右往左取，这时需要start值大于end值
	此时， 默认值会改变
	start省略不再是开头，而是list结尾；反之，end省略不再是list结尾，而是开头。
	这也是[::-1]能实现list和str反转的原因。
	==Note. 由于list切片是左闭右开区间，因此反向切片时end=0也取不到第一位，只有是用默认值才能反向取到第一位。

（3）反向切片
	使用：[::-1] 可以实现反转列表/字符串
	![[Pasted image 20260603090018.png]]
	输出：[50, 40, 30, 20, 10]

此外，也可以通过 reverse() 直接反转列表
![[Pasted image 20260603095915.png]]
输出：[4,3,2,1]

（4）字符串也支持切片
	![[Pasted image 20260603090229.png]]
	输出：Py
		thon
		nohtyP

### 列表中的常见方法汇总
![[Pasted image 20260603100416.png]]

### 案例笔记补充

（1）用户输入存入List

单个输入
	![[Pasted image 20260603160517.png]]

多个输入
	![[Pasted image 20260603160549.png]]

（2）列表合并

方法1: extend()
	list1.extend(list2)
	特点：修改 list1，list2 不变

方法2: +
	list3 = list1 + list2
	特点：生成新列表，原列表不变

方法3: 解包
	list3 = [*list1, *list2]
	
	特点：生成新列表，多个列表时可读性更好

==Note. **解包**
基本概念：\*list1
表示：把列表拆开，取出其中所有元素

合并多个列表：
![[Pasted image 20260603161256.png]]
效果：把多个列表中的元素，放入一个新列表

（3）去重思路
例如：nums = [1,2,3,3,4,4,5]

先创建一个新列表：result = []
然后遍历原列表，只保留不重复的部分
![[Pasted image 20260603161507.png]]
结果：[1,2,3,4,5]

核心思想：
遍历
↓
检查是否已存在
↓
不存在才加入

（4）列表推导式

列表推导式的本质是for + append 的简写

基本语法：
![[Pasted image 20260603162310.png]]
此处的“表达式”指要插入的新列表的对象。

例如：
![[Pasted image 20260603162404.png]]
等价于：
![[Pasted image 20260603162428.png]]

进阶版：
![[Pasted image 20260603162655.png]]
可以筛选插入新list的对象值

## 2. 字符串str

str可以理解成用来保存文本的数据类型。

字符串可以用单引号、双引号，
如果字符串内需要换行，可以用三引号。
![[Pasted image 20260605165135.png]]

字符串本质上是字符序列，因此它和list一样支持索引和反向索引。

字符串也可以切片，切片规则与list切片规则一致。
![[Pasted image 20260605165303.png]]

==Note. 字符串是不可变类型，不能直接修改。
如果想要修改，通常是生成新字符串。
	![[Pasted image 20260605165415.png]]
	![[Pasted image 20260605165452.png]]

### 常见的字符串方法

（1）去空格 strip()
	![[Pasted image 20260605165631.png]]
	如果传入参数如*，可以去除指定符号。

（2）大小写转换
	![[Pasted image 20260605165733.png]]

（3）查找
	查找时，会返回字符串第一次出现位置的索引。
	如果没有找到，则会返回-1
	![[Pasted image 20260605170116.png]]
	

（4）替换
	替换replace() 并不会修改原字符串，而是返回新字符串
	![[Pasted image 20260605170246.png]]

（5）分割
	![[Pasted image 20260605170353.png]]
	可以通过在括号中传入符号来根据其他符号切割。

（6）拼接
	![[Pasted image 20260605170445.png]]

（7）统计count（）
	可以统计某个内容出现了多少次
	![[Pasted image 20260605173816.png]]

（8）startswith和endswith
	![[Pasted image 20260605173951.png]]
	判断字符串是否以某个内容开头/结尾
	返回值为True/False


## 3.元组（tuple）

元组可以理解为不能修改的列表。

列表是：nums = [1, 2, 3]
元组是：nums = (1, 2, 3)

元组的定义：
![[Pasted image 20260606115356.png]]
元组名称 = （）可以定义一个空元组。
可以不写括号，但不建议

==Note. 只有一个元素时也要加逗号，否则会被读取成普通括号。

元组可以索引，切片，遍历
count（）：统计元素在元组中出现的次数
index（）：查找某元素在元组中的索引位置（第一次出现的位置）

元组不能修改，是不可变的。

==因此，元组的核心用途是保存一组不希望被修改的数据。

### 元组的组包与解包

（1）**组包**就是：把多个值自动打包成一个元组。
	![[Pasted image 20260606121401.png]]
	输出：(10, 20, 30)
		<class 'tuple'>

（2）**解包**就是：把元组里的值拆出来，分别赋给变量。
	![[Pasted image 20260606121529.png]]
	==用这种方式解包时，左右数量必须一致
	多变量赋值用的就是这种原理

（3）星号解包
	如果右边元素太多，可以用 `*` 收集剩余元素：
	![[Pasted image 20260606121803.png]]
	==b会变成列表，而不再是元组。
	可以通过
	![[Pasted image 20260606123007.png]]
	将元组变成list：a = [1,2,3,4,5]
	Note. 一个解包表达式里，\*只能有一个

## 4. 集合（set）

集合是一组无序、不可重复、可修改的数据容器，可以理解为一个自动去重的容器。

![[Pasted image 20260606135702.png]]
输出：{1, 2, 3}
重复的元素会自动消失。

### 1）创建集合

方式1：s = {1, 2, 3}

==空集合必须通过：s = set()定义
s = {}  定义出来的是字典。

方法2：从列表转换
![[Pasted image 20260606135848.png]]

### 2）集合的基本方法

（1）添加元素：add()
	![[Pasted image 20260606140116.png]]
	结果：{1, 2, 3, 4}
	==重复添加不会报错，也不会成功添加。

（2）删除元素：
	**remove()**
		删除存在的元素时可以成功删除，但是如果元素不存在，会报错。
	**discard()**
		如果元素存在则删掉，不存在也不报错。

（3）获取长度：len(s)

（4）更多其他方法
![[Pasted image 20260606140906.png]]

## 5.字典（dict）

字典类似于map，是一种用“名字”找“值”的容器。
字典中储存着键值对（key : value）类型的数据，可以根据key查找value。
键不能重复，可修改。
其中，key必须是不可变类型，value可以是任意类型。

示例：
![[Pasted image 20260607195131.png]]
==Note. 如果定义dict时出现了重复的键，后出现的对应value会覆盖先出现的value。

### 1）基本功能

（1）取值
	取值时，直接用 字典名[key]，可以取到value的值。
	例如：
	![[Pasted image 20260607195306.png]]
	输出：
		王林
		92
	==直接使用 字典名[key] 取值，如果key不存在，会报错，==
	此时可以使用get()实现安全取值，返回None。
	![[Pasted image 20260607200315.png]]
	也可以指定默认值：
	![[Pasted image 20260607200604.png]]

（2）添加与修改值
	![[Pasted image 20260607195708.png]]
	![[Pasted image 20260607195727.png]]
	使用：
	字典名[key] = value
	如果 key 原本不存在，就是新增。
	如果 key 已经存在，就是修改。

（3）删除
	使用del或 .pop()删除
	其中，使用del删除不会有返回值，.pop() 删除会删除并返回对应值。
	![[Pasted image 20260607200044.png]]
	![[Pasted image 20260607200102.png]]

（4）判断key是否存在
	对字典使用in，默认判断的事key不是value。
	![[Pasted image 20260607200755.png]]

（5）遍历字典
	遍历key
		获取所有的key：字典名称.keys()
		![[Pasted image 20260607200859.png]]
	遍历value
		获取所有的值：字典名称.values()
		![[Pasted image 20260607200931.png]]
	同时遍历key和value（遍历完整的键值对）
		获取所有的键值对：字典名称.items()
		![[Pasted image 20260607201034.png]]

## 数据容器总结与对比
![[Pasted image 20260607212805.png]]

# 核心语法-函数基础

## 1.函数定义
函数可以理解成一个代码工具箱。
当某段代码需要被反复使用时，可以将其定义为函数，以后可以反复使用。

函数的基本格式

```
def 函数名(参数):
    函数体
    return 返回值
```

例如：
```
def say_hello():
    print("Hello!")
```

调用函数：`say_hello()`

==Note. 函数定义之后不会自动执行，必须调用才会执行。
函数必须先定义，后调用。

## 2. 函数参数与返回值

参数是传给函数的数据。

比如：
```
def greet(name):
    print(f"你好，{name}！")
```

调用：
```
greet("Asa")
greet("小星")
```

输出：
```
你好，Asa！
你好，小星！
```

这里的name就像一个临时变量，用来接收传进来的值。
==形参只能在函数内部使用

### 多个参数

```
def introduce(name, age):
    print(f"我叫{name}，今年{age}岁。")
```

调用：`introduce("Asa", 28)`

输出：`我叫Asa，今年28岁。`

==参数顺序需要与函数定义时的参数顺序对应。

### return是什么

return是将函数结果提交出去。

例如：
```
def add(a, b):
    return a + b
```

调用时：
```
result = add(3, 5)
print(result)
```

输出： 8

其中的逻辑是：
```
add(3, 5)
→ 函数内部计算 3 + 5
→ return 8
→ result = 8
```

==Note. （1）没有return的函数会返回None
（2）return会结束函数

### 函数可以返回多个值

Python可以写：
```
def calculate(a, b):
    return a + b, a - b, a * b
```

调用时只需要：
```
sum_result, minus_result, multiply_result = calculate(10, 3)

print(sum_result)
print(minus_result)
print(multiply_result)
```

输出：
13
7
30

==本质上，它返回的是一个元组。
`round(数字， 保留小数位数)`可以在返回时保留指定位数的小数。

### 函数的说明文档

格式：
通常在函数的第一行，
```
def 函数名():
    """
    说明内容
    """
```

多行说明：
```
def get_average(score1, score2, score3):
    """
    计算三个成绩的平均分

    参数：
        score1: 第一个成绩
        score2: 第二个成绩
        score3: 第三个成绩

    返回：
        平均分
    """
    return (score1 + score2 + score3) / 3
```

**查看函数说明文档**
Python提供了函数`help()`
例如：
```
def add(a, b):
    """
    返回两个数字之和
    """
    return a + b

help(add)
```

输出类似：
```
Help on function add:

add(a, b)
    返回两个数字之和
```

说明文档不仅给杜代码的人看，
还可以：

- help()
- IDE提示
- 自动生成文档

使用。
所以更正式。

## 3. 函数的嵌套调用

函数的嵌套调用指的是在一个函数里调用另一个函数。

例如：
```
def say_hello():
    print("你好！")


def welcome():
    say_hello()
    print("欢迎学习Python！")


welcome()
```

输出：
你好！
欢迎学习Python！

这里就是welcome() 里面调用了 say_hello()

==依旧是之前强调的点，函数定义时不会被执行，只有被调用时才会执行，而且是按照被调用的顺序来执行。

# 核心语法-函数进阶

## 1. 变量作用域

变量作用域的核心可以理解为：**变量在哪里创建，就主要在哪里能用。**

**作用域**是一个变量“能被看见、能被使用”的范围。

### 1）局部变量

在函数内部定义的变量，叫**局部变量**。

例如：
```
def say_hello():
    name = "Asa"
    print(name)

say_hello()
```

其中，`name`只属于`say_hello()`函数。
函数执行结束后，它就没办法在外面使用了。

### 2）全局变量

在函数外部定义的变量，叫**全局变量**。

例如：
```
name = "Asa"

def say_hello():
    print(name)

say_hello()
print(name)
```

输出：
Asa
Asa

因为 `name` 定义在函数外面，函数里面也能读取它。

==Note. 函数内部可以读取全局变量，
但是函数里直接修改全局变量会出问题。

### 3）global：声明要使用全局变量

如果真的要在函数中修改全局变量，要写：
```
count = 0

def add():
    global count
    count += 1
    print(count)

add()
add()
```

输出：
1
2

`global count` 的意思是：
这个函数里的 `count` 指的是外面的全局变量，不是新建局部变量。

==大量使用全局变量会导致代码难以追踪

### 局部变量和全局变量重名

```
name = "全局Asa"

def test():
    name = "局部Asa"
    print(name)

test()
print(name)
```

输出：
局部Asa
全局Asa

==函数内部的 `name` 是局部变量，不会影响外面的 `name`。

==形参也是局部变量。

## 2. 参数传递方式

参数传递方式其实是在讲，调用函数的时候，参数怎么传进去。

### 1）位置参数（Positional Argument）

指按照位置匹配参数，如：
```
def subtract(a, b):
    print(a - b)

subtract(10, 3)
```

结果：7

通过位置对应，系统会认为：
```
a = 10
b = 3
```

### 2）关键字参数（Keyword Argument）

可以通过键值对，直接指定将参数传递给谁。

例如：
```
introduce(age=28, name="Asa")
```

对应：
```
name = Asa
age = 28
```

### 3）混合使用

混合使用时，位置参数必须放前面，关键字参数必须放后面。

例如：
允许：`introduce("Asa", age=28)`
不允许：`introduce(name="Asa", 28)`

### 4）默认参数

例如：
```
def greet(name, message="你好"):
    print(f"{message}，{name}")
```

调用时，如果输入：`greet("Asa")`
则输出：`你好，Asa`

如果输入：`greet("Asa", "晚上好")`
则输出：`晚上好，Asa`

可以理解为：
```
没传值
↓
用默认值

传了值
↓
覆盖默认值
```

==与混合参数同理，默认参数必须放在后面。

### 5）不定长位置参数 *

例如：
```
def get_sum(*nums):
    print(nums)
```

调用：`get_sum(1, 2, 3)`
输出：`(1, 2, 3)`

调用：`get_sum(1)`
输出：`(1,)`

也就是说，可以传任意个参数（0个也可以），Python会自动打包成元组。

### 6）不定长关键字参数 **

例如：
```
def show_info(**info):
    print(info)
```

调用：`show_info(name="Asa", age=28)`
输出：`{'name': 'Asa', 'age': 28}`

调用：`show_info(name="Asa")`
输出：`{'name': 'Asa'}`

==Python自动帮你打包成字典。

### 混合使用

例如：
```
def calculate(*nums, **kwargs):
    avg = sum(nums) / len(nums)

    round_digits = kwargs.get("round")
    should_print = kwargs.get("print")

    if round_digits is not None:
        avg = round(avg, round_digits)

    if should_print:
        print(avg)

    return avg
```

调用：
```
calculate(
    95,
    88,
    76,
    round=1,
    print=True
)
```

执行过程：
```
nums
↓
(95, 88, 76)

kwargs
↓
{
    "round": 1,
    "print": True
}
```

然后：`kwargs.get("round")`


==Note. 不定长位置参数适合处理数量不确定的数据，不定长关键字参数适合处理不确定的选项。

## 3. 函数作为参数

一个函数可以像普通变量一样，被传进另一个函数里使用。

例如：
```
def add(a, b):
    return a + b


def calculate(x, y, func):
    result = func(x, y)
    return result


print(calculate(3, 5, add))
```

输出： 8

==注意这里传的是`add`，不是`add()`，`add` 是把函数本身传进去；`add()` 是立刻执行函数，把执行结果传进去。

`func(x, y)`中，这里的 `func` 其实就是外面传进来的 `add`。

### 将函数作为参数，可以让函数更灵活

比如你有一个处理数字的函数：
```
def double(x):
    return x * 2


def square(x):
    return x ** 2


def process_number(num, func):
    return func(num)
```

调用时：
```
print(process_number(5, double))  # 10
print(process_number(5, square))  # 25
```

`process_number` 不关心你到底想翻倍还是平方，它只负责：
```
拿到数字
↓
调用你传进来的处理方法
```

这就是**把行为作为参数传进去**。

## 4. 匿名函数（lambda表达式）

`lambda` 本质上就是：临时写一个很短的小函数，不专门起名字。

基本格式：
```
lambda 参数: 返回值
```

使用时，可以配合函数作为参数：

```
def calculate(a, b, func):
    return func(a, b)


print(calculate(3, 5, lambda a, b: a + b))
```

这里的`lambda a, b: a + b`，就是一个临时函数。

再比如对列表排序：
```
students = [
    {"name": "Asa", "score": 95},
    {"name": "Tom", "score": 80},
    {"name": "Mia", "score": 88}
]

students.sort(key=lambda student: student["score"])

print(students)
```

意思是：排序时，每个 student 用` student["score"] `作为排序依据。

==`lambda` 只能写一个表达式，不能多个表达式嵌套。

## 案例1: 递归

递归就是函数在自己的函数体内调用自己。
但是递归不等于无限循环，递归必须有`终止条件（Base Case）`，否则会无限调用下去。

### 1.递归的两个组成部分

1）**终止条件**
	终止条件用于结束递归
	例如：
`	if n == 1:
    return 1`

2)**递归调用**
	将问题逐步缩小
	例如：
	`return n * factorial(n - 1)`
	这里：
	```factorial(5)
	↓
	factorial(4)
	↓
	factorial(3)
	...```
	不断向终止条件靠近。

### 2. 阶乘案例

数学定义：
```
5!
=
5 × 4 × 3 × 2 × 1
=
120
```

递归实现：
```
def factorial(n):
    if n == 1:
        return 1

    return n * factorial(n - 1)
```

递归的本质是：**当前层解决自己负责的部分，剩下的交给下一层。**

## 5. 类型注解

### 基本介绍

类型注解是Python中的一种语法特性，用于明确标识变量、函数参数和返回值的数据类型，从而使代码更清晰、更安全、更易维护。

**1）变量的类型注解**

例如：
```
name: str = "Asa"

age: int = 28

height: float = 168.5
```

这里的：`name: str`表示`name应该是字符串`

==Note. 类型注解 ≠ 类型检查，类型注解不会阻止代码运行。
l例如，`age: int = "Asa"`照样能跑。

 **2）函数中的类型注解**

例如：
```
def add(a: int, b: int) -> int:
    return a + b
```

表示:
```
a: int ———— 参数a应该是int
b: int ———— 参数b应该是int
-> int ———— 返回值应该是int
```

 **更多总结示例**：
```
# =========================
# 基本类型
# =========================

name: str = "Asa"
age: int = 28
height: float = 165.5
is_student: bool = True


# =========================
# List（列表）
# =========================

scores: list[int] = [90, 95, 88]

names: list[str] = [
    "Asa",
    "Tom",
    "Jack"
]

prices: list[float] = [
    12.5,
    15.8,
    20.0
]


# =========================
# Tuple（元组）
# =========================

student: tuple[str, int, float] = (
    "Asa",
    28,
    3.9
)

numbers: tuple[int, ...] = (
    1,
    2,
    3,
    4,
    5
)


# =========================
# Set（集合）
# =========================

ids: set[int] = {
    1,
    2,
    3
}

tags: set[str] = {
    "Python",
    "Java",
    "AI"
}


# =========================
# Dict（字典）
# =========================

scores_dict: dict[str, int] = {
    "Math": 95,
    "English": 88
}

user_info: dict[str, str] = {
    "name": "Asa",
    "city": "Chiang Mai"
}

prices_dict: dict[str, float] = {
    "Apple": 3.5,
    "Banana": 2.8
}


# =========================
# 函数参数与返回值注解
# =========================

def add(a: int, b: int) -> int:
    return a + b


def get_name() -> str:
    return "Asa"


def get_scores() -> list[int]:
    return [90, 95, 88]


def get_student_scores() -> dict[str, int]:
    return {
        "Math": 95,
        "English": 88
    }


def count_vowel(text: str) -> int:
    vowels = "aeiou"
    count = 0

    for c in text.lower():
        if c in vowels:
            count += 1

    return count
```

# 核心语法-模块

## 1.基本介绍

模块（module）可以理解成：
一个 `.py` 文件，就是一个模块。  
模块的作用是：把代码分开放，哪里需要哪里导入。

**模块的主要作用有三点：**
1. 复用代码
2. 拆分文件
3. 使用别人写好的功能

例如，一个文件叫：`math_tools.py`
里面写：
```
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

另一个文件叫：`main.py`
里面使用它：
```
import math_tools

print(math_tools.add(1, 2))
print(math_tools.subtract(5, 3))
```

这就是**导入模块**。

## 2. 导入模块

### 1）导入整个模块

语法：`import 模块名`
例如：`import math`

使用时：
```
print(math.pi)
print(math.sqrt(16))
```

优点是清楚：`math.sqrt` 一看就知道来自 `math` 模块。

### 2）只导入某个功能

语法：`form 模块名 import 函数名`
例如：`from math import sqrt`

使用时：`print(sqrt(16))`

优点是写起来短，但来源没那么明显。

### 3）起别名

例如：
```
import random as rd

print(rd.randint(1, 10))
```

### 4）不推荐但可能会见到

```
from math import *
```

意思是把 `math` 里面很多东西都导进来，可以直接写：
```
print(sqrt(16))
print(pi)
```

但不推荐，因为名字来源不清楚，容易冲突。

## 3.自定义模块

自定义模块就是：自己写一个`.py`文件，然后在另一个 `.py`文件里导入它。

例如有两个文件
```
math_tools.py
main.py
```

在 `math_tools.py` 里写：
```
def add(a: int, b: int) -> int:
    return a + b


def subtract(a: int, b: int) -> int:
    return a - b
```

然后在 `main.py` 里使用：
```
import math_tools

print(math_tools.add(3, 5))
print(math_tools.subtract(10, 4))
```

输出：
8
6

==重点是：**文件名就是模块名。**

`math_tools.py`导入时写：`import math_tools`
不要写：`import math_tools.py`

==定义常量时，名称全部大写。

**导入时，被导入模块的可执行代码会自动执行。**
此时可以使用：`__name__`(两个下划线，name， 两个下划线)
直接运行当前模块，`__name__`的值为`_main_`，被导入时，其值为模块名。

所以测试代码一般写成：
```
def add(a, b):
    return a + b


if __name__ == "__main__":
    print(add(1, 2))
```

意思是，只有直接运行 `math_tools.py` 时，才执行测试代码；如果它是被别人导入，就不执行测试代码。


另一个特殊变量：`__all__`

类似于模块对外开放名单。
在模块内写：
```
__all__ = [
    "add",
    "subtract"
]
```
时，
```
当别人使用：

from module import *

时

只导出这里列出的名字
```

类似于控制` import * `的导出列表，并不影响直接import整个模块的效果。

## 4. 软件包（package）

包的本质是装模块的文件夹。

```
文件夹里必须有

__init__.py

储存初始化信息，表示：

这是个包
```

速记版：
```
模块（module）
=
一个 .py 文件

包（package）
=
存放多个模块的文件夹

作用：
管理大量模块
组织项目结构

关系：

包
 ↓
模块
 ↓
函数
```

```
# =========================
# 假设项目结构
# =========================

project/

    main.py

    tools/

        __init__.py

        math_tools.py

        string_tools.py


# =========================
# 导入整个模块
# =========================

import tools.math_tools

result = tools.math_tools.add(1, 2)


# =========================
# 导入包中的模块
# =========================

from tools import math_tools

result = math_tools.add(1, 2)


# =========================
# 导入模块中的指定内容
# =========================

from tools.math_tools import add

result = add(1, 2)


# =========================
# 导入多个内容
# =========================

from tools.math_tools import add, subtract

result1 = add(1, 2)
result2 = subtract(5, 3)


# =========================
# 导入模块并起别名
# =========================

import tools.math_tools as mt

result = mt.add(1, 2)


# =========================
# 导入指定内容并起别名
# =========================

from tools.math_tools import add as plus

result = plus(1, 2)


# =========================
# 导入全部（不推荐）
# =========================

from tools.math_tools import *

result = add(1, 2)


# =========================
# __init__.py 统一导出
# =========================

# tools/__init__.py

from .math_tools import add
from .math_tools import subtract


# =========================
# 使用统一导出后的导入方式
# =========================

from tools import add

result = add(1, 2)
```

# 核心语法-面向对象基础

类与对象：
类描述的是一组具有相同属性（特征）和方法（功能/行为）的模板。
对象是类的实例，是基于类创建出来的（实例对象）。

## 1. 类与对象

### 1） 类是对一类事物的描述和抽象

定义类的语法：
```
class 类名:
    pass
```

类名规范：**采用大驼峰命名法**

例如：
```
Student
UserInfo
StudentSystem
```

### 2）对象是根据类创建出来的具体实例

例如：
```
类
↓
学生

对象
↓
Asa
Tom
Jack
```

### 3）创建对象的语法

创建对象：`对象名 = 类名()`
例如：stu = Student()

给对象添加属性：`对象名.属性名 = 值`
例如：
```
stu = Student()

stu.name = "Asa"
stu.age = 28
stu.score = 95
```

获取属性：
```
print(stu.name)
print(stu.age)
print(stu.score)
```

输出：
Asa
28
95

### 4）定义方法

方法本质上是定义在类中的函数

语法：
```
class Student:

    def study(self， 形参列表):
        方法体
```

==定义方法必须写self

### 5)调用方法

语法：`对象名.方法名()`

例如：
```
stu = Student()

stu.study()
```

### 6）在方法中访问属性

例如：
```
class Student:

    def study(self):
        print(f"{self.name}正在学习")
```

创建对象：
```
stu = Student()

stu.name = "Asa"

stu.study()
```

输出：`Asa正在学习`

此处的`self.name`，表示`当前对象的name属性`

### 7）dict

`__dict__`用来查看对象内部保存的所有属性。

例如：
```
class Student:
    pass


stu = Student()

stu.name = "Asa"
stu.age = 28
stu.score = 95

print(stu.__dict__)
```

输出：
```
{
    'name': 'Asa',
    'age': 28,
    'score': 95
}
```

### 8）在类中定义属性的两种方法

**直接定义：**

语法：
```
class 类名:

    属性名 = 默认值
```

例如：
```
class Student:

    name = ""
    age = 0
    score = 0
```

创建对象后，可以修改属性：
```
stu = Student()

stu.name = "Asa"
stu.age = 28
stu.score = 95
```

**初始化：`__init__()`**

`__init__`：初始化方法，对象创建后自动调用，主要用于设置对象的初始状态。

定义的语法：
```
class Student:

    def __init__(self, 参数列表):
        self.属性名 = 参数值
        self.属性名 = 参数值
```

例如：
```
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

创建对象：`stu = Student("Asa", 28)`

此时：
```
print(stu.name)
print(stu.age)
```

输出：
Asa
28

==Note：一个类通常只有一个`__init__`

## 2. 魔术方法

魔术方法就是：Python在特定情况下自动调用的方法。

它的特点是：`__xxx__`
前后都有两个下划线。

例如：
```
__init__
__str__
__dict__
__len__
```

这些方法一般不会手动调用，而是Python在执行操作时自动调用。

```
魔术方法（Magic Method）

特点：
1. 前后都有两个下划线
2. Python在特定情况下自动调用
3. 用于定制对象行为

常见魔术方法：

__init__()
作用：构造器，对象创建时自动执行

__str__()
作用：print(对象)时自动执行

__dict__
作用：查看对象内部属性

__len__()
作用：len(对象)时自动执行
```

### str（最常见）

例如：
```
class Car:

    def __init__(self, color):
        self.color = color


car = Car("red")

print(car)
```

输出：`<__main__.Car object at 0x123456>`

于是可以定义：
```
class Car:

    def __init__(self, color):
        self.color = color

    def __str__(self):
        return f"Car(color={self.color})"
```

再运行：`print(car)`
输出：`Car(color=red)`

### 对象的比较

 **gt（greater than）**：

例如：
```
class Student:

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __gt__(self, other):
        return self.score > other.score
```

此时：
```
s1 = Student("Asa", 95)
s2 = Student("Tom", 80)

print(s1 > s2)
```

输出：True

同理：`lt(less than)`, `eq(equal)`

总结：
```
对象比较魔术方法

__gt__(self, other)
作用：
定义 > 的比较规则

__lt__(self, other)
作用：
定义 < 的比较规则

__eq__(self, other)
作用：
定义 == 的比较规则

执行过程：

obj1 > obj2
↓
obj1.__gt__(obj2)

obj1 < obj2
↓
obj1.__lt__(obj2)

obj1 == obj2
↓
obj1.__eq__(obj2)
```

## 3. 实例属性与类属性

通过类创建出来的对象，叫实例

例如：
```
class Student:
    pass


stu1 = Student()
stu2 = Student()
```

这里：
```
Student 是类
stu1、stu2 是实例 / 对象
```

### 1）实例属性是什么

**属于某一个具体对象的属性**，叫实例属性
实例属性通过`实例对象.属性名`的方式操作

例如：
```
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


stu1 = Student("Asa", 28)
stu2 = Student("Tom", 20)
```

这里，
```
self.name = name
self.age = age
```

创建的就是实例属性，每个对象都有自己独立的一份。
修改 `stu1.name` 不会影响 `stu2.name`。

### 2）类属性

**直接定义在类里面，不写在** **`self`** **上的属性**，叫类属性
类属性通过`类名.属性名`的方式操作

例如：
```
class Student:
    school = "Python School"

    def __init__(self, name):
        self.name = name
```

这里的：`school = "Python School"`就是类属性。
它属于 `Student` 这个类，而不是某个单独对象。

==类属性是所有实例对象共享的

### 一个容易踩的坑：用对象修改类属性

使用：`stu1.school = "Asa School"`时
这不是修改类属性，而是给 `stu1` 单独创建了一个实例属性 `school`。

此时：
```
print(stu1.school)      # Asa School
print(stu2.school)      # AI School
print(Student.school)   # AI School
```

也就是说，`stu1.school` 会优先找实例自己的属性。如果找不到，才去类里找。

**查找顺序**
```
先找 stu1 自己有没有 school
↓
如果没有
↓
再去 Student 类里找 school

即，访问顺序：
对象.属性
先找实例属性
找不到再找类属性
```

# 核心语法-异常

异常是程序运行过程中出现的问题。

比如：
`num = int(input("请输入数字："))`

用户输入：abc

程序会报错：`ValueError`

如果不处理异常，用户乱输入，程序直接终止。
但是我们希望：
```
输入错了
↓
提示用户
↓
程序继续运行
```

此时我们就需要 `try except`，处理异常。

## 1. 基本写法

```
try:
    可能出错的代码
except:
    出错后执行的代码
```

例如：
```
try:
    num = int(input("请输入数字："))
    print(num)
except:
    print("输入错误，请输入数字！")
```

## 2. 捕获指定异常

通常，更推荐写清楚异常类型：
```
try:
    num = int(input("请输入数字："))
    print(num)
except ValueError:
    print("输入的不是数字！")
```

这里的 `ValueError` 就是：`值的格式不符合要求`，例如 `"abc"` 转 int 失败。

此外，也可以捕获多个异常：
```
try:
    a = int(input("请输入a："))
    b = int(input("请输入b："))
    print(a / b)

except ValueError:
    print("请输入数字！")

except ZeroDivisionError:
    print("除数不能为0！")
```

==常见异常：
```
ValueError：值不合法
ZeroDivisionError：除以0
IndexError：索引越界
KeyError：字典key不存在
FileNotFoundError：文件不存在
```

## 3. 获取异常信息

```
try:
    num = int(input("请输入数字："))
except ValueError as e:
    print("发生错误：", e)
```

`e` 里面保存具体错误信息。

## 4. else 与finally

**`else`** 表示：`没有发生异常时执行`

例如：
```
try:
    num = int(input("请输入数字："))
except ValueError:
    print("输入错误！")
else:
    print("转换成功：", num)
```

**`finally`** 表示：`无论有没有异常，都会执行`

例如：
```
try:
    file = open("test.txt", "r")
except FileNotFoundError:
    print("文件不存在")
finally:
    print("程序结束")
```

常用语：
关闭文件
释放资源
收尾工作

## 完整结构

```
try:
    可能出错的代码

except 异常类型:
    出错时执行

else:
    没出错时执行

finally:
    无论如何都执行
```

## 5. 异常的传递

异常传递是异常在函数调用中层层上报的过程，直到有人处理它，或者程序崩溃。

例如：
```
def test():
    print(10 / 0)

test()
```

运行：`ZeroDivisionError`

其中的过程为：
```
test()
↓
10/0
↓
异常产生
```

由于`test()`里面并没有处理异常，于是Python会将异常向外抛，这就是异常的传递。

通常，处理异常的思路为：
```
能处理的地方处理

不能处理的地方继续往上抛

最外层(main/run)负责兜底
```



