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