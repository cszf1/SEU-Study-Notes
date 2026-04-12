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
