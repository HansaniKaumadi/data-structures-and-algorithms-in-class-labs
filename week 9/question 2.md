
![Screenshot 2025-04-15 092927](https://github.com/user-attachments/assets/7dc7058c-66bc-4e32-a9be-382602243667)


## C++ Code Implementation

```cpp
#include <iostream>
#include <list>
using namespace std;

struct Node
{
    // A node will have two entities:
    // 1. An `int` called `label`
    // 2. A `list` of `int`s called `neighbours`
    int label;
    list<int> neighbours;
};

struct Graph
{
    // Graph will have an array of type "Node" with length specified by `n`
    int n = 8;
    Node *nodes = new Node[n];

    void intializenodes()
    {
        // Iterate through the nodes and assign labels
        for (int i = 0; i < n; i++)
        {
            nodes[i].label = i + 1;
        }
    }

    void addedge(int u, int v)
    {
        // For directed edges, only add v to u's neighbor list
        nodes[u - 1].neighbours.push_back(v);
    }

    void print()
    {
        // Iterate through each node and print its neighbours
        for (int i = 0; i < n; i++)
        {
            cout << nodes[i].label << "-->";
            for (auto nd : nodes[i].neighbours)
            {
                cout << nd << " ";
            }
            cout << "\n";
        }
    }
};

int main()
{
    Graph *g = new Graph;
    g->intializenodes();
    
    // Add directed edges from lower to higher numbered nodes
    // in the order to match expected output
    g->addedge(1, 2);
    g->addedge(1, 3);
    g->addedge(1, 5);
    g->addedge(1, 4);
    g->addedge(2, 3);
    g->addedge(2, 6);
    g->addedge(4, 6);
    g->addedge(4, 7);
    g->addedge(4, 8);
    g->addedge(5, 6);
    g->addedge(5, 7);
    g->addedge(5, 8);

    // Print the graph adjacency list
    g->print();
    
    return 0;
}
