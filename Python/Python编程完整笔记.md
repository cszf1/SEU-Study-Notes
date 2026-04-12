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
# Python 数据结构

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[Python基础语法](./Python基础语法.md)

---

## 核心数据结构

Python 的核心数据结构包括：**列表、元组、字典、集合**。相比 C++，Python 的数据结构更灵活、内置功能更强大。

### 2.1 列表（List）

列表是 Python 最常用的**可变序列**，类似 C++ 的 `vector`。

#### 基本操作

```python
# 创建列表
nums = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

# 索引访问（支持负索引）
print(nums[0])    # 1
print(nums[-1])   # 5（最后一个元素）

# 切片操作
print(nums[1:4])   # [2, 3, 4]
print(nums[::2])  # [1, 3, 5]（步长为2）

# 修改元素
nums[0] = 10
nums.append(6)        # 末尾添加
nums.insert(0, 0)     # 指定位置插入
nums.extend([7, 8])   # 合并列表
```

#### 常用方法

| 方法 | 功能 | 示例 |
|------|------|------|
| `append(x)` | 末尾添加元素 | `lst.append(6)` |
| `insert(i, x)` | 索引 i 处插入 | `lst.insert(0, x)` |
| `pop([i])` | 删除并返回索引 i 元素 | `lst.pop()` |
| `remove(x)` | 删除第一个 x | `lst.remove(x)` |
| `sort()` | 原地排序 | `lst.sort()` |
| `reverse()` | 原地反转 | `lst.reverse()` |
| `index(x)` | 查找 x 的索引 | `lst.index(x)` |
| `count(x)` | 统计 x 出现次数 | `lst.count(x)` |

```python
# 列表推导式（重要！）
squares = [x**2 for x in range(10)]      # [0, 1, 4, 9, 16, 36, 49, 64, 81]
evens = [x for x in range(20) if x % 2 == 0]  # [0, 2, 4, ..., 18]

# 二维列表
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix[1][2])  # 6
```

---

### 2.2 元组（Tuple）

元组是**不可变序列**，用于存储不变的数据，类似于 C++ 的 `const vector`。

```python
# 创建元组
point = (3, 4)
colors = ("red", "green", "blue")
single = (42,)  # 单元素元组需要逗号

# 不可修改
# point[0] = 5  # TypeError!

# 解包
x, y = point
a, b, c = colors

# 命名元组（类似结构体）
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(p.x, p.y)  # 3 4
```

**元组 vs 列表**：
- 元组：不可变，更快，更安全，用于固定数据
- 列表：可变，灵活，用于需要修改的数据

---

### 2.3 字典（Dict）

字典是**键值对**的集合，类似 C++ 的 `unordered_map`，但功能更强大。

```python
# 创建字典
student = {
    "name": "张三",
    "age": 18,
    "major": "电子信息"
}

# 访问（安全获取）
print(student["name"])        # 张三
print(student.get("score", 0))  # 0（键不存在返回默认值）

# 修改和添加
student["age"] = 19          # 修改
student["score"] = 95        # 添加新键值对

# 删除
del student["score"]
score = student.pop("age")

# 遍历
for key in student:          # 遍历键
    print(f"{key}: {student[key]}")

for key, value in student.items():  # 遍历键值对
    print(f"{key}: {value}")
```

#### 字典推导式

```python
squares = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

#### defaultdict（默认值字典）

```python
from collections import defaultdict

# 自动为不存在的键提供默认值
count = defaultdict(int)
count["apple"] += 1  # 不需要先判断键是否存在
print(count["banana"])  # 0（自动初始化为0）
```

---

### 2.4 集合（Set）

集合是**无序、不重复**的元素集合，用于去重和集合运算。

```python
# 创建集合
fruits = {"apple", "banana", "orange"}
nums = set([1, 2, 2, 3, 3, 4])  # {1, 2, 3, 4}（自动去重）

# 添加/删除
fruits.add("grape")
fruits.remove("banana")      # 不存在会报错
fruits.discard("melon")      # 不存在不报错

# 集合运算
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)   # 并集: {1, 2, 3, 4, 5, 6}
print(a & b)   # 交集: {3, 4}
print(a - b)   # 差集: {1, 2}
print(a ^ b)   # 对称差集: {1, 2, 5, 6}

