```c++
#include <iostream>
#include <vector>
#include <cstring>
using namespace std;
const int MAXN = 110;
int n, m;
vector<int> adj[MAXN];
int match[MAXN];
bool visited[MAXN];

bool dfs(int u) {
    for (int v : adj[u]) {
        if (!visited[v]) {
            visited[v] = true;
            if (match[v] == -1 || dfs(match[v])) {
                match[v] = u;
                return true;
            }
        }
    }
    return false;
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < m; ++i) {
        int a, b;
        cin >> a >> b;
        adj[a].push_back(b);
    }
    memset(match, -1, sizeof(match));
    int maxMatch = 0;
    for (int u = 1; u <= n; ++u) {
        memset(visited, false, sizeof(visited));
        if (dfs(u)) ++maxMatch;
    }
    cout << n - maxMatch << endl;
    return 0;
}

```
