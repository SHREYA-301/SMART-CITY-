# Kruskal's Algorithm for Minimum Spanning Tree (MST) in C++

```html
<pre>
<code>
#include <iostream>

using namespace std;

class d {
public:
    int u;
    int v;
    int w;
};

// Function to check if two vertices are in the same set
int find(int arr[50], int u, int v) {
    if (arr[u] == arr[v]) {
        return 1;
    } else {
        return 0;
    }
}

// Function to union two sets
void union_set(int arr[50], int u, int v, int n) {
    int temp = arr[u];
    for (int i = 0; i < n; i++) {
        if (arr[i] == temp) {
            arr[i] = arr[v];
        }
    }
}

// Function to merge two sorted arrays into a single sorted array
void Merge(d B[], int p, d C[], int q, d A[]) {
    int i = 0, j = 0, k = 0;

    while (i < p && j < q) {
        if (B[i].w <= C[j].w) {
            A[k++] = B[i++];
        } else {
            A[k++] = C[j++];
        }
    }
    while (i < p) {
        A[k++] = B[i++];
    }
    while (j < q) {
        A[k++] = C[j++];
    }
}

// Function to sort an array using Merge Sort
void MergeSort(d A[], int n) {
    if (n > 1) {
        int mid = n / 2;

        d B[50], C[50];
        for (int i = 0; i < mid; i++) {
            B[i] = A[i];
        }
        for (int i = mid; i < n; i++) {
            C[i - mid] = A[i];
        }

        MergeSort(B, mid);
        MergeSort(C, n - mid);
        Merge(B, mid, C, n - mid, A);
    }
}

int main() {
    int n, e;
    cout << "Enter the number of vertices and edges: ";
    cin >> n >> e;

    d d1[50];
    cout << "Enter the edges (u v w):" << endl;
    for (int i = 0; i < e; i++) {
        cin >> d1[i].u >> d1[i].v >> d1[i].w;
    }

    // Sort the edges by weight
    MergeSort(d1, e);

    int arr[50];
    for (int i = 0; i < n; i++) {
        arr[i] = i;
    }

    d mst[50];
    int mstCount = 0;
    int cost = 0;

    for (int i = 0; i < e; i++) {
        if (!find(arr, d1[i].u, d1[i].v)) {
            mst[mstCount++] = d1[i];
            cost += d1[i].w;
            union_set(arr, d1[i].u, d1[i].v, n);
        }
    }

    cout << "Edges in the Minimum Spanning Tree (u v w):" << endl;
    for (int i = 0; i < mstCount; i++) {
        cout << mst[i].u << " " << mst[i].v << " " << mst[i].w << endl;
    }

    cout << "Total weight of MST: " << cost << endl;

    return 0;
}
</code>
</pre>
