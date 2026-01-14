```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; ++i) cin >> a[i];
    int steps = 0;
    int current_end = 0;
    int current_farthest = 0;
    for (int i = 0; i < n - 1; ++i) {
        current_farthest = max(current_farthest, i + a[i]);
        if (i == current_end) {
            steps++;
            current_end = current_farthest;
            if (current_end >= n - 1) break;
        }
    }
    cout << steps << endl;
    return 0;
}

```
