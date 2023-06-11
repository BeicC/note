* 1003
```c
#include <bits/stdc++.h>
using namespace std;
struct Node{
	int v,w;
};
int N,M,S,D,team[550];
int dis[550],cnt[550],road[550],sum[550];
vector<Node> edge[550];
unordered_set<int> pre[550];
bool vis[550];

bool SPFA(){
	for (int i = 0; i < N; i++) dis[i] = 1e9;
	dis[S] = 0,sum[S] = team[S],cnt[S] = 1, road[S] = 1;
	queue<int> que; que.push(S);
	
	while (!que.empty()){
		int now = que.front();
		que.pop(); vis[now] = false;
		//cout<<"size:"<<que.size()<<endl;		
		for (auto &p : edge[now]){

			int v = p.v,w = p.w;
			if (dis[v] > dis[now] + w){
				//if (cnt[v] == N-1) return false;
				dis[v] = dis[now] + w;
				road[v] =road[now];
				//cout<<1<<" "<<v<<" "<<road[v]<<now<<endl;
				sum[v] = sum[now] + team[v];
				pre[v].clear();
				pre[v].insert(now);
				que.push(v);
				//cout<<v<<" "<<sum[v]<<endl;

			}else if (dis[v] == dis[now] + w){
				pre[v].insert(now);
				int ans = 0;
				for (auto &c : pre[v]) ans += road[c];
				road[v] = ans;
				//cout<<v<<" "<<road[v]<<now<<endl;
				if (sum[v] < sum[now] + team[v]) {
						
					sum[v] = sum[now] + team[v];
									
				}
				que.push(v);
			}
		}
	}
	return true;
}

int main()
{
	cin >> N >> M >> S >> D;
	for (int i = 0; i < N; i++) cin >> team[i];
	for (int i = 0; i < M; i++){
		int u,v,w;
		cin >> u >> v >> w;
		edge[u].push_back({v,w});
		edge[v].push_back({u,w});
	}

	SPFA();
	
	cout<<road[D]<<" "<<sum[D];
	
	return 0;
}
```
* 1004
```c
#include <iostream>
#include <cstdio>
#include <queue>
using namespace std;
struct Node{
	int num, child_num;
	int child[110];
}node[110];
bool vis[110];
int ret[110];
int main()
{
	int n, m;
	cin>>n>>m;
	for (int i = 0; i < m; i++){
		int cur_root, k, child_root;
		cin>>cur_root>>k;
		for (int j = 0; j < k; j++){
			cin>>child_root;
			node[cur_root].child_num++;
			int child_num = node[cur_root].child_num;
			node[cur_root].child[child_num] = child_root;
		}
	}
	queue<int> que; que.push(1); vis[1] = true;
	int level = 0;
	while (!que.empty()){
		int ans = 0, k = que.size();
		for (int i = 0; i < k; i++){
			int now = que.front(); que.pop();
			if (node[now].child_num == 0) ans++;
			else{
				for (int j = 1; j <= node[now].child_num; j++){
					int c_sno = node[now].child[j];
					if (vis[c_sno] == false){
						vis[c_sno] = true;
						que.push(c_sno);
					}
				}
			}
		}
		ret[++level] = ans;
	}
	for (int i = 1; i < level; i++){
		cout<<ret[i]<<" ";
	}
	cout<<ret[level]<<endl;

	return 0;
}

```