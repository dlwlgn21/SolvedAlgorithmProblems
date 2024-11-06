```C++
#define _CRT_SECURE_NO_WARNINGS
#include <iostream> 
#include <vector> 
#include <queue>
#include <stack> 
#include <unordered_map> 
#include <unordered_set>
#include <map> 
#include <string> 
#include <list> 
#include <stdint.h>
#include <algorithm> 
#include <cmath> 
#include <string.h> 
#include <assert.h> 
#include <climits>
#include <cfloat>
#include <iomanip>
using namespace std;
void FastIO() { ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL); }


const int MAX = 1000 + 4;
int N, M, R;
vector<int> graph[MAX];
bool visited[MAX];
void DFS(const int curr)
{
    visited[curr] = true;
    cout << curr << ' ';
    for (const int& next : graph[curr])
    {
        if (!visited[next])
            DFS(next);
    }
}
void BFS(const int start)
{
    visited[start] = true;
    queue<int> q;
    q.push(start);

    while (!q.empty())
    {
        const int curr = q.front();
        q.pop();
        cout << curr << ' ';
        for (const int& next : graph[curr])
        {
            if (!visited[next])
            {
                visited[next] = true;
                q.push(next);
            }
        }
    }

}
int main()
{
    FastIO();
    cin >> N >> M >> R;
    int u, v;
    for (int i = 0; i < M; ++i)
    {
        cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u);
    }

    for (int i = 1; i <= N; ++i)
    {
        if (graph[i].size() >= 2)
            sort(graph[i].begin(), graph[i].end());
    }

    DFS(R);
    cout << '\n';
    std::fill(&visited[0], &visited[MAX], false);
    BFS(R);
    return 0;
}
```