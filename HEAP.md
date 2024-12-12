<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MaxHeap Program</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        textarea {
            width: 100%;
            height: 500px;
            font-family: monospace;
            font-size: 14px;
            border: 1px solid #ccc;
            padding: 10px;
            resize: none;
            background-color: #f9f9f9;
        }
        h1 {
            color: #333;
        }
    </style>
</head>
<body>
    <h1>MaxHeap C++ Program</h1>
    <p>Below is the C++ code for the MaxHeap implementation. You can copy it for use in your projects.</p>
    <textarea readonly>
#include <iostream>
#include <vector>
using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    void HeapifyUp(int i) {
        while (i > 1 && heap[i / 2] < heap[i]) {
            swap(heap[i], heap[i / 2]);
            i = i / 2;
        }
    }

    void HeapifyDown(int i) {
        int n = heap.size() - 1;
        int v = heap[i];
        bool isHeap = false;

        while (!isHeap && 2 * i <= n) {
            int j = 2 * i;

            if (j < n && heap[j] < heap[j + 1])
                j++;

            if (v >= heap[j])
                isHeap = true;
            else {
                heap[i] = heap[j];
                i = j;
            }
        }
        heap[i] = v;
    }

public:
    MaxHeap() {
        heap.push_back(-1); // Placeholder to simplify index calculations
    }

    void insert(int value) {
        heap.push_back(value);
        HeapifyUp(heap.size() - 1);
    }

    void deleteMax() {
        if (heap.size() > 1) {
            cout << "Deleted root: " << heap[1] << endl;
            heap[1] = heap.back();
            heap.pop_back();
            if (heap.size() > 1) {
                HeapifyDown(1);
            }
        } else {
            cout << "Heap is empty!" << endl;
        }
    }

    void printHeap() {
        if (heap.size() > 1) {
            cout << "Heap elements: ";
            for (size_t i = 1; i < heap.size(); i++) {
                cout << heap[i] << " ";
            }
            cout << endl;
        } else {
            cout << "Heap is empty!" << endl;
        }
    }

    void printRoot() {
        if (heap.size() > 1) {
            cout << "Root element (max): " << heap[1] << endl;
        } else {
            cout << "Heap is empty!" << endl;
        }
    }
};

int main() {
    MaxHeap maxHeap;
    int choice, value;

    do {
        cout << "\nMenu:\n";
        cout << "1. Insert\n";
        cout << "2. Delete Root\n";
        cout << "3. Print Heap\n";
        cout << "4. Print Root\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> value;
                maxHeap.insert(value);
                break;
            case 2:
                maxHeap.deleteMax();
                break;
            case 3:
                maxHeap.printHeap();
                break;
            case 4:
                maxHeap.printRoot();
                break;
            case 5:
                cout << "Exit\n";
                break;
            default:
                cout << "Invalid choice! Please try again.\n";
        }
    } while (choice != 5);

    return 0;
}
    </textarea>
</body>
</html>
