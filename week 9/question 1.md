
![Screenshot 2025-04-15 092818](https://github.com/user-attachments/assets/a65199c5-08cf-42b1-8428-bb91037a38e4)


![Screenshot 2025-04-15 092904](https://github.com/user-attachments/assets/bee6fed6-aec8-4f6b-ae50-749f0995adb5)

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
        // Select node `u` and push `v` into `u`'s neighbour list
        // Select node `v` and push `u` into `v`'s neighbour list
        nodes[u - 1].neighbours.push_back(v);
        nodes[v - 1].neighbours.push_back(u);
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

    // Add the edges for the graph
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
