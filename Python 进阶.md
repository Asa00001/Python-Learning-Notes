# 第一章 面向对象基础 

## 1.面向对象和面向过程

**编程思想**
	就是人们利用计算机来解决问题的思维

### 分类

1）面向过程
	一种编程思想，强调的是以步骤为基础完成各种操作

2）面向对象
	**参考思路**：概述、思想特点、举例、总结
	一种编程思想，强调的是以对象为基础完成各种操作，它是基于面向过程的。
	面向对象的三大思想特点：
	a. 更符合人们的思考习惯
	b. 把复杂的事情简单化
	c. 把程序员从执行者变成指挥者
	举例：越符合当时的场景越好

## 2.封装简介

面向对象通常具有三大特性，即：
```
封装
继承
多态
```

**封装**：把数据和操作数据的方法放到一起，并隐藏不希望别人直接操作的内容。
**继承**：新的类，可以直接拥有旧类的功能。
**多态**：同一个方法调用，不同对象表现不同。

### 封装

在面向对象中，封装就是隐藏对象的属性和实现细节，仅对外公开接口，控制在程序中属性的读和修改的访问级别，将抽象得到的数据和行为相结合，形成一个整体。
也就是将数据与操作数据的源代码进行结合，形成类，其中数据和函数都是类的成员。

封装的目的是简化编程，增强安全性和复用性。
	- 使用者不知道具体的实现细节，而只是要通过外部接口
	- 以特定的访问权限来使用类的成员

### 继承

继承就是子类继承父类的属性和方法，使子类对象具有父类的特征和行为。
可以提高代码的复用性。

只要是继承，都会满足`is - a`的关系。
即，子类 is a 父类的实例。

### 多态

多态是指不同类的对象对同一消息作出响应，即同一消息可根据发送对象的不同而采取多种不同的行为方式。
即，同一个函数，接收不同的对象，有不同的效果。

## 3. 定义类格式介绍

类和对象：
![[Pasted image 20260711103414.png]]

类：对现实事物的抽象描述
对象：对现实事物的具体体现

### 入门案例 - 汽车类

```
"""
案例：演示定义汽车类，使用类中的成员
"""

class Car:
    # 属性

    # 行为
    def run(self):
        print("车车跑起来了……")


my_car = Car()

my_car.run()
```

## 4. self关键字

self是python内置的关键字，用于指向对象实例本身。

一个类可以有多个对象，通过self，可以定位到具体调用函数的对象。

### 类内访问
在类外访问类中的行为，需要通过`对象名.`的方式访问
在类内访问，需要用`self.`的方式访问
==类内的`self`等价于类外的`对象`。==

例如：
```
#需求：定义汽车类，类内有run（）函数，并在work（）中调用run（）函数，创建该类对象，调用上述函数

class Car:
	def run(self):
		print(f"{self}汽车在跑……")

	def work(self):
		print(f"我是work函数，我的self是{self}")
		self.run() #self代表本类当前对象的引用

c1 = Car()
c1.run()
c1.work()
```

## 5. 属性

属性表示的是固有特征，在Python中使用变量表示，
例如人的姓名、年龄、身高、体重，都属于属性。

### 1）在类外添加和获取对象属性

设置属性：
	`对象名.属性名 = 属性值`
	特点：该属性独属于这个对象，即，该类的其他对象没有这个属性。

获取对象的属性：
	`对象名.属性名`

### 2）在类内设置和获取对象的属性

类内通过`self.`的方式访问成员属性

类内设置属性，需要结合魔法方法`__init__`

## 6. 魔法方法

在Python中，有一些可以给Python类增加魔力的特殊方法，它们被双下划线包围，我们称之为魔法方法。
魔法方法在特殊情况下会被自动调用，不需要开发者手动调用。
```
__魔法方法名__()
```

### 1）`__init__()`方法

在Python中，当新创建一个对象时，则会自动触发`__init__()`方法。

无参数情况：
	不需要外面传递参数，初始化属性值

有参数情况：
	需要外面传递参数，初始化属性值

无参版示例：
```
class Car:

	def __init__(self):
		self.color = "red"
		self.wheel = 4

c1 = Car()

print(f"汽车颜色为：{c1.color}，轮胎有{c1.wheel}个。")

print('**' * 35)

c2 = Car()
c2.color = "black"

print(f"汽车颜色为：{c2.color}，轮胎有{c2.wheel}个。")
```

有参版示例：
```
class Car:
	def __init__(self, color, wheels):
		self.color = color
		self.wheels = wheels

c1 = Car("red", 4)
print(f"汽车颜色为：{c1.color}，轮胎有{c1.wheels}个。")

print('**' * 35)

c2 = Car("black", 6)
print(f"汽车颜色为：{c2.color}，轮胎有{c2.wheels}个。")
```

### 2）`__str()__`方法

当使用`print()`函数打印对象的时候，会自动调用对象所在类的`__str()__`魔法方法。
该魔法方法默认打印的是对象的地址值，无意义，因此一般会重写`__str()__`魔法方法。

`__str()__`需要返回一个字符串。

### 3）`__del_`方法
当删除对象时（`调用del删除对象`或`文件执行结束后`），Python解释器会默认调用`__del__`方法。
如果说`__init__`是在对象出生时被自动调用，那么`__del__`就是在对象死亡时自动调用。

综合案例：
```
class Car:

	def __init__ (self, brand):
		self.brand = brand

	def __str__ (self):
		return f"品牌：{self.brand}"

	def __del__(self):
		print("已删除")

c1 = Car("福特")
print(c1)

print(c1.brand)
print("*" * 35)

del c1

print("程序结束。")
```

输出：
```
品牌：福特
福特
***********************************
已删除
程序结束。
```

如果不调用`del c1`，则输出为：
```
品牌：福特
福特
***********************************
程序结束。
已删除
```

## 2. 创建类的格式

| **写法**                   | **Python 3 中的意义**        |
| ------------------------ | ------------------------ |
| `class Student:`         | ✅ 最推荐，默认继承 `object`      |
| `class Student():`       | ✅ 可以写，但括号为空，没有额外作用       |
| `class Student(object):` | ✅ 显式写出继承 `object`，和第一种等价 |
`class Student():`的括号中，可以写父类名表示继承，
可以把括号理解成：
**“我要继承谁，就把谁写进括号里。”**

只是当什么都不写的时候，Python 会默默帮你写成：
```
class Student(object):
```

所以现在我们几乎都会直接写：
```
class Student:
```

## 3. 继承（Inheritance）

面向对象中代码的继承，指子类继承父类的属性和方法。

```
class 类名(父类名):
	pass
```

继承可以提高代码的复用性，但是耦合性增强了。

继承：一个类从另一个已有的类获得其成员的相关特性，就叫做继承（站在子类角度）。
派生：从一个已有的类产生一个新的类，称为派生（站在父类角度）。

父类也就是基类，子类也就是派生类（拓展类）。

### 1）单继承

单继承指一个类只继承自一个父类。

### 2）多继承

多继承指一个类同时继承了多个父类，并且同时具有所有父类的属性和方法。

基本语法：
```
#父类1
class Father:
	pass

#父类2
class Mother:
	pass

#子类
class Son(Father, Mother):
	pass
```

如果多个父类中有同名方法，则会优先调用父类列表中排名靠前的父类的方法。
可以使用`类名.__mro__属性`或`类名.mro()`方法查看调用的先后顺序。

**MRO（Method Resolution Order）方法解析顺序。**

# 第二章 面向对象高级

## 1. 子类重写父类功能

重写也叫做覆盖，就是当子类属性或方法与父类的属性或方法名字相同时，从父类继承下来的成员可以重新定义。
子类重写父类的属性和方法，会优先调用子类的属性和方法。
重写的本质是，子类创建了一个与父类方法同名的方法，使用时被优先调用。

### 子类中仍想保留父类的行为，则需要在子类中调用父类方法
1）方法一
	可以直接使用父类名来进行调用，使用方法为：`父类名.父类方法名(self)`
	相当于把父类的self换成子类自己的self，然后直接使用。

2）方法二
	`super().父类函数名()`
	此方法遵循就近原则，无法精准访问（有就用，没有就往后继续查找）。

### 继承与多层继承

多层继承：类A继承类B，类B继承类C，这就是多层继承。

## 2. 封装
封装属于面向对象的三大特征之一，即隐藏对象的属性和实现细节，仅对外提供公共的访问方式。
封装可以为属性和方法提供私有权限。

封装可以提高代码的安全性（私有）和复用性（函数）
封装的弊端：代码量可能增加（私有内容外界想访问，必须提供公共的访问接口）

在Python中，可以为属性和方法设置私有权限，即设置某个属性和方法不能继承给子类。
设置私有属性和方法的方式：在属性名或方法名前面加上`__`（两个下划线）格式。

- 私有属性外部无法访问
```
class Person:
	def __init__(self):
		self.__money = 10000 # 私有属性，外部无法直接访问
```

```
print(p1.__money) # 尝试访问私有属性，会报错
```

- 可以通过类名访问私有属性，但是不推荐
```
print(p1._Person__money) # 通过类名访问私有属性，虽然可以访问，但不推荐这样做
#同理可以强制修改私有属性
```
### getter和setter

- 定义访问接口getter，可以合法访问私有属性
```
def get_money(self):
	return self.__money # 提供一个公共方法来访问私有属性
```

```
print(p1.get_money()) # 通过公共方法访问私有属性，推荐这样做
```

- 通过定义setter，允许合法修改私有属性
```
def set_money(self, amount):
	if amount >= 0:
		self.__money = amount # 提供一个公共方法来修改私有属性
	else:
		print("金额不能为负数！")
```

```
p1.set_money(15000) # 通过公共方法修改私有属性，推荐这样做
```

Note. 当我们写
```
p1.__money = 50000
```
此时不会修改私有属性，而是重新定义了一个属性名为`__money`的普通属性。

尝试：
```
class Person:
    def __init__(self):
        self.__money = 10000

p1 = Person()

p1.__money = 50000

print(p1.__dict__)
```

