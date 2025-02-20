---
layout: page
permalink: /blogs/ProgLang/Clang++/index.html
title: C++与面向对象编程
---
## **C++与面向对象编程**

## 1. C++简介

### 1.1 C++是什么
C++是一种通用的编程语言，它支持过程式编程、面向对象编程和泛型编程。C++最初由Bjarne Stroustrup在贝尔实验室开发，作为C语言的扩展。C++的设计目标是提供比C语言更高级的功能，同时保持与C语言的兼容性。

### 1.2 C++的特点
C++具有以下特点：

1. **高性能**：C++是一种编译型语言，它提供了对硬件的低级访问，因此可以编写高性能的程序。

2. **灵活性**：C++是一种多范式的语言，它支持过程式编程、面向对象编程和泛型编程。这使得C++可以用于各种不同的编程任务。

3. **可移植性**：C++是一种跨平台的语言，它可以在不同的操作系统和硬件平台上运行。

4. **丰富的库**：C++标准库提供了许多有用的功能，如输入输出、字符串处理、数学计算等。

## 2. 面向对象编程
面向对象编程（Object-Oriented Programming，OOP）是一种编程范式，它将程序视为一组相互交互的对象。每个对象都有自己的状态和行为，并且可以与其他对象进行交互。

### 2.1 类和对象
在面向对象编程中，类（Class）是对象的蓝图或模板。它定义了对象的状态和行为。对象（Object）是类的实例，它具有类定义的状态和行为。

### 2.2 三大特性
面向对象编程有3大特性：封装、继承和多态。

1. **封装**：封装是将对象的状态和行为封装在一个类中，并对外隐藏。这可以通过访问修饰符（如public、private和protected）来实现。

2. **继承**：继承是面向对象编程中的一个重要概念。它允许一个类（子类）继承另一个类（父类）的属性和方法。子类可以重写父类的属性和方法，也可以添加自己的属性和方法。

3. **多态**：多态是面向对象编程中的另一个重要概念。它允许一个对象以不同的方式表现，具体取决于它的类型。多态可以通过继承和虚函数实现。

### 2.3 基本结构
面向对象编程的基本结构包括类定义、对象创建、成员函数和成员变量等。

```cpp
#include <iostream>

using namespace std;

class MyClass {
public:
    void myFunction(int Variable) {
        myVariable = Variable;
        cout << "Hello, World!"<< myVariable << endl;
    }

private:
    int myVariable;

};

int main() {
    MyClass myObject;
    myObject.myFunction(10);
    return 0;
}
```

### 2.4 构造函数和析构函数
构造函数是类的一个特殊成员函数，它在对象创建时自动调用。析构函数是类的一个特殊成员函数，它在对象销毁时自动调用。

```cpp
#include <iostream>

using namespace std;

class MyClass {
public:
    MyClass() {
        cout << "Object created" << endl;
    }

    ~MyClass() {
        cout << "Object destroyed" << endl;
    }

    void myFunction() {
        cout << "Hello, World!" << endl;
    }
}

int main() {
    MyClass myObject;
    myObject.myFunction();
    return 0;
}
```


### 2.5 封装
封装是将对象的属性和方法封装在一个类中，并对外隐藏。这可以通过访问修饰符（如public、private和protected）来实现。
```cpp
#include <iostream>

using namespace std;

class MyClass {
public:
    void myFunction(int Variable) {
        myVariable = Variable;
        cout << "Hello, World!"<< myVariable << endl;
    }

private:
    int myVariable;

};

int main() {
    MyClass myObject;
    myObject.myFunction(10);
    return 0;
}
```

上述代码中，myVariable是一个私有成员变量，只能在类内部访问。myFunction是一个公有成员函数，可以在类外部访问。通过封装，我们可以控制对对象的访问，并保护对象的内部状态。


### 2.6 继承

继承是面向对象编程的一个基本概念，它允许一个类（称为子类）继承另一个类（称为父类）的属性和方法。子类可以重写父类的成员函数，并添加自己的成员函数。

```cpp
#include <iostream>

using namespace std;

class ParentClass {
public:
    void myFunction() {
        cout << "Hello, World!" << endl;
    }
};

class ChildClass : public ParentClass {
public:
    void myFunction() {
        cout << "Hello, Child!" << endl;
    }
};

int main() {
    ChildClass myObject;
    myObject.myFunction();
    return 0;
}
```

上述代码中，ChildClass继承了ParentClass，并重写了myFunction函数。当创建ChildClass的对象并调用myFunction函数时，将输出"Hello, Child!"。

