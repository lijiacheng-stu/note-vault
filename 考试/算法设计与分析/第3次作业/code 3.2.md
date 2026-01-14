```c++
#include <bits/stdc++.h>
using namespace std;
struct Item { int c, v; };                 // (Ci, Vi)
struct Query { long long budget; int idx; };// (Yi, 原始下标)
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int N, M;
    if (!(cin >> N >> M)) return 0;
    const int MAX_DAY = 300;
    static vector<Item> itemsByDay[MAX_DAY + 1];
    static vector<Query> queriesByDay[MAX_DAY + 1];
    vector<int> answers(M);
    int totalValueSum = 0;
    int maxDay = 0;
    for (int i = 0; i < N; ++i) {
        int c, v, t;
        cin >> c >> v >> t;
        if (t < 0) t = 0;
        if (t > MAX_DAY) t = MAX_DAY;
        itemsByDay[t].push_back({c, v});
        totalValueSum += v;
        if (t > maxDay) maxDay = t;
    }
    for (int i = 0; i < M; ++i) {
        int x; long long y;
        cin >> x >> y;
        if (x < 0) x = 0;
        if (x > MAX_DAY) x = MAX_DAY;
        queriesByDay[x].push_back({y, i});
        if (x > maxDay) maxDay = x;
    }
    const long long INF = (1LL << 62);
    vector<long long> minCost(totalValueSum + 1, INF);
    minCost[0] = 0;
    int reach = 0;
    auto do_suffix_min = [&](int upto) {
        for (int val = upto - 1; val >= 0; --val)
            if (minCost[val + 1] < minCost[val]) minCost[val] = minCost[val + 1];
    };
    for (int day = 0; day <= maxDay; ++day) {
        if (!itemsByDay[day].empty()) {
            for (const auto &it : itemsByDay[day]) {
                int v = it.v;
                int c = it.c;
                int upper = min(totalValueSum, reach + v);
                for (int val = upper; val >= v; --val) {
                    long long cand = minCost[val - v] + (long long)c;
                    if (cand < minCost[val]) minCost[val] = cand;
                }
                reach = upper;
            }
        }
        if (!queriesByDay[day].empty()) {
            if (reach > 0) do_suffix_min(reach);
            auto &qs = queriesByDay[day];
            sort(qs.begin(), qs.end(),
                 [](const Query &a, const Query &b){ return a.budget < b.budget; });
            int p = 0;
            for (const auto &q : qs) {
                while (p < reach && minCost[p + 1] <= q.budget) ++p;
                answers[q.idx] = p;
            }
        }
    }
    for (int i = 0; i < M; ++i) {
        cout << answers[i] << '\n';
    }
    return 0;
}

```