# 判断关系
print(3 in a)           # True
print(a.issubset(b))    # False
print(a.isdisjoint(b))  # False（有交集）
```

---

### 2.5 数据结构对比

| 数据结构 | 可变性 | 有序性 | 重复元素 | 访问方式 | C++类比 |
|----------|--------|--------|----------|----------|---------|
| list | ✅可变 | ✅有序 | ✅允许 | 索引/切片 | vector |
| tuple | ❌不可 | ✅有序 | ✅允许 | 索引/切片 | const vector |
| dict | ✅可变 | Python3.7+有序 | 键不可重复 | 键访问 | unordered_map |
| set | ✅可变 | ❌无序 | ❌不允许 | 成员检查 | unordered_set |

---

### 2.6 实际应用示例

#### 栈和队列

```python
# 栈（用列表模拟）
stack = []
stack.append(1)      # push
stack.append(2)
top = stack.pop()    # pop
print(top)           # 2

# 队列
from collections import deque
queue = deque()
queue.append(1)
queue.append(2)
queue.popleft()      # O(1) 出队
```

#### 统计词频

```python
from collections import Counter

text = "python python java c++ python java"
words = text.split()
counter = Counter(words)
print(counter.most_common(2))  # [('python', 3), ('java', 2)]
```

---

*笔记整理 by 佩弦 | 2026-04-09*
# Python 函数

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[Python基础语法](./Python基础语法.md) | [Python数据结构](./Python数据结构.md)

---

## 一、函数基础

### 1.1 定义与调用

Python 使用 `def` 关键字定义函数，区别于 C++ 的 `返回类型 函数名()` 格式。

```python
# Python 函数定义
def greet(name):
    """问候函数"""
    return f"你好，{name}！"

# 调用函数
message = greet("张三")
print(message)  # 你好，张三！
```

```cpp
// C++ 函数对比
#include <iostream>
#include <string>
using namespace std;

string greet(string name) {
    return "你好，" + name + "！";
}

int main() {
    cout << greet("张三") << endl;
    return 0;
}
```

**关键区别**：
- Python 不需要声明返回类型
- Python 使用缩进（4空格）而不是大括号
- Python 不需要参数类型声明

### 1.2 参数默认值

Python 支持参数默认值，C++ 也有默认参数，但语法不同。

```python
def power(base, exponent=2):
    """计算 base 的 exponent 次方，默认平方"""
    return base ** exponent

print(power(3))      # 9（使用默认值 exponent=2）
print(power(2, 3))   # 8（2 的 3 次方）
print(power(base=2, exponent=3))  # 关键字参数，可不按顺序
```

**注意**：默认参数必须放在非默认参数右边。

### 1.3 函数文档字符串

Python 特有功能，用于描述函数功能。

```python
def calculate_area(radius):
    """
    计算圆的面积
    
    参数:
        radius (float): 圆的半径
    返回:
        float: 圆的面积
    """
    return 3.14159 * radius ** 2
```

---

## 二、参数传递

### 2.1 位置参数与关键字参数

```python
def introduce(name, age, major):
    print(f"我是{name}，{age}岁，专业{major}")

# 位置参数（按顺序）
introduce("李四", 20, "电子信息")  

# 关键字参数（指定参数名，可乱序）
introduce(age=21, major="计算机", name="王五")

# 混合使用：位置参数在前，关键字参数在后
introduce("赵六", major="自动化", age=19)
```

### 2.2 可变参数 *args 和 **kwargs

这是 Python 独有的强大特性，C++ 需要用模板或 va_list 实现类似功能。

```python
# *args：接收任意数量的位置参数（打包成元组）
def sum_all(*numbers):
    """求任意数量数字的和"""
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))           # 6
print(sum_all(10, 20, 30, 40))    # 100

# **kwargs：接收任意数量的关键字参数（打包成字典）
def print_info(**info):
    """打印任意关键字参数"""
    for key, value in info.items():
        print(f"{key}: {value}")

print_info(name="张三", age=20, major="电子信息")
# 输出：
# name: 张三
# age: 20
# major: 电子信息

# 组合使用
def flexible_func(*args, **kwargs):
    print(f"位置参数: {args}")
    print(f"关键字参数: {kwargs}")

flexible_func(1, 2, 3, name="test", value=100)
# 输出：
# 位置参数: (1, 2, 3)
# 关键字参数: {'name': 'test', 'value': 100}
```

### 2.3 解包参数

将列表或字典解包为函数参数。

```python
# 解包列表为位置参数
nums = [1, 2, 3, 4, 5]
print(sum_all(*nums))  # 等价于 sum_all(1, 2, 3, 4, 5)

