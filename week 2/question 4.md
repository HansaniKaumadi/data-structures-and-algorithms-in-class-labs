
![Screenshot 2025-04-15 004509](https://github.com/user-attachments/assets/e239b45a-a386-4c6d-8f9a-7a7fa80a61cb)

### C++ Code Implementation

```cpp
#include <iostream>
#include <vector>
#include <sstream>

using namespace std;

// Function to perform selection sort
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]); // Swap the found minimum element with the first element
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
    
    selectionSort(numbers); // Sort the numbers
    
    for (size_t i = 0; i < numbers.size(); i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    return 0;
}
