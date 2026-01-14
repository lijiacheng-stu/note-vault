```c++
#include<bits/stdc++.h>
using namespace std;
const int MAX_D=100000;
int d[25];
int m;
int n=30;
int vis[MAX_D*25*2 + 1];

void dfs(int deep,int x,int v){
    if(deep==m){
        n = min(n,v);
        return;
    }
    if(v>=n) return;
    int position = x + d[deep];
    vis[position]++;
    dfs(deep+1,position,v+(vis[position] == 1));
    vis[position]--;
    position = x - d[deep];
    vis[position]++;
    dfs(deep+1,position,v+(vis[position] == 1));
    vis[position]--;
}

int main(){
    cin>>m;
    for(int i=0;i<m;i++) cin >> d[i];
    vis[25* MAX_D]=1;
    vis[25* MAX_D+d[0]] = 1;
    dfs(1,25* MAX_D+d[0],2);
    cout<<n<<endl;
}

```