# README

**《More C++ idioms》**翻译

---

**译者的话：**

很喜欢这本书，但是没有中文版。便有了翻译这本书的想法，时间，水平有限，有任何疏漏，欢迎大家 pull request : )

你可以在[这里](https://en.wikibooks.org/wiki/More_C%2B%2B_Idioms)免费下载到这本书的PDF。

---

**目录**

1. 不使用 operator & 取地址
2. 

---

#### **1 取址器**

##### 1.0.1 目的

在不使用取地址运算符的情况下，取得对象的地址。

##### 1.0.1 别名

##### 1.0.3 动机

C++允许重载取地址运算符，取地址运算符的返回类型却不一定是对象的实际地址。重载取地址运算符的做法是非常有争议的，

但语言无疑允许这样做。取址器是不使用取地址运算符获得对象实际地址的一种方法。

在下面的例子中，由于取地址运算符是类私有的，main 函数会编译失败。即使没有私有的访问控制，返回类型double也不能够自动转成指针类型。

~~~
class nonaddressable{
public:
    typedef double useless_type;
private:
    useless_type operator&() const;
};

int main(){

    noaddressable na;
    noaddressable * naptr = &na;    // Compiler error here.
}

~~~
##### 1.0.4 解决方案和示例代码

取址器用类型转换获得一个对象的地址。

~~~
template <class T>
T * addressof(T& v){

    return reinterpret_cast<T*>(& const_cast<char&>(reinterpret_cast<const volatile char&>(v)));
}

int main(){

    noaddressable na;
    noaddressable * naptr = &na;
}
~~~

##### 1.0.5 已知的用处

* Boost 中的 addressof 

在C++11的 <memory> 头文件中已经定义了这个函数

##### 1.0.6 相关的做法

##### 1.0.7 引用

---

#### **2 代数抽象基类**

##### 2.0.1 目的

为了隐藏单个范型抽象

##### 2.0.1 别名

* 状态法

##### 2.0.3 动机

在纯的像 Smalltalk 面向对象语言中，变量像标签那样在运行时绑定到对象。变量名绑定对象就像是给对象贴上标签.

这些语言中的赋值就像是从一个对象上把标签扯下来贴到另一个对象上。然而，在 C 和 C++ 中，变量不是对象的标签而是实际的地址或者偏移。

赋值不是重新变量名重新绑定对象，赋值意味着用旧值覆盖新值。代数抽象基类是在C++中利用委托和多态来模拟变量跟对象的绑定。

代数抽象基类在实现中使用了“信封手法”，代数抽象基类的目的，就可以够写出如下的代码:

~~~
Number n1 = Complex (1,2);  // n1是一个复数
Number n2 = Real (10);      // n2是一个实数
Number n3 = n1 + n2;    // n3是n1和n2的和
Number n2 = n3;     // "重新贴标签" 
~~~

##### 2.0.4 解决方案和示例代码

代数抽象基类的实现代码如下。

~~~
template <class T>
T * addressof(T& v){

    return reinterpret_cast<T*>(& const_cast<char&>(reinterpret_cast<const volatile char&>(v)));
}

int main(){

    noaddressable na;
    noaddressable * naptr = &na;
}
~~~

##### 2.0.5 已知的用处

##### 2.0.6 相关的做法

* 

* 信封手法

##### 2.0.7 引用

---
#### **3 取址器**

##### 3.0.1 目的

##### 3.0.1 别名

##### 3.0.3 动机

##### 3.0.4 解决方案和示例代码

##### 3.0.5 已知的用处

##### 3.0.6 相关的做法

---
#### **4 取址器**

##### 4.0.1 目的

##### 4.0.1 别名

##### 4.0.3 动机

##### 4.0.4 解决方案和示例代码

##### 4.0.5 已知的用处

---
#### **5 取址器**

##### 5.0.1 目的

##### 5.0.1 别名

##### 5.0.3 动机

##### 5.0.4 解决方案和示例代码

##### 5.0.5 已知的用处

##### 5.0.6 相关的做法

---

