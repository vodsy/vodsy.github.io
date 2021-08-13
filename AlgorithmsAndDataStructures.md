## Algorithms and Data Structures


  The artifact I have chosen for the data structures and algorithms category is a school project on binary search trees. This project contains both a data structure (the binary search tree) and an algorithm (the search function for the binary search tree). The enhancement I chose to make for this was converting the already created, unbalanced binary search tree to a balanced binary search tree. Binary search trees are most commonly used for quick access of data. If this project were to be built upon, deployed, and used consistently there’s a chance the tree would become more and more unbalanced. This would affect the speed of access. Adding a menu option to balance the unbalanced tree will allow users to run a “balancing act” to balance the data structure and optimize lookup times.
  
  The process works by first converting the unbalanced tree to a sorted vector using inorder traversal. The sorted vector is then converted to a balanced tree. Below is the basic pseudocode I used for the recursive solution to building a balanced binary search tree from a sorted vector:

```
Find middle of array
Make middle node the root
Find middle of left half
Make left-middle left child of root
Find middle of right half
Make right-middle right child of root
```

Below are screenshots of the new methods as well as the C++ code.


![image](https://user-images.githubusercontent.com/57910664/129355818-875590c0-8e76-4439-9a15-91fc2843b05f.png)
_Figure 1: Choice number 5 added to convert unbalanced BST to balanced BST_




![image](https://user-images.githubusercontent.com/57910664/129355862-f9f06fb3-2938-49b0-a0e0-2a1219cc71e3.png)
_Figure 2: Choosing option five creates a new node pointer to the root of the already created, unbalanced BST_




![image](https://user-images.githubusercontent.com/57910664/129355908-352becef-cfc2-4b69-b363-744c6b839e1b.png)
_Figure 3: This method creates an empty vector of node pointers, calls the method to store unbalanced BST nodes in the vector in order, and then calls the method to build the balanced BST_




![image](https://user-images.githubusercontent.com/57910664/129355950-fb25ffd6-ff2e-46f1-81ea-e8e2b6059f65.png)
_Figure 4: The method for storing the nodes in order is a simple inorder traversal of the unbalanced BST_




![image](https://user-images.githubusercontent.com/57910664/129355995-dbdff862-07df-41b9-bc2c-c8459e23db2d.png)
_Figure 5: This is the main algorithm that takes the sorted vector and recursively builds a balanced BST_



### C++ Code

```
//============================================================================
// Name        : BinarySearchTree.cpp
// Author      : Jonathan Handy
// Version     : 1.0
// Copyright   : Copyright © 2017 SNHU COCE
// Description : Hello World in C++, Ansi-style
//============================================================================

#include <iostream>
#include <time.h>

#include "CSVparser.hpp"

using namespace std;

//============================================================================
// Global definitions visible to all methods and classes
//============================================================================

// forward declarations
double strToDouble(string str, char ch);

// define a structure to hold bid information
struct Bid {
    string bidId; // unique identifier
    string title;
    string fund;
    double amount;
    Bid() {
        amount = 0.0;
    }
};

// Create internal structure for tree node
struct Node {

	Bid bid;
	Node* left;
	Node* right;
	Node* parent;

	// Create default constructors for nodes
	Node () {
		left = right = parent = nullptr;
	}

	Node (Bid myBid) {
		bid = myBid;
		left = right = parent = nullptr;
	}

};

//============================================================================
// Binary Search Tree class definition
//============================================================================

/**
 * Define a class containing data members and methods to
 * implement a binary search tree
 */
class BinarySearchTree {

private:
    void addNode(Node* node, Bid bid);
    void inOrder(Node* node);
    Node* removeNode(Node* node, string bidId);

public:
    Node* root;
    BinarySearchTree();
    virtual ~BinarySearchTree();
    void InOrder(Node* node);
    void Insert(Bid bid);
    void Remove(string bidId);
    Bid Search(string bidId);
};

/**
 * Default constructor
 */
BinarySearchTree::BinarySearchTree() {

    // initialize housekeeping variables
	root = nullptr;
}

/**
 * Destructor
 */
BinarySearchTree::~BinarySearchTree() {
    // recurse from root deleting every node
}

/**
 * Display the bid information to the console (std::out)
 *
 * @param bid struct containing the bid info
 */
void displayBid(Bid bid) {
    cout << bid.bidId << ": " << bid.title << " | " << bid.amount << " | "
            << bid.fund << endl;
    return;
}

/**
 * Traverse the tree in order
 */
void BinarySearchTree::InOrder(Node* node) {

	if (node == nullptr) {
		return;
	}
	  InOrder(node->left);
	  displayBid(node->bid);
	  InOrder(node->right);
}


/**
 * Insert a bid
 */
void BinarySearchTree::Insert(Bid bid) {
    // Implement inserting a bid into the tree

	// Logic to see if tree exists with a root
	 if (root == nullptr) {
	    root = new Node;
	    root->bid = bid;
	    root->left = nullptr;
	    root->right = nullptr;
	 }
	  else {
		  // Call addNode function if tree already exists
		  addNode(root, bid);
	 }

}

/**
 * Remove a bid
 */
void BinarySearchTree::Remove(string bidId) {
    // Implement removing a bid from the tree
	int key = stoi(bidId);
	Node* cur = root;
	Node* myPointer = nullptr; // Helper variable
	Node* suc = nullptr;



	while (cur != nullptr) { // Search for node
		if (key == stoi(cur->bid.bidId)) { // Node found
			if ((cur->left == nullptr) && (cur->right == nullptr)) {       // Remove leaf
				if (cur->parent == nullptr) { // Node is root
					root = nullptr;
				}
	            else if (cur->parent->left == cur) {
	            	myPointer = cur->parent->left;
	            	cur->parent->left = nullptr;
	            	delete myPointer;
	            }
	            else {
	            	myPointer = cur->parent->right;
	                cur->parent->right = nullptr;
	                delete myPointer;
	            }
				cout << "\nNode with bid ID " << bidId << " has been removed.\n" << endl;
			}
	         else if (cur->left && (cur->right == nullptr)) {    // Remove node with only left child
	            if (cur->parent == nullptr) {// Node is root
	            	myPointer = root;
	                root = cur->left;
	                delete myPointer;
	            }
	            else if (cur->parent->left == cur) {
	            	myPointer = cur;
	                cur->parent->left = cur->left;
	                delete myPointer;
	            }
	            else {
	            	myPointer = cur;
	                cur->parent->right = cur->left;
	                delete myPointer;
	            }
	            cout << "\nNode with bid ID " << bidId << " has been removed.\n" << endl;
	         }
	         else if ((cur->left == nullptr) && cur->right) {     // Remove node with only right child
	            if (cur->parent == nullptr) { // Node is root
	            	myPointer = root;
	                root = cur->right;
	                delete myPointer;
	            }
	            else if (cur->parent->left == cur) {
	            	myPointer = cur;
	                cur->parent->left = cur->right;
	                delete myPointer;
	            }
	            else {
	            	myPointer = cur;
	                cur->parent->right = cur->right;
	                delete myPointer;
	            }
	            cout << "\nNode with bid ID " << bidId << " has been removed.\n" << endl;
	         }
	         else {                                  // Remove node with two children
	            // Find successor (leftmost child of right subtree)
	            suc = cur->right;
	            while (suc->left != nullptr) {
	               suc = suc->left;
	            }
	            cur = suc;                      // Copy successor to current node
	            delete suc;     // Remove successor from right subtree
	            cout << "\nNode with bid ID " << bidId << " has been removed.\n" << endl;
	         }
	         return; // Node found and removed
		}
	      else if (key > stoi(cur->bid.bidId)) { // Search right
	         cur = cur->right;
	      }
	      else {                    // Search left
	         cur = cur->left;
	      }

	}
	cout << "\nNode with bid ID " << bidId << " can not be found.\n" << endl;
	return; // Node not found
}


/**
 * Search for a bid
 */
Bid BinarySearchTree::Search(string bidId) {
    // Implement searching the tree for a bid

	int key = stoi(bidId);
	Node* cur = root;

	while (cur != nullptr) {
	      if (key == stoi(cur->bid.bidId)) {
	         return cur->bid; // Found
	      }
	      else if (key < stoi(cur->bid.bidId)) {
	         cur = cur->left; // Look left
	      }
	      else if (key > stoi(cur->bid.bidId)) {
	         cur = cur->right; // Look right
	      }
	      else {
	    	  cur = nullptr;

	      }

	}
	Bid bid; // Empty bid
	return bid; //Not found, return empty bid
}

/**
 * Add a bid to some node (recursive)
 *
 * @param node Current node in tree
 * @param bid Bid to be added
 */
void BinarySearchTree::addNode(Node* node, Bid bid) {
    // Implement inserting a bid into the tree

	Node* cur = node;

	// Logic to ensure true binary search tree
	while (cur != nullptr) {
		if (bid.bidId < cur->bid.bidId) {
			if (cur->left == nullptr) {
				cur->left = new Node(bid);
				cur->left->parent = cur; //Set parent of new node
				cur = nullptr; // Breaks the while loop
			}
			else {
				// Continues the loop/traversal to find appropriate insert point
				cur = cur->left;
			}
		}
		else {
			if (cur->right == nullptr) {
				cur->right = new Node(bid);
				cur->right->parent = cur; //Set parent of new node
	            cur = nullptr; // Breaks the while loop
			}
	        else {
				// Continues the loop/traversal to find appropriate insert point
	            cur = cur->right;
	        }
		}

	}

}

// Recursive function to construct binary tree with sorted vector
Node* BinarySearchTree::buildBalancedTree(vector<Node*> &nodes, int start, int end) {

    // base case
    if (start > end)
        return NULL;

    // Get the middle element and make it root
    int mid = (start + end) / 2;
    Node *root = nodes[mid];

    // Use in order traversal to build tree
    root->left  = buildBalancedTree(nodes, start, mid-1);
    root->right = buildBalancedTree(nodes, mid+1, end);

    return root;
}

// Function to store nodes in order
void BinarySearchTree::storeNodesInOrder(Node* root, vector<Node*> &nodes) {

    // Base case
    if (root==NULL)
        return;

    // Store nodes in order
    storeNodesInOrder(root->left, nodes);
    nodes.push_back(root);
    storeNodesInOrder(root->right, nodes);

}

// Function to convert unbalanced BST to balanced BST
Node* BinarySearchTree::ConvertUnbalancedToBalanced(Node* root) {

    vector<Node*> nodes;
    storeNodesInOrder(root, nodes);

    // Constuct balanced BST from sorted nodes vector
    int n = nodes.size();

    return buildBalancedTree(nodes, 0, n-1);

}



//============================================================================
// Static methods used for testing
//============================================================================

/**
 * Load a CSV file containing bids into a container
 *
 * @param csvPath the path to the CSV file to load
 * @return a container holding all the bids read
 */
void loadBids(string csvPath, BinarySearchTree* bst) {
    cout << "Loading CSV file " << csvPath << endl;

    // initialize the CSV Parser using the given path
    csv::Parser file = csv::Parser(csvPath);

    // read and display header row - optional
    vector<string> header = file.getHeader();
    for (auto const& c : header) {
        cout << c << " | ";
    }
    cout << "" << endl;

    try {
        // loop to read rows of a CSV file
        for (unsigned int i = 0; i < file.rowCount(); i++) {

            // Create a data structure and add to the collection of bids
            Bid bid;
            bid.bidId = file[i][1];
            bid.title = file[i][0];
            bid.fund = file[i][8];
            bid.amount = strToDouble(file[i][4], '$');

            //cout << "Item: " << bid.title << ", Fund: " << bid.fund << ", Amount: " << bid.amount << endl;

            // push this bid to the end
            bst->Insert(bid);
        }
    } catch (csv::Error &e) {
        std::cerr << e.what() << std::endl;
    }
}

/**
 * Simple C function to convert a string to a double
 * after stripping out unwanted char
 *
 * credit: http://stackoverflow.com/a/24875936
 *
 * @param ch The character to strip out
 */
double strToDouble(string str, char ch) {
    str.erase(remove(str.begin(), str.end(), ch), str.end());
    return atof(str.c_str());
}

/**
 * The one and only main() method
 */
int main(int argc, char* argv[]) {

    // process command line arguments
    string csvPath, bidKey;
    switch (argc) {
    case 2:
        csvPath = argv[1];
        bidKey = "98385";
        break;
    case 3:
        csvPath = argv[1];
        bidKey = argv[2];
        break;
    default:
        csvPath = "eBid_Monthly_Sales_Dec_2016.csv";
        bidKey = "98385";
    }

    // Define a timer variable
    clock_t ticks;

    // Define a binary search tree to hold all bids
    BinarySearchTree* bst;

    Bid bid;

    int choice = 0;
    while (choice != 9) {
        cout << "Menu:" << endl;
        cout << "  1. Load Bids" << endl;
        cout << "  2. Display All Bids" << endl;
        cout << "  3. Find Bid" << endl;
        cout << "  4. Remove Bid" << endl;
        cout << "  5. Convert Unbalanced to Balanced" << endl;
        cout << "  9. Exit" << endl;
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {

        case 1: {
            bst = new BinarySearchTree();

            // Initialize a timer variable before loading bids
            ticks = clock();

            // Complete the method call to load the bids
            loadBids(csvPath, bst);

            //cout << bst->Size() << " bids read" << endl;

            // Calculate elapsed time and display result
            ticks = clock() - ticks; // current clock ticks minus starting clock ticks
            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;
            break;
        }

        case 2: {
        	Node* node = bst->root;
            bst->InOrder(node);
            break;
        }

        case 3: {
            ticks = clock();

            bid = bst->Search(bidKey);

            ticks = clock() - ticks; // current clock ticks minus starting clock ticks

            if (!bid.bidId.empty()) {
            	cout << endl;
                displayBid(bid);
            } else {
            	cout << "\nBid Id " << bidKey << " not found.\n" << endl;
            }

            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;

            break;
        }

        case 4: {
            bst->Remove(bidKey);
            break;
        }

        case 5: {
            Node* unbalancedRoot = bst->root;
            ConvertUnbalancedToBalanced(unbalancedRoot);
        }
        }
    }

    cout << "Good bye." << endl;

	return 0;
}
```
