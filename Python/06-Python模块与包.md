# 第6章 Python模块与包

## 6.1 模块基础

### 什么是模块？

模块是一个包含 Python 代码的文件（`.py` 文件），可以将相关的代码组织在一起，便于复用和维护。

```python
# my_module.py
def greet(name):
    return f"Hello, {name}!"

PI = 3.14159
```

### 导入模块

```python
# 方式1：导入整个模块
import my_module
print(my_module.greet("Alice"))  # Hello, Alice!
print(my_module.PI)              # 3.14159

# 方式2：导入特定函数或变量
from my_module import greet, PI
print(greet("Bob"))  # Hello, Bob!

# 方式3：给模块起别名
import my_module as mm
print(mm.greet("Charlie"))

# 方式4：导入所有（不推荐）
from my_module import *
```

### 模块的搜索路径

当导入模块时，Python 按以下顺序搜索：

1. 当前目录
2. `PYTHONPATH` 环境变量中的目录
3. Python 默认路径（site-packages 等）

```python
import sys
print(sys.path)  # 查看模块搜索路径
```

## 6.2 标准库模块

Python 自带丰富的标准库，常用的有：

### os 模块 - 操作系统相关

```python
import os

# 文件和目录操作
os.getcwd()           # 获取当前工作目录
os.listdir('.')       # 列出当前目录文件
os.mkdir('new_dir')   # 创建目录
os.rmdir('old_dir')   # 删除空目录

# 路径操作
os.path.join('dir', 'file.txt')  # 拼接路径
os.path.split('/home/user/file.txt')  # 分割路径
os.path.exists('file.txt')       # 检查文件是否存在
os.path.isfile('file.txt')       # 是否是文件
os.path.isdir('folder')          # 是否是目录
```

### random 模块 - 随机数

```python
import random

random.random()        # [0, 1) 随机浮点数
random.randint(1, 10)  # [1, 10] 随机整数
random.choice(['a', 'b', 'c'])  # 随机选择
random.shuffle([1, 2, 3, 4])    # 洗牌
random.sample([1, 2, 3, 4], 2)  # 随机抽样
```

### datetime 模块 - 日期时间

```python
from datetime import datetime, timedelta

now = datetime.now()
print(now)                    # 2024-01-15 10:30:45.123456
print(now.strftime("%Y-%m-%d %H:%M"))  # 格式化字符串

# 时间运算
tomorrow = now + timedelta(days=1)
print(tomorrow)
```

### json 模块 - JSON 数据

```python
import json

# Python 对象转 JSON 字符串
data = {'name': 'Alice', 'age': 20}
json_str = json.dumps(data)
print(json_str)  # {"name": "Alice", "age": 20}

# JSON 字符串转 Python 对象
parsed = json.loads(json_str)
print(parsed)  # {'name': 'Alice', 'age': 20}

# 读写 JSON 文件
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2)

with open('data.json', 'r') as f:
    loaded = json.load(f)
```

### collections 模块 - 集合数据结构

```python
from collections import Counter, defaultdict, deque

# Counter: 计数器
words = ['apple', 'banana', 'apple', 'cherry', 'banana', 'apple']
counter = Counter(words)
print(counter)  # Counter({'apple': 3, 'banana': 2, 'cherry': 1})

# defaultdict: 默认字典
dd = defaultdict(list)
dd['fruits'].append('apple')
print(dd)  # defaultdict(<class 'list'>, {'fruits': ['apple']})

# deque: 双端队列
dq = deque()
dq.appendleft('first')
dq.append('last')
print(list(dq))  # ['first', 'last']
```

## 6.3 包的概念

包是包含 `__init__.py` 的目录，用于组织多个模块。

```
my_package/
├── __init__.py      # 包初始化文件
├── module1.py        # 模块1
├── module2.py        # 模块2
└── sub_package/      # 子包
    ├── __init__.py
    └── module3.py
```

### `__init__.py` 的作用

```python
# __init__.py 可以控制包的导入行为

# 例如：指定默认导出
from .module1 import ClassA
from .module2 import function_b

# 或者为空，只作为包标识
```

### 相对导入

在包内部模块中，可以使用相对导入：

```python
# 在 my_package/module1.py 中
from . import module2          # 导入同级的 module2
from .sub_package import module3  # 导入子包的模块

# 也可以使用相对导入的指定成员
from .module2 import specific_function
```

## 6.4 模块的高级用法

### `__name__` 变量

每个模块都有一个 `__name__` 属性：

- 当模块被直接运行时，`__name__` == `"__main__"`
- 当模块被导入时，`__name__` == 模块名

```python
# my_module.py

def main():
    print("This is the main function")

if __name__ == "__main__":
    # 只有直接运行此文件时才执行
    main()
    print("Module is being run directly")
else:
    print("Module is being imported")
```

### `__all__` 列表

控制 `from module import *` 导入的内容：

```python
# my_module.py
__all__ = ['public_func', 'PublicClass']

def public_func():
    pass

def _private_func():  # 以下划线开头
    pass

class PublicClass:
    pass
```

### 动态导入

```python
# 动态导入模块
module_name = 'json'
module = __import__(module_name)
print(module.dumps({'a': 1}))

# 或者使用 importlib
import importlib
module = importlib.import_module('json')
```

## 6.5 虚拟环境

### 为什么需要虚拟环境？

不同项目可能需要不同版本的依赖包，虚拟环境可以隔离项目环境。

### 创建和使用

```bash
# 创建虚拟环境
python -m venv myenv

# 激活虚拟环境
# Windows:
myenv\Scripts\activate
# Linux/Mac:
source myenv/bin/activate

# 安装包
pip install requests

# 退出虚拟环境
deactivate
```

### pip 包管理

```bash
pip install package_name       # 安装
pip install package==1.2.3     # 安装指定版本
pip install -r requirements.txt # 从文件安装
pip list                       # 列出已安装包
pip show package_name          # 查看包信息
pip uninstall package_name    # 卸载
pip freeze > requirements.txt  # 导出依赖
```

## 6.6 实战示例：创建一个命令行工具

```python
# mycli/__init__.py
from .cli import main

# mycli/cli.py
import sys
import os

def read_file(filename):
    """读取文件并返回内容"""
    try:
        with open(filename, 'r', encoding='utf-8') as f:
            return f.read()
    except FileNotFoundError:
        print(f"错误：文件 {filename} 不存在")
        sys.exit(1)

def word_count(text):
    """统计词数"""
    words = text.split()
    return len(words)

def main():
    if len(sys.argv) < 2:
        print("用法：python -m mycli.cli <文件名>")
        sys.exit(1)
    
    filename = sys.argv[1]
    content = read_file(filename)
    
    lines = content.count('\n') + 1
    words = word_count(content)
    chars = len(content)
    
    print(f"行数: {lines}")
    print(f"词数: {words}")
    print(f"字符数: {chars}")

if __name__ == "__main__":
    main()
```

## 本章小结

| 概念 | 说明 |
|------|------|
| 模块 | 单个 `.py` 文件，包含相关代码 |
| 包 | 包含 `__init__.py` 的目录，组织多个模块 |
| 导入方式 | `import`, `from...import`, `as` |
| 标准库 | Python 自带的常用模块（os, random, json 等） |
| 虚拟环境 | 隔离项目依赖的工具 |
| `__name__` | 判断模块是直接运行还是被导入 |

---

*学习日期：2026-04-13*
