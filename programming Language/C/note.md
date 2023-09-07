# C "Modules"
## reference
* [Kris Jordan](https://www.youtube.com/watch?v=8KyZedtkEhk)
## Header File
* 背景
将一个C程序分为`.c`和`.h`，目的是为了模块化
* 好处
    * `.h`头文件，可以理解为Java中的接口，如果不关心function的细节，那么我只需要看头文件就行了
* convention
    * 方法名:`filename_print()`
    因为一个程序可能会引入很多个header file，这样做是为了防止命名冲突
## include guard
```c
#ifndef POINT_H

#define POINT_H

//some declaration here


#endif
```
这就是个if语句，只不过是给C preprocessor看的
每个头文件都应该用这对`#ifndef`包裹
* 背景
```c
#include <stdio.h>
#include "point.h"

// some main code
```
C文件在编译之前，会先进行预处理
当preprocessor扫描到`#include <stdio.h>`时，它会到某个地方找到`stdio.h`文件，直接将里面的内容原封不到的粘贴过来
如果我自己写的`point.h`里面同样引用了`stdio.h`，最终预处理的效果就是，出现了两块与`stdio.h`代码，编译器直接报错：重复定义
上述include guard就是来控制C preprocessor的

## `#include`中`<>`与`""`之间的区别
```c
#include <stdio.h>
/*
当预处理器(C preprocessor)看到<>时，预处理器就会去系统的特定地方去找stdio.h这个文件
*/
#include "point.h"
/*
当预处理器(C preprocessor)看到""时，预处理器就会当前目录找stdio.h这个文件
*/
```
* Q：标准库在Linux中的那个目录下存放着？
`/usr/include`和`/usr/lib`
>--sysroot=dir
Use dir as the logical root directory for headers and libraries.  For example, if the compiler normally searches for headers in /usr/include and libraries in /usr/lib, it instead searches dir/usr/include and dir/usr/lib.
## inspect `.o` file
* utility programe:`objdump`
# Function Pointers
## referece
* [Kris Jordan](https://www.youtube.com/watch?v=RtLFA99aEzo&t=50s)
> ps:函数名其实是地址
```c
#include <stdio.h>
const int a = 1;
int main(){
    printf("%p\n",&a);
    printf("%p\n",main); //0x55893ba00149
}
```
* function pointer
```c
#include <stdio.h>
int add(int,int);

int main(){
    int (*function_pointer)(int,int); //声明一个函数指针
    function_pointer = add;
    printf("1+2=%d\n",add(1,2));
    printf("1+2=%d\n",function_pointer(1,2));
    return 0;
}
int add(int a,int b){
    return a+b;
}
```
* 函数指针声明的步骤
1、`int function_pointer(int,int)`
2、`int *function_pointer(int,int)`
3、`int (*function_pointer)(int,int)`
# Dynamic Memory Allocation
## `malloc`,`calloc`和`realloc`的区别
* `malloc(n)`会分配连续n的内存，但不会初始化（里面的数据是garbage）
* `calloc(n)`和`malloc`差不多，但是会将这些内存初始化为0
* `void* realloc(void *pointer,size_t size)`:重新开一块`size`的内存，并且把`pointer`指向的内容复制过来
## difference between static Array and dynamic array
```c
int f(int n){
    int a[n]; //这种是static array，如果n非常大，会导致StackOverflow
    int *b = (int *)malloc(sizeof(int)*n) //动态分配内存就会导致这种问题
}
```
# Input And Output
## reference
* [The.C.Programming.Language.2nd.Edition]()
## 文件的理解
```txt
//a.txt
Hello
World!
this
is
```
在内存中长这样
`H`,`e`,`l`,`l`,`o`,`10(LF)`,`W`,....,`i`,`s`,`10(LF)`,`-1`
## scanf family

## printf family
### sprintf
* `int sprintf(char* string,char *format,arg1,arg2....)`
与`printf`作用差不多，只不过把输出的内容放到`string`里,而不是标准输出
### fprintf
* `int fprintf(FILE* fp, char *format,....)`
将内容输出到fp文件指针指向的文件中
所以`fprintf(stdout,format,...)`等价于`printf()`
## stdin,stdout,stderr
* 可以把`stdin`,`stdout`,`stderr`看成文件
> When a C program is started, the operating system environment is responsible for opening three files and providing file pointers for them. These files are the standard input, the standard output, and the standard error; the corresponding file pointers are called stdin, stdout, and stderr, and are declared in<stdio.h>. 
* 在C语言中，`stdin`,`stdout`,`stderr`是文件指针`FILE *`
之所以可以在main函数中直接使用`stdin`字符串，是因为`stdin`定义在`stdio.h`的`#define`里
```c
//stdio.h
/* Standard streams.  */
extern FILE *stdin;     /* Standard input stream.  */
extern FILE *stdout;        /* Standard output stream.  */
extern FILE *stderr;        /* Standard error output stream.  */
/* C89/C99 say they're macros.  Make them happy.  */
#define stdin stdin
#define stdout stdout
#define stderr stderr
```
## file access 系列
### fopen
* `FILE *fopen(char *name, char *mode)`
如果name不存在，则返回NULL
如果存在，则返回一个FILE指针。注意：这个指针指向的位置并不是文件数据的缓冲区，而是指向一个结构体
该结构体大概如下所示
```c
typedef struct FILE{
    void *databuffer;
    void *character_position;
    void *mode; //是读还是写？
    .....
}FILE
```
### fclose
* `int fclose(FILE* fp)`
1、释放`struct FILE`内存
2、flush buffer that putc use
### fscanf
* `int fscanf(FILE *ptr,char *format,...)`
### fprintf
* `int fprintf(FILE *ptr,char *format,...)`
### exit
在main函数最后，`exit(0)`和`return 0`等价
在其他函数中，当调用`exit()`，会terminate the whole process,而不是仅仅返回
```c
#include <stdio.h>
#include <stdlib.h>

void f(){
    printf("Executing f\n");
    exit(0);
}

int main(){
    f();
    printf("Back from f\n"); //You never get "Back from f"
}
```