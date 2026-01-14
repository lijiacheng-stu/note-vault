```c++
//状态表示：f[i][j]表示已有i个人压入栈，且有j个人弹出栈的所有方案
/*
状态计算：现将每个时刻的操作分为两类：(1)入栈 (2)出栈
另设当前栈容量为cur，栈中元素为size
(1) 此时需判断能否入栈：i)i < n  ii)size < cur
f[i+1][j] = f[i+1][j] + f[i][j]
(2) 此时需判断能否出栈，即保证size > 0
f[i][j+1] = f[i][j+1] + f[i][j]
*/

#include <iostream>
#include <cstring>

using namespace std;

typedef long long LL;

const int N = 1010 , MOD = 998244353;

LL f[N][N];

int main() {
    
    int n,t,p,d;
    cin >> n >> t >> p >> d;
    int q = p+d;

    memset(f,0,sizeof(f));

    //0个人入栈,0个人出栈也是一种方案
    f[0][0] = 1;

    //开始DP
    for(int i=0;i<=n;i++){
        for(int j=0;j<=i;j++){
            if(f[i][j] == 0){    //若为0，则表明当前方案不可达
                continue;
            }

            int stack_size = i-j;   //记录当前栈中元素个数
            //情况(1)
            if(i<n){
                int cur;    //记录当前栈容量
                if(i+1 <= t){
                    cur = p;
                }else{
                    cur = q;
                }
                if(stack_size < cur){
                    f[i+1][j] = (f[i+1][j] + f[i][j])%MOD;
                }
            }
            //情况(2)
            if(stack_size > 0){
                f[i][j+1] = (f[i][j+1] + f[i][j])%MOD;
            }
        }
    }

    cout << f[n][n] << endl;

    return 0;
}
```