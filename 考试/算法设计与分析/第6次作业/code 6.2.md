```c++
#include <stdio.h>
#include <string.h>

#define MAXM 10
#define MAXN 10
#define MAXSTATE (1 << 8)

int m, n;
char seats[MAXM][MAXN + 1];
int validMask[MAXM];
int dp[MAXM][MAXSTATE];

int countBits(int x) {
    int cnt = 0;
    while (x) {
        x &= (x - 1);
        cnt++;
    }
    return cnt;
}

int main() {
    scanf("%d %d", &m, &n);
    for (int i = 0; i < m; i++) {
        scanf("%s", seats[i]);
    }
    for (int i = 0; i < m; i++) {
        validMask[i] = 0;
        for (int j = 0; j < n; j++) {
            if (seats[i][j] == '.') {
                validMask[i] |= (1 << j);
            }
        }
    }
    memset(dp, -1, sizeof(dp));
    dp[0][0] = 0;
    for (int i = 0; i < m; i++) {
        for (int cur = 0; cur < (1 << n); cur++) {
            if ((cur & validMask[i]) != cur) continue;
            if (cur & (cur << 1)) continue;
            int students = countBits(cur);
            if (i == 0) {
                dp[i][cur] = students;
            } else {
                for (int prev = 0; prev < (1 << n); prev++) {
                    if (dp[i - 1][prev] == -1) continue;
                    if ((cur & (prev << 1)) != 0) continue;
                    if ((cur & (prev >> 1)) != 0) continue;
                    if (dp[i][cur] < dp[i - 1][prev] + students) {
                        dp[i][cur] = dp[i - 1][prev] + students;
                    }
                }
            }
        }
    }
    int ans = 0;
    for (int state = 0; state < (1 << n); state++) {
        if (dp[m - 1][state] > ans) {
            ans = dp[m - 1][state];
        }
    }
    printf("%d\n", ans);
    return 0;
}

```