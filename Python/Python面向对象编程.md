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
