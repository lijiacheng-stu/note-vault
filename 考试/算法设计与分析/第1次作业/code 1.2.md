```c++
#include <cstdio>  // 包含 scanf, printf
#include <algorithm> // 包含 swap
using namespace std;

// 1. 全局数组，防止栈溢出，稍微开大一点点
int nums[1005][1005];
int r[1005], c[1005]; // r代表行映射，c代表列映射

int main() {
    int n, m, q;
    // 题目提示输入量大，必须用 scanf
    scanf("%d %d %d", &n, &m, &q);

    // 2. 初始化映射数组 (千万别忘了这一步！)
    // 最开始第1行就是第1行，第1列就是第1列
    for(int i = 1; i <= n; i++) r[i] = i;
    for(int j = 1; j <= m; j++) c[j] = j;

    // 3. 读入矩阵
    for(int i = 1; i <= n; i++) {
        for(int j = 1; j <= m; j++) {
            scanf("%d", &nums[i][j]);
        }
    }

    // 4. 处理操作
    while(q--) {
        int op, x, y;
        scanf("%d %d %d", &op, &x, &y);

        if(op == 0) {
            // 交换行：只交换行的“标签”
            swap(r[x], r[y]);
        }
        else if(op == 1) {
            // 交换列：只交换列的“标签”
            swap(c[x], c[y]);
        }
        else {
            // 查询：去“现在的x行”和“现在的y列”找
            printf("%d\n", nums[r[x]][c[y]]);
        }
    }
    return 0;
}
```