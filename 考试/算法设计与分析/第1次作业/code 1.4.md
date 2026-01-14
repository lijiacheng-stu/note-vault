```c++
#include <iostream>

using namespace std;

typedef long long LL;
const int N = 300010;

int n, m;
int c[N], p_c[N], s[N];

int main () {
    scanf("%d", &n);
    for (int i = 0; i < n; i ++ ) {
        int x;
        scanf("%d", &x);
        c[x] ++ ; // 数值为x的卡片有多少张
    }
    
    for (int i = 1; i < N; i ++ ) {
        if (c[i] == 0) continue; // 如果数值为i的卡片数量为0则跳过
        for (int j = i; j < N; j ++ ) {
            LL p = i * j;
            if (p >= N) break;
            if (c[j] == 0) continue; // 如果数值为j的卡片数量为0则跳过
            if (i == j) p_c[p] += c[i] * (c[i] - 1); // 若两张卡片数值一样，则乘积的数量为组合数
            else p_c[p] += c[i] * c[j] * 2;
        }
    }

    s[0] = 0;
    for (int i = 1; i < N; i ++ )  s[i] = s[i - 1] + p_c[i]; // 所有乘积小于等于i的卡片对数量
    
    LL total = (LL)n * (n - 1); // 总数
    scanf("%d", &m);
    while (m -- ) {
        int p;
        scanf("%d", &p);
        
        LL res = total - s[p - 1]; // 所有乘积小于p的卡片对数量
        printf("%lld\n", res);
    }
    
    return 0;
}       

```