```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <cstring>
using namespace std;

const int N = 10010, INF = 0x3f3f3f3f;
int n, f[N][3][3], mp[128], ans;
vector<string> g(2);

int solve(vector<string>& g) {
    memset(f, 0x3f, sizeof f);
    f[0][0][0] = 0;
    
    for (int i = 1; i <= n; ++i) {
        int up = mp[g[0][i - 1]];
        int down = mp[g[1][i - 1]];
        
        for (int pre_up = 0; pre_up < 3; ++pre_up) {
            for (int pre_down = 0; pre_down < 3; ++pre_down) {
                if (f[i - 1][pre_up][pre_down] == INF) continue;
                
                for (int k = 0; k < 4; ++k) {
                    int cost = 0;
                    int tmp_up = up, tmp_down = down; 
                    
                    if (k & 1) { 
                        if (tmp_up) continue;
                        tmp_up = 3; cost++;
                    }
                    if (k & 2) { 
                        if (tmp_down) continue; 
                        tmp_down = 3; cost++;
                    }
                    
                    int cur_up, cur_down;
                    
                    if (tmp_up == 3) cur_up = 0;
                    else if (tmp_up == 1) {
                        if (pre_up == 2) continue;
                        cur_up = 1;
                    } else if (tmp_up == 2) {
                        if (pre_up == 1) continue;
                        cur_up = 2;
                    } else cur_up = pre_up;
                    
                    if (tmp_down == 3) cur_down = 0;
                    else if (tmp_down == 1) {
                        if (pre_down == 2) continue;
                        cur_down = 1;
                    } else if (tmp_down == 2) {
                        if (pre_down == 1) continue;
                        cur_down = 2;
                    } else cur_down = pre_down;
                    
                    if (cur_up && cur_down && cur_up + cur_down == 3) continue;
                    
                    if (cur_up && !cur_down && tmp_down != 3) cur_down = cur_up;
                    else if (!cur_up && cur_down && tmp_up != 3) cur_up = cur_down;
                    
                    if (f[i][cur_up][cur_down] > f[i - 1][pre_up][pre_down] + cost) {
                        f[i][cur_up][cur_down] = f[i - 1][pre_up][pre_down] + cost;
                    }
                }
            }
        }
    }
    
    int res = INF;
    for (int i = 0; i < 3; ++i)
        for (int j = 0; j < 3; ++j)
            res = min(res, f[n][i][j]);
    return res;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cin >> n >> g[0] >> g[1];
    
    mp['.'] = 0; mp['C'] = 1; mp['S'] = 2; mp['#'] = 3;

    vector<string> g1 = g;
    for (auto& s : g1) replace(s.begin(), s.end(), 'P', 'S');
    ans = solve(g1);
    
    vector<string> g2 = g;
    for (auto& s : g2) replace(s.begin(), s.end(), 'P', 'C');
    ans = min(ans, solve(g2));
    
    if (ans == INF) cout << -1 << endl;
    else cout << ans << endl;
    return 0;
}
```