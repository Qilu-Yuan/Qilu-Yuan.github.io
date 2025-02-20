---
layout: page
permalink: /blogs/ProgLang/Clang/index.html
title: C语言基本语法暨学习笔记
---

## **C语言基本语法**

## 0. CLion配置
下载CLion: [Other Versions - CLion (jetbrains.com)](https://www.jetbrains.com/clion/download/)

下载mingw-w64: [Releases · niXman/mingw-builds-binaries · GitHub](https://github.com/niXman/mingw-builds-binaries/releases)

## 1. 数据基本类型
### 1.1 变量的定义

变量类型 变量名;

1.不能是c语言标识符

2.首字母只能是字母或下划线，组成为数字、字母、下划线

3.区分大小写


### 1.2 变量类型
```c
int a = 1; //整型变量
printf("%d\n", a);

long long b = 100ll; //长整型
printf("%lld\n", b);

//浮点型
float c = 1.0;
printf("the float is %.1f\n", c);
double c0 = 1000.0;
printf("the float is %.1lf\n", c0);

//字符型：单引号是字符型，双引号是字符串型
char ccc1[] = "h";
char c2[7] = "nihao\n";
printf("%s\n%s", ccc1, c2);

//布尔型
bool boolen = true;
cout << boolen << endl;
```
### 1.3 强制类型转换
```c
double a = 10.01;
printf("%lf\n", a);
int b = (int)a;
printf("%d,%d", (int)a, b);
```
### 1.4 符号常量与const常量
```c
#define pi 3.14
const double pi = 3.14;
```
### 1.5 运算符
1.算数运算符<br>
加（+）减（-）乘（*）除（/）<br>
取模（余数）%<br>
自增++<br>
自减--<br>

2.关系运算符<br>
<, >, ≤, ≥, ==, ≠<br>
3.逻辑运算符
&&, ||, !（与，或，非）<br>
4.条件运算符<br>
```c
max = a > b ? a : b;

if (a > b) {
    max = a;
} else {
    max = b;
}
```

## 2. scanf/printf输入和输出 , 顺序结构
### 2.1赋值表达式
```c
int a = 5;
a = 10;
```
### 2.2 scanf/printf和cin/cout
```c
int a;
printf("Please input the value of a:");
scanf("%d", &a);
printf("2*a = %d", 2 * a);

int b;
cin >> b;
cout << "a*b=" << a * b << endl;
```
### 2.3 getchar/putchar输入和输出
```c
char c1, c2, c3;
c1 = getchar();
getchar();
c2 = getchar();
c3 = getchar();
c1 = 'a';
putchar(c1);
putchar(c2);
putchar(c3);
```
### 2.4 注释
单行注释<br>
```c
// 单行注释
```
多行注释<br>
```c
/*
多行注释
*/
```
### 2.5 typedef
```c
typedef char* PCHAR;
PCHAR pa, pb; //char *pa; char *pb;
pa = "hello";
pb = "hello"; //正常
pb = 'h'; //报错，不能将char类型的值赋给PCHAR类型实体
return 0;
```

```c
#include <iostream>
using namespace std;
typedef int (*A)(char, char);
int fun0(char a, char b);
int fun1(char a, char b);
int main() {
    A a;
    a = fun0;
    a('a', 'b');
    a = fun1;
    a('a', 'b');
    return 0;
}
int fun0(char a, char b) {
    cout << "fun0" << endl;
    return 0;
}
int fun1(char a, char b) {
    cout << "fun1" << endl;
    return 0;
}
```

### 2.6常用math函数

fabs() 绝对值；<br>

floor()向下取整；cell()向上取整<br>

pow(a,b) a的b次方<br>

sqrt()算数平方根<br>

log()自然对数为底对数<br>

sin(); cos(); tan(); asin(); acos(); atan()<br>

round()四舍五入<br>

## 3. 选择结构
### 3.1 if语句
```c
if (a > 1) {
    
} else {
    
}
```
### 3.2 if 语句的嵌套
```c
if () {
    //...
    if () {
        //...
    } else {
        //...
    }
    //...
}
```
### 3.3 switch语句
```c
switch () {
    case :
        ...
        break;
    case :
        ...
        break;
    default:
        ...
}
```

## 4. 循环结构
### 4.1 while循环
```c
while () {
    ....
}
```
### 4.2 do…while循环
```c
do {
    ...
} while ();
```
### 4.3 for循环
```c
for (表达式A; 表达式B; 表达式C) {
    
}
```
执行顺序：执行A—>判定B—>成立则执行内部语句—>执行C—>判定B—>不成立退出，成立则继续执行内部语句

### 4.4 break和continue语句

break: 退出整个当前循环<br>

continue: 退出本次循环，直接进入下一次循环<br>
## 5. 数组
### 5.1一维数组
```c
int a[10]; //定义数组
a[5]; //访问数组
```
### 5.2 冒泡排序

通过交换，最大值（最小值）移动到数组的一端<br>
```c
int a[5] = {3, 1, 5, 2, 4};

for (int i = 1; i <= 4; i++) {
    for (int j = 0; j < 5 - i; j++) {
        if (a[j] > a[j + 1]) { //最大值往后移动
            int temp = a[j];
            a[j] = a[j + 1];
            a[j + 1] = temp;
        }
    }
}
```
### 5.3二维数组
```c
int a[5][6];
double db[10][10];
```
### 5.4 memset——对数组中每一个元素赋予相同的值
```c
int a[10]; 
memset(a, 0, sizeof(a));
```
### 5.5 字符数组
初始化<br>
```c

char str[15] = {'G', 'o', 'o', 't', 'o', 'r', 'y', '!'};
```
输入输出<br>
```c
char str[15];
scanf("%s", &str);
printf("%s", str);

gets(str);
puts(str);
```
3.字符数组存放方式

字符数组的每一位都是一个char字符。一维字符数组的末尾都有一个空字符\0
### 5.6 string.h类处理字符数组
```c
strlen(); //字符数组长度
strcmp(a, b); //字符串大小比较
strcpy(a, b); //将b赋予给a
strcat(a, b); //a接到b之后
```

### 5.7 sscanf和sprintf
```c
char buff[10] = {0}; //声明字符串
int a = 13; //任意变量
int b = 26;
char str[] = "sc";
sprintf(buff, "%d%d%s", a, b, str); //将a变量按照格式写入buff中
printf("%s", buff);    
```
<br>

```c  
char buff[20] = {0}; //用于承接Todayis
char buff2[20] = {0}; //用于承接2015-02-27
char buff3[20] = {0}; //用于承接12:22:30
char strbuf[] = "Todayis 2015-02-27 12:22:30";
sscanf(strbuf, "%s %s %s", buff, buff2, buff3); //注意"%s %s %s"间隔%s有空格
printf("buff:%s\r\n", buff);
printf("buff2:%s\r\n", buff2);
printf("buff3:%s\r\n", buff3);
```

## 6. 函数
### 6.1 函数的定义
```c
/*
返回类型 函数名称(参数类型 参数) {
    函数主体
}
*/
int func(int a) {
    int b;
    b = a;
    return b;
}
```
### 6.2 main函数

一个程序只有一个主函数，并且无论主函数在哪个位置，整个程序都是从主函数的第一句开始执行。

### 6.3 数组作为函数的参数

数组作为参数时，参数中数组第一维不需要填写长度。函数中对数组元素的修改等同于对原数组的修改。

### 6.4 函数的嵌套调用

即在一个函数中调用另一个函数，与普通调用几乎没区别

### 6.5 函数的递归调用

一个函数调用其自身

### 6.6 函数的内部的static变量

普通变量在函数调用完成后被释放，如果需要某个变量在整个程序的运行过程中不被释放加入static关键字
## 7. 指针
### 7.1 指针的基本用法

1 指针的概念<br>

内存地址：内存中每个字节单位都有一个编号<br>

指针：指针就是内存地址<br>

指针变量：用于存放地址的变量<br>

2格式<br>
```c
int a = 5;
int* p = &a; //指针变量的定义并赋予a的地址。
int* p2;
```
3 指针操作符<br>
```c
// & 取地址操作符
// * 取值操作符
```
4 指针变量的初始化和赋值<br>
```c
//将普通变量的地址赋值给指针p
int a = 10;
int* p = &a;
//将数组的首地址赋值给指针q
int arr[] = {1, 2, 3, 4, 5};
int* q = arr;
//将指针变量p保存的地址赋值给另一个变量
int* r = p;
```
### 7.2指针运算

1 算术运算（+，-）<br>

对指针的操作即让指针向前向后移动<br>
```c
char str[32] = "HelloWorld";
char* p = str; //H
p++; //e
p--; //H
```
2 关系运算 > ≥ < ≤ == ≠<br>

指针之间的关系运算比较的是它指向地址的高低<br>

指向高地址的指针是大于指向低地址的指针<br>
### 7.3其他

1 指针大小和段错误<br>

1.1 指针的大小<br>
```c
int* p;
sizeof(p);
```
1.2 使用指针时的段错误

(1) 野指针

(2) 内存泄露

2 指针修饰

const 常量化

(1) 修饰普通变量
```c
const int a = 10;
int const b = 20;
int *p = &a, *q = &b;
//此时a和b只读，不可以修改。但是可以通过指针修改。
*p = 1;
*q = 2;
```
(2) 修饰指针指向的内容
```c
const int *p;
int const *q;
//指向的内容不能改变，但指向可以改变，即*p不能改变
int a = 10;
int b = 20;
p = &a;
q = &b;
```
(3) 修饰指针指向
```c
int a = 100;
//指针指向不能更改，指向的内容可以更改
int *const p = &a;
```

## 8. 结构体
### 8.1 结构体的定义
```c
struct Stu {
    char name[10];
    int age;
    double height;
} yuanql = {"yuanql1", 20, 1.77}; //定义时赋值
strcpy(yuanql.name, "yuanql");
yuanql.age = 22;
yuanql.height = 1.75;
```
### 8.2 访问结构体元素

“.”操作和“- >”操作

### 8.3 结构体初始化

1.先定义再赋值<br>

2.构造函数<br>
```c
struct Stu {
    char gender;
    int age;
    double height;
    Stu() {}; //默认生成的构造函数
    //自定义的构造函数
    Stu(char _gender, int _age, double _height) : gender(_gender), age(_age), height(_height) {}
};

int main() {
    Stu xiaoming('M', 15, 1.75); //定义时赋值
    //先定义再赋值
    xiaoming.gender = 'M';
    xiaoming.age = 12;
    xiaoming.height = 1.75;
    //构造函数
    xiaoming = Stu('M', 22, 1.75);
    printf("%c,%d,%.2lf", xiaoming.gender, xiaoming.age, xiaoming.height);
    // cout << xiaoming.name << " " << xiaoming.age << " " << xiaoming.height << endl;
}
```

## 9. 补充
### 9.1复杂度

时间复杂度<br>

即算法需要执行基本运算的次数所处的等级，其中基本运算就是类似加减乘除这种计算机直接实现的运算。时间复杂度是评判算法时间效率的有效标准。在时间复杂度中，高等级幂次会覆盖低等级幂次。<br>

空间复杂度<br>

与时间复杂度类似，空间复杂度表示算法需要消耗的最大数据空间。<br>

编码复杂度<br>

编码复杂度是一个定性的概念，并没有什么量化的标准。对于一个问题来说，如果使用了冗长的算法思想，那么代码量会非常巨大，其编码复杂度会非常大。<br>
## 10. 黑盒测试
### 10.1 单点测试

对单点测试来说，系统会判断每组数据的输出结果是否正确。如果输出正确，那么对该组数据来说就通过了测试，并获得了这组数据的分值。在这种情况下，题目的总得分等于通过的数据的分值之和。PAT就是采用了单点测试，并且对每组数据都会给出相应的测评结果。l

### 10.2 多点测试

多点测试要求程序能一次运行所有数据，所有数据完全正确才算通过
(1)while...EOF型<br>

C语言中使用EOF（即End Of File）来代表-1<br>
```c
while (scanf("%d", &n) != EOF) {
    .....
}
```
(2)while....break型<br>

这种类型是while.… EOF 型的延伸，题目要求当输入的数据满足某个条件时停止输入。这种类型是while.… EOF 型的延伸，题目要求当输入的数据满足某个条件时停止输入。<br>

(3)while(T--)型<br>

在这种类型中，题目会给出测试数据的组数，然后才给出相应数量组数的输入数据。<br>
```c
#include <stdio.h>
int main() {
    int T, a, b;
    scanf("%d", &T);
    while (T--) {
        scanf("%d%d", &a, &b);
        printf("%d\n", a + b);
    }
    return 0;
}
```
以上就是多点测试的三种输入类型。下面讲解三种常见的输出类型。<br>

(1）正常输出<br>

这种输出类型要求需要每两组输出数据中间没有额外的空行,即输出数据是连续的多行。<br>

(2）每组数据输出之后都额外加一个空行<br>

这个要求非常容易实现，只需要在每组输出结束之后额外输出一个换行符n即可。<br>

(3)两组输出数据之间有一个空行,最后一组数据后面没有空行<br>

这一般是在第三种输入类型 while(T--)的情况下，只需要通过判断T是否已经减小到0来判断是否应当输出额外的换行。<br>

最后需要指出，在多点测试中，每一次循环都要重置一下变量和数组，否则在下一组数据来临的时候变量和数组的状态就不是初始状态了，而重置数组一般使用memset函数或f函数。<br>

