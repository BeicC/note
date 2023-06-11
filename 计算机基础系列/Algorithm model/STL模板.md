# STL模板
## 万能头文件
`#include <bits/stdc++.h>`

## Some instructions

在STL中，函数中默认的排序方式都是按小于号进行的，这也就解释了为什么priotity_queue和sort在重载符号的时候重载小于号

## string

头文件定义 # include <string> 属于STL行列，而定义cstring或string.h分别属于c++和c中的头文件

---

参考：https://www.cnblogs.com/maowang1991/p/4181806.html

1.与其他头文件的差别

1.

\#include <cstring>  //不可以定义string s；可以用到strcpy等函数
using  namespace  std;

\#include <string>  //可以定义string s；可以用到strcpy等函数
using  namesapce  std;

\#include <string.h>  //不可以定义string s；可以用到strcpy等函数

2.

1）文件cstring，和string.h对应，c++版本的头文件，包含比如strcpy之类的字符串处理函数
2）文件string.h，和cstring对应，c版本的头文件，包含比如strcpy之类的字符串处理函数
3）文件string，包含std::string的定义，属于STL范畴
4）CString，MFC里的的字符串类

string.h是C语言中字符串操作函数的头文件
cstring是c++对C语言中的strcpy之类的函数申明，包含cstring之后，就可以在程序中使用C语言风格的strcpy之类的函数。

string是c++语言中string类模板的申明 
CString是MFC中定义的字符串类，MFC中很多类及函数都是以CString为参数的，另外CString类重载了（LPCSTR）运算符，所以如果你在MFC下面使用CString类，就可以直接用CString类做为参数来调用需要一个C语言风格字符串的win  api函数，编译器会自动调用(LPCSTR)成员函数完成从CString到一个C风格字符串的转换。如果你在MFC下使用C++语言中标准的 string类，那么在调用需要C语言风格的字符串为参数的win  api时，你必须显示调用sting.c_str()成员函数，来完成同样的转换，也就是说在使用MFC里，如果用CString类，会比sting类方便那么一点点。

3.

(1).首先说cstring与string.h:
cstring和string.h其实里面都是C标准库提供的东西，某些实现中cstring的内容
就是: 
 namespace  std 
 { 
 \#include  <string.h> 
 } 
cstring是C++的组成部分，它可以说是把C的string.h的升级版，但它不是C的组成部分。
所以如果你用的是C++，那么请用cstring,如果你用的是C请用string.h。

(2).string与cstring: 
一般一个C++库老的版本带“.h”扩展名的库文件，比如iostream.h，在新标准后的标准库中都有一个不带“.h”扩展名的相对应，区别除了后者的好多改进之外，还有一点就是后者的东东都塞进了“std”名字空间中。   
==string，它是C++定义的std::string所使用的文件，是string类的头文件，属于STL范畴。它有很多对字符串操作的方法。==

4.string.h是C++标准化（1998年）以前的C++库文件，在标准化过程中，为了兼容以前，标准化组织将所有这些文件都进行了新的定义，加入到了标准库中，加入后的文件名就新增了一个"c"前缀并且去掉了.h的后缀名，所以string.h头文件成了cstring头文件。但是其实现却是相同的或是兼容以前的。相当于标准库组织给它盖了个章，说“你也是我的标准程序库的一份子了”

5.cstring代表的是string.h，但是被封装到了std里面，譬如调用strlen函数，需要写成std::strlen(yourstr)才行，这个使用方法比较符合C++的标准要求string就是C++标准库里面的string模板（确切地说应该是一个特化的模板），但是他同样包含了C风格字符串操作函数的定义（应该是通过包含string.h实现的）string.h就不需要使用名字空间了，这个是C风格字符串操作的一个函数库，strlen，strcpy，strcat，strcmp……都在这里面了，不过既然是C风格的库，当然不需要namespace支持了。

---

2.string 的比较

两个string是这样比较的：string的比较不是先比较位数，在逐位比较大小的，而是先逐位比较大小，在比较位数

3.string.substr

定义在<string>中；