### 2.7 多态
多态是面向对象编程的一个基本概念，它允许一个对象在不同的情况下表现出不同的行为。多态可以通过虚函数和抽象类来实现。
```cpp
#include <iostream>

using namespace std;

class ParentClass {
public:
    virtual void myFunction() {
        cout << "Hello, World!" << endl;
    }
};

class ChildClass : public ParentClass {
public:
    void myFunction() override {
        cout << "Hello, Child!" << endl;
    }
};

int main() {
    ParentClass* myObject = new ChildClass();
    myObject->myFunction();
    delete myObject;

    ParentClass myObject2;
    myObject2.myFunction();
    
    return 0;
}
```

上述代码中，ParentClass中的myFunction函数被声明为虚函数，ChildClass重写了该函数。在main函数中，创建了一个指向ChildClass对象的ParentClass指针，并调用myFunction函数。由于myFunction函数是虚函数，因此将调用ChildClass中的重写函数，输出"Hello, Child!"。 第二次调用myFunction函数时，将调用ParentClass中的函数，输出"Hello, World!"。




## 3. C++的语法
C++是一种高级编程语言，它具有许多语法特性，如变量、数据类型、控制结构、函数等。

### 3.1 变量和数据类型
C++支持多种数据类型，如整数、浮点数、字符、字符串等。变量是用于存储数据的内存位置。
### 3.2 控制结构
C++提供了多种控制结构，如if语句、for循环、while循环等，用于控制程序的执行流程。

### 3.3 函数
函数是用于执行特定任务的代码块。C++函数可以接受参数并返回值。


## 4. 命名空间

命名空间是C++中用于组织代码的一种机制，它可以将代码组织成不同的模块，避免命名冲突。命名空间使用关键字namespace来定义。
```cpp
#include <iostream>

namespace MyNamespace {
    void myFunction() {
        std::cout << "Hello, World!" << std::endl;
    }
}

int main() {
    MyNamespace::myFunction();
    return 0;
}
```
上述代码中，定义了一个名为MyNamespace的命名空间，并在其中定义了一个名为myFunction的函数。在main函数中，通过MyNamespace::myFunction来调用该函数。





## 5. C++的标准库
C++标准库提供了一系列有用的功能，如输入输出、字符串处理、数学计算等。这些功能可以通过包含相应的头文件来使用。
例如，要使用输入输出功能，需要包含iostream头文件：
### 5.1 输入输出 iostream
```cpp
#include <iostream>

using namespace std;

int main() {
    int num;
    cout << "Enter a number: ";
    cin >> num;
    cout << "You entered: " << num << endl;
    return 0;
}
```
上述代码中，使用了iostream头文件中的cout和cin对象来执行输入输出操作。<br>


### 5.2 String类
C++标准库中的String类用于处理字符串。String类提供了一些方法，如length()、substr()、find()、replace()等，用于操作字符串中的数据。
```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string str = "Hello, World!";
    cout << "Length: " << str.length() << endl;
    cout << "Substring: " << str.substr(7, 5) << endl;
    cout << "Find: " << str.find("World") << endl;
    str.replace(7, 5, "C++");
    cout << "Replace: " << str << endl;
    return 0;
}
```
上述代码中，使用了string头文件中的String类来处理字符串。String类提供了一些方法，如length()、substr()、find()、replace()等，用于操作字符串中的数据。

### 5.3 SStream类
C++标准库中的StringStream类用于在内存中创建一个字符串流，可以用于输入输出操作。StringStream类提供了一些方法，如str()、clear()、operator<<()、operator>>()等，用于操作字符串流中的数据。
```cpp
#include <iostream>
#include <sstream>

using namespace std;

int main() {
    stringstream ss;
    ss << "Hello, World!";
    string str = ss.str();
    cout << str << endl;
    return 0;
}
```

### 5.4 fstream类
C++标准库中的fstream类用于处理文件输入输出操作。fstream类提供了一些方法，如open()、close()、read()、write()等，用于操作文件中的数据。
```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main() {
    ofstream outfile("test.txt");
    outfile << "Hello, World!" << endl;
    outfile.close();

    ifstream infile("test.txt");
    string line;
    while (getline(infile, line)) {
        cout << line << endl;
    }
    infile.close();
    return 0;
}
```
上述代码中，使用了fstream头文件中的fstream类来处理文件输入输出操作。fstream类提供了一些方法，如open()、close()、read()、write()等，用于操作文件中的数据。


### 6. C++标准库中的常用容器
C++标准库中提供了一些常用的容器，如vector、list、map、set等，用于存储和管理数据。这些容器提供了一些方法，如push_back()、insert()、erase()、find()等，用于操作容器中的数据。

### 6.1 vector类
C++标准库中的vector类是一个动态数组，可以存储任意类型的数据。vector类提供了一些方法，如push_back()、insert()、erase()、find()等，用于操作vector中的数据。
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> vec;
    vec.push_back(1);
    vec.push_back(2);
    vec.push_back(3);

    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
    cout << endl;

    vec.insert(vec.begin() + 1, 4);
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
    cout << endl;

    vec.erase(vec.begin() + 2);
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
    cout << endl;

    vec.fill(5);
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
    cout << endl;

    return 0;
}

