```c++
#include <iostream>
#include <vector>
#include <cstring>
using namespace std;
const int MAXN = 1005;
vector<int> adj[MAXN];
int matchR[MAXN];
bool visited[MAXN];
int n, m, k;

bool dfs(int r) {
    for (int c : adj[r]) {
        if (!visited[c]) {
            visited[c] = true;
            if (matchR[c] == -1 || dfs(matchR[c])) {
                matchR[c] = r;
                return true;
            }
        }
    }
    return false;
}

int main() {
    cin >> n >> m >> k;
    for (int i = 0; i < k; i++) {
        int r, c;
        cin >> r >> c;
        adj[r].push_back(c);
    }
    memset(matchR, -1, sizeof(matchR));
    int result = 0;
    for (int r = 1; r <= n; r++) {
        memset(visited, false, sizeof(visited));
        if (dfs(r)) result++;
    }
    cout << result << endl;
    return 0;
}

```