出自柳神🤩

![](C:\Users\DELL\Pictures\cs\未命名图片.png)

## memset

定义在：<cstring>里；

==memset只能赋值0，或-1，或无限大，或无限小，其他的值都不能通过memset来进行赋值!==（为什么？）

因为memset是按照字节进行赋值

注意：如果把数组全部赋值，memset是要比普通的for要快不少的，但如果你是在for循环里面写memset了，就不行了，因为默认的memset是把全部字节给赋值，你想如果每循环一个就糊一下，用的时间也太多了吧。

memset清结构体 ： memset(str , 0 , sizeof(str)); //都给他糊上0（NULL，false）

```c++
//memset清空char数组
memset(a,0,sizeof(a)/sizeof(char));
//用过memset后，里面的每一个char里面的值都是'/0'
```

1：这个只能在int和long long里用，比较好记；

```c++
memset(a,127,sizeof(a));

即得到无穷大。

memset(a,128,sizeof(a));

即得到无穷小，与上述的值互为相反数。

memset(a,60,sizeof(a));

即近似为第一个式子的数值的一半。

memset(a,0,sizeof(a));赋值0

memset(a,-1,sizeof(a));赋值-1
```

2:比较高端的操作：

```c++
memset(a,0x3f,sizeof(a)) //只有在用memset的时候是0x3f，因为0x3f3f3f3f的每个字节都是0x3f，而memset恰好是用字节进行赋值的，在平时的时候定义无穷大要写成inf = 0x3f3f3f3f !!
```

原因：0x3f3f3f3f的十进制是1061109567，也就是10^9级别的（和0x7fffffff一个数量级），而一般场合下的数据都是小于10^9的，所以它可以作为无穷大使用而不致出现数据大于无穷大的情形。 
另一方面，由于一般的数据都不会大于10^9，所以当我们把无穷大加上一个数据时，它并不会溢出（这就满足了“无穷大加一个有穷的数依然是无穷大”），事实上0x3f3f3f3f+0x3f3f3f3f=2122219134，这非常大但却没有超过32-bit int的表示范围，所以0x3f3f3f3f还满足了我们“无穷大加无穷大还是无穷大”的需求。 
最后，0x3f3f3f3f还能给我们带来一个意想不到的额外好处：如果我们想要将某个数组清零，我们通常会使用memset(a,0,sizeof(a))这样的代码来实现（方便而高效），但是当我们想将某个数组全部赋值为无穷大时（例如解决图论问题时邻接矩阵的初始化），就不能使用memset函数而得自己写循环了（写这些不重要的代码真的很痛苦），我们知道这是因为memset是按字节操作的，它能够对数组清零是因为0的每个字节都是0，现在好了，如果我们将无穷大设为0x3f3f3f3f，那么奇迹就发生了，0x3f3f3f3f的每个字节都是0x3f！所以要把一段内存全部置为无穷大，我们只需要memset(a,0x3f,sizeof(a))。 
所以在通常的场合下，0x3f3f3f3f真的是一个非常棒的选择。

3：其他赋值：

```c++
memset(arr,0x7F,sizeof(arr)); //它将arr中的值全部赋为2139062143，这是用memset对int赋值所能达到的最大值
memset(arr,0x80,sizeof(arr)); //set int to -2139062144
```

## vector

定义在：<vector>中

vector在不指定大小的情况下是不能直接用下标进行访问的，因为还没有分配内存，只能push_back

### 常用操作：

vector<int> v； 

vector<int>a(10,1) ：定义具有10个整型元素的向量，且给出的每个元素初值为1

v.push_back（）：在vector的末尾加入元素

**v.pop_back（）：将vector的最后一个元素弹出**

v.back（）：返回vector的最后一个元素

v.clear(); :清空a中的元素

v.insert(v.begin()+n,m) : 在v的第n个位置插入元素m，在其后的都往后稍稍。

vecto.resize(x,p) 将空间变为x，并且每个元素都是p，如果不写p就拓展出来的默认为0，如果没有拓展，里面的值是不变的

