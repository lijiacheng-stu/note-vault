```c++
#include<iostream>
#include<vector>
#include<queue>
#include<climits>
#include<algorithm>
using namespace std;
const int MAXN = 110;
const int MAXM = 220;

struct Edge{
	int to, cap, cost, rev;
};
vector<Edge> graph[MAXN];
int min_cost[MAXN], pre_dot[MAXN], pre_index[MAXN];
bool inqueue[MAXN] = {false};

void add_edge(int from, int to, int cap, int cost){
	graph[from].push_back({to, cap, cost, (int)graph[to].size()});
	graph[to].push_back({from, 0, -cost, (int)(graph[from].size()-1)});
}

bool spfa(int s, int t, int n){
	fill(min_cost, min_cost+n+1, INT_MAX);
	queue<int> q;
	min_cost[s] = 0;
	q.push(s);
	inqueue[s] = true;
	while(!q.empty()){
		int x = q.front();
		q.pop();
		inqueue[x] = false;
		for(int i=0;i<(int)graph[x].size();i++){
			Edge& e = graph[x][i];
			if(e.cap>0&&min_cost[e.to]>min_cost[x]+e.cost){
				min_cost[e.to] = min_cost[x]+e.cost;
				pre_dot[e.to] = x;
				pre_index[e.to] = i;
				if(!inqueue[e.to]){
					q.push(e.to);
					inqueue[e.to] = true;
				}
			}
		}
	}
	return min_cost[t] != INT_MAX;
}

int main(){
	int n, m;
	cin>>n>>m;
	for(int i=0;i<m;i++){
		int a, b, c, d;
		cin>>a>>b>>c>>d;
		add_edge(a, b, c, d);
	}
	int flow=0, cost=0;
	int s=1, t=n;
	while(spfa(s, t, n)){
		int f = INT_MAX;
		for(int i=t;i!=s;i=pre_dot[i]){
			f = min(f, graph[pre_dot[i]][pre_index[i]].cap);
		}
		flow += f;
		cost += f * min_cost[t];
		for(int i=t;i!=s;i=pre_dot[i]){
			Edge& e = graph[pre_dot[i]][pre_index[i]];
			e.cap -= f;
			graph[i][e.rev].cap += f;
		}
	}
	cout<<flow<<" "<<cost<<endl;
	return 0;
}

```