输出会变成：
```
{
    '_Person__money': 10000,
    '__money': 50000
}
```

## 3. 多态（Polymorphism)

多态指的是一个函数接收不同的参数，有不同的效果。

实现多态的三个条件
- 有继承（定义父类、定义子类、子类继承父类）
- 函数重写（子类重写父类的函数）
- 父类引用指向子类对象（子类对象传给父类对象调用者）

例如：
```
class Animal:
    def speak(self):
        pass


class Dog(Animal):
    def speak(self):
        return "汪汪汪"


class Cat(Animal):
    def speak(self):
        return "喵喵喵"


def animal_sound(animal):
    print(animal.speak())


dog = Dog()
cat = Cat()

animal_sound(dog)
animal_sound(cat)
```

输出：
```
汪汪汪
喵喵喵
```

这里：
```
animal.speak()
```
始终没有改变。

变化的是：
```
Dog → speak()
Cat → speak()
```

因此：
**同样的方法调用，在不同对象上产生不同的行为，这就是多态。**

**Note. **
Python 更强调：**对象能做什么（Behavior），而不是对象属于什么（Type）。**
因此，只要对象拥有：`speak()`
即可：`animal_sound(obj)`

例如：
```
class Robot:
    def speak(self):
        return "电子狗：汪"

robot = Robot()

animal_sound(robot)
```
也可以正常运行。

此时可以使用类型注解（Type Hint），
```
def animal_sound(animal: Animal):
    print(animal.speak())
```

语法是：
```
变量名:类型
```

虽然无法强制确保用户的输入类型正确（**类型注解默认不会参与运行时检查**），但是能使IDE提示，程序员也可以作为参考。

示例：
```
class Hero:
	def power(self):
		pass

class HeroFighter(Hero):
	def power(self):
		return 60

class AdvancedFighter(Hero):
	def power(self):
		return 80

class EnemyFighter:
	def power(self):
		return 70

def object_play(hero: Hero, enemy: EnemyFighter):
	if hero.power() > enemy.power():
		print("英雄获胜")
	elif hero.power() < enemy.power():
		print("敌人获胜")
	else:
		print("平局")

object_play(HeroFighter(), EnemyFighter()) # 输出: 敌人获胜

object_play(AdvancedFighter(), EnemyFighter()) # 输出: 英雄获胜
```

### 小节
![[Pasted image 20260719145620.png]]

## 4. 抽象类（接口）

这种设计的含义是：
- 父类来确定有哪些方法（父类制定接口标准）
- 具体方法由子类来实现

这种写法就叫做抽象类（也可称之为接口）

抽象类：含有抽象方法的类
抽象方法：方法体是空实现（pass）的方法

抽象类一般充当父类用，用来制定标准。

## 5. 对象属性和类属性介绍

对象属性指的是属于每个对象的属性，即每个对象的属性值可能都不同。
修改A对象的属性，不影响B对象的属性。
对象属性定义到init中，每个对象都有自己的内存，只能通过`对象名.`的方式调用。

类属性指的是类所拥有的属性，它被共享于整个类中（即都可以直接调用）
A对象修改属性，B对象访问的是修改后的属性。
调用类属性：
```
类名.属性名 #推荐使用
对象名.类属性名
```

### 类属性与实例属性

**类变量**
	类变量是属于类本身的一个变量，类似于`static`，不需要实例化就可以存在。
	当实例化对象时，每个实例化对象都会指向这一份已经存在的变量，而不是各自单独存储。

**实例变量**
	如果使用`__init__()`方法，或者在类外添加，使实例拥有某个变量，则这个变量属于实例变量。
	实例变量由每个实例各自存储，进行修改也只影响本实例的表现。

访问时，Python会按顺序查找。
首先确定实例是否有自己的变量，如果有，则使用实例变量，否则会查找是否存在该名称的类变量。

在实例中对类变量进行修改，该操作实际上是构建了一个同名的实例变量。

### 类方法与静态方法

**类方法**
类方法指类所拥有的方法，并需要使用装饰器`@classmethod`来标识其位类方法。
同时需要注意，对于类方法的第一个参数必须是类对象，通常以cls作为第一个参数名。
```
@classmethon
def 类方法名(cls):
	…
```

调用方式：
```
类名.方法名 #推荐使用
对象名.类方法名
```

**静态方法**
静态方法需要通过装饰器`@staticmethod`来标识其位静态方法，且静态方法不需要再定义参数。
```
@staticmethod
def 静态方法名():
	pass
```

调用方式：
```
类名.方法名 #推荐使用
对象名.静态方法名
```

区别：
- 类方法的第一个参数必须是类对象，静态方法无参数要求。
- 可以理解为，如果函数中要用类对象，就定义成类方法，否则定义成静态方法。
- 除此并无区别。

## 一些补充知识点
### `__dict__`属性

`__dict__`是Python内置的属性，可以把对象转成字典形式，会返回**对象所有实例属性**组成的一个字典。

例如：
```
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

stu = Student("Asa", 28)
```

打印：`print(stu.__dict__)`

结果：
```
{
    "name": "Asa",
    "age": 28
}
```

**`__dict__`** **不负责保存数据。**
它只是把对象里的实例变量提取出来，并以字典形式返回。

学生对象转字典：`my_dict = s1.__dict__`
字典转学生对象：`s2 = Student(** my_dict)`

### `open()`—— 打开文件

基本语法：
```
open(文件路径, 打开模式, encoding="utf-8") as f
```

例如：
```
open("students.txt", "w", encoding="utf-8") as f
```

作用：
打开指定文件，并返回一个**文件对象（File Object）**，以后所有文件操作都通过这个对象完成。

例如：
```
f.read()

f.write()

f.close()
```

 **常见打开模式**
 **`"r"`**: 读取（Read）
 ```
 open("students.txt", "r")
 ```
要求：文件必须存在。

**`"w"`**: 写入（Write）
```
open("students.txt", "w")
```

特点：
- 文件不存在 → 自动创建
- 文件存在 → 清空原内容重新写入

**`"a"`**: 追加（Append）
```
open("students.txt", "a")
```

特点：
内容追加到文件最后。
不会覆盖原来的内容。

### `with open()`—— 自动关闭文件

作用：自动管理文件资源。
代码执行结束后，Python 会自动关闭文件。
因此无需手动`f.close()`

等价思想：
```
f = open(...)

try:
    ...
finally:
    f.close()
```

所以：`with open(...)`就是 Python 推荐的文件操作方式。

### `as f`

例如：
```
with open(...) as f:
```

意思是：
把打开后的文件对象保存到变量`f`

因此, `f.write(...)`实际上就是：
“对这个文件进行写入操作。”

变量名可以任意命名：
```
as file

as f

as student_file
```
都可以。

### `str()`

老师代码：`f.write(str(stu_dict))`

这里：`stu_dict`
原本是：
```
[
    {"name":"Asa"},
    {"name":"Tom"}
]
```

属于：`list对象`

调用：`str(stu_dict)`之后, 变成`"[{'name':'Asa'}, {'name':'Tom'}]"`
属于`字符串（String）`
最后：`f.write(...)`把这串字符串写进文件。

### 整个保存流程

这节课的数据流：
```
Student对象
        │
        ▼
__dict__
        │
        ▼
dict
        │
        ▼
列表(list)
        │
        ▼
str()
        │
        ▼
字符串(String)
        │
        ▼
write()
        │
        ▼
students.txt
```

# 第三章 闭包（Closure）和装饰器（Decorator）与深浅拷贝

## 1. 闭包（Closure）

通常在调用完一个函数后，函数内定义的变量就会被销毁，但有时会需要保存函数内的这个变量，并对其进行一系列操作，此时就需要引入闭包的概念。
闭包可以延长函数内变量的生命周期。

闭包可以保存函数内的变量，而不会随着调用完函数而被销毁。

### 闭包的语法

在函数嵌套的前提下，内部函数使用了外部函数的变量，并且外部函数返回了内部函数，这种使用外部函数变量的内部函数称为闭包。

```
def 外部函数名（外部参数）：
	def 内部函数名（内部参数）：
		使用外部函数的变量
	return 内部函数名 #不要加小括号
```
==`return 内部函数名`返回函数这个对象本身
`return 内部函数名()` 返回的是内部函数的执行结果==

**闭包的构成条件**
1）有嵌套：在函数嵌套的前提下
2）有引用：内部函数引用外部函数的变量或者外部函数的参数
3）有返回：外部函数返回了内部函数名

### `nonlocal`关键字

`nonlocal`：声明能够让内部函数去修改外部函数的变量
==不声明的情况下，可以使用但是不能修改==

没有生命nonlocal的变量，编译器会将其当成内部函数自己的局部变量处理，从而报错。

**闭包不是“内层函数神奇地随便读取外层变量”。**
它之所以能在外层函数结束后继续使用那个变量，是因为 Python 在创建闭包时，确实会把这个变量纳入闭包环境，给内层函数保留访问它的通道。
**闭包通过引用外层变量自动建立捕获关系；****`nonlocal`** **用来声明对这个已捕获变量进行重新赋值。**

## 2. 装饰器（Decorator）

装饰器的作用是在不改变原有函数的基础上，给原有函数增加额外功能。
装饰器本质上是一个闭包函数。

**装饰器的构成条件**
1）有嵌套：在函数嵌套的前提下
2）有引用：内部函数使用了外部函数的变量
3）有返回：外部函数返回了内部函数名
4）有额外功能：给需要转是的原有函数增加额外功能

### 装饰器语法

方式一：传统方法
```
装饰后的函数名 = 装饰器名（被装饰的函数名）
装饰后的函数名（）
```

方式二：语法糖
```
在要被装饰的函数上，直接写@装饰器名， 之后直接调用函数即可。
```

- ==装饰器本身需要自己写==
- ==使用装饰器后，无法调用装饰前的函数==


**定义装饰器的步骤**

1）定义外部函数，形参列表接受要被装饰的函数名（对象）
2）定义内部函数
3）增加额外功能
4）访问外部函数的引用
5）在外部函数中返回内部函数（对象）

