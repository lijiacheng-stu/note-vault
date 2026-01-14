```c++
#include <bits/stdc++.h>
using namespace std;

int a[10005]; // 存每个传送门的传送范围

int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];

    if (n <= 1) { cout << 0 << endl; return 0; } // 特判不用动的情况

    // cur:  当前步数能覆盖到的最远下标
    // next: 下一步能触及到的最远下标
    // ans:  跳跃次数
    int cur = 0, next = 0, ans = 0;

    // 核心循环：只跑到 n-2
    // 为什么？因为我们的目标是到达 n-1。
    // 如果我们已经在 n-2，且能跳到 n-1，那也是最后一步了，不需要从 n-1 再起跳。
    for (int i = 0; i < n - 1; i++) {
        // 1. 贪心：记录这一步范围内，能跳到的最远位置
        next = max(next, i + a[i]);

        // 2. 边界检查：如果我们走到了当前步数的尽头
        if (i == cur) {
            ans++;       // 必须再跳一次
            cur = next;  // 更新边界

            // 剪枝：如果已经能覆盖终点了，可以直接结束（不写这行也能过）
            if (cur >= n - 1) break;
        }
    }

    cout << ans << endl;
    return 0;
}
```
