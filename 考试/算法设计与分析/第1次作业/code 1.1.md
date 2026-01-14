```c++
#include <iostream>
using namespace std;

int n, m, t;
int a[26], b[26], c[26], d[26];
// 注意：结果可能很大且为负数，初始值要给一个极小的 long long
long long max_num = -9000000000000000000;

// 2. 核心递归函数
void findMax(int cur[], int step) {
    int rem = m - step;
    // --- 第一部分：算分更新最大值 ---
    long long sum = 0;
    for(int i = 0; i < n; i++) {
        int val = cur[i];
        // 如果剩奇数步，说明最后一步需要做个异或才能结束，这里提前模拟一下
        if(rem % 2 != 0) val = val ^ b[i];
        sum += (long long)val * c[i];
    }
    if(sum > max_num) max_num = sum;
    // 如果没步数了，就结束
    if(rem == 0) return;

    // --- 第二部分：递归走路 ---
    int new_a[26]; // 局部数组
    // 走法1 (消耗1步)：直接置换 + t
    // 公式：新[i] = 旧[d[i]] + t
    for(int i = 0; i < n; i++) {
        new_a[i] = cur[d[i]] + t;
    }
    findMax(new_a, step + 1);
    // 走法2 (消耗2步)：先异或 b 再置换 + t
    // 公式：新[i] = (旧[d[i]] ^ b[d[i]]) + t
    if(rem >= 2) {
        for(int i = 0; i < n; i++) {
            new_a[i] = (cur[d[i]] ^ b[d[i]]) + t;
        }
        findMax(new_a, step + 2);
    }
}

int main() {
    // 普通的输入，没有任何花哨技巧
    cin >> n >> m >> t;
    for(int i = 0; i < n; i++) cin >> a[i];
    for(int i = 0; i < n; i++) cin >> b[i];
    for(int i = 0; i < n; i++) cin >> c[i];
    // 注意：读 d 的时候减 1，转成 0-based 下标
    for(int i = 0; i < n; i++) {
        cin >> d[i];
        d[i] = d[i] - 1;
    }
    findMax(a, 0);
    cout << max_num << endl;
    return 0;
}
```