示例代码：
传统方法：
```
def check_login(fn_name): #fn_name：被引用的函数名
	def fn_inner():
		print("校验登陆……登录成功！")
		fn_name()
	
	return fn_inner

def comment():
	print("发表评论")

comment = check_login(comment)
comment()
```

语法糖：
```
def check_login(fn_name): #fn_name：被引用的函数名
	def fn_inner():
		print("校验登陆……登录成功！")
		fn_name()
	return fn_inner

@check_login
def comment():
	print("发表评论")

comment()
```

输出：
```
校验登陆……登录成功！
发表评论
```

### 装饰器的使用
![[Pasted image 20260723190532.png]]
装饰器内部函数格式要和被装饰的函数保持一致。
有参无返回的示例：
```
#定义无参无返回的求和函数，在不改变功能代码的前提下提供友好提示

#定义装饰器

def my_decorator(fn_name):

	def fn_inner(a, b):

		print("正在努力计算中……")

		fn_name(a, b)

	return fn_inner

  

#定义原函数

@my_decorator
def get_sum(a, b):

	sum = a+b

	print(f"sum:{sum}")

get_sum(10, 20)
```

输出：
```
正在努力计算中……
sum:30
```

很好理解，装饰器的内部函数调用需要装饰的函数时，需要提供内部函数所需的参数，
因此，装饰器内部函数格式要和被装饰的函数保持一致。


无参无返回示例：
```
#定义装饰器

def my_decorator(fn_name):

	def fn_inner():
		print("正在努力计算中……")
		return fn_name()
	
	return fn_inner

  

#定义原函数

@my_decorator
def get_sum():
	a = 10
	b = 20
	return a+b

print(get_sum())
```

输出：
```
正在努力计算中……
sum:30
```

由于a+b是作为返回值存在，想要打印需要自己单独操作。

==用传统写法，装饰器可以放在被装饰函数下面（没有顺序要求）；
但是用语法糖的情况下，装饰器一定要写在被装饰函数的上面==

### 可变参装饰器的使用

定义一个可以计算多个数据和字典value值和的函数，并给其友好提示
示例：
```
#1. 定义装饰器

def my_decorator(fn_name):

	def fn_inner(*args, **kwargs):

		print("计算中……")

		return fn_name(*args, **kwargs)

	return fn_inner

#2. 定义原函数

@my_decorator
def get_sum(*args, **kwargs):
	sum = 0
	for i in args:
		sum += i
		
	for v in kwargs.values():
		sum += v
	
	return sum

sum = get_sum(1, 2, 3, a=1, b=2, c=3)
print(f"计算结果为：{sum}")
```

输出：
```
计算中……
计算结果为：12
```

踩到的一个小坑：
```
定义装饰器时，
		return fn_name(*args, **kwargs)
忘记写return，导致输出结果为
计算中……
计算结果为：None

很显然，fn_name(*args, **kwargs)的结果传给了装饰器，但没被接住。
```

### 多个装饰器的使用

多个装饰器的本质就是，多个函数一次包装同一个原函数。
多个装饰器的装饰过程是：里函数最近的装饰器先装饰，然后外面的装饰器再进行装饰，由内到外的装饰过程。

例如：
```
@A
@B
def func():
    ...
```

等价于：
```
func = B(func)
func = A(func)
```

可以看出：
- **从下往上包装**
- **从外往内调用**

**调用过程：**
例如：
```
@check_login
@check_token
def comment():
    print("发表评论")
```

实际上等价于：
```
comment = check_token(comment)
comment = check_login(comment)
```

形成的调用链为：
```
调用 comment()

        │
        ▼
登录检查（最外层）
        │
        ▼
验证码检查
        │
        ▼
真正的 comment()
```

因此输出顺序：
```
校验登录
校验验证码
发表评论
```

因为每个装饰器都会：

1. 接收一个函数
2. 返回一个新的包装函数（wrapper）

所以下一个装饰器接收到的，不再是原函数，而是**上一层包装后的函数**。

因此形成了一层一层的嵌套（套娃）。

传统写法比较清晰，相当于comment被check_token包裹，而后两者的整体被check_login包裹。
从外到内是执行过程，而功能从内到外逐渐完整。

语法糖类似，从上往下是执行的过程，而从原函数往上，是功能逐渐完整的过程。

### 带参数的装饰器

带参数的装饰器，需要先接收参数，再返回真正的装饰器
一个装饰器的参数只能有一个，
如果装饰器有多个参数，可以在该装饰器的外面包裹一层，把该装饰器当作其内部函数。

一个小例子：
```
#需求：定义一个技能装饰减法，又能装饰加法的装饰器。

#1. 定义装饰器

def my_decorator(flag):
	def outer(fn_name):
		def fn_inner(a, b):
			if flag == '+':
				print("努力计算加法中……")
			elif flag == '-':
				print("努力计算减法中……")
			return fn_name(a, b)
		return fn_inner
	return outer

#2. 定义原函数，表示加法运算

@my_decorator('+')
def get_sum(a, b):
	return a+b

#3. 定义原函数，表示减法运算

@my_decorator('-')
def get_sub(a, b):
	return a-b

print(get_sum(20, 10), get_sub(20, 10))
```

## 3. 深拷贝与浅拷贝

浅拷贝：创建新对象，其内容是原对象的引用。
浅拷贝只拷贝了一层，拷贝了最外围的对象本身，内部的元素都只是拷贝了一个引用而已。

记忆：
- 所谓的深浅拷贝，分别指的是`copy`模块的`copy()`和`deepcopy()`
- 深拷贝拷贝得多，浅拷贝拷贝得少
- 深浅拷贝主要是针对可变类型（准确来说是对象内部包含可变对象）来讲的，深拷贝拷贝所有层，浅拷贝只拷贝第一层。如果是针对不可变类型，则用法跟普通赋值没有区别。

### 为什么需要拷贝？
直接赋值并不会创建新对象，而是多个变量指向同一对象。

```
a = [1, 2, 3]
b = a
```

此时
```
a ───┐
     ▼
   [1,2,3]
     ▲
b ───┘
```

修改任意一个变量，另一个变量都会受到影响。

### 浅拷贝（Shallow Copy）

使用：
```
import copy

new_obj = copy.copy(old_obj)
```

**特点**
- 创建一个新的**最外层对象**
- **内层嵌套对象不会重新创建**
- 内层对象仍然共享引用

例如：
```
a = [1, 2, 3]
b = [11, 12, 13]

c = [1, 2, a, b]

d = copy.copy(c)
```

对象关系：
```
c ─────► 新列表①
           │
           ├────► a
           └────► b

d ─────► 新列表②
           │
           ├────► a（共享）
           └────► b（共享）
```

可以看到：
- c 和 d 是两个不同的列表
- 但是里面引用的是同一个 a、b

修改内层列表：
```
a.append(100)
b.remove(13)
```

结果：
```
c
# [1, 2, [1, 2, 3, 100], [11, 12]]

d
# [1, 2, [1, 2, 3, 100], [11, 12]]
```

说明：**浅拷贝共享了内层对象。**

修改最外层：
```
c.remove(1)
```

结果：
```
c
# [2, [1,2,3,100], [11,12]]

d
# [1,2,[1,2,3,100],[11,12]]
```

说明：**最外层列表已经是两个独立的对象。**

因此：**浅拷贝创建了新的最外层对象，只共享里面引用的对象。**

### 深拷贝

使用：
```
e = copy.deepcopy(c)
```

特点：
- 创建新的最外层对象
- 递归复制所有嵌套对象
- 整棵对象树完全独立

对象关系：
```
c

列表①
 ├── a①
 └── b①


e

列表②
 ├── a②
 └── b②
```

所有对象都是新的。

因此：
```
a.append(100)
```
不会影响`e`，因为e 内部拥有属于自己的 a。

### 深拷贝与浅拷贝的对比

| **操作**          | **最外层对象** | **内层对象** |
| --------------- | --------- | -------- |
| 赋值（=）           | 共用        | 共用       |
| copy.copy()     | 新建        | 共用       |
| copy.deepcopy() | 新建        | 新建       |
可以理解为：
```
赋值：
变量共享整个对象

↓

浅拷贝：
复制第一层对象
里面继续共享

↓

深拷贝：
递归复制所有对象
完全独立
```

实际使用时，可以根据需求决定是否使用深拷贝。
如果对象内部只有不可变对象：
```
int
float
bool
str
```
则深浅拷贝实际没有区别。

如果对象内部包含：
```
list
dict
set
```
这些可变对象，才需要考虑使用的拷贝类型。

深浅拷贝真正的区别，不是”复制了几层”，而是：
**哪些对象被重新创建了，哪些对象仍然共享引用。**

可以把整个对象看成一棵对象树：
- **浅拷贝**：创建新的树根，但树枝仍然连接着原来的对象。
- **深拷贝**：从树根开始，把整棵树重新创建一遍，因此两棵树完全独立。

# 第四章 网编和多线程

网编：用来实现不同计算机上进行的，程序间数据交互（IP、端口号、协议）
进程、线程都是程序（CPU）实现多任务的手段。

进程（Process）=CPU分配资源的最小单位
线程（Thread）=CPU调度资源的基本单位

进程间数据隔离，线程间数据共享。

## 1. 网络编程

将具有独立功能的多台计算机通过通信线路和通信设备连接起来，在网络管理软件及网络通信协议下，实现资源共享和信息传递的虚拟平台。

网编三要素：
IP地址、端口、协议
### 1）定位设备——IP地址

IP地址是标识网络设备中的唯一地址，可以理解成：**网络中的地址。**
每个网络中的设备都有自己的IP地址。

IPV4：
	4字节，十进制，例如：192.168.88.100

IPV6:
	8字节，十六进制

两个DOS命令：
	查看IP：
		windows：ipconfig
		Linux、Mac：ifconfig
	测试网络连接：
		ping ip地址或者域名

### 2）定位程序——端口号

