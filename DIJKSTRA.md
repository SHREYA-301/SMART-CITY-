# Dijkstra's Algorithm in C++

```html
<pre>
<code>
#include <iostream>
#include <climits>

using namespace std;

class Dijkstra
{
public:
    int cost[100][100];
    int v; // Number of vertices
    int dist[10]; // Array to store shortest distances
    int path[10]; // Array to store predecessors
    int visited[10]; // Array to mark visited vertices

    void read_cost(int cost[100][100], int v);
    void initiate(int arr[10], int n);
    void shortest_path(int src);
    void print_path(int src);
};

void Dijkstra::read_cost(int cost[100][100], int v)
{
    cout << "Enter the cost matrix:\n";
    for (int i = 0; i < v; i++)
    {
        for (int j = 0; j < v; j++)
        {
            cin >> cost[i][j];
            if (cost[i][j] == 0 && i != j)
            {
                cost[i][j] = INT_MAX; // Set non-edges to infinity
            }
        }
    }
}

void Dijkstra::initiate(int arr[10], int n)
{
    for (int i = 0; i < n; i++)
    {
        arr[i] = 0;
    }
}

void Dijkstra::shortest_path(int src)
{
    // Initialize distances and visited array
    for (int i = 0; i < v; i++)
    {
        dist[i] = INT_MAX;
        visited[i] = 0;
        path[i] = -1;
    }
    dist[src] = 0; // Distance to source is 0

    for (int count = 0; count < v - 1; count++)
    {
        // Find the vertex with the minimum distance
        int min_dist = INT_MAX, u;

        for (int i = 0; i < v; i++)
        {
            if (!visited[i] && dist[i] < min_dist)
            {
                min_dist = dist[i];
                u = i;
            }
        }

        visited[u] = 1; // Mark the chosen vertex as visited

        // Relax the edges of the chosen vertex
        for (int i = 0; i < v; i++)
        {
            if (!visited[i] && cost[u][i] != INT_MAX && dist[u] != INT_MAX && dist[u] + cost[u][i] < dist[i])
            {
                dist[i] = dist[u] + cost[u][i];
                path[i] = u; // Update the path
            }
        }
    }
}

void Dijkstra::print_path(int src)
{
    cout << "Vertex\tDistance from Source\tPath" << endl;
    for (int i = 0; i < v; i++)
    {
        cout << i << "\t" << dist[i] << "\t\t";

        // Print the path
        int temp = i;
        while (temp != -1 && temp != src)
        {
            cout << temp << " <- ";
            temp = path[temp];
        }
        if (i != src)
            cout << src;

        cout << endl;
    }
}

int main()
{
    Dijkstra d;
    int src;

    cout << "Enter the number of vertices: ";
    cin >> d.v;

    d.read_cost(d.cost, d.v);

    cout << "Enter the source vertex: ";
    cin >> src;

    d.shortest_path(src);
    d.print_path(src);

    return 0;
}
</code>
</pre>
