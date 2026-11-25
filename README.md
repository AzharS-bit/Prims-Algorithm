# Prims-Algorithm#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

typedef pair<int, int> iPair;

void primMST(vector<vector<iPair>>& graph, int V) {
    priority_queue<iPair, vector<iPair>, greater<iPair>> pq;
    vector<int> key(V, INT_MAX);
    vector<int> parent(V, -1);
    vector<bool> inMST(V, false);

    int src = 0;
    pq.push(make_pair(0, src));
    key[src] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        inMST[u] = true;

        for (auto& [v, weight] : graph[u]) {
            if (!inMST[v] && key[v] > weight) {
                key[v] = weight;
                pq.push(make_pair(key[v], v));
                parent[v] = u;
            }
        }
    }

    cout << "Edges in MST:\n";
    for (int i = 1; i < V; ++i)
        cout << parent[i] << " - " << i << "\n";
}

int main() {
    int V = 5;
    vector<vector<iPair>> graph(V);

    graph[0].emplace_back(1, 2);
    graph[0].emplace_back(3, 6);
    graph[1].emplace_back(0, 2);
    graph[1].emplace_back(2, 3);
    graph[1].emplace_back(3, 8);
    graph[1].emplace_back(4, 5);
    graph[2].emplace_back(1, 3);
    graph[2].emplace_back(4, 7);
    graph[3].emplace_back(0, 6);
    graph[3].emplace_back(1, 8);
    graph[4].emplace_back(1, 5);
    graph[4].emplace_back(2, 7);

    primMST(graph, V);

    return 0;
}
