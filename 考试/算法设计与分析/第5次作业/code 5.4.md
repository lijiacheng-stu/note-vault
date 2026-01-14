```c++
#include <bits/stdc++.h>
using namespace std;

int n, m;
char g[20][20];   // 存地图
bool vis[20][20]; // 标记走过的点
string ans = "";  // 存当前的全局最大值
int dx[] = {0, 0, 1, -1}; // 方向数组
int dy[] = {1, -1, 0, 0};

// DFS: x,y是坐标, s是当前拼成的字符串
void dfs(int x, int y, string s) {
    // 1. 更新答案：如果 s 更长，或者 s 长度一样但值更大
    if (s.size() > ans.size() || (s.size() == ans.size() && s > ans)) {
        ans = s;
    }

    // 2. 向四个方向试探
    for (int i = 0; i < 4; i++) {
        int nx = x + dx[i];
        int ny = y + dy[i];

        // 越界检查 + 障碍检查 + 访问检查
        if (nx >= 0 && nx < n && ny >= 0 && ny < m && g[nx][ny] != '#' && !vis[nx][ny]) {
            vis[nx][ny] = 1;              // 标记
            dfs(nx, ny, s + g[nx][ny]);   // 递归 (字符串累加)
            vis[nx][ny] = 0;              // 回溯 (这一步很关键！)
        }
    }
}

void solve() {
    cin >> n >> m;
    ans = ""; // 每个测试用例都要重置答案
    memset(vis, 0, sizeof(vis)); // 清空访问标记

    for (int i = 0; i < n; i++) cin >> g[i]; // 读入地图

    // 3. 全图枚举起点
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (g[i][j] != '#') { // 只要不是障碍，就可以作为起点
                vis[i][j] = 1;
                string start = ""; start += g[i][j]; // string(1, char) 也可以
                dfs(i, j, start);
                vis[i][j] = 0; // 记得回溯起点
            }
        }
    }
    cout << ans << endl;
}

int main() {
    int t;
    cin >> t;
    while (t--) solve();
    return 0;
}
```