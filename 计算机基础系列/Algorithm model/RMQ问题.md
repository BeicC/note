## ST表

参考博客：https://www.jvruo.com/archives/481/

可以用来求区间最值，与线段树不同的是：Sparse table只能离线查询，不能更新。优点是代码量少，速度快

建表：NlogN，查询O（1）

利用的是倍增思想

某一块答案都是一个数的时候可以用ST表

板子：

```c++
int dp[MAXN][25];
int query(int l, int r){ //查询nums[l]~nums[r]之间的最小值
    int k = floor(log((double)(r - l + 1)) / log(2.0));
    return min(dp[l][k], dp[r - (1<<k) + 1][k]);
}
int maxSumMinProduct(vector<int>& nums) {
    int n = nums.size();

    for (int i = 0; i < n; i++) dp[i][0] = nums[i];//建表
    for (int j = 1; j <= 20; j++){
        for (int i = 0; i+(1<<j) <= n; i++){
            dp[i][j] = min(dp[i][j-1], dp[i+(1<<(j-1))][j-1]);
        }
    }
```

