# Python 标准库

> 大一上学期 | 东南大学 | 电子信息类

**前置知识**：[01-Python基础语法](./01-Python基础语法.md) | [02-Python数据结构](./02-Python数据结构.md) | [03-Python函数](./03-Python函数.md) | [04-Python面向对象编程](./04-Python面向对象编程.md) | [05-Python文件操作与异常处理](./05-Python文件操作与异常处理.md) | [06-Python模块与包](./06-Python模块与包.md)

---

## 概述

Python标准库是Python自带的"内置电池"（Batteries Included），包含大量模块，无需额外安装即可使用。掌握常用标准库模块能快速解决80%的常见编程问题。

---

## 1. os 模块 - 操作系统接口

用于与操作系统交互，实现文件/目录管理、进程管理、环境变量访问等功能。

### 核心功能

```python
import os

# 目录操作
os.getcwd()           # 获取当前工作目录
os.chdir('/path')     # 切换目录
os.listdir('.')       # 列出目录内容
os.mkdir('new_dir')   # 创建目录
os.makedirs('a/b/c')  # 递归创建目录
os.rmdir('dir')       # 删除空目录

# 文件操作
os.remove('file.txt') # 删除文件
os.rename('old.txt', 'new.txt')  # 重命名

# 路径操作（跨平台）
os.path.join('folder', 'file.txt')  # 拼接路径
os.path.split('/a/b/c.txt')          # ('/a/b', 'c.txt')
os.path.exists('file.txt')           # 判断是否存在
os.path.isfile('file.txt')          # 是否为文件
os.path.isdir('folder')             # 是否为目录
os.path.basename('/a/b.txt')        # 'b.txt'
os.path.dirname('/a/b.txt')          # '/a'

# 环境变量
os.getenv('PATH')                    # 获取环境变量
os.environ['MY_VAR'] = 'value'      # 设置环境变量
```

### 注意事项
- 使用 `import os` 而非 `from os import *`，避免覆盖内置的 `open()` 函数

---

## 2. sys 模块 - 系统参数

访问Python解释器和运行环境的参数。

### 核心功能

```python
import sys

# 命令行参数
# 运行: python script.py arg1 arg2
print(sys.argv)  # ['script.py', 'arg1', 'arg2']

# Python信息
print(sys.version)       # Python版本
print(sys.platform)      # 操作系统平台
print(sys.executable)    # Python解释器路径

# 模块搜索路径
print(sys.path)          # 模块搜索路径列表
sys.path.append('/my/path')  # 添加搜索路径

# 标准流
sys.stdin   # 标准输入
sys.stdout  # 标准输出
sys.stderr  # 标准错误（重定向后仍可见）

# 退出程序
sys.exit(0)  # 0表示正常退出，非0表示异常
sys.exit("Error message")  # 带消息退出
```

---

## 3. datetime 模块 - 日期时间

处理日期和时间的核心模块。

### 核心类

```python
from datetime import datetime, date, time, timedelta

# 获取当前时间
now = datetime.now()           # 2026-04-14 22:53:25.123456
today = date.today()           # 2026-04-14

# 构造指定时间
dt = datetime(2026, 4, 14, 10, 30, 0)

# 格式化输出
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
# 输出: '2026-04-14 22:53:25'
formatted = now.strftime("%A, %B %d, %Y")
# 输出: 'Tuesday, April 14, 2026'

# 解析字符串
dt = datetime.strptime("2026-04-14 10:30", "%Y-%m-%d %H:%M")

# 时间计算
tomorrow = now + timedelta(days=1)
last_week = now - timedelta(weeks=1)
next_hour = now + timedelta(hours=1)

# 日期运算
date1 = date(2026, 4, 14)
date2 = date(2026, 4, 20)
delta = date2 - date1  # datetime.timedelta(days=6)
print(delta.days)  # 6

# 提取组件
print(now.year, now.month, now.day)       # 2026, 4, 14
print(now.hour, now.minute, now.second)   # 22, 53, 25
```

---

## 4. json 模块 - JSON处理

JSON（JavaScript Object Notation）是常用的数据交换格式。

### 基本操作