# 解包字典为关键字参数
info = {"name": "李四", "age": 21, "major": "通信工程"}
introduce(**info)  # 等价于 introduce(name="李四", age=21, major="通信工程")
```

---

## 三、返回值

### 3.1 基本返回值

```python
def add(a, b):
    return a + b

# Python 允许返回多个值（实际是返回元组）
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers)

low, high, total = get_stats([1, 5, 3, 9, 2])
print(f"最小:{low}, 最大:{high}, 总和:{total}")
```

```cpp
// C++ 返回多个值需要用结构体或引用
#include <vector>
#include <algorithm>
using namespace std;

struct Stats {
    int min_val;
    int max_val;
    int sum;
};

Stats get_stats(vector<int> numbers) {
    Stats s;
    s.min_val = *min_element(numbers.begin(), numbers.end());
    s.max_val = *max_element(numbers.begin(), numbers.end());
    s.sum = 0;
    for (int n : numbers) s.sum += n;
    return s;
}
```

### 3.2 无返回值

```python
# 无 return 或 return None
def print_hello(name):
    print(f"Hello, {name}")
    return None  # 可省略

result = print_hello("World")
print(result)  # None
```

---

## 四、作用域与命名空间

### 4.1 LEGB 规则

Python 按 LEGB 顺序查找变量：
- **L**ocal：本地作用域（函数内部）
- **E**nclosing：闭包作用域（外层函数）
- **G**lobal：全局作用域（模块级别）
- **B**uilt-in：内置作用域（Python 内置函数）

```python
x = "全局变量"

def outer():
    x = "外层变量"
    
    def inner():
        x = "内层变量"
        print(x)  # 内层变量
    
    inner()
    print(x)  # 外层变量

outer()
print(x)  # 全局变量
```

### 4.2 global 和 nonlocal 关键字

```python
counter = 0

def increment():
    global counter  # 声明使用全局变量
    counter += 1
    return counter

print(increment())  # 1
print(increment())  # 2

# nonlocal 用于内层函数修改外层变量
def outer():
    count = 0
    
    def inner():
        nonlocal count
        count += 1
        return count
    
    return inner

f = outer()
print(f())  # 1
print(f())  # 2
```

---

## 五、匿名函数 lambda

lambda 表达式用于创建小型匿名函数，类似 C++ 的 lambda。

```python
# lambda 基本语法
square = lambda x: x ** 2
print(square(5))  # 25

# 多参数 lambda
add = lambda a, b: a + b
print(add(3, 4))  # 7

# 结合内置函数使用
numbers = [5, 2, 8, 1, 9]

# sorted + lambda（按绝对值排序）
sorted_nums = sorted(numbers, key=lambda x: -x)  # 降序
print(sorted_nums)  # [9, 8, 5, 2, 1]

# map + lambda
squared = list(map(lambda x: x**2, numbers))
print(squared)  # [25, 4, 64, 1, 81]

# filter + lambda
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 8]
```

```cpp
// C++ lambda 对比
#include <algorithm>
#include <vector>
#include <cmath>
using namespace std;

int main() {
    vector<int> numbers = {5, 2, 8, 1, 9};
    
    // sorted
    sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a > b;  // 降序
    });
    
    // map 等价用 transform
    vector<int> squared(numbers.size());
    transform(numbers.begin(), numbers.end(), squared.begin(),
              [](int x) { return x * x; });
    
    return 0;
}
```

---

## 六、装饰器（Decorator）

装饰器是高阶函数，用于在不修改原函数的情况下增强功能。理解装饰器需要先理解函数可以像变量一样传递。

### 6.1 基础装饰器

```python
def log_decorator(func):
    """日志装饰器：打印函数调用信息"""
    def wrapper(*args, **kwargs):
        print(f"[LOG] 调用函数: {func.__name__}")
        result = func(*args, **kwargs)
        print(f"[LOG] 函数执行完毕")
        return result
    return wrapper

@log_decorator
def add(a, b):
    """加法函数"""
    return a + b

# 等价于：add = log_decorator(add)
result = add(3, 4)
print(f"结果: {result}")

