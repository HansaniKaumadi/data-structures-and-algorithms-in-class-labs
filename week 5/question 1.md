![Screenshot 2025-04-15 095958](https://github.com/user-attachments/assets/8c6ba1eb-58d1-4896-9938-825b10a23ecf)

![Screenshot 2025-04-15 100013](https://github.com/user-attachments/assets/413c5e17-7640-4da0-82a1-24b3330fe64c)

### C++ Code Implementation

```cpp
#include <iostream>

class Stack {
private:
    int top;        // Index of the top element in the stack
    int stack_size; // Maximum capacity of the stack
    int* arr;       // Dynamic array to store stack elements

public:
    // Constructor to initialize the stack with a given size
    Stack(int size) {
        this->stack_size = size;  // Set the maximum size
        this->arr = new int[size]; // Allocate memory for the stack array
        this->top = -1;  // Set top to -1 to indicate an empty stack
    }

    // Function to add a new element to the stack
    void push(int newData) {  
        this->top++;  // Increment the top index

        // Check for stack overflow
        if (top < stack_size) {  
            arr[top] = newData;  // Store the new element at the top
        } else {
            std::cout << "Stack Overflow" << std::endl;
            this->top--; // Revert the top index
        }
    }

    // Function to remove and return the top element from the stack
    int pop() {  
        // Check if the stack is empty (underflow condition)
        if (top == -1) {  
            std::cout << "Stack Underflow" << std::endl;  
            return -1;  // Return an invalid value
        } else { 
            int previousTop = arr[top];  // Store the top element
            top--;  // Decrement the top index
            return previousTop;  // Return the removed element
        }
    }

    // Function to check if the stack is empty
    bool isEmpty() {  
        return top == -1; // If top is -1, stack is empty
    }

    // Function to check if the stack is full
    bool isFull() {  
        return top + 1 == stack_size; // If top reaches max size, stack is full
    }

    // Function to display all elements from top to bottom
    void display() {  
        if (top == -1) {  // Check if stack is empty
            std::cout << "Stack is empty" << std::endl; 
        } else { 
            for (int i = top; i >= 0; i--) {  // Print elements from top to bottom
                std::cout << arr[i] << " "; 
            }
            std::cout << std::endl;  
        }
    }

    // Function to get the top element of the stack
    int stackTop() {  
        if (top == -1) {
            std::cout << "Stack is empty" << std::endl;
            return -1;  
        }
        return arr[top];  // Return the element at the top
    }
};

int main() {
    Stack myStack(5);
    std::string instruction;

    while (true) {
        std::cin >> instruction;

        if (instruction == "push") {
            int data;
            std::cin >> data;
            myStack.push(data);
        } else if (instruction == "pop") {
            myStack.pop();
        } else if (instruction == "display") {
            myStack.display();
        } else if (instruction == "isEmpty") {
            if (myStack.isEmpty()) std::cout << "True\n";
            else std::cout << "False\n";
        } else if (instruction == "isFull") {
            if (myStack.isFull()) std::cout << "True\n";
            else std::cout << "False\n";
        } else if (instruction == "exit") {
            break;
        } else if (instruction == "stackTop") { 
            std::cout << myStack.stackTop() << std::endl;
        } else {
            std::cout << "Invalid instruction. Valid instructions: push, pop, display, isEmpty, isFull, stackTop, exit.\n";
        }
    }

    return 0;
}

