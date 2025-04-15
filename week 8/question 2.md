
![Screenshot 2025-04-15 093859](https://github.com/user-attachments/assets/e824536c-a53e-4524-a120-d66417dade1b)


### C++ Code Implementation

```cpp
#include <iostream>
using namespace std;

struct Node {
    string user_name;
    string password;
    Node* link;
};

struct LinkedList {
    Node* head = NULL;
    Node* tail = NULL;
    int length = 0;

    void insert(string user_name, string password) {
        if (head == NULL) {
            Node* temp = new Node;
            temp->user_name = user_name;
            temp->password = password;
            temp->link = NULL;
            head = temp;
            length++;
        } else {
            Node* temp = new Node;
            temp->user_name = user_name;
            temp->password = password;
            temp->link = NULL;
            Node* tail = head;
            while (tail->link != NULL) {
                tail = tail->link;
            }
            tail->link = temp;
            length++;
        }
    }

    void search(string user_name) {
        Node* temp = head;
        for (int i = 0; i < length; i++) {
            if (temp->user_name == user_name) {
                cout << "Password: " << temp->password << "\n";
                break;
            } else {
                temp = temp->link;
            }
        }
    }

    void print_list() {
        if (head == NULL) {
            cout << "[]" << endl;
        } else {
            Node* temp = head;
            cout << "[";
            while (temp != NULL) {
                cout << temp->user_name << ", ";
                temp = temp->link;
            }
            cout << "]" << endl;
        }
    }
};

struct HashTable {
    int MAX_LENGTH = 3;
    int MAX_CHAIN_LENGTH = 2;
    LinkedList* passwords = new LinkedList[MAX_LENGTH];

    bool isFull() {
        bool full = true;
        for (int i = 0; i < MAX_LENGTH; i++) {
            if (passwords[i].head == NULL) {
                full = false;
            }
        }
        return full;
    }

    int hashfunc(string user_name) {
        int sum = 0;
        for (char c : user_name) {
            sum += (int)c;
        }
        return sum % MAX_LENGTH;
    }

    bool is_slot_empty(int hash) {
        return passwords[hash].head == NULL;
    }

    int insert(string user_name, string user_password) {
        int hash = hashfunc(user_name);
        if (passwords[hash].length >= MAX_CHAIN_LENGTH) {
            return 1; // Failed to insert
        }
        passwords[hash].insert(user_name, user_password);
        return 0; // Success
    }

    void print_hashtable() {
        for (int i = 0; i < MAX_LENGTH; i++) {
            cout << "[" << i << "]-->";
            passwords[i].print_list();
        }
    }

    int hash_lookup(string user_name) {
        int hash = hashfunc(user_name);
        if (is_slot_empty(hash)) {
            return 1; // Not found
        }
        passwords[hash].search(user_name);
        return 0; // Found
    }
};

int main() {
    HashTable* hashtbl = new HashTable;
    cout << hashtbl->isFull() << "\n";

    int command = 0;
    string user_name;
    string password;
    while (command != -1) {
        cin >> command;
        switch (command) {
            case 1:
                cin >> user_name >> password;
                cout << "Inserting " << user_name << "...\n";
                cout << (hashtbl->insert(user_name, password) ? "Failed" : "Succeeded") << "\n";
                break;
            case 2:
                cin >> user_name;
                cout << "Looking up " << user_name << "...\n";
                cout << (hashtbl->hash_lookup(user_name) ? "Not found" : "Found") << "\n";
                break;
            case 3:
                hashtbl->print_hashtable();
                break;
            case -1:
                break;
        }
    }
    return 0;
}
