![Screenshot 2025-04-15 100033](https://github.com/user-attachments/assets/9b5530c7-7b69-4cd2-a8fd-e2287aae470f)

### C++ Code Implementation

```cpp
#include <iostream>

class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

class Stack {
private:
    Node* top; // Pointer to the top node of the stack

public:
    // Constructor
    Stack() {
        top = nullptr; // Initially, the stack is empty
    }

    // Push operation
    void push(int value) {
        Node* newNode = new Node(value);
        newNode->next = top; // New node points to the old top
        top = newNode; // Update top to the new node
    }

    // Pop operation
    void pop() {
        if (isEmpty()) {
            std::cout << "Stack is empty. Cannot pop.\n";
            return;
        }
        Node* temp = top;
        top = top->next; // Move top pointer to the next node
        delete temp; // Free memory
    }

    // Check if stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Get the top element
    int stackTop() {
        if (isEmpty()) {
            std::cout << "Stack is empty.\n";
            return -1; // Return an error value
        }
        return top->data;
    }

    // Display elements from top to bottom
    void display() {
        if (isEmpty()) {
            std::cout << "Stack is empty.\n";
            return;
        }
        Node* temp = top;
        while (temp) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << "\n";
    }
};

int main() {
    Stack myStack;
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
        } else if (instruction == "stackTop") {
            std::cout << myStack.stackTop() << "\n";
        } else if (instruction == "exit") {
            break;
        } else {
            std::cout << "Invalid instruction. Valid instructions: push, pop, display, isEmpty, stackTop, exit.\n";
        }
    }

    return 0;
}
