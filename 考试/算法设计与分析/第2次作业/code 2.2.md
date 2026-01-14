```c++
#include <bits/stdc++.h>
using namespace std;

long long merge_count(vector<long long> &arr, vector<long long> &tmp, int l, int r) {
    if (l >= r) return 0;
    int mid = (l + r) / 2;
    long long inv = merge_count(arr, tmp, l, mid) + merge_count(arr, tmp, mid + 1, r);
    int i = l, j = mid + 1, k = l;
    while (i <= mid && j <= r) {
        if (arr[i] <= arr[j]) tmp[k++] = arr[i++];
        else {
            tmp[k++] = arr[j++];
            inv += mid - i + 1;
        }
    }
    while (i <= mid) tmp[k++] = arr[i++];
    while (j <= r) tmp[k++] = arr[j++];
    for (int t = l; t <= r; ++t) arr[t] = tmp[t];
    return inv;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int N;
    long long A, B;
    cin >> N >> A >> B;
    vector<long long> D(N), tmp(N);
    for (int i = 0; i < N; ++i) cin >> D[i];
    long long inv = merge_count(D, tmp, 0, N - 1);
    cout << inv * min(A, B) << "\n";
    return 0;
}

```