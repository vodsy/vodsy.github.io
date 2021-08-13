## Algorithms and Data Structures


  The artifact I have chosen for the data structures and algorithms category is a school project on binary search trees. This project contains both a data structure (the binary search tree) and an algorithm (the search function for the binary search tree). The enhancement I chose to make for this was converting the already created, unbalanced binary search tree to a balanced binary search tree. Binary search trees are most commonly used for quick access of data. If this project were to be built upon, deployed, and used consistently there’s a chance the tree would become more and more unbalanced. This would affect the speed of access. Adding a menu option to balance the unbalanced tree will allow users to run a “balancing act” to balance the data structure and optimize lookup times.
  The process works by first converting the unbalanced tree to a sorted vector using inorder traversal. The sorted vector is then converted to a balanced tree. Below is the basic pseudocode I used for the recursive solution to building a balanced binary search tree from a sorted vector:

'''
Find middle of array
Make middle node the root
Find middle of left half
Make left-middle left child of root
Find middle of right half
Make right-middle right child of root
'''

Below are screenshots of the new methods. I will also attach the .cpp file in the submission.