### 二维vector：

初始化：vector<vector<int>> dist(m, vector<int>(n，x)); // 初始化一个m行n列的vector，里面的数值为x（可以不写，不写的话默认为0） 

排序：vector<vector<int>>& reservedSeats  如果写成sort(reservedSeats.begin(),reservedSeats.end())，就是按照reservedSeats [i] [0]进行从小到大排序https://leetcode-cn.com/problems/cinema-seat-allocation/。

对二维vector进行resize

```c++
vector <vector<int> > v1;
vector<int> temp(4)
v1.resize(5,temp)
```

### 类中初始化：

```c++
//c++11以后
class Foo(){
private:
    vector<string> name = vector<string>(5);
    vector<int> val{vector<int>(5,0)};
}

//c++11以前
class Foo {
private:
    vector<string> name;
    vector<int> val;
 public:
  Foo() : name(5), val(5,0) {}
};

```



## min(max)

他是定义在#include <algorithm> 中的，我也不知道为啥我一直以为他是在cmath中 :(



## map && unordered_map

1.map查找元素的两种方式

1.m.count(key)：由于map不包含重复的key，因此m.count(key)取值为0，或者1，表示是否包含。

2.m.find(key)：返回迭代器，判断是否存在。

2.map的遍历

1.直接用aotu，但auto是在c++11之后才有的，所以在dev5.11中不能用auto

2.老老实实的用迭代器：

```c++
map <  CString , 结构体名>  maps;    
map <  CString , 结构体名>  : : iterator      iter;
```

3.map与unordered_map的区别

3.1头文件不同map: #include < map >    unordered_map: #include < unordered_map >

3.2map的内部实现为一颗红黑树，而unordered_map的内部实现为哈希表

3.3map内部的元素是有序的，而unordered_map内部的元素是无序的，所以对于map的插入和查询其复杂度是**lg（n）**，而unordered_map的插入和查询时O(1)的

3.4unordered_ map占的内存要比map高，但是它查询快啊

4.map || unordered_map 一些要注意的点

map.clear():清空map
习惯用key作为下标来访问map中的value，如string valueStr = dataMap[key]; 在测试的时候发现一个不存在的key值取出了一个非null的值。原来用下标取值的算法是先查找是否有此key，没有就插入一个默认值作为该key的value。**所以以后判断key值是否存在用count，不要用下标直接去访问**

## queue

定义在<queue>中；

queue<int> q；

q.front（）返回队列首元素的值；

q.push（）向队列添加元素；

## priority_queue

1.一些说明

定义在<queue>中

==第三个参数比较重要，支持一个比较结构，默认是less，默认情况下，会选择第一个参数决定的类的<运算符来做这个比较函数。==

只需要把数输入进去，就能自动排序（堆）；

一些常用的操作：top 访问队头元素，empty 队列是否为空，push 插入元素到队尾 (并排序)，pop 弹出队头元素，size() 队列中元素的数目。

默认从高到低排列

```c++
//升序队列
priority_queue <int,vector<int>,greater<int> > q; //greater 竟然有更大的意思
//降序队列
priority_queue <int,vector<int>,less<int> >q;

//greater和less是std实现的两个仿函数（就是使一个类的使用看上去像一个函数。其实现就是类中实现一个operator()，这个类就有了类似函数的行为，就是一个仿函数类了）

```

2.注意事项.

1.如果里面放的是pair，那么是根据pair的first进行默认排序的，如果first相同，在对于second进行默认排序

2.优先队列里放pair：priority_queue<pair<int,int> > que; 记得里面是有一个空格的

3.自定义排序

如果是基本数据类型或者是pair，想要从小到大排列，都可以用系统自带的仿函数实现

```c++
priority_queue<int, vector<int>, greater<int> > q;
priority_queue<pair<int,int>,vector<pair<int,int> >,greater<pair<int,int> > > coll;
```

如果是自己写的结构体，就要重载< 了

