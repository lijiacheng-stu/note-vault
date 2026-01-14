```c++
#include <bits/stdc++.h>
using namespace std;
long long C[20][20];
int N;
long long Sum;
bool used[20];
int ans[20];
bool found = false;

void dfs(int idx, long long cur) {
    if (found) return;
    if (idx == N) {
        if (cur == Sum) found = true;
        return;
    }
    for (int v = 1; v <= N; v++) {
        if (!used[v]) {
            long long next = cur + v * C[N - 1][idx];
            if (next > Sum) continue;
            used[v] = true;
            ans[idx] = v;
            dfs(idx + 1, next);
            if (found) return;
            used[v] = false;
        }
    }
}

int main() {
    if (!(cin >> N >> Sum)) return 0;
    for (int i = 0; i < 20; ++i) {
        for (int j = 0; j < 20; ++j) C[i][j] = 0;
    }
    for (int i = 0; i <= N; i++) {
        C[i][0] = C[i][i] = 1;
        for (int j = 1; j < i; j++)
            C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
    }
    dfs(0, 0);
    if (!found) {
        cout << "GG";
    } else {
        for (int i = 0; i < N; i++) {
            if (i) cout << " ";
            cout << ans[i];
        }
    }
    return 0;
}

```