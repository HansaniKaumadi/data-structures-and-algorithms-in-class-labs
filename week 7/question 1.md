![Screenshot 2025-04-15 094931](https://github.com/user-attachments/assets/6dfb1ac2-ade2-48a3-a8ef-75e349e4606d)


### C++ Code Implementation

```cpp
#include <iostream>
#include <sstream>
#include <vector>
using namespace std;

// Function to heapify the tree
void heapify(int arr[], int n, int root) {
    int largest = root;         // Initialize largest as root
    int left = 2 * root + 1;    // left child
    int right = 2 * root + 2;   // right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != root) {
        swap(arr[root], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Function to perform heap sort
void heapSort(int arr[], int n) {
    // Build max heap
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // Extract elements from heap one by one
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);       // Move current root to end
        heapify(arr, i, 0);         // call max heapify on reduced heap
    }
}

// Function to display the contents of the array
void displayArray(int arr[], int n) {
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}

// Main function
int main() {
    string input;
    getline(cin, input);

    stringstream ss(input);
    int num;
    vector<int> heap_arr;

    while (ss >> num) {
        heap_arr.push_back(num);
    }

    int n = heap_arr.size();

    heapSort(heap_arr.data(), n);

    displayArray(heap_arr.data(), n);
}