# 输出：
# [LOG] 调用函数: add
# [LOG] 函数执行完毕
# 结果: 7
```

### 6.2 带参数的装饰器

```python
def timer(seconds):
    """计时装饰器工厂"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            import time
            start = time.time()
            result = func(*args, **kwargs)
            elapsed = time.time() - start
            print(f"{func.__name__} 执行耗时: {elapsed:.4f}秒")
            return result
        return wrapper
    return decorator

@timer(2)
def slow_function():
    import time
    time.sleep(1)
    return "完成"

slow_function()
```

---

## 七、生成器（Generator）

生成器是一种特殊的迭代器，用 `yield` 关键字返回值，按需生成数据，节省内存。

```python
# 普通函数返回列表
def first_n_squares_list(n):
    return [i**2 for i in range(n)]

# 生成器按需生成
def first_n_squares_gen(n):
    for i in range(n):
        yield i ** 2

# 对比
squares_list = first_n_squares_list(5)
print(squares_list)  # [0, 1, 4, 9, 16]  一次性全部生成

squares_gen = first_n_squares_gen(5)
print(next(squares_gen))  # 0
print(next(squares_gen))  # 1
print(next(squares_gen))  # 4

# 生成器常用于大数据处理
def fibonacci(limit=1000000):
    """斐波那契数列生成器"""
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

for num in fibonacci(1000):
    print(num, end=" ")
```

```cpp
// C++ 等价用类实现迭代器
class Fibonacci {
    int a = 0, b = 1;
    int limit;
public:
    Fibonacci(int lim) : limit(lim) {}
    
    int next() {
        int result = a;
        a = b;
        b = a + b;
        return result;
    }
    
    bool has_next() {
        return a < limit;
    }
};
```

---

## 知识点总结

| 特性 | Python | C++ 对比 |
|------|--------|----------|
| 定义语法 | `def func():` | `返回类型 func() {}` |
| 参数类型 | 不声明类型 | 必须声明 |
| 默认参数 | `def f(a, b=1)` | `void f(int a, int b=1)` |
| 可变参数 | `*args, **kwargs` | `template...` 或 `va_list` |
| 多返回值 | `return a, b` | 结构体/引用 |
| 匿名函数 | `lambda x: x**2` | `[](int x){ return x*x; }` |
| 装饰器 | `@decorator` | 无直接等价 |
| 生成器 | `yield` | 类+迭代器 |

---

## 练习题

1. 编写一个函数，使用可变参数 `*args` 计算任意数量数字的乘积。

2. 写一个装饰器 `retry`，使被装饰的函数失败时最多重试 3 次。

3. 实现一个生成器函数 `primes(limit)`，返回小于 `limit` 的所有素数。

4. 用 `lambda` 和 `filter` 找出列表中所有以字母 'A' 开头的字符串。

---

**相关链接**：
- 下一章：[Python 类与对象](./Python类与对象.md)
- 《Python编程：从入门到实践》第9章
- 《Hello 算法》第9章
# Python 面向对象编程

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[Python基础语法](./Python基础语法.md) | [Python数据结构](./Python数据结构.md) | [Python函数](./Python函数.md)

---

## 一、类与对象基础

### 1.1 定义类

Python 使用 `class` 关键字定义类，区别于 C++ 的 `class 类名 {}` 格式。

```python
# Python 类定义
class Student:
    """学生类"""
    
    # 类属性（所有实例共享）
    school_name = "东南大学"
    
    # 初始化方法（类似C++构造函数）
    def __init__(self, name, student_id):
        # 实例属性
        self.name = name
        self.student_id = student_id
        self._grade = 0  # 受保护属性（约定）
        self.__score = 0  # 私有属性（名称重整）
    
    # 实例方法
    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score
            self._grade = "优秀" if score >= 90 else "及格" if score >= 60 else "不及格"
    
    def get_info(self):
        return f"{self.name} (学号: {self.student_id})"
    
    # 字符串表示（类似C++的operator<<）
    def __str__(self):
        return f"Student({self.name}, {self.student_id})"
```

**C++对比**：
```cpp
// C++ 类定义
class Student {
private:
    string name;
    string student_id;
    int score;
public:
    Student(string n, string id) : name(n), student_id(id), score(0) {}
    void setScore(int s) { score = s; }
    string getInfo() { return name + " " + student_id; }
};
```

### 1.2 创建对象

```python
# 创建实例
student1 = Student("张三", "2026001")
student2 = Student("李四", "2026002")

# 调用方法
student1.set_score(95)
print(student1.get_info())  # 张三 (学号: 2026001)
print(student1)  # Student(张三, 2026001)
```

---

## 二、属性访问控制

Python 的访问控制采用**命名约定**，而非语法强制：

| 标记 | 含义 | 示例 |
|------|------|------|
| `_protected` | 受保护，类外部慎用 | `_name` |
| `__private` | 私有，触发名称重整 | `__score` |
| 无标记 | 公开，可自由访问 | `name` |

```python
student = Student("王五", "2026003")

# 公开属性
print(student.name)  # 王五

# 受保护属性（可访问，但不推荐）
print(student._grade)  # 0

# 私有属性（实际可通过名称重整访问，但不推荐）
# print(student.__score)  # AttributeError
print(student._Student__score)  # 0，绕过了封装
```

**建议**：使用 `@property` 装饰器实现安全的属性访问。

---

## 三、@property 装饰器

类似 C++ 的 getter/setter，但以属性方式访问：

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius  # 调用 setter
    
    @property
    def radius(self):
        """获取半径"""
        return self._radius
    
    @radius.setter
    def radius(self, value):
        """设置半径（带验证）"""
        if value <= 0:
            raise ValueError("半径必须为正数")
        self._radius = value
    
    @property
    def area(self):
        """计算面积（只读属性）"""
        return 3.14159 * self._radius ** 2

# 使用
c = Circle(5)
print(c.radius)  # 5，调用 @property
c.radius = 10   # 调用 @radius.setter
print(c.area)   # 314.159，只读属性
# c.area = 100  # AttributeError
```

**C++对比**：
```cpp
class Circle {
private:
    double radius;
public:
    double getRadius() const { return radius; }
    void setRadius(double r) { if(r>0) radius = r; }
    double getArea() const { return 3.14159 * radius * radius; }
};
```

---

## 四、继承

### 4.1 单继承

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        raise NotImplementedError

class Dog(Animal):
    """Dog 继承自 Animal"""
    
    def speak(self):
        return f"{self.name} says: 汪汪！"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says: 喵~"

# 多态
animals = [Dog("旺财"), Cat("咪咪")]
for animal in animals:
    print(animal.speak())
```

**C++对比**：
```cpp
class Animal {
protected:
    string name;
public:
    Animal(string n) : name(n) {}
    virtual string speak() = 0;  // 纯虚函数
};

class Dog : public Animal {
public:
    Dog(string n) : Animal(n) {}
    string speak() override { return name + " says: 汪汪！"; }
};
```

### 4.2 多继承

Python 支持多继承（慎用）：

```python
class Flyable:
    def fly(self):
        return "正在飞翔"

class Swimmable:
    def swim(self):
        return "正在游泳"

class Duck(Animal, Flyable, Swimmable):
    """鸭子继承自动物、会飞、会游泳"""
    pass

duck = Duck("唐老鸭")
print(duck.speak())  # 唐老鸭 says: 嘎嘎！
print(duck.fly())    # 正在飞翔
print(duck.swim())  # 正在游泳
```

---

## 五、特殊方法（魔术方法）

Python 类可以定义特殊方法，实现运算符重载等功能：

| 方法 | 作用 | 示例 |
|------|------|------|
| `__init__` | 初始化 | `obj = Class(args)` |
| `__str__` | 字符串表示 | `print(obj)` |
| `__repr__` | 调试表示 | `repr(obj)` |
| `__len__` | 长度 | `len(obj)` |
| `__eq__` | 相等比较 | `obj1 == obj2` |
| `__add__` | 加法运算 | `obj1 + obj2` |
| `__call__` | 可调用对象 | `obj()` |

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __add__(self, other):
        """向量加法"""
        return Vector(self.x + other.x, self.y + other.y)
    
    def __eq__(self, other):
        """向量相等"""
        return self.x == other.x and self.y == other.y

v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)      # Vector(4, 6)
print(v1 == v2)     # False
```

---

## 六、类方法与静态方法

### 6.1 实例方法、类方法、静态方法对比

```python
class MathUtils:
    PI = 3.14159
    
    def __init__(self, value):
        """实例方法：需要实例调用，能访问实例和类属性"""
        self.value = value
    
    def double(self):
        """实例方法"""
        return self.value * 2
    
    @classmethod
    def create_from_degrees(cls, degrees):
        """类方法：通过类调用，能访问类属性"""
        radians = degrees * cls.PI / 180
        return cls(radians)  # 创建实例
    
    @staticmethod
    def absolute(x):
        """静态方法：通过类调用，不能访问实例/类属性"""
        return abs(x)

# 调用方式
m = MathUtils(2)
print(m.double())                    # 4，实例调用
print(MathUtils.create_from_degrees(180))  # 类调用
print(MathUtils.absolute(-5))         # 5，类调用
```

### 6.2 静态方法适用场景

```python
class StringUtils:
    @staticmethod
    def is_palindrome(s):
        """判断回文数"""
        return s == s[::-1]
    
    @staticmethod
    def to_snake_case(name):
        """驼峰转蛇形"""
        import re
        return re.sub(r'(?<!^)(?=[A-Z])', '_', name).lower()

print(StringUtils.is_palindrome("上海自来水来自海上"))  # True
print(StringUtils.to_snake_case("HelloWorld"))  # hello_world
```

---

## 七、Python vs C++ 面向对象对比

| 特性 | Python | C++ |
|------|--------|-----|
| 类定义 | `class Name:` | `class Name {};` |
| 构造函数 | `__init__` | `ClassName(args)` |
| 析构函数 | `__del__` | `~ClassName()` |
| self/this | `self`（显式） | `this`（隐式） |
| 访问控制 | 命名约定 `_` `__` | `private/public/protected` |
| 继承 | `class A(B):` | `class A : public B {}` |
| 多继承 | 支持 | 支持（复杂） |
| 虚函数 | 默认虚 | 需 `virtual` |
| 纯虚函数 | `raise NotImplementedError` | `= 0` |
| 属性装饰器 | `@property` | getter/setter 方法 |

---

## 八、练习题

### 基础练习
1. 定义一个 `BankAccount` 类，包含账户名、余额，实现存钱、取钱方法
2. 使用 `@property` 实现只读的属性访问

### 进阶练习
1. 定义一个 `Stack` 类，实现栈的 push、pop、is_empty 操作
2. 使用 `__str__` 方法自定义打印格式

### 对比练习
1. 将以下 C++ 类改写为 Python：
```cpp
class Point {
private:
    double x, y;
public:
    Point(double a=0, double b=0) : x(a), y(b) {}
    double distance(const Point& p) {
        return sqrt((x-p.x)*(x-p.x) + (y-p.y)*(y-p.y));
    }
};
```

---

## 九、总结

Python 面向对象编程要点：
1. **类定义**：`class` + `__init__` + `self`
2. **访问控制**：`_` 受保护，`__` 私有，约定 > 强制
3. **属性访问**：`@property` 装饰器实现安全访问
4. **继承**：简单直观的语法，支持多继承
5. **特殊方法**：实现运算符重载和内置函数行为
6. **方法类型**：实例方法、类方法、静态方法各有用途

> 🎵 对比 C++ 学习，Python 的 OOP 更简洁灵活，但需要养成良好的命名约定习惯
# Python 文件操作与异常处理

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[Python基础语法](./Python基础语法.md) | [Python数据结构](./Python数据结构.md) | [Python函数](./Python函数.md)

---

## 一、文件操作

### 1.1 文件读取

Python 文件操作比 C++ 更简洁，无需显式关闭文件（可用 `with` 语句自动管理）。

```python
# 读取整个文件
with open('data.txt', 'r', encoding='utf-8') as f:
    content = f.read()
    print(content)

# 逐行读取
with open('data.txt', 'r', encoding='utf-8') as f:
    for line in f:
        print(line.strip())  # strip() 去除换行符

# 读取所有行到列表
with open('data.txt', 'r', encoding='utf-8') as f:
    lines = f.readlines()
```

**C++ 对比**：
```cpp
// C++ 文件读取
#include <fstream>
using namespace std;

int main() {
    ifstream fin("data.txt");
    string line;
    while (getline(fin, line)) {
        cout << line << endl;
    }
    fin.close();
    return 0;
}
```

| 模式 | 说明 |
|------|------|
| `'r'` | 读取（默认）|
| `'w'` | 写入（覆盖）|
| `'a'` | 追加 |
| `'rb'`/`'wb'` | 二进制模式 |

### 1.2 文件写入

```python
# 写入文件（覆盖）
with open('output.txt', 'w', encoding='utf-8') as f:
    f.write("Hello, Python!\n")
    f.write("第二行内容")

# 追加写入
with open('log.txt', 'a', encoding='utf-8') as f:
    f.write("新的日志条目\n")
```

### 1.3 二进制文件

```python
# 读取图片等二进制文件
with open('image.png', 'rb') as f:
    data = f.read()
    print(f"图片大小: {len(data)} 字节")

# 写入二进制文件
with open('copy.bin', 'wb') as f:
    f.write(data)
```

### 1.4 JSON 数据存储

Python 内置 `json` 模块，适合存储结构化数据。

```python
import json

# 写入 JSON
data = {
    "name": "张三",
    "scores": [95, 87, 92],
    "passed": True
}

with open('data.json', 'w', encoding='utf-8') as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 读取 JSON
with open('data.json', 'r', encoding='utf-8') as f:
    loaded_data = json.load(f)
    print(loaded_data["name"])
```

**输出**：
```json
{
  "name": "张三",
  "scores": [95, 87, 92],
  "passed": true
}
```

---

## 二、异常处理

### 2.1 基础 try-except

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("错误：除数不能为零")
```

### 2.2 捕获多个异常

```python
try:
    num = int(input("输入数字: "))
    result = 10 / num
except ValueError:
    print("输入无效，请输入数字")
except ZeroDivisionError:
    print("除数不能为零")
```

### 2.3 完整异常结构

```python
try:
    with open('data.txt', 'r') as f:
        content = f.read()
except FileNotFoundError:
    print("文件不存在")
except PermissionError:
    print("没有读取权限")
else:
    # 没有异常时执行
    print(f"成功读取 {len(content)} 个字符")
finally:
    # 无论是否有异常都执行
    print("操作完成")
```

### 2.4 异常传播与 raise

```python
def divide(a, b):
    if b == 0:
        raise ValueError("除数不能为零")
    return a / b

try:
    result = divide(10, 0)
except ValueError as e:
    print(f"捕获异常: {e}")
```

---

## 三、综合实践：数据处理程序

```python
import json

def load_students(filename):
    """加载学生数据"""
    try:
        with open(filename, 'r', encoding='utf-8') as f:
            return json.load(f)
    except FileNotFoundError:
        print(f"文件 {filename} 不存在，返回空列表")
        return []
    except json.JSONDecodeError:
        print("JSON 格式错误")
        return []

def save_students(filename, students):
    """保存学生数据"""
    try:
        with open(filename, 'w', encoding='utf-8') as f:
            json.dump(students, f, ensure_ascii=False, indent=2)
        return True
    except PermissionError:
        print("没有写入权限")
        return False

def add_student(students):
    """添加学生"""
    try:
        name = input("姓名: ")
        score = int(input("成绩: "))
        if score < 0 or score > 100:
            raise ValueError("成绩必须在 0-100 之间")
        students.append({"name": name, "score": score})
        print(f"已添加 {name}")
    except ValueError as e:
        print(f"输入错误: {e}")

# 主程序
students = load_students('students.json')
print(f"当前有 {len(students)} 名学生")

while True:
    cmd = input("\n1-添加 2-查看 0-退出: ")
    if cmd == '1':
        add_student(students)
    elif cmd == '2':
        for s in students:
            print(f"{s['name']}: {s['score']}")
    elif cmd == '0':
        if save_students('students.json', students):
            print("已保存")
        break
```

---

## 四、与 C++ 对比总结

| 特性 | Python | C++ |
|------|--------|-----|
| 文件读取 | `open('file', 'r')` | `ifstream fin("file")` |
| 自动关闭 | `with` 语句自动管理 | 需手动 `close()` |
| 异常捕获 | `try-except` | `try-catch` |
| 自定义异常 | `raise Exception()` | `throw exception()` |
| JSON 支持 | 内置 `json` 模块 | 需第三方库 (nlohmann/json) |

---

## 五、学习要点

1. **优先使用 `with` 语句**：自动管理文件资源，避免忘记关闭
2. **异常处理原则**：只捕获能处理的异常，不要静默吞掉所有错误
3. **JSON 优于自定义格式**：结构化数据优先用 JSON，便于跨语言交换
4. **错误信息要有用**：给用户有意义的错误提示

---

**下节预告**：[Python 测试与调试](./Python测试与调试.md)
