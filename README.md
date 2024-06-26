# Balance-a-Binary-Search-Tree

Given the root of a binary search tree, return a balanced binary search tree with the same node values. If there is more than one answer, return any of them.

A binary search tree is balanced if the depth of the two subtrees of every node never differs by more than 1.

Example 1:

Input: root = [1,null,2,null,3,null,4,null,null]
Output: [2,1,3,null,null,null,4]
Explanation: This is not the only correct answer, [3,1,4,null,2] is also correct.

Example 2:

Input: root = [2,1,3]
Output: [2,1,3]
 
Constraints:

The number of nodes in the tree is in the range [1, 104].
1 <= Node.val <= 105

# Explaination #

# Intuition
The task is to transform a given Binary Search Tree (BST) into a balanced BST. A balanced BST ensures that the depth of the two subtrees of every node never differs by more than one. To achieve this, the approach involves converting the BST into a sorted array (via in-order traversal) and then constructing a balanced BST from this sorted array.

# Approach
1) In-Order Traversal:
Perform an in-order traversal of the given BST to retrieve the node values in a sorted manner.
This is because an in-order traversal of a BST yields a sorted sequence of node values.

2) Sorted Array to Balanced BST:
Utilize the sorted array obtained from the in-order traversal to construct a balanced BST.
Recursively pick the middle element of the current segment of the array to ensure that the tree is balanced. The middle element becomes the root, and the left and right halves of the array become the left and right subtrees, respectively.

Step-by-Step:

i)   Define a list to store the nodes in the sorted order.
ii)  Traverse the BST using in-order traversal and populate the list.
iii) Use a helper function to convert the sorted list into a balanced BST.
         * The base case is when the start index is greater than the end index, returning null.
         * Calculate the middle index of the current segment.
         * Create a tree node with the middle element.
         * Recursively construct the left and right subtrees using the left and right segments of the array, respectively.
         
# Complexity

Time Complexity:-

In-Order Traversal: O(N), where N is the number of nodes in the BST. This is because each node is visited exactly once.
Constructing Balanced BST: O(N), as each node from the sorted array is visited once to create the new tree.
Overall time complexity: O(N).

Space Complexity
In-Order Traversal: O(N), to store the nodes in a list.
Constructing Balanced BST: O(log N), due to the recursion stack depth (height of the balanced tree).
Overall space complexity: O(N) (dominated by the space used to store the nodes in the list).


# JAVA CODE

class Solution {

    public TreeNode balanceBST(TreeNode root) {
    
        inOrder(root);
        
        return bst(0, ordered.size() - 1);
    }
    
    private TreeNode bst(int start, int end) {
    
        if (start > end) return null;
        
        else if (start == end) {
        
            TreeNode ret = ordered.get(start);
            
            ret.left = null;
            
            ret.right = null;
            
            return ret;
        } else {
        
            int mid = start + (end - start) / 2;
            
            TreeNode ret = ordered.get(mid);
            
            ret.left = bst(start, mid - 1);
            
            ret.right = bst(mid + 1, end);
            
            return ret;
        }
    }
    
    private void inOrder(TreeNode node) {
        if (node == null) return;
        
        inOrder(node.left);
        
        ordered.add(node);
        
        inOrder(node.right);
    }
    
    private List<TreeNode> ordered = new ArrayList<>();
}