一台电脑通常不会只运行一个程序，那数据到了电脑以后应该交给谁？

于是就有：**端口号（Port）**
每个软件都有自己的端口。

知名端口号：指众所周知的端口号，范围从0到1023，自定义端口时尽量规避这个范围。
动态端口号：一般程序员开发应用程序使用的端口号称为动态端口号，范围是从1024到65535。

例如：
```
192.168.1.100
        │
        ├──80
        │   浏览器
        │
        ├──3306
        │   MySQL
        │
        ├──8080
        │   Spring Boot
        │
        └──5000
            Python程序
```

所以，端口号负责定位具体程序。

因此真正的定位其实是：
```
IP
+
Port
```

例如：
```
192.168.1.100:8080
```

意思就是：找到这台电脑上的8080 端口程序。

一个简化对应关系：
|**元素**|**作用**|
|---|---|
|IP|找到哪台设备|
|Port|找到设备上的哪个程序|
|Socket|在两个程序之间建立通信通道|

**通过 IP 定位目标设备，通过端口号定位目标程序，再利用 Socket 建立通信，让两个程序能够交换数据。**

### 3）通信协议

协议定义通信规则，符合协议可以通信，否则无法通信。

TCP（Transmission Control Protocol)简称传输控制协议，是一种面向连接的、可靠的、基于字节流的传输层通信协议，使用得最多。

TCP的特点：
- 面向有连接
- 采用字节流传输数据，理论无大小限制
- 安全（可靠）协议，
- 效率相对UDP协议较低
- 区分客户端和服务器端

TCP建立连接（三次握手）：
- 客户端向服务端发送请求，等待服务端确认
- 服务端收到请求后回复给客户端以确认连接请求。
- 客户端收到确认后，再次发送请求确认服务端，服务端收到正确请求后，如果正确则连接建立成功，完成三次握手，随后客户端与服务端之间可以开始传输数据了。

TCP断开连接（四次挥手）：
- 当主机A完成数据传输后，提出停止TCP连接请求
- 主机B收到请求后对其作出回应，确认这一方向上的TCP连接将关闭
- 主机B端提出反方向的连接关闭请求
- A对B的请求进行确认，双方想的关闭结束

UDP协议

## 2. 创建Socket对象

socket简称套接字，是进程之间通信的一个工具。
通信双方都堵有自己的socket对象，数据在socket之间通过数据包（UDP）或者字节流（TCP）
的形式进行传输

socket能实现不同主机之间的进程间通信，Python中有专门的socket类。
```
#导入socket模块
import socket
```

要使用socket，则通常要使用到socket模块下的socket类创建socket对象。
`socket(AddressFaminyType)`

创建socket对象的示例代码：
```
import socket

#参1：Address Family，地址值，即Ipv4还是Ipv6 默认值：AF_INFT(ipv4) AF_INFT(ipv6)
#参2:Socket Type，Socket类型，即TCP还是UDP 默认值SOCKET_STREAM(TCP) SOCKET_STREAM(UDP)

socket_obj = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print(socket_obj)
```

输出：
```
asa@Master-4 PythonLearning % /usr/local/bin/python3 "/Users/asa/Desktop/PythonLear
ning/advanced_course/class 04/socket_using.py"
<socket.socket fd=3, family=2, type=1, proto=0, laddr=('0.0.0.0', 0)>
```

### TCP程序开发流程

TCP网络应用程序开发分为：
- TCP服务端程序开发
```
先启动
绑定 IP 和端口
持续等待客户端连接
```
- TCP客户端程序开发
```
主动找到服务端的 IP 和端口
发起连接
连接成功后收发数据
```

流程图：
![[Pasted image 20260727131958.png]]

**TCP服务端开发流程：**
1. 创建 Socket
2. 绑定 IP 和端口
3. 设置监听
4. 等待客户端连接
5. 接收或发送数据
6. 关闭连接

Python中大致会写成：
```
import socket

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server_socket.bind(("127.0.0.1", 8080))

server_socket.listen()

client_socket, client_address = server_socket.accept()

data = client_socket.recv(1024)
print(data.decode("utf-8"))

client_socket.send("消息已收到".encode("utf-8"))

client_socket.close()
server_socket.close()
```

**1️⃣ 创建服务端Socket**
```
server_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)
```

这里创建的是一个 Socket 对象。

两个参数分别表示：
```
AF_INET
使用 IPv4 地址

SOCK_STREAM
使用面向连接的字节流通信，也就是 TCP
```

所以这句可以理解成：创建一个使用 IPv4 和 TCP 协议的网络通信接口。

**2️⃣ 绑定IP和端口**
```
server_socket.bind(("127.0.0.1", 8080))
```

`bind()` 的作用是：给服务端 Socket 指定一个固定的本地地址。

这里传入的是一个元组：`("127.0.0.1", 8080)`
表示：
```
127.0.0.1
只允许本机访问

8080
使用本机的 8080 端口
```

**3️⃣ 设置监听**
```
server_socket.listen()
```

这一句的作用是：把这个普通 Socket 变成监听 Socket。
它监听的是：**客户端的连接请求。**

**4️⃣ 等待客户端连接**
```
client_socket, client_address = server_socket.accept()
```

`accept()` 的作用是：等待某个客户端连接进来。
它通常是一个**阻塞操作**,也就是说，如果暂时没有客户端连接，程序就会停在这里等着。
```
服务端运行到 accept()
        ↓
没有客户端
        ↓
一直等待
```

它会返回两个东西：
```
client_socket:它不是原来的server——socket，而是专门负责和这一个客户端通信的新socket
所以服务端这里实际上会出现两个 Socket：
	server_socket：负责监听新的连接
	client_socket：负责和已连接的客户端收发数据
这里的server_socket类似于餐厅的reception，负责接待更多客户端（监听新的连接）

client_address:客户端的地址
例如：("127.0.0.1", 53124)
	其中，
	127.0.0.1: 客户端 IP
	53124: 客户端临时端口
```

**5️⃣ 接收客户端数据**
```
data = client_socket.recv(1024)
```
`recv()` 表示：从连接中接收数据。
这里的 `1024` 表示：本次最多接收 1024 字节(不是字符)

`recv()`返回的也是字节数据`bytes`，徐国祥要转换成字符串，需要解码：
```
message = data.decode("utf-8")
```

完整写法：
```
data = client_socket.recv(1024)
message = data.decode("utf-8")
print(message)
```

 **`recv()`也可能阻塞**，如果客户端暂时没有发送任何数据，服务端通常会停在这里等，此时可能会出现，新的用户无法被监听到，此时会需要引入多线程的知识。

**6️⃣ 向客户端发送数据**
```
client_socket.send("消息已收到".encode("utf-8"))
```

网络传输一般发送的是字节数据，字符串不能直接发送，所以需要先编码：
```
"消息已收到".encode("utf-8")
```
得到`bytes`，然后再发送。

也可写作：
```
client_socket.sendall(
    "消息已收到".encode("utf-8")
)
```
`sendall()` 会尽力把所有数据发送完。

两者的区别可大致理解成：
```
send()
发送一部分或全部数据

sendall()
保证把这一批数据完整交给系统发送
```
所以实际写程序时，经常更推荐 `sendall()`。

**7️⃣ 关闭Socket**
```
client_socket.close()
server_socket.close()
```

两个 Socket 的职责不同，关闭时也要分开理解。

```
client_socket.close(): 结束和当前客户端的通信。

server_socket.close(): 服务端彻底停止监听，不再接受新的客户端。
```

如果服务端想长期运行，通常不会每服务一个客户端就立刻关闭 `server_socket`。
而会放进循环：
```
while True:
    client_socket, client_address = server_socket.accept()
    ...
    client_socket.close()
```
这样服务端处理完一个客户端之后，还能继续等待下一个客户端。

**TCP客户端的开发流程**
1. 创建 Socket
2. 连接服务端
3. 发送或接收数据
4. 关闭连接

示例：
```
import socket

client_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)

client_socket.connect(("127.0.0.1", 8080))

client_socket.sendall(
    "你好，服务端".encode("utf-8")
)

data = client_socket.recv(1024)
print(data.decode("utf-8"))

client_socket.close()
```

**1️⃣ 创建客户端Socket**

和服务端一样：
```
client_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)
```

表示：创建一个使用 IPv4 和 TCP 的 Socket。

**2️⃣ 连接服务器**

```
client_socket.connect(("127.0.0.1", 8080))
```

`connect()` 表示：主动连接指定的服务端。
**这里填写的地址必须和服务端绑定的地址对应。**

**3️⃣ 发送和接收数据**

客户端发送：
```
client_socket.sendall(
    "你好，服务端".encode("utf-8")
)
```

客户端接收：
```
data = client_socket.recv(1024)
```

从连接建立后来看，客户端和服务端其实没有绝对的“发送方”和“接收方”。

TCP 是双向通信，也就是：**双方都可以发，也都可以收。**

### 一个完整的小案例

服务端:
```
import socket

server_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)

server_socket.bind(("127.0.0.1", 8080))
server_socket.listen()

print("服务端已启动，等待客户端连接……")

client_socket, client_address = server_socket.accept()

print(f"客户端已连接：{client_address}")

data = client_socket.recv(1024)
message = data.decode("utf-8")

print(f"客户端发来：{message}")

client_socket.sendall(
    "服务端已经收到消息".encode("utf-8")
)

client_socket.close()
server_socket.close()
```

客户端:
```
import socket

client_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)

client_socket.connect(("127.0.0.1", 8080))

client_socket.sendall(
    "你好，我是客户端".encode("utf-8")
)

data = client_socket.recv(1024)
message = data.decode("utf-8")

print(f"服务端回复：{message}")

client_socket.close()
```

运行顺序一定是：
```
先运行服务端
再运行客户端
```

### 端口复用

假如服务端的socket关闭程序后马上再运行，会运行失败。
这是因为，socket关闭后，**操作系统还没有立即把这个端口释放。**

**`TIME_WAIT`**：

