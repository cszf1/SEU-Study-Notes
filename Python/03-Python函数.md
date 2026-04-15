# Python 函数

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[01-Python基础语法](./01-Python基础语法.md) | [02-Python数据结构](./02-Python数据结构.md)

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
