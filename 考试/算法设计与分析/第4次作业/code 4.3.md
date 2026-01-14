```c++
#include <bits/stdc++.h>
using namespace std;

int a[100005];
vector<int> counts; // 用来存每种颜色有多少个球

int main() {
    int n, k;
    cin >> n >> k;
    for (int i = 0; i < n; i++) cin >> a[i];
    // 第一步：排序原数组，方便统计每种颜色的数量
    sort(a, a + n);
    // 第二步：统计频率
    int cur = 1; // 当前颜色的数量，至少是1
    for (int i = 1; i < n; i++) {
        if (a[i] == a[i-1]) {
            cur++; // 颜色一样，数量+1
        } else {
            counts.push_back(cur); // 颜色变了，保存上一种的数量
            cur = 1; // 重置计数器
        }
    }
    counts.push_back(cur); // 别忘了保存最后一种颜色的数量
    // 第三步：对“数量”进行排序 (贪心：先删数量少的)
    sort(counts.begin(), counts.end());

    int ans = counts.size(); // 一开始的颜色总数
    // 第四步：遍历数量，看 k 能消除几种
    for (int x : counts) {
        if (k >= x) {
            k -= x;   // 消耗 k
            ans--;    // 成功消除一种颜色
        } else {
            break;    // 剩下的球太多了，k 不够删完一种，停
        }
    }

    cout << ans << endl;
    return 0;
}
```