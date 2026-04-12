# Python 数据结构

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[01-Python基础语法](./01-Python基础语法.md)

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
