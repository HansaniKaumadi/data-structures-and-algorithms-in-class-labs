
![Screenshot 2025-04-15 004306](https://github.com/user-attachments/assets/a242c0a3-8748-473c-b572-06154ddab980)

### C++ Code Implementation

```cpp
#include <iostream>
#include <vector>
#include <sstream> // For string stream to read input

using namespace std;

// Function to perform insertion sort
void insertionSort(vector<int>& arr) {
    size_t n = arr.size(); // Use size_t for safety
    for (size_t i = 1; i < n; i++) {
        int key = arr[i]; // Store the current element
        int j = i - 1;
        
        // Move elements that are greater than key one position ahead
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key; // Place key at the correct position
    }
}

int main() {
    vector<int> numbers; // Vector to store input numbers
    string input;
    
    getline(cin, input); // Read entire line of input
    
    stringstream ss(input);
    int num;
    
    // Read numbers from input line
    while (ss >> num) {
        numbers.push_back(num);
    }
    
    // Sort the numbers using insertion sort
    insertionSort(numbers);
    
    for (size_t i = 0; i < numbers.size(); i++) { // Fixed loop condition
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    return 0;
}
