# 105. Construct Binary Tree from Preorder and Inorder Traversal


[link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```
solution
---------------------------------------------------------------
preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

inOrderIndexMap<Integer, Integer>
process subtree (0, preorder.length, [9,3,15,20,7])
// recursive
----> 1st call 
root of this subtree is preorder[0] = 3
index of 3 in inorder = 1, left [9] | right [15,20,7]
process subtree (0+1, left.length, [9])

----> 2nd call
root of this subtree is preorder[1] = 9
index of 9 in inorder = 0, there are 4 on the right of in order
left [] | right [] 
// these left and right arrays are derived from the inorder array passed in
left and right are both empty, no more recusive call
return to 1st call

----> 1st call
process subtree (left.length+1, right.length, [15, 20, 7])

-----> 3rd call
root of this subtree is preorder[2] = 20
left [15], right [7]
process subtree (2+1, left.length, [15])

-----> 4th call 
root of this subtree is preorder[3] = 15
left [], right []
left and right are both empty , no more recursive call
return to 3rd call

-----> 3rd call
process subtree (3 + left.length, right.length, [7])

----> 5th call
root of this subtree is preorder[ 3 + left.length ] = 7
left [], right []
left and right are both empty, no more recursive call
return to 3rd call

-----> 3rd call
return node 20
return to 2nd call

-----> 2nd call
return node 9 
return to 1st call

-----> 1st call
return node 3

my attempt
--------------------------------------------------------------
axioms:

- for a node B to be a left child of a node A, in preorder it must be [A,B,.....], in inorder it must be [B, A, ....]

- for a node B to be a right child of a node A, in preorder it must be [A, C, B, .....], in in order it must be [A, B, ......]

- every node must be the child node of a node, so at least one of the above axiom will satisfy. Except the root node

--------------------------------------------------------------
preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

indexMap<num, index>
nodeMap<num, TreeNode>

// step through preorder array
-----------------------------------
index -> 0
preorder[i] = 3 is always root

--------------------------------------
index -> 1
preorder[i] = 9 

check if 9 is a left child of anyone using first axiom:
potential parent: preorder[i-1] = 3
if (indexMap.get(3) - 1 == indexMap.get(9) ) {
 //9 is a left child of 3
 nodeMap.get(3).left = nodeMap.get(9);
 continue; // avoid unnessecary if check following
}

check if 9 is a right child of anyone using second axiom:
potential parent = inorder[i-2];
i-2 is out of bound, 9 is not a right child of anyone

-----------------------------------------------
index -> 2
preorder[i] = 20

check if 20 is a left child of anyone using first axiom:
portential parent preorder[i-1] = 9
if (indexMap.get(9) -1 == indexMap.get(20)) {
    
}
not true, 20 is not a left child of anyone

check if 20 is a right child of anyone using second axiom:
potential parent preorder[i-2] = 3
if (indexMap.get(20) - 1 == indexMap.get(3)) {
    // true, 20 is a right child of 3
    nodeMap.get(3).right = nodeMap.get(20);
}


----------------------------------------------
index -> 3
preorder[i] = 15

check if 15 is a left child of anyone using first axiom:
portential parent preorder[i-1] = 20
if (indexMap.get(20) -1 == indexMap.get(15)) {
    //true, 15 is a right child of 20
    nodeMap.get(20).right = nodeMap.get(15);
    continue;
}

check if 20 is a right child of anyone using second axiom:
first axiom already satisfied, for loop continued to next index

---------------------------------------------
index -> 4
preorder[i] = 7

check if 7 is a left child of anyone using first axiom:
potential parent preorder[i-1] = 15
if (indexMap.get(15) -1 == indexMap.get(7)) {
    //false
}

check if 20 is a right child of anyone using second axiom:
potential parent preorder[i-2] = 20
if (indexMap.get(7) -1 == indexMap.get(20)) {
    //true, 7 is a right child of 20
    nodeMap.get(20).right = nodeMap.get(7);
}

--------------------------------------------
return nodeMap.get(preorder[0]);


```


## code

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        HashMap<Integer, Integer> inOrderIndexMap = new HashMap<>();
        for(int i = 0 ; i < inorder.length ;i ++) {
            inOrderIndexMap.put(inorder[i], i);
        }
        
        return helper(0, preorder.length - 1, 0, inorder.length - 1, preorder, inorder, inOrderIndexMap);
    }
    
    TreeNode helper(int preStart, int preEnds, int inStart, int inEnd, int[] preOrder, int[] inOrder, HashMap<Integer, Integer> inOrderIndexMap) {
        // first val is always root of the subtree
        int root = preOrder[preStart];
        
        int indexOfRootInInOrder = inOrderIndexMap.get(root);
        
        int leftLength = indexOfRootInInOrder - inStart; // inorder[indexOfRootInOrder] should not be included, hence no + 1
        int rightLength = inEnd - indexOfRootInInOrder; // inorder[indexOfRootInOrder] should not be included, hence no + 1
        
        TreeNode leftChild = null;
        TreeNode rightChild = null;
        if (leftLength > 0) {
            leftChild = helper(preStart + 1, preStart + leftLength, inStart, indexOfRootInInOrder - 1, preOrder, inOrder, inOrderIndexMap);
        }
        
        if (rightLength > 0) {
            rightChild = helper(preStart + leftLength + 1, preStart + leftLength + rightLength, indexOfRootInInOrder + 1, inEnd, preOrder, inOrder, inOrderIndexMap);
        }
        return new TreeNode(
            root, 
            leftChild,
            rightChild);
    
        
    }
}
    
    
```