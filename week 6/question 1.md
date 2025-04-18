![Screenshot 2025-04-15 095642](https://github.com/user-attachments/assets/08323a7c-0596-4487-aebf-cd1140c3b034)

### C++ Code Implementation

```cpp
#include <iostream>
using namespace std;

struct node {
  int key;
  struct node *left, *right;
};

// Utility function to create a new node
struct node *newNode(int key) {
    struct node *temp = new node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Inorder traversal
void traverseInOrder(struct node *root) {
    if (root != NULL) {
        traverseInOrder(root->left);
        cout << root->key << " ";
        traverseInOrder(root->right);
    }
}

// Insert a node
struct node *insertNode(struct node *node, int key) {
     if (node == NULL) {
        return newNode(key);
    }
    if (key < node->key) {
        node->left = insertNode(node->left, key);
    } else if (key > node->key) {
        node->right = insertNode(node->right, key);
    }
    return node;
}

// Utility function to find the minimum value node in a subtree
struct node *minValueNode(struct node *node) {
    struct node *current = node;
    while (current && current->left != NULL)
        current = current->left;
    return current;
}

// Deleting a node
struct node *deleteNode(struct node *root, int key) {
    if (root == NULL)
        return root;

    if (key < root->key) {
        root->left = deleteNode(root->left, key);
    } else if (key > root->key) {
        root->right = deleteNode(root->right, key);
    } else {
        if (root->left == NULL) {
            struct node *temp = root->right;
            delete root;
            return temp;
        } else if (root->right == NULL) {
            struct node *temp = root->left;
            delete root;
            return temp;
        }
        struct node *temp = minValueNode(root->right);
        root->key = temp->key;
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

// Driver code
int main() {
  struct node *root = NULL;

  int operation;
  int operand;
  cin >> operation;

  while (operation != -1) {
    switch(operation) {
      case 1: // insert
        cin >> operand;
        root = insertNode(root, operand);
        cin >> operation;
        break;
      case 2: // delete
        cin >> operand;
        root = deleteNode(root, operand);
        cin >> operation;
        break;
      default:
        cout << "Invalid Operator!\n";
        return 0;
    }
  }
  
  traverseInOrder(root);
}
