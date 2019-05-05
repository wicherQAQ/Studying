## 结构类型

声明结构的形式

struct structName{
	int age;
	int sex;
};

struct{
	int age;
	int sex;
}p1,p2;

struct structName{
	int age;
	int sex;
}p1,p2;

# 结构的初始化

struct structName{
	int age;
	int sex;
};

struct structName s1 = {11,12};
struct structName s1 = {.age=11,.sex=12};

注意：初始化不赋值则默认为0;
要访问整个结构，直接用结构变量的名字。
对于整个结构，可以做赋值、取地址、，也可以传递给函数参数。

p1=(struct point){5,10};强制类型转化，相当于p1.x=5;p1.y=10;
p1=p2;//相当于p1.x = p2.x; p1.y = p2.y;

##结构指针

和数组不同，结构变量的名字并不是结构变量的地址，必须要用&运算符
struct date *pDate = &today;

#结构作为函数参数

int numberOfDate(struct date d)
1.整个结构可以作为参数的值传入函数
2.可在函数内新建一个结构变量，并将调用者的结构的值赋值给新建的结构变量
3.也可以返回一个结构
4.这与数组完全不同

## Typedef

# 申明新的类型名称

typedef long int64_t;
typedef struct ADate {
	int month;
	int day;
	int year;
} Date;

int64_t i = 10000000;
Date t = {9,1,2005};

## union联合

可以用做文件的处理

## 静态本地变量
静态本地变量实际上是特殊的全局变量
他们位于相同的内存区域
静态本地变量具有全局的生存期，函数内的局部作用域

note：关于返回指针的函数
1.返回本地变量的地址是危险的
2.返回全局变量或静态本地变量的地址是安全的。
3.返回在函数内malloc的内存是安全的，但是容易造成问题
4.最好的做法是返回传入的指针

tips：
1.不要使用全局来在函数传递参数的结果
2.尽量避免使用全局变量
3.*使用全局变量和静态本地变量的函数是线程不安全的

## 编译预处理指令
#开头的是编译预处理指令
它们不是c语言的成分，但是c语言离不开编译预处理指令
#define用来定义一个宏

#include <stdio.h>

#define PI 3.14

编译的过程

编译预处理
.c--->.i--->.s--->.o--->a.out

# 定义像函数的宏
原则：
一切都要有括号
	整个值要有括号
	参数出现的每个地方都要有括号
	
#define cube(x)((x)*(x)*(x))
 # 带参数的宏（没有类型检查）
 在大型程序的代码中使用非常普遍
 可以非常复杂，如“产生”函数
 部分宏会被inline函数替代
 
## 项目
对于项目，dev c++的编译会把一个项目中的所有的员代码文件都编译后，链接起来
有的ide有分开的编译(compile)和构建(build)两个按钮；前者是对单个源代码文件编译，后者是对整个项目做链接

##大程序文件

1.在函数前面加上static就使得它成为只能在所在的编译单元中被使用的函数
2.在全局变量前面加上static就使得他成为只能在所在的编译单元中被使用的全局变量

## 变量的声明
int i;是变量的定义
extern int i;是变量的声明

# 声明和定义
声明式不产生代码的东西
	函数原型
	变量声明
	结构声明
	宏声明
	枚举声明
	类型声明
	inline声明
定义是产生代码的东西

## 标准头文件结构

运用条件编译和宏，保证这个头文件在一个编译单元中只会被#include一次
#pragma once也能起到相同的作用，但不是所有的编译器都支持

#ifndef _LIST_HEAD_
#define _LIST_HEAD_

#include "node.h"

typedef struct _list{
	Node* head;
	Node* tail;
}List;

#endif
