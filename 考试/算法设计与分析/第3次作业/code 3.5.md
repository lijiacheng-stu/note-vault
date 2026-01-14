```c++
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

const int MOD = 998244353;
const int MAXN = 5005;

bool can[MAXN][MAXN];
int dp[MAXN];
int ndp[MAXN];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    string s, tmp;
    if (cin >> tmp) {
        if (isdigit(tmp[0])) {
            cin >> s;
        } else {
            s = tmp;
        }
    }

    int n = s.length();
    if (n % 2 != 0) {
        cout << 0 << endl;
        return 0;
    }

    for(int j=0; j<=n; ++j) can[n][j] = false;
    can[n][0] = true;

    for (int i = n - 1; i >= 0; --i) {
        for (int j = 0; j <= i + 1 && j <= n; ++j) {
            can[i][j] = false;
            if (s[i] == '(' || s[i] == '*') {
                if (j + 1 <= n && can[i + 1][j + 1]) {
                    can[i][j] = true;
                }
            }
            if (can[i][j]) continue;
            if (s[i] == ')' || s[i] == '*') {
                if (j - 1 >= 0 && can[i + 1][j - 1]) {
                    can[i][j] = true;
                }
            }
        }
    }

    if (!can[0][0]) {
        cout << 0 << endl;
        return 0;
    }

    for(int j=0; j<=n; ++j) dp[j] = 0;
    dp[0] = 1;

    for (int i = 0; i < n; ++i) {
        for(int j=0; j<=n; ++j) ndp[j] = 0;
        for (int j = 0; j <= i + 1 && j <= n; ++j) {
            if (dp[j] == 0) continue;
            if (s[i] == '(' || s[i] == '*') {
                if (j + 1 <= n) {
                    ndp[j + 1] = (ndp[j + 1] + dp[j]) % MOD;
                }
            }
            if (s[i] == ')' || s[i] == '*') {
                if (j - 1 >= 0) {
                    ndp[j - 1] = (ndp[j - 1] + dp[j]) % MOD;
                }
            }
        }
        for(int j=0; j<=n; ++j) dp[j] = ndp[j];
    }

    cout << dp[0] << endl;

    string min_s = "";
    int bal = 0;
    for (int i = 0; i < n; ++i) {
        if (s[i] == '(') {
            min_s += '(';
            bal++;
        } else if (s[i] == ')') {
            min_s += ')';
            bal--;
        } else {
            if (bal + 1 <= n && can[i + 1][bal + 1]) {
                min_s += '(';
                bal++;
            } else {
                min_s += ')';
                bal--;
            }
        }
    }
    cout << min_s << endl;

    string max_s = "";
    bal = 0;
    for (int i = 0; i < n; ++i) {
        if (s[i] == '(') {
            max_s += '(';
            bal++;
        } else if (s[i] == ')') {
            max_s += ')';
            bal--;
        } else {
            if (bal - 1 >= 0 && can[i + 1][bal - 1]) {
                max_s += ')';
                bal--;
            } else {
                max_s += '(';
                bal++;
            }
        }
    }
    cout << max_s << endl;
    return 0;
}

```