```python
import json

# Python对象 → JSON字符串
data = {
    "name": "Alice",
    "age": 30,
    "hobbies": ["reading", "hiking"]
}

json_str = json.dumps(data)           # 紧凑格式
json_pretty = json.dumps(data, indent=4, ensure_ascii=False)  # 美化输出

# JSON字符串 → Python对象
parsed = json.loads(json_str)
print(parsed["name"])  # 'Alice'

# 文件操作
with open('data.json', 'w', encoding='utf-8') as f:
    json.dump(data, f, indent=2, ensure_ascii=False)  # 写入文件

with open('data.json', 'r', encoding='utf-8') as f:
    loaded = json.load(f)  # 从文件读取

# 处理中文
json.dumps({"名字": "张三"}, ensure_ascii=False)
```

---

## 5. collections 模块 - 高级数据结构

提供比内置列表、字典更强大的数据结构。

### defaultdict - 默认字典

```python
from collections import defaultdict

# 自动初始化不存在的键
dd = defaultdict(int)  # 默认值为0
dd["apple"] += 1
print(dd["banana"])  # 0（自动初始化）

dd = defaultdict(list)  # 默认值为空列表
dd["fruits"].append("apple")
print(dd["vegetables"])  # []（自动初始化）

# 统计水果数量
fruit_basket = ["apple", "banana", "apple", "orange", "banana"]
counter = defaultdict(int)
for fruit in fruit_basket:
    counter[fruit] += 1
print(counter)  # {'apple': 2, 'banana': 2, 'orange': 1}
```

### Counter - 计数器

```python
from collections import Counter

words = ["apple", "banana", "apple", "orange", "banana", "apple"]
counter = Counter(words)

print(counter)              # Counter({'apple': 3, 'banana': 2, 'orange': 1})
print(counter.most_common(2))  # [('apple', 3), ('banana', 2)]
print(counter["apple"])     # 3
print(list(counter.elements()))  # ['apple', 'apple', 'apple', 'banana', 'banana', 'orange']
```

### deque - 双端队列

```python
from collections import deque

d = deque([1, 2, 3])

d.append(4)           # 右侧添加
d.appendleft(0)       # 左侧添加
print(d)              # deque([0, 1, 2, 3, 4])

d.pop()               # 右侧移除 → 4
d.popleft()           # 左侧移除 → 0
print(d)              # deque([1, 2, 3])

# 限制最大长度
d = deque(maxlen=3)
d.extend([1, 2, 3, 4, 5])  # deque([3, 4, 5])，超出自动移除最旧元素
```

### namedtuple - 命名元组

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)

print(p.x, p.y)       # 10, 20
print(p[0], p[1])    # 10, 20（仍可用索引访问）
```

---

## 6. re 模块 - 正则表达式

强大的文本模式匹配工具。

### 基本语法

```python
import re

text = "我的邮箱是 test@example.com，电话是 138-1234-5678"

# 搜索
match = re.search(r'\d{3}-\d{4}-\d{4}', text)
if match:
    print(match.group())  # 138-1234-5678

# 查找所有
emails = re.findall(r'\w+@\w+\.\w+', text)
print(emails)  # ['test@example.com']

# 替换
new_text = re.sub(r'\d{3}-\d{4}-\d{4}', '***-****-****', text)
print(new_text)  # 我的邮箱是 test@example.com，电话是 ***-****-****

# 分割
parts = re.split(r'[,，;；]', "a,b,c；d;e")
print(parts)  # ['a', 'b', 'c', 'd', 'e']
```

### 常用元字符

| 元字符 | 含义 | 示例 |
|--------|------|------|
| `\d` | 数字 | `\d{3}` = 3位数字 |
| `\w` | 字母、数字、下划线 | |
| `\s` | 空白字符 | |
| `.` | 任意字符（除换行） | |
| `^` | 字符串开头 | |
| `$` | 字符串结尾 | |
| `*` | 0次或多次 | |
| `+` | 1次或多次 | |
| `?` | 0次或1次 | |
| `{n,m}` | n到m次 | |

---

## 7. subprocess 模块 - 执行外部命令

在Python中运行系统命令和外部程序。

```python
import subprocess

