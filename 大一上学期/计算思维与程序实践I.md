# 计算思维与程序实践 I（C++）

> 大一上学期 | 东南大学吴健雄学院 | 电子信息类

---

## 目录

1. [C++ 基础语法](#1-c-基础语法)
2. [控制结构](#2-控制结构)
3. [函数](#3-函数)
4. [数组与指针](#4-数组与指针)
5. [结构体与字符串](#5-结构体与字符串)
6. [文件操作](#6-文件操作)

---

## 1. C++ 基础语法

### 1.1 程序结构

```cpp
#include <iostream>      // 头文件包含
using namespace std;     // 使用标准命名空间

// 主函数
int main() {
    // 语句
    cout << "Hello, World!" << endl;
    return 0;
}
```

### 1.2 数据类型

| 类型 | 关键字 | 大小（典型） | 范围 |
|------|--------|-------------|------|
| 整型 | `int` | 4字节 | -2³¹ ~ 2³¹-1 |
| 短整型 | `short` | 2字节 | -32768 ~ 32767 |
| 长整型 | `long` | 4或8字节 | |
| 字符型 | `char` | 1字节 | -128 ~ 127 |
| 布尔型 | `bool` | 1字节 | true/false |
| 单精度 | `float` | 4字节 | 6位有效数字 |
| 双精度 | `double` | 8字节 | 15位有效数字 |

#### 常量定义
```cpp
const int MAX = 100;        // const 常量
#define PI 3.14159          // 宏定义
enum { RED, GREEN, BLUE };  // 枚举
```

### 1.3 变量与输入输出

#### 变量声明
```cpp
int a = 10;
double x = 3.14;
char c = 'A';
bool flag = true;
```

#### cin / cout
```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cin >> a >> b;                    // 输入
    cout << "a + b = " << a + b << endl;  // 输出
    
    // 格式化输出
    cout << fixed << setprecision(2) << 3.14159 << endl;  // 3.14
    return 0;
}
```

### 1.4 运算符

#### 算术运算符
`+ - * / %`

> **注意**：`/` 整数除法取整，`%` 取余要求操作数为整数

#### 关系运算符
`== != > < >= <=`

#### 逻辑运算符
`&& || !`

#### 赋值运算符
`= += -= *= /= %=`

#### 自增自减
`++a`（先增后用） vs `a++`（先用后增）

### 1.5 表达式与类型转换

```cpp
// 隐式转换：低精度向高精度转换
int i = 10;
double d = 3.14;
double result = i + d;  // i 转为 double

// 显式转换（强制类型转换）
int n = 5, m = 2;
double r = (double)n / m;  // 2.5，而不是 2
```

---

## 2. 控制结构

### 2.1 条件语句

#### if-else
```cpp
if (condition1) {
    // 语句块1
} else if (condition2) {
    // 语句块2
} else {
    // 语句块3
}
```

#### switch
```cpp
switch (expression) {
    case value1:
        // 语句
        break;
    case value2:
        // 语句
        break;
    default:
        // 语句
}
```

### 2.2 循环语句

#### while 循环
```cpp
int i = 1;
while (i <= 10) {
    cout << i << " ";
    i++;
}
```

#### do-while 循环
```cpp
int n;
do {
    cin >> n;
} while (n <= 0);  // 至少执行一次
```

#### for 循环
```cpp
// 基本形式
for (int i = 0; i < n; i++) {
    cout << i << endl;
}

// 典型用法
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        // 嵌套循环
    }
}
```

#### 范围for循环（C++11）
```cpp
int arr[] = {1, 2, 3, 4, 5};
for (int x : arr) {
    cout << x << " ";
}
```

### 2.3 跳转语句

| 语句 | 作用 |
|------|------|
| `break` | 跳出当前循环或switch |
| `continue` | 跳过本次循环，进入下一次 |
| `return` | 退出函数 |
| `goto` | 跳转到标号（不推荐） |

---

## 3. 函数

### 3.1 函数定义

```cpp
// 返回类型 函数名(参数列表)
// {
//     函数体
// }

int add(int a, int b) {
    return a + b;
}

// 无返回值
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}
```

### 3.2 函数原型（声明）

```cpp
// 先声明
int max(int a, int b);
int min(int a, int b);

// 后定义
int max(int a, int b) {
    return (a > b) ? a : b;
}
```

### 3.3 参数传递

#### 值传递
```cpp
void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}  // 无法交换原变量！
```

#### 引用传递
```cpp
void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}  // 可以交换原变量
```

#### 指针传递
```cpp
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// 调用
swap(&x, &y);
```

#### 数组传递
```cpp
// 数组名作为指针传递
void sort(int arr[], int n);
void print(int *arr, int n);
```

### 3.4 默认参数

```cpp
int power(int base, int exp = 2) {
    int result = 1;
    for (int i = 0; i < exp; i++) {
        result *= base;
    }
    return result;
}

power(3);    // 9 (exp=2)
power(3, 3); // 27 (exp=3)
```

### 3.5 函数重载

```cpp
// 同名函数，不同参数
int max(int a, int b) {
    return (a > b) ? a : b;
}

double max(double a, double b) {
    return (a > b) ? a : b;
}

int max(int a, int b, int c) {
    return max(max(a, b), c);
}
```

### 3.6 递归函数

```cpp
// 阶乘
long long factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

// 斐波那契数列
long long fibonacci(int n) {
    if (n <= 2) return 1;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// 汉诺塔
void hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        cout << from << " -> " << to << endl;
        return;
    }
    hanoi(n - 1, from, aux, to);
    cout << from << " -> " << to << endl;
    hanoi(n - 1, aux, to, from);
}
```

### 3.7 变量作用域

| 类型 | 作用域 | 生命周期 |
|------|--------|---------|
| 局部变量 | 函数内 | 函数结束 |
| 全局变量 | 文件内 | 程序结束 |
| `static` 局部变量 | 函数内 | 程序结束 |
| `static` 全局变量 | 文件内 | 程序结束 |

```cpp
int global = 10;  // 全局变量

void func() {
    int local = 5;           // 局部变量
    static int staticLocal = 0;  // 静态局部变量，保留值
    global++;
    staticLocal++;
}
```

---

## 4. 数组与指针

### 4.1 一维数组

#### 定义与初始化
```cpp
int a[10];           // 未初始化
int b[5] = {1, 2, 3}; // b[0]=1, b[1]=2, b[2]=3, b[3]=0, b[4]=0
int c[] = {1, 2, 3, 4, 5};  // 自动确定大小
```

#### 数组作为函数参数
```cpp
// 三种等价写法
void func(int arr[], int n);
void func(int *arr, int n);
void func(int arr[10], int n);
```

### 4.2 二维数组

```cpp
int matrix[3][4];           // 3行4列
int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};

// 矩阵遍历
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 4; j++) {
        cout << matrix[i][j] << " ";
    }
    cout << endl;
}

// 传参
void printMatrix(int m, int n, int matrix[][10]);
```

### 4.3 指针基础

```cpp
int n = 10;
int *p = &n;      // p 指向 n 的地址

cout << p << endl;    // 地址
cout << *p << endl;   // 值：10

// 指针运算
p++;      // 指向下一个 int
*p = 20;  // 修改 n 的值
```

### 4.4 指针与数组

```cpp
int arr[] = {1, 2, 3, 4, 5};
int *p = arr;  // 等价于 int *p = &arr[0];

// 等价关系
arr[i] == *(arr + i) == *(p + i) == p[i]
&arr[i] == arr + i == p + i

// 遍历方式
for (int i = 0; i < 5; i++) {
    cout << *(p + i) << endl;
}
```

### 4.5 指针与函数

```cpp
// 返回指针
int* findMax(int *arr, int n) {
    int *pmax = arr;
    for (int i = 1; i < n; i++) {
        if (*(arr + i) > *pmax) {
            pmax = arr + i;
        }
    }
    return pmax;
}

// 指向函数的指针
int (*funcPtr)(int, int) = max;
int result = funcPtr(3, 5);  // 5
```

### 4.6 动态内存分配

```cpp
#include <cstdlib>

// 分配
int *p = (int*)malloc(sizeof(int) * n);  // C
int *p = new int[n];                      // C++

// 释放
free(p);    // C
delete[] p; // C++
// delete p; // 释放单个对象
```

```cpp
// 动态二维数组
int** createMatrix(int rows, int cols) {
    int **matrix = new int*[rows];
    for (int i = 0; i < rows; i++) {
        matrix[i] = new int[cols];
    }
    return matrix;
}

void deleteMatrix(int **matrix, int rows) {
    for (int i = 0; i < rows; i++) {
        delete[] matrix[i];
    }
    delete[] matrix;
}
```

### 4.7 const 与指针

```cpp
const int n = 10;
const int *p1 = &n;    // 不能通过 p1 修改 n
int const *p2 = &n;    // 同上
int *const p3 = &n;    // p3 指向固定地址
const int *const p4 = &n;  // 都不能改
```

---

## 5. 结构体与字符串

### 5.1 结构体

#### 定义
```cpp
struct Student {
    string name;
    int age;
    int score;
};  // 注意分号！

// 或者 typedef
typedef struct {
    int x;
    int y;
} Point;
```

#### 使用
```cpp
Student s1;              // 定义
s1.name = "张三";
s1.age = 18;
s1.score = 95;

Student s2 = {"李四", 19, 88};  // 初始化

// 结构体数组
Student class[30];

// 结构体指针
Student *p = &s1;
p->name = "王五";  // 等价于 (*p).name
```

#### 结构体与函数
```cpp
void printStudent(Student s) {
    cout << s.name << " " << s.age << " " << s.score << endl;
}

void modifyStudent(Student &s) {
    s.score = 100;
}

// 结构体指针作为参数
void modifyByPointer(Student *p) {
    p->score = 100;
}
```

### 5.2 字符串

#### C风格字符串
```cpp
char str1[] = "Hello";      // 自动加 '\0'
char str2[10] = "Hello";
char str3[10] = {'H', 'e', 'l', 'l', 'o', '\0'};

// 常用函数
#include <cstring>
strlen(str1);     // 长度（不含\0）
strcpy(str1, str2);  // 复制
strcat(str1, str2);  // 连接
strcmp(str1, str2);  // 比较：0相等，>0 str1>str2，<0 str1<str2
```

#### C++ string类
```cpp
#include <string>

string s1 = "Hello";
string s2 = "World";

// 操作
s1 + s2;           // 连接
s1.length();       // 长度
s1.substr(0, 3);    // 子串
s1.find("ll");     // 查找
s1[0];             // 访问字符
s1 == s2;          // 比较
```

### 5.3 常用库函数

#### 数学函数
```cpp
#include <cmath>
abs(x);          // 绝对值
fabs(x);         // 浮点数绝对值
sqrt(x);         // 平方根
pow(x, n);       // 幂
sin(x), cos(x), tan(x);  // 三角函数
log(x), exp(x);  // 对数和指数
ceil(x), floor(x);  // 向上/下取整
```

#### 随机数
```cpp
#include <cstdlib>
#include <ctime>

srand(time(0));  // 初始化随机种子
rand();          // 0~RAND_MAX 之间的整数
rand() % 100;    // 0~99
rand() % 100 + 1; // 1~100

// 生成 [a, b] 区间随机数
int random = a + rand() % (b - a + 1);
```

---

## 6. 文件操作

### 6.1 文件读写

#### 使用 ifstream / ofstream
```cpp
#include <fstream>

// 写入文件
ofstream outFile("output.txt");
if (outFile.is_open()) {
    outFile << "Hello, File!" << endl;
    outFile << 123 << " " << 456.78 << endl;
    outFile.close();
}

// 读取文件
ifstream inFile("input.txt");
if (inFile.is_open()) {
    string line;
    while (getline(inFile, line)) {
        cout << line << endl;
    }
    inFile.close();
}
```

#### 检查文件是否打开成功
```cpp
ofstream outFile("test.txt");
if (!outFile) {
    cerr << "无法打开文件" << endl;
    return 1;
}
```

### 6.2 文本与二进制文件

```cpp
// 文本模式（默认）
ifstream infile("data.txt");
ofstream outfile("result.txt");

// 二进制模式
ifstream infile("data.bin", ios::binary);
ofstream outfile("result.bin", ios::binary);

// 二进制读写
int data[] = {1, 2, 3, 4, 5};
outfile.write(reinterpret_cast<char*>(data), sizeof(data));
infile.read(reinterpret_cast<char*>(data), sizeof(data));
```

### 6.3 文件定位

```cpp
#include <fstream>

fstream file("data.txt");

// 定位到开头
file.seekg(0);

// 定位到末尾
file.seekg(0, ios::end);

// 从开头偏移10字节
file.seekg(10, ios::beg);

// 获取当前位置
streampos pos = file.tellg();
```

---

## 算法示例

### 排序算法

#### 冒泡排序
```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}
```

#### 选择排序
```cpp
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        swap(arr[i], arr[minIdx]);
    }
}
```

#### 插入排序
```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### 查找算法

#### 顺序查找
```cpp
int sequentialSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

#### 二分查找（要求数组有序）
```cpp
int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
```

### 常见数学问题

#### 最大公约数（欧几里得算法）
```cpp
int gcd(int a, int b) {
    return b == 0 ? a : gcd(b, a % b);
}

int lcm(int a, int b) {
    return a / gcd(a, b) * b;
}
```

#### 素数判定
```cpp
bool isPrime(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n % 2 == 0 || n % 3 == 0) return false;
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }
    return true;
}
```

#### 求素数（埃拉托斯特尼筛法）
```cpp
void sieveOfEratosthenes(int n) {
    vector<bool> isPrime(n + 1, true);
    isPrime[0] = isPrime[1] = false;
    
    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
    }
    
    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) cout << i << " ";
    }
}
```

---

## 易错点提示

> ⚠️ **语法基础**
> - C++ 语句以分号结束，不要遗漏
> - 大括号 `{}` 必须配对使用
> - 变量名区分大小写：`Max` 和 `max` 是不同变量

> ⚠️ **输入输出**
> - `cin >>` 会跳过空格和换行
> - `getline()` 可以读取包含空格的字符串
> - 使用 `endl` 刷新缓冲区，或使用 `\n`

> ⚠️ **数组**
> - 数组下标从 0 开始，到 n-1 结束
> - 数组作为参数传递时，退化为指针
> - 数组大小必须是常量或常量表达式

> ⚠️ **指针**
> - 使用指针前必须初始化
> - `NULL` 指针不指向任何对象
> - `delete` 和 `delete[]` 不要混淆
> - 野指针（未初始化或已释放的指针）很危险

> ⚠️ **函数**
> - 函数要先声明后使用
> - return 语句类型要与函数返回类型匹配
> - 递归要有终止条件，避免无限递归导致栈溢出

> ⚠️ **字符串**
> - C风格字符串以 `\0` 结尾
> - 比较字符串用 `strcmp()`，不要用 `==`
> - string 可以直接用 `==` 比较

> ⚠️ **文件操作**
> - 操作文件前检查是否成功打开
> - 读写完毕记得关闭文件
> - 路径使用双斜杠或反斜杠转义

---

## 附录：C++ 代码模板

### 完整程序模板
```cpp
#include <bits/stdc++.h>  // 包含所有标准库（部分编译器支持）
using namespace std;

int main() {
    // 代码
    
    return 0;
}
```

### 输入输出优化
```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
// 之后使用 cin/cout 更快
```

### 常用头文件
```cpp
#include <iostream>      // 输入输出
#include <vector>        // 动态数组
#include <string>        // 字符串
#include <algorithm>     // 常用算法
#include <cmath>         // 数学函数
#include <cstdlib>       // 标准库
#include <ctime>         // 时间
#include <fstream>       // 文件操作
```

---

**整理时间**：大一上学期末  
**适用教材**：《C++程序设计》或《程序设计基础》  
**重要程度**：⭐⭐⭐⭐⭐
