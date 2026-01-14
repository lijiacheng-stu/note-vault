```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    vector<int> up(n, 1);
    vector<int> down(n, 1);
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (a[i] > a[j]) {
                up[i] = max(up[i], down[j] + 1);
            } else if (a[i] < a[j]) {
                down[i] = max(down[i], up[j] + 1);
            }
        }
    }
    int ans = 0;
    for (int i = 0; i < n; i++) ans = max(ans, max(up[i], down[i]));
    cout << ans << endl;
    return 0;
}

```