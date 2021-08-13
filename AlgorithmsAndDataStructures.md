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

Below are screenshots of the new methods and [here](https://github.com/vodsy/BinarySearchTreeProject) is a link to the C++ file.


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