# 运行命令并获取输出
result = subprocess.run(['ls', '-la'], capture_output=True, text=True)
print(result.stdout)  # 命令输出
print(result.stderr)  # 错误输出
print(result.returncode)  # 返回码（0表示成功）

# 执行并立即输出
subprocess.run(['echo', 'Hello'], check=True)

# 获取输出（管道）
proc = subprocess.Popen(['ping', '-c', '3', 'localhost'],
                        stdout=subprocess.PIPE,
                        text=True)
output, _ = proc.communicate()
print(output)

# 检查命令是否成功
try:
    subprocess.run(['ls', '/valid/path'], check=True, capture_output=True)
    print("命令执行成功")
except subprocess.CalledProcessError as e:
    print(f"命令失败: {e}")
```

---

## 8. sqlite3 模块 - SQLite数据库

轻量级嵌入式数据库，无需独立服务器。

```python
import sqlite3

# 连接数据库（不存在则创建）
conn = sqlite3.connect('test.db')
cursor = conn.cursor()

# 创建表
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age INTEGER
    )
''')

# 插入数据
cursor.execute('INSERT INTO users (name, age) VALUES (?, ?)', ('Alice', 30))
cursor.execute('INSERT INTO users (name, age) VALUES (:name, :age)', 
               {'name': 'Bob', 'age': 25})
conn.commit()  # 必须提交事务

# 查询数据
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()
for row in rows:
    print(row)  # (1, 'Alice', 30), (2, 'Bob', 25)

# 带参数的查询
cursor.execute('SELECT * FROM users WHERE age > ?', (20,))
results = cursor.fetchall()

# 更新和删除
cursor.execute('UPDATE users SET age = ? WHERE name = ?', (31, 'Alice'))
cursor.execute('DELETE FROM users WHERE name = ?', ('Bob',))
conn.commit()

# 关闭连接
conn.close()
```

---

## 9. pickle 模块 - 对象序列化

将Python对象转换为字节流（用于存储或传输）。

```python
import pickle

# 序列化对象
data = {'a': [1, 2, 3], 'b': {'x': 10, 'y': 20}}

with open('data.pkl', 'wb') as f:
    pickle.dump(data, f)

# 反序列化
with open('data.pkl', 'rb') as f:
    loaded = pickle.load(f)
print(loaded)  # {'a': [1, 2, 3], 'b': {'x': 10, 'y': 20}}

# 内存序列化
bytes_data = pickle.dumps(data)
restored = pickle.loads(bytes_data)

# 注意：pickle安全性，不加载来源不明的pickle文件
```

---

## 10. argparse 模块 - 命令行参数

创建命令行界面工具。

```python
import argparse

parser = argparse.ArgumentParser(
    description='文件处理工具',
    prog='file_tool'
)

# 位置参数
parser.add_argument('filename', help='输入文件名')

# 可选参数
parser.add_argument('-o', '--output', default='output.txt', help='输出文件名')
parser.add_argument('-n', '--number', type=int, default=10, help='处理数量')
parser.add_argument('-v', '--verbose', action='store_true', help='详细输出')
parser.add_argument('-m', '--mode', choices=['fast', 'slow'], default='fast')

args = parser.parse_args()

print(f"输入: {args.filename}")
print(f"输出: {args.output}")
print(f"数量: {args.number}")
print(f"详细: {args.verbose}")
print(f"模式: {args.mode}")
```

运行示例：
```bash
python file_tool.py input.txt -o result.txt -n 20 -v
```

---

## 11. logging 模块 - 日志记录

记录程序运行日志，用于调试和监控。

```python
import logging

# 基础配置
logging.basicConfig(
    level=logging.INFO,  # 日志级别
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S',
    handlers=[
        logging.FileHandler('app.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)

logger.debug("调试信息")   # 不会输出（低于INFO级别）
logger.info("一般信息")
logger.warning("警告信息")
logger.error("错误信息")
logger.critical("严重错误")

# 推荐写法
def process_data(data):
    try:
        result = int(data)
        logger.info(f"成功处理: {result}")
        return result
    except ValueError as e:
        logger.error(f"处理失败: {e}")
        raise
```

---

## 12. csv 模块 - CSV文件处理

读写CSV（逗号分隔值）格式文件。

```python
import csv

# 写入CSV
with open('users.csv', 'w', newline='', encoding='utf-8') as f:
    writer = csv.writer(f)
    writer.writerow(['ID', 'Name', 'Age'])  # 写入表头
    writer.writerows([
        [1, 'Alice', 30],
        [2, 'Bob', 25],
        [3, 'Charlie', 35]
    ])

# 读取CSV
with open('users.csv', 'r', encoding='utf-8') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# 使用字典读写
with open('users.csv', 'r', encoding='utf-8') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"{row['Name']} - {row['Age']}")

with open('new_users.csv', 'w', newline='', encoding='utf-8') as f:
    writer = csv.DictWriter(f, fieldnames=['Name', 'Age'])
    writer.writeheader()
    writer.writerow({'Name': 'David', 'Age': 28})
```

---

## 13. hashlib 模块 - 哈希算法

计算数据的哈希值，常用于数据完整性校验和密码存储。

```python
import hashlib

text = "Hello, World!"

# MD5（已不安全，仅用于兼容性）
md5 = hashlib.md5(text.encode()).hexdigest()
print(f"MD5: {md5}")

# SHA-256（推荐）
sha256 = hashlib.sha256(text.encode()).hexdigest()
print(f"SHA-256: {sha256}")

# SHA-1（已不安全）
sha1 = hashlib.sha1(text.encode()).hexdigest()

# SHA-512
sha512 = hashlib.sha512(text.encode()).hexdigest()

# 大文件哈希
with open('large_file.bin', 'rb') as f:
    sha256 = hashlib.sha256()
    for chunk in iter(lambda: f.read(4096), b''):
        sha256.update(chunk)
    print(f"文件SHA-256: {sha256.hexdigest()}")

# 密码哈希（使用加盐）
salt = b'random_salt'
password = "my_password"
hashed = hashlib.pbkdf2_hmac('sha256', password.encode(), salt, 100000)
print(f"加盐哈希: {hashed.hex()}")
```

---

## 14. pathlib 模块 - 面向对象路径操作（推荐）

现代Python推荐的路径操作方式。

```python
from pathlib import Path

# 创建路径对象
p = Path('/home/user/documents')
p = Path('.') / 'folder' / 'file.txt'  # 路径拼接

# 路径属性
print(p.parent)      # 父目录
print(p.name)        # 文件名
print(p.stem)        # 不带扩展名的文件名
print(p.suffix)      # 扩展名
print(p.exists())    # 是否存在
print(p.is_file())   # 是否为文件
print(p.is_dir())    # 是否为目录

# 目录操作
Path('new_folder').mkdir(parents=True, exist_ok=True)
Path('old_folder').rmdir()  # 空目录

# 遍历目录
for item in Path('.').iterdir():
    print(item.name)

# 文件操作
content = Path('file.txt').read_text(encoding='utf-8')
Path('file.txt').write_text('Hello', encoding='utf-8')

# 递归遍历
for py_file in Path('.').rglob('*.py'):
    print(py_file)
```

---

## 常用模块速查表

| 类别 | 模块 | 主要用途 |
|------|------|----------|
| 系统交互 | `os`, `sys`, `platform` | 文件操作、环境变量、系统信息 |
| 日期时间 | `datetime`, `time` | 日期计算、格式化、定时 |
| 数据序列化 | `json`, `pickle`, `csv` | 数据存储和交换 |
| 数据结构 | `collections` | defaultdict, Counter, deque |
| 文本处理 | `re`, `string` | 正则表达式、字符串工具 |
| 数学 | `math`, `random`, `statistics` | 数学运算、随机数 |
| 数据库 | `sqlite3` | SQLite数据库操作 |
| 命令行 | `argparse`, `subprocess` | 命令行参数、系统命令 |
| 日志 | `logging` | 程序日志记录 |
| 路径 | `pathlib` | 面向对象路径操作 |
| 哈希 | `hashlib` | 加密哈希计算 |

---

## 学习建议

1. **优先掌握高频模块**：`os`, `sys`, `datetime`, `json`,