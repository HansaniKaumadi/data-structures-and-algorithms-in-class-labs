
![Screenshot 2025-04-15 004321](https://github.com/user-attachments/assets/6dba1381-2d3a-49e0-8131-8ed4f02d8582)

### C++ Code Implementation

```cpp
#include <iostream>
#include <vector>
#include <sstream>

using namespace std;

// Function to perform bubble sort
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]); // Swap if the element is greater than the next one
            }
        }
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
    
    bubbleSort(numbers); // Sort the numbers
    
    for (size_t i = 0; i < numbers.size(); i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    return 0;
}