\\\输出结果：123 1234 134 555
```

上述代码中，使用了vector类来存储整数数据，并使用push_back()、insert()、erase()等方法来操作vector中的数据。

### 6.2 list类
C++标准库中的list类是一个双向链表，可以存储任意类型的数据。list类提供了一些方法，如push_back()、insert()、erase()、find()等，用于操作list中的数据。
```cpp
#include <iostream>
#include <list>

using namespace std;

int main() {
    list<int> lst;
    lst.push_back(1);
    lst.push_back(2);
    lst.push_back(3);

    for (list<int>::iterator it = lst.begin(); it != lst.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    lst.insert(lst.begin() + 1, 4);
    for (list<int>::iterator it = lst.begin(); it != lst.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    lst.erase(lst.begin() + 2);
    for (list<int>::iterator it = lst.begin(); it != lst.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
    }
\\\输出结果：1 2 3
1 4 2 3
1 4 3
```
上述代码中，使用了list类来存储整数数据，并使用push_back()、insert()、erase()等方法来操作list中的数据。

### 6.3 map类
C++标准库中的map类是一个关联容器，用于存储键值对。map类提供了一些方法，如insert()、erase()、find()等，用于操作map中的数据。
```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<int, string> m;
    m.insert(pair<int, string>(1, "one"));
    m.insert(pair<int, string>(2, "two"));
    m.insert(pair<int, string>(3, "three"));

    for (map<int, string>::iterator it = m.begin(); it != m.end(); ++it) {
        cout << it->first << " " << it->second << endl;
    }

    m.erase(2);
    for (map<int, string>::iterator it = m.begin(); it != m.end(); ++it) {
        cout << it->first << " " << it->second << endl;
    }

    return 0;
    }
\\\输出结果：1 one 2 two 3 three
1 one 3 three
```
上述代码中，使用了map类来存储整数和字符串的键值对，并使用insert()、erase()等方法来操作map中的数据。

### 6.4 set类
C++标准库中的set类是一个关联容器，用于存储唯一的元素。set类提供了一些方法，如insert()、erase()、find()等，用于操作set中的数据。
```cpp
#include <iostream>
#include <set>

using namespace std;

int main() {
    set<int> s;
    s.insert(1);
    s.insert(2);
    s.insert(3);

    for (set<int>::iterator it = s.begin(); it != s.end(); ++it) {
        cout << *it << endl;
    }

    s.erase(2);
    for (set<int>::iterator it = s.begin(); it != s.end(); ++it) {
        cout << *it << endl;
    }

    return 0;
}
\\\输出结果：1 2 3
1 3
```
上述代码中，使用了set类来存储整数，并使用insert()、erase()等方法来操作set中的数据。

### 6.5 迭代器
C++标准库中的迭代器是一种泛型指针，用于遍历容器中的元素。迭代器提供了访问容器中元素的能力，并且可以用于修改容器中的元素。
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    for (vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
        cout << *it << endl;
    }

    return 0;
}
\\\输出结果：1 2 3 4 5
```
上述代码中，使用了vector类来存储整数，并使用迭代器来遍历vector中的元素。


## 7. 模板
### 7.1 函数模板
C++标准库中的函数模板是一种泛型函数，用于处理不同类型的数据。函数模板使用模板参数来表示数据类型，并可以在函数定义中使用这些参数。
```cpp
#include <iostream>

using namespace std;

template <typename T>
T max(T a, T b) {
    return a > b ? a : b;
}

int main() {
    cout << max(1, 2) << endl; // 输出 2
    cout << max(3.14, 2.71) << endl; // 输出 3.14
    cout << max("apple", "banana") << endl; // 输出 banana

    return 0;
}
```
### 7.2 类模板
C++标准库中的类模板是一种泛型类，用于处理不同类型的数据。类模板使用模板参数来表示数据类型，并可以在类定义中使用这些参数。
```cpp
#include <iostream>

using namespace std;

template <typename T>
class Stack {
public:
    void push(T value);
    T pop();
private:
    vector<T> data;
};

template <typename T>
void Stack<T>::push(T value) {
    data.push_back(value);
}

template <typename T>
T Stack<T>::pop() {
    T value = data.back();
    data.pop_back();
    return value;
}

int main() {
    Stack<int> intStack;
    intStack.push(1);
    intStack.push(2);
    intStack.push(3);

    cout << intStack.pop() << endl; // 输出 3
    cout << intStack.pop() << endl; // 输出 2
    cout << intStack.pop() << endl; // 输出 1

    Stack<string> stringStack;
    stringStack.push("hello");
    stringStack.push("world");

    cout << stringStack.pop() << endl; // 输出 world
    cout << stringStack.pop() << endl; // 输出 hello

    return 0;
}
```
