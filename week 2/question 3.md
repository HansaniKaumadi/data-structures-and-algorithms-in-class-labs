
![Screenshot 2025-04-15 004335](https://github.com/user-attachments/assets/c3ee53ba-a492-443d-a276-68f1523c78a9)

### C++ Code Implementation

```cpp
#include <iostream>
#include <vector>
#include <sstream>

using namespace std;

// Function to perform optimized bubble sort
void optimizedbubbleSort(vector<int>& arr) {
    int n = arr.size();
    bool swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]); // Swap if the element is greater than the next one
                swapped = true;
            }
        }
        if (!swapped) // If no elements were swapped, the array is already sorted
            break;
    }
}

int main() {
    vector<int> numbers;
    string input;
    
    getline(cin, input); // Read entire line of input
    stringstream ss(input);
    int num;
    
    while (ss >> num) {
        numbers.push_back(num);
    }
    
    optimizedbubbleSort(numbers); // Sort the numbers
    
    for (size_t i = 0; i < numbers.size(); i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    return 0;
}
