```c++
#include <iostream>
#include <vector>
using namespace std;
bool is_prime[40];

void init_primes() {
    for (int i = 2; i < 40; ++i) {
        bool ok = true;
        for (int j = 2; j * j <= i; ++j)
            if (i % j == 0) { ok = false; break; }
        is_prime[i] = ok;
    }
}

int n;
vector<int> path;
bool used[21];
bool found = false;

void dfs() {
    if (found) return;
    if ((int)path.size() == n) {
        found = true;
        for (int i = 0; i < n; ++i) {
            if (i > 0) cout << " ";
            cout << path[i];
        }
        cout << '\n';
        return;
    }
    for (int num = 1; num <= n; ++num) {
        if (used[num]) continue;
        if (!path.empty() && !is_prime[path.back() + num]) continue;
        used[num] = true;
        path.push_back(num);
        dfs();
        if (found) return;
        path.pop_back();
        used[num] = false;
    }
}

int main() {
    init_primes();
    cin >> n;
    if (n == 1) {
        cout << "1\n";
        return 0;
    }
    if (n >= 15) {
        cout << "-1\n";
        return 0;
    }
    dfs();
    if (!found) {
        cout << "-1\n";
    }
    return 0;
}

```