这是 TCP 的一个状态，意思可以理解成：
**“我知道程序已经结束了，但是我再等一会儿。”`**

这里的“等”是指，
- 网络里有没有迟到的数据包。
- 双方是否真的都结束通信。

所以：
```
Server关闭

↓

TIME_WAIT

↓

过几十秒

↓

真正释放端口
```

因此，程序结束了，但是端口暂时还不能重新绑定。

**解决方法：端口复用**

Python 提供了：`setsockopt()`

使用时，
```
server_socket.setsockopt(
    socket.SOL_SOCKET,
    socket.SO_REUSEADDR,
    True
)
```

这一句必须放在`bind()`之前，例如：
```
server_socket = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)

server_socket.setsockopt(
    socket.SOL_SOCKET,    #要设置 Socket 本身的选项(Socket设置)
    socket.SO_REUSEADDR,    #允许重新使用这个地址（IP+端口）
    True    #开启
)

server_socket.bind(("192.168.1.100",10086))
```

```
端口复用

不是为了多个程序共用端口。

而是为了：

程序刚关闭以后，

能够立即重新使用这个端口。
```

## 3. 扩展-编解码问题

编码（Encode）：将字符串（str）转换为字节（bytes），方便计算机存储或网络传输。
`字符串.encode(码表）`

解码（Decode）：将字节（bytes）转换回字符串（str），方便人阅读。
`字符串.decode(码表）`

### 常见码表
- ASCII：只支持英文、数字、部分特殊符号。
- GBK：中文一般占 **2 字节**。
- UTF-8：中文一般占 **3 字节**，目前最常用。

英文、数字、常见特殊符号在 ASCII、GBK、UTF-8 中通常都是 **1 字节**。

### 二进制数据（bytes）

Python 中：`b"Hello"`表示：`bytes`
这是二进制数据特殊写法，即`b"字母/数字/特殊符号"`，该方式对中文无效。

即，`b"你好"`不能直接这样写。
需要：
```
"你好".encode("utf-8")
```

得到：
```
b'\xe4\xbd\xa0\xe5\xa5\xbd'
```

**网络传输、文件存储等底层操作处理的是 bytes，而人阅读和编程通常使用的是 str，因此需要通过 encode() 和 decode() 在两者之间转换。**

## 4. 多任务的介绍

### 并发和并行

多个任务同时执行能够充分利用CPU资源，大大提高程序执行效率。

串行（顺序执行、Serial）：必须做完一个才能做下一个

多任务是指在同一时间内执行多个任务（给我们的感觉）。

多任务的两种表现形式：并发和并行

**并发（Concurrency）**：并发是指在一段时间内，多个任务交替推进

**并行（Parallelism）**：是存在多个执行者，同时工作，属于真正的同时执行

==并发于并行不冲突==

简单的图解：

串行:
```
用户A

↓

全部处理完

↓

用户B
```
B 必须等。

并发:
```
处理A一点

↓

处理B一点

↓

再处理A

↓

再处理B
```
大家都在推进。
单核CPU一定是并发执行多任务的。

并行
如果电脑有多个 CPU 核心：
```
CPU1
↓

处理A

CPU2
↓

处理B
```
真的一起执行。

**所有并行都属于一种并发，但并发不一定是并行。**

## 补充-文件读取相关知识

### 1）open()
`open()` 用于**打开文件**，返回一个文件对象（File Object），之后可以通过该对象进行读写操作。

基本语法：
```
open(文件路径, 打开模式, encoding="utf-8")
```

例如：
```
f = open("test.txt", "r", encoding="utf-8")
```

常见参数：
- 文件路径（path）
- 打开模式（mode）
- 编码（encoding，文本文件常用）

### 2)文件打开模式

| **模式** | **含义**                    |
| ------ | ------------------------- |
| `"r"`  | 只读（Read），文件不存在会报错         |
| `"w"`  | 写入（Write），不存在会创建，存在会清空原内容 |
| `"a"`  | 追加（Append），内容写到文件末尾       |
| `"rb"` | 二进制读取（Read Binary）        |
| `"wb"` | 二进制写入（Write Binary）       |
| `"ab"` | 二进制追加（Append Binary）      |
**Binary（二进制）模式**主要用于图片、视频、音频等非文本文件。

**读取图片时，必须使用re/wb**
这是因为，图片本质上并不是文字，而是一串二进制数据。
如果使用：
```
open("cat.png", "r")
```
Python 会尝试按照 UTF-8 等编码去解析图片内容，通常会报错。

因此：**所有非文本文件，都应该使用 Binary（二进制）模式。**

### 3)read(8192)

例如：
```
while True:
    data = f.read(8192)
```

表示：每次读取 **8192 Byte（8KB）** 数据。

原因:
- 避免一次性读取整个大文件，占用大量内存。
- 边读边发送，效率更高。

### 4)shutdown(socket.SHUT_WR)

作用：**告诉服务器：“我已经发送完所有数据了。”**

注意：
不是关闭整个 Socket，而是**关闭发送方向（Write）。**

仍然可以：`recv()`
接收服务器返回的信息。

如果没有shutdown，服务器和客户端都会在`recv()`等待回应，形成死锁。

## 5. 单进程和多进程

进程（Process）是CPU资源分配的最小单位，它是操作系统进行资源分配和调度运行的基本单位。
通俗来讲，一个正在运行的App就是一个进程。

多进程的作用：
充分利用CPU资源，提高程序的执行效率/

多进程的基本工作方式：程序运行起来是显著进程，在主进程上创建子进程

### 如何实现多进程

**多进程的无参示例**

1）导入进程工具包
`import multiprocessing`

2）通过进程类实例化进程对象
`子进程对象 = multiprocessing.Process(target=函数名)`

3）启动进程执行任务
`进程对象.start()`

![[Pasted image 20260729132248.png]]
流程：
```
创建 Process 对象
        ↓
start()
        ↓
操作系统创建子进程
        ↓
子进程执行 target 指定的函数
```

示例代码：
```
import multiprocessing

#定义函数，表示编写代码
def coding():
	for i in range(1, 11):
	print(f"正在敲第{i}遍代码……")

#定义函数，表示听音乐
def music():
	for i in range(1, 11):
	print(f"正在听第{i}遍音乐……")

#避免递归构建子进程
if __name__ == "__main__":

#创建两个进程对象，分别关联上述两个目标函数
#进程p1关联coding函数，p1抢到CPU资源，就会执行这个函数
p1 = multiprocessing.Process(target=coding)
p2 = multiprocessing.Process(target=music)

#进程启动，可以开始抢CPU资源了（同一个进程不能重复开）
p1.start()
p2.start()
```

**多进程的带参示例**

位置参数：
```
Process(
    target=coding,
    args=("Asa", 10)
)
```

相当于：`coding("Asa", 10)`

关键字参数：
```
Process(
    target=coding,
    kwargs={
        "name": "Asa",
        "count": 10
    }
)
```

相当于：`coding(name="Asa", count=10)`

示例代码：
```
import multiprocessing

def coding(name, num):
	for i in range(1, num+1):
		print(f"{name}正在敲第{i}遍代码……")

def music(name, num):
	for i in range(1, num+1):
		print(f"{name}正在听第{i}遍音乐……")

if __name__ == "__main__":
p1 = multiprocessing.Process(target=coding, args=("Asa", 10))
p2 = multiprocessing.Process(target=coding, args=("StarBridge", 10))

p1.start()
p2.start()
```

**args的注意事项**

一个参数：`args=(10,)`

注意：
必须有逗号，否则：
`args=(10)`只是整数。


### 获取进程的编号

**进程编号（Process ID，PID）** 是操作系统为每个进程分配的唯一标识，用于识别和管理进程。

在**同一时刻**，一个操作系统中不会有两个进程拥有相同的 PID；当一个进程结束后，它的 PID 可能会被操作系统重新分配给新的进程使用。

 **获取进程编号的目的**
获取进程编号可以帮助我们了解程序的运行情况，并验证主进程与子进程之间的关系。

通过查看：
- 当前进程 PID
- 父进程 PPID
可以知道当前进程是由哪个父进程创建出来的。

**获取进程编号的两种方式**
`os.getpid()`
`multiprocessing.current_process().pid`

其中：
- `current_process()` 是函数
- 返回当前进程对象
- `.pid` 是该对象的属性

**查看当前进程的ppid（父进程id）**
`os.getppid()`

通常情况下，
`if __name__ == "__main__":`
中创建的子进程，其父进程都是当前运行 Python 程序的主进程。

而主进程本身也是由其他程序启动的，例如：
```
Terminal
    │
    └── Python（主进程）
            │
            ├── 子进程1
            └── 子进程2
```

继续向上追溯：
```
launchd（系统）
      │
      └── Finder
            │
            └── VS Code
                  │
                  └── Terminal
                        │
                        └── Python
```

因此，整个操作系统中的进程可以看作一棵**进程树（Process Tree）**，所有进程最终都能一路找到共同的祖先。

### 进程的注意点

**1）进程之间不共享全局变量**

例子：
```
import multiprocessing

num = 100

def work():
    global num
    num += 1
    print(num)

if __name__ == "__main__":
    p = multiprocessing.Process(target=work)
    p.start()

    print(num)
```

结果通常是：
```
101    ← 子进程
100    ← 主进程
```

原理：
当`p.start()`的时候，操作系统并不是两个进程共同使用同一块内存，而是：
主进程拥有`num = 100`，
创建子进程时，系统会复制（更准确地说，是为子进程建立自己的一份运行环境）：
```
主进程

num = 100
```
↓
```
子进程

num = 100
```

于是：
```
主进程

num = 100
```

和：
```
子进程

num = 100
```
其实已经没有关系了。

后来子进程：
```
num += 1
```

变成：
```
子进程

num = 101
```

而主进程：
```
num = 100
```

完全没变化。

所以最后输出：
```
子进程：

101

主进程：

100
```

这是因为，**进程最大的特点就是资源隔离。**

每个进程都有自己的内存空间，这也是进程安全性的来源。

**2）默认情况下，主进程会等待子进程结束**

例如：
```
def work():
    for i in range(5):
        print(i)
```

```
p.start()

print("主进程结束")
```

程序会变成：
```
子进程继续运行……

0

1

2

3

4
```

因为：**Python 默认会等待所有非守护进程结束。**

可以理解成：
```
主进程

↓

等等……

↓

孩子还没回来……

↓

继续等……

↓

所有子进程结束

↓

主进程退出
```

不让主进程等待子进程的两个方法：

1️⃣方法一：守护进程（Daemon Process）
```
p.daemon = True
```

注意，必须放在：
```
p.start()
```
之前。

例如：
```
p = multiprocessing.Process(target=work)

p.daemon = True

p.start()
```

可以理解成：**“这个孩子不是必须完成工作的。”**

于是：
```
主进程结束

↓

守护进程也立即结束
```

举个例子：
```
主进程

↓

运行5秒

↓

结束
```

守护进程本来还准备工作100秒，但是主进程结束，守护进程也会一起结束。

所以，守护进程最大的特点是**依附于主进程**，
主进程活它活，主进程死它也死。

一些后台进程，例如
```
日志记录

状态刷新

缓存清理

定时检测
```
这些都属于“有最好，没有也无所谓。”

主程序关了，它们也没必要继续工作。

2️⃣方法二：强制关闭子进程
```
p.terminate()
```

例如：
```
p.start()

time.sleep(3)

p.terminate()
```

意思就是：
```
主进程：

你不用干了。

结束吧。
```

系统直接结束子进程。

注意，这是强制结束，不会考虑：
```
你有没有保存数据？

有没有写文件？

有没有释放资源？
```

而是直接结束。

所以，一般只在：
- 卡死
- 无限循环
- 超时

这种情况才会使用。

## 6. 线程介绍

### 1）线程的概念
在 Python 中，实现多任务除了可以使用**进程（Process）**，还可以使用**线程（Thread）**。

**进程（Process）**
进程是**操作系统分配资源的基本单位**。

当创建一个进程时，操作系统会为其分配独立的资源，例如：
- 内存空间
- 文件资源
- 网络资源
- 进程编号（PID）
因此，不同进程之间默认**资源隔离、数据互不共享**。

**线程（Thread）**
线程是**CPU 调度的基本单位**，是真正执行代码的执行流。
线程必须依附于进程存在，一个进程中至少包含一个线程，这就是**主线程（Main Thread）**。

除了主线程之外，还可以创建多个自定义线程，实现多个任务同时执行。

例如：
```
Python进程
│
├── 主线程（Main Thread）
├── 线程1（Coding）
└── 线程2（Music）
```

使用多个线程后，多任务可并发执行，提高程序运行效率。
### 2）线程的实现方式

Python 使用 **threading 模块** 创建线程。

导入模块：
```
import threading
```

创建线程:
```
t = threading.Thread(target=函数名)
```

启动线程:
```
t.start()
```

例如：
```
import threading

def coding():
    print("正在写代码")

t = threading.Thread(target=coding)
t.start()
```

**线程传递参数**

线程传递参数的情况与多进程完全相同。

1️⃣位置参数
```
t = threading.Thread(
    target=coding,
    args=("Asa", 10)
)
```

相当于：
```
coding("Asa", 10)
```

**注意：由于参数需要以元组形式传递，因此只有一个参数时，需要写成** **`(value,)`****。**

2️⃣关键字参数
```
t = threading.Thread(
    target=coding,
    kwargs={
        "name": "Asa",
        "num": 10
    }
)
```

相当于：
```
coding(name="Asa", num=10)
```

![[Pasted image 20260730120411.png]]
### 3）start()的作用

创建线程：
```
t = threading.Thread(...)
```
只是创建了一个**线程对象**。

真正开始执行线程的是：
```
t.start()
```

只有调用 `start()` 后，线程才会开始运行。

### 4）主线程（Main Thread）

Python程序启动时，会自动创建一个主线程。
创建新的线程后，主线程并不会结束，而是继续执行自己的代码。

例如：
```
for i in range(5):
    print("这里是main")
```

如果写在：
```
t1.start()
t2.start()
```

之前，那么主线程会先执行完这部分代码，再启动其他线程。
如果写在它们之后，则主线程会与t1, t2竞争CPU资源。

主线程本身也是线程，它与其他线程共同运行于同一个进程中。

### 5）线程之间的数据共享

**线程共享同一个进程的资源**

例如：
```
money = 100
```

多个线程修改：
```
money += 50
```

所有线程看到的都是**同一个** **`money`**。

因此：**同一个进程中的线程之间可以共享数据。**

### 小结-线程与进程的区别
| **多线程（Thread）** | **多进程（Process）** |
| --------------- | ---------------- |
| 一个进程中的多个执行流     | 多个独立进程           |
| 共享内存和资源         | 独立内存和资源          |
| 创建速度快           | 创建速度较慢           |
| 资源消耗少           | 资源消耗较大           |
| 通信方便            | 通信相对复杂           |
| 一个线程异常可能影响整个进程  | 一个进程崩溃通常不会影响其他进程 |
Python中，多进程开发比单进程多线程开发稳定性要强。

# 第五章-生成器与正则表达式

## 1. 线程的注意点

### 1）线程之间执行是无序的

**线程什么时候获得 CPU 执行权，是由操作系统调度决定的。**

因此，无法保证线程的执行顺序。

两种CPU调度策略

**① 均分时间片（Time Slice）**
CPU将时间均分，每个任务得到同样多的时间，无论是否正在执行。

**② 抢占式调度（Preemptive Scheduling）**
线程什么时候运行、运行多久，程序员通常不能自己决定，而是由操作系统调度，现代操作系统基本都采用这种方式。

使用`time.sleep()`可以观察到线程切换，但它并不是控制线程谁先运行，
而是**让当前线程主动放弃 CPU 一段时间。**

**sleep() 对线程最大的影响就是：主动让出 CPU。**
而不是：**命令 CPU 去执行另一个线程。**

这一点很重要，因为最终到底执行谁，还是**操作系统调度。**

### 2）主线程会等待所有子线程执行结束再结束

假设：
```
t1.start()
t2.start()

print("main结束")
```

程序不会因为
```
main结束
```
打印完就退出。

而是：
```
主线程结束自己的代码

↓

等待 t1

↓

等待 t2

↓

整个 Python 进程退出
```

这也是为什么很多时候：
即使 main 已经没有代码了，程序还在继续运行。

**有些线程并不是程序真正要完成的任务，他只是辅助其他线程工作的**
此时，为了让这类线程与主线程一起结束，可以将其设置成守护线程：

1️⃣构造时直接指定
```
t = threading.Thread(target=work, daemon=True)
```
意思就是：

创建线程的时候，就告诉 Python：**“这个线程是守护线程。”**

这是最简洁、最现代的写法。

2️⃣`setDaemon(True)`（已弃用）
```
t = threading.Thread(target=work)
t.setDaemon(True)
```
了解即可
- 目前还能用（很多版本还能正常运行）
- 但是官方不建议继续使用
- 将来的 Python 版本有可能直接删除

3️⃣修改daemon属性
```
t = threading.Thread(target=work)
t.daemon = True
```

这个就是目前最常见的写法之一。

意思就是，创建线程对象：
```
t = threading.Thread(...)
```

然后修改对象里面的一个属性：
```
t.daemon = True
```

最后：
```
t.start()
```
启动。

**注意，不论使用哪一种写法，都需要在`start()`之前设置！**

例如：
```
t = threading.Thread(target=work)
t.daemon = True
t.start()
```



### 3）线程之间共享全局变量

例如：
```
money = 100
```

线程 A：
```
money += 50
```

线程 B：
```
print(money)
```

B 很可能打印：
```
150
```

因为：
**大家访问的是同一份** **`money`****。**

这也是线程和进程最大的区别。

### 4）线程之间共享全局变量可能导致数据错误

例如：

初始：
```
num = 0
```

线程 A：
```
num += 1
```

线程 B：
```
num += 1
```

理想状态下，`num == 2`，
但实际上，可能还是`num == 1`

这是因为，
```
线程A

读取 num=0
```

与此同时：
```
线程B

也读取 num=0
```

然后：
```
线程A

0+1

写回1
```

接着：
```
线程B

0+1

也写回1
```

于是：

本来应该：
```
0

↓

1

↓

2
```

结果变成：
```
0

↓

1
```

这就叫：**数据竞争（Race Condition）**

也就是说，线程1读取完数据，还没进行进一步操作，线程2就抢到了CPU资源，
此时线程2读取到的数据依旧是没修改的数据。

为了避免这种现象，需要保证一个线程读取完数据后、更改数据之前，另一个线程只能等待。

## 2. 互斥锁（Lock）

### 1）互斥锁的概念

互斥锁可以理解成一把只有钥匙的门锁

共享数据所在的代码区域：
```
读取 num
修改 num
写回 num
```

相当于一个房间。

线程进入之前必须先拿锁：
```
线程A拿到锁
        ↓
线程B只能等待
        ↓
线程A完成修改
        ↓
线程A释放锁
        ↓
线程B拿到锁
```

这样同一时刻只能有一个线程修改共享数据。

“互斥”的意思就是：**彼此排斥，同一时刻只允许一个线程进入。**

### 2）如何创建互斥锁

```
import threading

lock = threading.Lock()
```
这会创建一个锁对象。

完整流程是：
```
lock.acquire()

# 需要保护的共享数据操作

lock.release()
```

其中：
```
lock.acquire()
```
表示获取锁。

```
lock.release()
```
表示释放锁。

完整示例：
```
import threading

num = 0
lock = threading.Lock()


def add():
    global num

    for _ in range(100000):
        lock.acquire()

        num += 1

        lock.release()


t1 = threading.Thread(target=add)
t2 = threading.Thread(target=add)

t1.start()
t2.start()

t1.join()
t2.join()

print(num)
```

加锁后，执行过程会变成：
```
线程A获取锁
线程A执行 num += 1
线程A释放锁

线程B获取锁
线程B执行 num += 1
线程B释放锁
```
最终结果就能稳定保持正确。

### 3)阻塞等待

假设线程A已经获得了锁：
```
lock.acquire()
```

这时线程B也执行：
```
lock.acquire()
```

线程B不会报错，也不会直接跳过去。
它会：**阻塞等待。**

也就是：
```
线程B：锁被别人拿走了，我在这里等着。
```

直到线程A执行：
```
lock.release()
```
线程B才有机会获得锁并继续运行。

### 4） 更推荐的写法： with lock

手动写
```
lock.acquire()

num += 1

lock.release()
```

有一个危险。

假设中间报错：
```
lock.acquire()

num += "abc"  # 报错

lock.release()
```

因为程序在中间异常退出了，`release()` 没有执行。

锁就可能一直没有释放，其他线程全都卡住。

因此更推荐：
```
with lock:
    num += 1
```

完整代码：
```
import threading

num = 0
lock = threading.Lock()


def add():
    global num

    for _ in range(100000):
        with lock:
            num += 1


t1 = threading.Thread(target=add)
t2 = threading.Thread(target=add)

t1.start()
t2.start()

t1.join()
t2.join()

print(num)
```

`with lock:` 会自动完成：
```
lock.acquire()
```

执行完代码块后，再自动：
```
lock.release()
```

即使中间出现异常，也更容易确保锁被释放。

所以平时优先记：
```
with lock:
    # 临界区代码
```

### 5） 临界区

被锁保护的共享数据操作区域，叫：

**临界区（Critical Section）**

例如：
```
with lock:
    num += 1
```

这里的：
```
num += 1
```
就是临界区。

因为这一部分涉及共享数据，并且不允许多个线程同时执行。
### 拓展知识

1️⃣**死锁（Deadlock）**

死锁通常是由于**锁没有在合适的时机释放**，或者**多个线程互相等待对方释放锁**造成的。

例如：
```
线程A：拿着锁1，等待锁2

线程B：拿着锁2，等待锁1
```

双方都在等待：
```
线程A：等你先放。

线程B：等你先放。
```
最终谁也无法继续执行。

死锁的结果
- 程序停止响应
- 线程一直处于等待状态
- 无法继续向下执行

因此，使用锁时一定要保证**获取锁后能够正常释放锁。**

2️⃣**多把锁**
实际项目中，一个程序可能会存在多把锁。

例如：
```
锁A：保护用户信息

锁B：保护订单信息

锁C：保护库存信息
```

如果多个线程获取锁的顺序不一致，就可能导致死锁。

因此，开发中通常会尽量：
- 减少锁的数量
- 保持获取锁的顺序一致
- 及时释放锁
这样可以降低死锁发生的概率。

此外，可能会出现一种锁对象没有统一的情况，
如果面对同一共享数据，加了不同的多把锁，
此时对于共享数据而言，由于不同线程并没有争取同一把锁，于是会出现相当于没锁的情况。

可以理解为，锁保护的不是变量本身，而是“拿着同一把锁的人（同一个Lock对象）”。

因此，**多个线程要同步同一份共享数据时，必须使用同一个** **`Lock`** **对象；如果每个线程使用不同的锁对象，则无法实现互斥，等同于没有加锁。**

3️⃣**互斥锁的代价**

锁保证了安全，但是会降低并发效率。

因此，使用互斥锁的原则是：
**锁的范围越小越好，但必须完整保护共享数据操作。**

真正需要警惕的不是共享数据本身，而是多个线程同时修改一份共享数据。

## 3. Python迭代器（Iterator）

迭代（Iteration）是按照一定顺序，逐个访问一组数据的过程。

列表、元组、字符串、字典、集合、`range` 等，都可以被 `for` 循环遍历，因此它们属于**可迭代对象（Iterable）**。

**可迭代对象 (Iterable)**
表示：可以从中获取迭代器，并能够被 `for` 循环遍历的对象。

常见可迭代对象：
```
list
tuple
str
dict
set
range
```

迭代器（Iterator）是Python中的一种对象，用于在数据集合中逐个访问元素，而不需要暴露数据集合的底层实现。

迭代器表示：真正负责逐个取出数据，并保存当前迭代位置的对象。

它提供了一种遍历几何元素的标准方式，适用于任何支持迭代的数据结构。
如列表、元组等，`range()`就是一个迭代器。

迭代器具有两个核心方法：
```
__iter__() #返回迭代器对象
__next__() #返回下一个数据
```

没有更多数据时，`__next__()`需要：
```
raise StopIteration
```

自定义的类，只要重写了`__iter__()`和`__next__`方法，就可以称为迭代器。

手动管理：需要显示地实现`__iter__()`和`__next__`方法
状态管理：迭代器需要自己管理迭代的状态，包括当前位置和结束条件。
内存使用：内存使用取决于迭代器的实现，通常是惰性计算（即按需生成数据）。

### 自定义迭代器

```
class MyIterator:
    def __init__(self, start, end):
        self.current_value = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.current_value >= self.end:
            raise StopIteration #终止条件

        value = self.current_value
        self.current_value += 1
        return value
```

使用：
```
my_iter = MyIterator(1, 6)

for i in my_iter:
    print(i)
```

输出：
```
1
2
3
4
5
```

### 自定义迭代器的执行过程

初始状态：
```
current_value = 1
end = 6
```

第一次调用：
```
next(my_iter)
```

返回：`1`
同时把状态更新为：
```
current_value = 2
```
之后每调用一次 `next()`，都会继续向后移动。

当：
```
current_value >= end
```

时，抛出：
```
StopIteration
```
表示迭代结束。

for循环的本质也是基于迭代器的原理：
```
获取迭代器
    ↓
不断调用 next()
    ↓
遇到 StopIteration 后结束
```

**迭代器的特点**：
- 按顺序逐个返回数据。
- 会保存当前迭代位置。
- 数据取出后不会自动回到起点。
- 迭代结束后通常不能重新使用，需要重新创建迭代器。
- 适合处理不需要一次全部加载的数据。

迭代器更像一个记录“当前走到哪里”的对象，而不是数据容器本身。

## 4. Python生成器（Generator）

生成器（Generator）是一种特殊的迭代器

生成器不会一次性准备所有数据，而是在需要时逐个生成数据，因此属于：
**惰性计算（Lazy Evaluation）**

生成器保存的主要不是所有结果，而是：
```
生成数据的规则
+
当前执行状态
```

### 1）生成器表达式

列表推导式：
```
nums = [i for i in range(1, 11)]
```

会立即创建完整列表：
```
[1, 2, 3, ..., 10]
```

生成器表达式：
```
nums = (i for i in range(1, 11))
```

创建的是生成器对象：
```
print(nums)
# <generator object ...>

print(type(nums))
# <class 'generator'>
```
此时数据还没有全部生成。

### 2）从生成器中获取数据

可以使用`next()`从生成器中获取数据。

例如：
```
even_nums = (i for i in range(1, 11) if i % 2 == 0)

print(next(even_nums))  # 2
print(next(even_nums))  # 4
```

之后继续遍历：
```
for i in even_nums:
    print(i)
```

输出：
```
6
8
10
```

这是因为`2, 4`已经被消费，生成器会从之前暂停的位置继续，而不是重新开始。

**生成器是一次性消费的**

生成器内部可以理解为保存了一个执行位置。
每调用一次：`next(generator)`，生成器就向后运行，返回一个值，然后暂停。
已经返回的值不会自动保存，也不会再次返回。

所以生成器通常是：**一次性、向前消费的数据流。**

当生成器耗尽后，再继续：`next(generator)`，会抛出`StopIteration`。

### 3）使用yield创建生成器

**生成器函数**
只要函数中出现`yield`，这个函数就不再是普通函数，而是生成器函数。

例如：
```
def my_generator():
    for i in range(1, 11):
        yield i
```

调用：
```
my_yield = my_generator()
```

不会立刻执行函数体，而是创建一个生成器对象。
```
print(type(my_yield))
# <class 'generator'>
```

`yield value`会完成两件事：
1. 向调用方产出一个值。
2. 暂停函数并保存当前状态。

下一次调用：`next(generator)`时，会从上一次暂停的位置继续执行。

执行示例：
```
def my_generator():
    print("函数开始")

    for i in range(1, 4):
        print(f"准备生成：{i}")
        yield i
        print(f"{i}之后继续执行")

    print("函数结束")
```

测试：
```
g = my_generator()

print("生成器已创建")
print(next(g))
print(next(g))
```

调用：
```
g = my_generator()
```
时，函数体不会执行。

第一次`next(g)`
执行到`yield 1`，返回1并暂停。

第一次`next(g)`
从`yield 1`之后继续执行，而不是函数从头开始。

### 4）生成器与迭代器的关系

手写迭代器时，需要自己实现：
```
__iter__()
__next__()
StopIteration
```

还需要自己保存：
```
self.current_value
```

生成器函数只需要`yield`，Python 会自动帮助完成：
- 保存执行位置。
- 保存局部变量状态。
- 实现迭代器协议。
- 迭代完成后产生 `StopIteration`。

所以可以理解为：**生成器是 Python 提供的一种更简洁的迭代器实现方式。**

### 5）生成器的实际用途：分批处理数据案例

```
import math


def dataset_loader(batch_size):
    with open(
        "advanced_course/class 05/story",
        "r",
        encoding="utf-8"
    ) as f:
        lines = f.readlines()

        total_batches = math.ceil( #math.ceil(number)表示对number向上取整
            len(lines) / batch_size
        )

        for i in range(total_batches):
            yield lines[
                i * batch_size:
                (i + 1) * batch_size
            ]
```

假设文件有 20 行，每批 8 行：
```
第一批：0:8
第二批：8:16
第三批：16:24
```

第三批虽然切片终点超过列表长度，Python 也不会报错，而是返回剩余数据。

生成器的核心优势是：**按需生成数据，避免一次性占用大量内存。**
## 5. Property属性

普通getter：
```
class Student:
    def __init__(self, name):
        self._name = name

    def get_name(self):
        return self._name
```

调用：
```
student.get_name()
```

Python 更希望调用方可以自然地写成：
```
student.name
```
同时又能保留 getter 中的业务逻辑。

这就是 `property` 的作用。

### 1）`@property `装饰器

```
class Student:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name
```

调用：
```
student = Student("Asa")

print(student.name)
```

虽然调用方式看起来像访问普通属性：
```
student.name
```

实际上执行的是：
```
def name(self):
```

因此：`@property` 将方法包装成了属性。

### 2）setter

如果希望属性可以赋值，可以定义：
```
@属性名.setter
```

例如：
```
class Student:
    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("年龄不能小于0")

        self._age = value
```

使用：
```
student.age = 20
```

看起来像普通赋值，但实际执行的是：
```
def age(self, value):
```

因此可以在 setter 中完成：
- 参数校验。
- 数据转换。
- 日志记录。
- 状态更新。
- 权限控制。

### 3）Property的类属性写法

除了装饰器写法，还可以使用`property()`创建property对象。

例如：
```
class Student:
    def __init__(self, age):
        self._age = age

    def get_age(self):
        return self._age

    def set_age(self, value):
        if value < 0:
            raise ValueError("年龄不能小于0")

        self._age = value

    age = property(get_age, set_age)
```

调用方式仍然是：
```
student.age
student.age = 20
```

这里：
```
age = property(get_age, set_age)
```
表示把 getter 和 setter 组合成一个 property 属性。

两种写法功能基本相同，但更推荐装饰器写法。

`property` 本身是 Python 的内置类，
```
age = property(get_age, set_age)
```
是在创建一个 property 对象。

装饰器写法，则可以理解成一种更易读的语法形式。

### property的主要作用

`property` 的主要作用是：
让调用方像访问普通属性一样使用对象，同时保留方法中的逻辑与封装能力。

优点包括：
- 调用代码自然。
- 隐藏 getter/setter。
- 保持外部接口稳定。
- 可以增加参数校验。
- 可以修改内部实现而不影响调用方。
- 有利于封装对象内部状态。

## 6. 正则表达式

**正则表达式（Regular Expression，Regex）**是一种用于匹配字符串的小语言。

常用于：
- 判断字符串是否符合格式
- 搜索符合规则的内容
- 批量提取文本
- 替换字符串
- 分割字符串

正则表达式语法不需要完全记忆，但是需要知道Python如何使用正则表达式。

Python使用正则表达式，首先需要导入：
```
import re
```

此处的`re`就是 **regular expression（正则表达式）** 模块

`re`中的常用方法：

| 方法 | 作用 | 常见程度 |
|------|------|---------|
| `re.match()` | 从字符串开头开始匹配 | ⭐⭐⭐⭐ |
| `re.search()` | 整个字符串搜索第一个匹配 | ⭐⭐⭐⭐⭐ |
| `re.findall()` | 找出所有匹配，返回列表 | ⭐⭐⭐⭐⭐ |
| `re.finditer()` | 返回所有匹配的迭代器 | ⭐⭐⭐ |
| `re.sub()` | 替换匹配内容 | ⭐⭐⭐⭐ |
| `re.split()` | 按匹配规则切割字符串 | ⭐⭐⭐ |
### 1）match()

只能从头开始匹配。

例如：
```
import re

text = "abc123"

print(re.match(r"\d+", text))
```

输出：
```
None
```

因为需要从头匹配，而`abc123`开头不是数字。

### 2)search()

在字符串里寻找第一个符合条件的地方。

```
import re

text = "abc123"

print(re.search(r"\d+", text))
```

他会一直找：
```
abc123
   ^^^
```
直到找到`123`。

所以：**`search()`** **比** **`match()`** **更常用。**

### 3)findall()

找出所有符合条件的表达。

```
import re

text = "abc123xyz456"

print(re.findall(r"\d+", text))
```

得到：
```
['123', '456']
```

这在数据处理中比较常见。

### 4)sub()

替换。

```
import re

text = "abc123xyz456"

print(re.sub(r"\d+", "*", text))
```

结果：
```
abc*xyz*
```

可用于清洗文本。

使用`sub()`之前，Python也可以先编译正则：
```
pattern = re.compile(r"\d+")
```

之后直接使用：
```
pattern.match()
pattern.search()
pattern.findall()
pattern.sub()
```
避免反复编译，能够提高代码的可读性，也有一定的性能优势。

### 5)split()

按照正则切割。

```
import re

text = "Tom,Jack;Lucy"

print(re.split(r"[,;]", text))
```

输出：
```
['Tom', 'Jack', 'Lucy']
```

这里的：
```
[,;]
```
表示逗号或分号。

### 常用元字符与数量匹配

**元字符：**

|**表达式**|**含义**|**示例**|
|---|---|---|
|`.`|任意单个字符（除换行）|`a.c`|
|`\d`|一个数字|`3`|
|`\D`|非数字|`a`|
|`\w`|字母、数字、下划线|`abc_123`|
|`\W`|非字母数字下划线|`# @ !`|
|`\s`|空白字符（空格、Tab、换行等）|`" "`|
|`\S`|非空白字符|`abc`|

**数量匹配：**

| **表达式** | **含义**        |
| ------- | ------------- |
| `*`     | 0 次或多次        |
| `+`     | 1 次或多次        |
| `?`     | 0 次或 1 次      |
| `{n}`   | 恰好 n 次        |
| `{m,n}` | m~n 次（左闭右闭区间） |

**字符集合：`[abc]`**
表示匹配`a, b, c`中的任意一个。

例如：
`[0-9]`：表示匹配任意数字
`[A-Z]`：表示任意大写字母
`[a-z]`：表示任意小写字母

**否定字符集合：`[^指定字符]`**
表示匹配除了指定字符之外的任意一个字符。

例如：`[^abc]`
可以匹配除`a, b, c`之外的任意一个字符。
### 开始与结束

`^`：表示字符串开始
`$`：表示字符串结束

匹配开头、结尾以及整串字符串的方法：

| **需求**  | **推荐方法**                    |
| ------- | --------------------------- |
| 匹配开头    | `re.match()`                |
| 匹配结尾    | `re.search(r"...$")`        |
| 匹配整个字符串 | `re.fullmatch()`（或 `^...$`） |

### 推荐使用Raw String

由于Python中`\`本身就是转义符，会有一些以`\`开头的特殊表达。
为了避免出现误解，推荐在表达式中使用`r""`，这可以保证在`""`内的全部内容都被交给正则表达式编译。

例如：
```
text = "abc123def456ghi789"

result = re.sub(r"\d", "#", text)

print(result) # Output: abc#def#ghi#
```

### Match对象（re.Match）

`re.match()`和`re.search()`成功匹配后，返回的是Match对象。

如果没有成功，则返回None。

因此实际开发中通常会先判断：
```
result = re.search(r"\d+", text)

if result:

    print(result.group())
```

Match对象常用方法：

|**方法**|**作用**|**返回值**|
|---|---|---|
|`group()`|获取匹配到的字符串|`str`|
|`start()`|获取匹配开始的位置|`int`|
|`end()`|获取匹配结束的位置（不包含该位置）|`int`|
|`span()`|获取匹配范围 `(start, end)`|`tuple`|

一个完整例子：
```
import re

text = "abc123def"

result = re.search(r"\d+", text)

if result:
    print(result.group())
    print(result.start())
    print(result.end())
    print(result.span())
```

输出：
```
123
3
6 #end()返回6，这是因为字符串中数字部分的切片是左闭右开区间，左端点为3，右端点为6
(3, 6) 
```

### 三个进阶表达——分组与反向引用

**1️⃣`|`：或（OR）**
表示匹配左右任意一个表达式。

基本语法：
```
表达式1|表达式2
```

例如：
```
cat|dog
```

此时匹配`cat`或`dog`都合法。

与`[]`的区别：
- `[]` —— 字符集合（单个字符）
- `|` —— 表达式选择（多个完整表达式）

**2️⃣（）：分组（Capture Group）

括号的作用有两个。

**作用一：保存匹配结果**
Regex 在匹配过程中，会自动保存括号匹配到的内容。

例如：
```
(\d+)-(\w+)
```

匹配：
```
123-abc
```

Regex 内部会自动保存：
```
Group1 = 123

Group2 = abc
```

匹配完成后，可以通过Match对象读取：

`result.group()`或`result.group(0)`，返回`123-abc`.
`result.group(1)`返回`123`
`result.group(2)`返回`abc`

**作用二：改变匹配范围**

例如：
```
ab+
```
表示`a`后面有一个或多个`b`。

即：
```
ab
abb
abbb
```

而：
```
(ab)+
```
表示整个ab重复，

即：
```
ab
abab
ababab
```

也就是说，括号不仅可以保存分组内容，还可以改变运算范围。

**命名分组（Named Group）**
命名分组可以为括号分组指定名称，便于读取和维护复杂的正则表达式。
命名之后编号仍然能正常使用。

基本语法：`(?P<name>\d+)`
作用：把这个分组命名为：name。

获取方式：`result.group("name")`

**3️⃣`\1, \2, ...`：反向引用（Back Reference）**
作用：引用前面分组保存的内容。

Regex在匹配过程中，如果前面的括号已经匹配成功，立刻就可以通过`\1`等表达，再次引用前方保存的内容。

例如：
```
(\w+)\s+\1
```

匹配：
```
hello hello
```

匹配成功，而匹配：
```
hello world
```
会匹配失败。

同理，多个分组时：
```
(\d+)-(\w+)-\2
```

可以成功匹配：
```
123-abc-abc
```

其中，
```
Group1 = 123
Group2 = abc
```

总结：

| **表达式**   | **作用**               |
| --------- | -------------------- |
| ｜         | 匹配符号两边任意一组字符串        |
| `()`      | 分组、保存匹配内容，同时可以改变匹配范围 |
| `\1`、`\2` | 在当前匹配过程中引用前面分组保存的内容  |
