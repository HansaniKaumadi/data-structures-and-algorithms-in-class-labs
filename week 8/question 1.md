
![Screenshot 2025-04-15 093817](https://github.com/user-attachments/assets/2c9ba27e-7e49-4a8f-86e9-864f360e2b53)

## C++ Code Implementation

```cpp
#include <cstring>
#include <string>
#include <iostream>
using namespace std;

struct HashTable
{
    int MAX_LENGTH = 3;
    string *passwords = new string[MAX_LENGTH];

    void intialize_hashtable()
    {
        for (int i = 0; i < MAX_LENGTH; i++)
        {
            passwords[i].clear();
        }
    }

    bool isFull()
    {
        bool full = true;
        for (int i = 0; i < MAX_LENGTH; i++)
        {
            if (passwords[i].empty())
            {
                full = false;
            }
        }
        return full;
    }

    int hashfunc(string user_name)
    {
        int sum = 0;
        for (char c : user_name)
        {
            sum += c;
        }
        return sum % MAX_LENGTH;
    }

    bool is_slot_empty(int hash)
    {
        return passwords[hash].empty();
    }

    int insert(string user_name, string user_password)
    {
        int hash = hashfunc(user_name);
        if (is_slot_empty(hash))
        {
            passwords[hash] = user_password;
            return 0; // success
        }
        return 1; // failed due to collision
    }

    int hash_lookup(string user_name)
    {
        int hash = hashfunc(user_name);
        if (!is_slot_empty(hash))
        {
            cout << passwords[hash] << "\n";
            return 0; // found
        }
        return 1; // not found
    }

    int delete_item(string user_name)
    {
        int hash = hashfunc(user_name);
        if (is_slot_empty(hash))
        {
            return 1; // deletion failed
        }
        passwords[hash].clear();
        return 0; // deletion succeeded
    }

    void print_hashtable()
    {
        for (int i = 0; i < MAX_LENGTH; i++)
        {
            cout << "[" << i << "]-->" << passwords[i] << "\n";
        }
    }
};

int main()
{
    HashTable *hashtbl = new HashTable;
    hashtbl->intialize_hashtable();
    cout << hashtbl->isFull() << "\n";

    int command = 0;
    string user_name;
    string password;

    while (command != -1)
    {
        cin >> command;
        switch (command)
        {
        case 1:
            cin >> user_name >> password;
            cout << "Inserting " << user_name << "...\n";
            cout << (hashtbl->insert(user_name, password) ? "Failed" : "Succeeded") << "\n";
            break;
        case 2:
            cin >> user_name;
            cout << "Deleting " << user_name << "...\n";
            cout << (hashtbl->delete_item(user_name) ? "Failed" : "Succeeded") << "\n";
            break;
        case 3:
            cin >> user_name;
            cout << "Looking up " << user_name << "...\n";
            cout << (hashtbl->hash_lookup(user_name) ? "Not found" : "Found") << "\n";
            break;
        case 4:
            hashtbl->print_hashtable();
            break;
        case -1:
            break;
        }
    }
    return 0;
}
