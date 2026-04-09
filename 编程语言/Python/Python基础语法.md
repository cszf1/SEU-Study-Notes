# Python 基础语法

## 一、变量与数据类型

### 1.1 变量定义
Python 是动态类型语言，不需要声明变量类型。

```python
# 直接赋值
name = "张三"        # 字符串
age = 20             # 整数
height = 1.75        # 浮点数
is_student = True    # 布尔值

# 多变量赋值
a, b, c = 1, 2, 3
x = y = z = 0
```

### 1.2 数据类型

| 类型 | 说明 | 示例 |
|------|------|------|
| `int` | 整数 | `42`, `-7` |
| `float` | 浮点数 | `3.14`, `1.0e-5` |
| `str` | 字符串 | `"hello"`, `'world'` |
| `bool` | 布尔值 | `True`, `False` |
| `None` | 空值 | `None` |

```python
# 类型转换
int("42")      # 字符串转整数 → 42
float("3.14")  # 字符串转浮点 → 3.14
str(42)        # 整数转字符串 → "42"

# 类型检查
type(42)       # <class 'int'>
isinstance(42, int)  # True
```

---

## 二、运算符

### 2.1 算术运算符

```python
10 + 3   # 加法 → 13
10 - 3   # 减法 → 7
10 * 3   # 乘法 → 30
10 / 3   # 除法 → 3.333...（总是返回浮点数）
10 // 3  # 整除 → 3（向下取整）
10 % 3   # 取余 → 1
10 ** 3  # 幂运算 → 1000
```

### 2.2 比较运算符

```python
==  # 等于
!=  # 不等于
>   # 大于
<   # 小于
>=  # 大于等于
<=  # 小于等于
```

### 2.3 逻辑运算符

```python
and  # 与
or   # 或
not  # 非

# 示例
age = 20
age >= 18 and age <= 25  # True
age < 18 or age > 60     # False
not False                # True
```

---

## 三、控制流程

### 3.1 条件语句

```python
# if-elif-else
score = 85

if score >= 90:
    print("优秀")
elif score >= 80:
    print("良好")
elif score >= 60:
    print("及格")
else:
    print("不及格")

# 三元表达式
result = "及格" if score >= 60 else "不及格"
```

### 3.2 循环语句

```python
# for 循环
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# 遍历列表
fruits = ["苹果", "香蕉", "橙子"]
for fruit in fruits:
    print(fruit)

# 遍历字典
person = {"name": "张三", "age": 20}
for key, value in person.items():
    print(f"{key}: {value}")

# while 循环
count = 0
while count < 5:
    print(count)
    count += 1

# break 和 continue
for i in range(10):
    if i == 3:
        continue  # 跳过本次循环
    if i == 7:
        break     # 退出循环
    print(i)

# enumerate 获取索引
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

---

## 四、函数

### 4.1 函数定义

```python
# 基本函数
def greet(name):
    """问候函数"""
    return f"你好，{name}！"

message = greet("张三")  # "你好，张三！"

# 默认参数
def power(base, exp=2):
    return base ** exp

power(3)      # 9（使用默认值）
power(3, 3)   # 27

# 可变参数
def sum_all(*args):
    return sum(args)

sum_all(1, 2, 3, 4)  # 10

# 关键字参数
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="张三", age=20)
```

### 4.2 Lambda 表达式

```python
# lambda 参数: 表达式
square = lambda x: x ** 2
square(5)  # 25

# 常用场景：排序
students = [("张三", 85), ("李四", 92), ("王五", 78)]
students.sort(key=lambda x: x[1], reverse=True)  # 按成绩降序

# 与 map/filter 配合
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))     # [1, 4, 9, 16, 25]
evens = list(filter(lambda x: x%2==0, numbers))  # [2, 4]
```

---

## 五、数据结构

### 5.1 列表（List）

```python
# 创建列表
fruits = ["苹果", "香蕉", "橙子"]

# 索引和切片
fruits[0]      # "苹果"（第一个元素）
fruits[-1]     # "橙子"（最后一个元素）
fruits[1:3]    # ["香蕉", "橙子"]
fruits[::2]    # ["苹果", "橙子"]（步长为2）

# 常用方法
fruits.append("葡萄")     # 末尾添加
fruits.insert(1, "西瓜")  # 指定位置插入
fruits.remove("香蕉")     # 删除指定元素
fruits.pop()              # 删除并返回最后一个

# 列表推导式
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

### 5.2 字典（Dictionary）

```python
# 创建字典
person = {"name": "张三", "age": 20, "city": "北京"}

# 访问和修改
person["name"]              # "张三"
person.get("job", "无业")   # "无业"（不存在时返回默认值）
person["job"] = "学生"      # 添加/修改

# 常用方法
person.keys()    # 所有键
person.values()  # 所有值
person.items()   # 所有键值对

# 字典推导式
squares = {x: x**2 for x in range(5)}
```

### 5.3 元组（Tuple）

```python
# 创建元组（不可变）
point = (3, 4)

# 解包
x, y = point

# 用作字典键（因为不可变）
locations = {(0, 0): "原点", (1, 0): "x轴"}
```

### 5.4 集合（Set）

```python
# 创建集合（无序、不重复）
fruits = {"苹果", "香蕉", "橙子"}
numbers = set([1, 2, 2, 3, 3, 3])  # {1, 2, 3}

# 集合运算
a = {1, 2, 3}
b = {2, 3, 4}
a | b   # 并集 {1, 2, 3, 4}
a & b   # 交集 {2, 3}
a - b   # 差集 {1}
```

---

## 六、字符串操作

```python
# 格式化
name, age = "张三", 20
f"我叫{name}，今年{age}岁"  # f-string（推荐）

# 常用方法
s = "  Hello, World!  "
s.strip()       # "Hello, World!"（去除首尾空格）
s.lower()       # 小写
s.upper()       # 大写
s.replace("World", "Python")
s.split(", ")   # ["Hello", "World!"]
",".join(["a", "b", "c"])  # "a,b,c"

# 查找
"hello".startswith("he")  # True
"hello".endswith("lo")    # True
"ll" in "hello"           # True
```

---

## 七、文件操作

```python
# 读取文件
with open("data.txt", "r", encoding="utf-8") as f:
    content = f.read()        # 读取全部
    for line in f:            # 逐行迭代
        print(line.strip())

# 写入文件
with open("output.txt", "w", encoding="utf-8") as f:
    f.write("Hello, World!\n")

# 追加写入
with open("log.txt", "a", encoding="utf-8") as f:
    f.write("新的日志行\n")
```

---

## 八、异常处理

```python
try:
    num = int(input("请输入数字："))
    result = 10 / num
except ValueError:
    print("输入的不是有效数字")
except ZeroDivisionError:
    print("不能除以零")
except Exception as e:
    print(f"发生错误：{e}")
else:
    print(f"结果是：{result}")
finally:
    print("程序执行完毕")
```

---

## 九、模块导入

```python
import math
math.sqrt(16)  # 4.0

from math import sqrt, pi
sqrt(16)  # 4.0

import numpy as np  # 起别名
```

---

## 总结

| 特性 | 说明 |
|------|------|
| 动态类型 | 变量不需要声明类型 |
| 缩进敏感 | 用缩进表示代码块，通常4个空格 |
| 一切皆对象 | 函数、类、模块都是对象 |
| 强类型 | 不同类型运算需要显式转换 |