```c++
# include<bits/stdc++.h> 
using namespace std;

struct node
 
{
 
      int x, y;
 
      node(int x=0, int y=0):x(x),y(y){}
 
};
 
bool operator<(node a, node b)
 
{
 
      if(a.x > b.x) return 1;
 
      else if(a.x == b.x)
 
           if(a.y >= b.y)   return 1;
 
      return 0;
 
}
 
int main()
 
{
 
      priority_queue<node> pq;  
 
      pq.push(node(1,2)); pq.push(node(2,2));
 
      pq.push(node(2,3)); pq.push(node(3,3));
 
      pq.push(node(3,4)); pq.push(node(4,4));
 
      pq.push(node(4,5)); pq.push(node(5,5));
 
      while(!pq.empty())
 
      {
 
           cout<<pq.top().x<<pq.top().y<<endl;
 
           pq.pop();
 
      }
 
      return 0;
 
}
```



4.一些猜想

为什么优先队列默认的是大根堆但比较符号是<？其实是大于号还是小于号无所谓的，因为优先队列内部是用堆实现的，而当一个新的元素插进堆的时候，需要比较他和他父节点的大小，所以大于号还是小于号起到的作用是一样的，只是默认的是小于号罢了

理解了这个，也就很容易理解结构体的重载了，把结构体或者说其他基本数据类型进行从小到大放置时，其实就是改变一下<的意义

## lower(upper)_bound

这俩都定义在<algorithm>中，使用前提：数组需要有序（升序数组用lower，降序用upper）

```c++
lower_bound(a+l,a+r,m)
```

一些说明：

​	作用：在数组中l到r区间内查找第一个大于等于m的下标

   1.如果m在区间中没有出现过，那么**返回第一个比m大的**数的下标。

   2.如果m比所有区间内的数都大，那么返回r。这个时候会越界，小心**。**

   3.如果区间内有多个相同的m，返回**第一个m**的下标。

   4.lower_bound()返回值是一个**迭代器**,返回指向大于等于key的第一个值的位置

## to_string

定义在<string>头文件里，作用是把数字给转化为字符串



## sort

定义在<algorithm>中.

要知道sort排序是根据指针进行选定范围的：

```c++
sort(arr.begin(),arr.end());//arr为vector
sort(arr,arr+n);//arr为普通数组
```

### lambda表达式

1. 在c++11之后才能用
2. 形式[说明符] (参数表) -> 返回值类型{语句块}
3. 参考：http://c.biancheng.net/view/433.html

## set

初步理解：可以去重，内部是有序的，所以可以在set里用lower_bound进行二分查找

注意：set.end()与vector.end()不同，set.begin()和set.end()是左闭右闭的

方法：set.insert(x)：把x插入set里面

​			set.erase(x)：把x从set里面删去

​			set.lower_bound(x)：返回第一个大于等于x的迭代器。如果没有符合条件的，那么返回set.end()

## max_element

std::max_element(*begin, *end) 返回指向最大元素的指针，用 *max_element()就可以把这个数表示出来
```c++
int Max = *max_element(v.begin(),v.end());
```

## copy

std::copy(*input_first, *input_end, *outputfirst), 将第一个数组赋值到第二个数组中，复杂度为一样为n，只不过这样写高级点

## stoi

头文件：#include <string>

c++11之后才具有，可以把一个string转化为int；

```c++
string nums = "0213";
int res = stoi(nums);
cout<<res;//输出213
```

## to_string

头文件：#include <string>

c++11只有才具有，把一个int转化为string

## isdigit

定义在<cctype>中

来判断一个**字符**是不是数字，如果是返回非0，否则返回0

## unique

先排个序， 然后unique(begin(), end() ) 把容器里面的重复的元素挪到容器后边，返回指针指向后面的第一个重复元素

```c++
sort(word.begin(), word.end());//word = "aabbcc", unique之后 word = "abcabc"
word.erase(unique(word.begin(), word.end()), word.end()); // word = "abc"
```

## next_permutation()

求当前全排列的下一个

```c++
next_permutation(v.begin(), v.end());
```

具体实现：https://www.cnblogs.com/DWVictor/p/10301666.html

