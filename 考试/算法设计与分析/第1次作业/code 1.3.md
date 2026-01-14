```c++
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
const int MOD = 2013;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int q, a, b;
    cin >> q >> a >> b;

    vector<int> seq;
    seq.push_back(1); // F[0]
    seq.push_back(1); // F[1]

    unordered_map<long long, int> seen;
    seen[1LL * 1 * MOD + 1] = 1; // (F[1], F[0]) at index 1

    int cycleStart = -1, period = -1;
    for (int i = 2; ; ++i) {
        int f_prev2 = seq[i - 2];
        int f_prev1 = seq[i - 1];
        int f_curr = (1LL * a * f_prev1 + 1LL * b * f_prev2) % MOD;
        seq.push_back(f_curr);

        long long state = 1LL * f_curr * MOD + f_prev1;
        if (seen.count(state)) {
            cycleStart = seen[state];
            period = i - cycleStart;
            break;
        }
        seen[state] = i;
    }

    vector<int> prefix(seq.begin(), seq.begin() + cycleStart);
    vector<int> cycle(seq.begin() + cycleStart, seq.begin() + cycleStart + period);

    while (q--) {
        long long n;
        cin >> n;
        if (n < (long long)prefix.size()) {
            cout << prefix[n] << endl;
        } else {
            long long offset = (n - cycleStart) % period;
            cout << cycle[offset] << endl;
        }
    }
    return 0;
}

```