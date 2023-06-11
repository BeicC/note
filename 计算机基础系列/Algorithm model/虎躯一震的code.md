怎么使一个数x的二进制上的第i位 1变成0，0变成1？

```c++
x ^= (1 << i)

//补充说明异或操作
    //简单理解就是不进位加法，如1+1=0，,0+0=0,1+0=1。
```

枚举二进制的子集的通用方法

```c++
function get_subset(bitmask)
    subset = bitmask
    answer = [bitmask]
    while subset != 0
        subset = (subset - 1) & bitmask
        put subset into the answer list
    end while
    return answer
end function
//其中bitmask 表示一个二进制数，subset 会遍历所有bitmask 的子集，并将所有的子集放入 answer 中。需要注意的是，bitmask 本身也是bitmask 的一个子集，因此answer 在初始时就包含bitmask 本身。

```

