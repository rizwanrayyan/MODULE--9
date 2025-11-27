# Ex.No:4

# Ex.Name:Write the findMin module of the B tree in CPP.

## Date:09/10/2025

## Aim:
To write a C++ function to find and return the minimum value stored in a B-Tree node structure.

## Algorithm:
```
1. Start from the root node.
2. Check if the current node is a **leaf**:

   * If yes → the minimum key is the first key of this node.
3. If the node is not a leaf:

   * Move to the **leftmost child** (child index 0).
   * Repeat the process until reaching a leaf node.
4. Return the first key from the leaf node as the minimum value.
```




## Program:
```cpp
void findMin(BTreeNode *myNode)
{
    BTreeNode *curr=myNode;
    while(curr->link[0]!=NULL)
    {
        curr=curr->link[0];
    }
    cout<<endl<<"Min="<<curr->val[1];
}
```


## Output:
<img width="584" height="216" alt="image" src="https://github.com/user-attachments/assets/6ef6bcc0-eeb1-4d61-af43-95b3fe916e4d" />



 ## Result:
Thus, the findMin() module of the B-Tree was successfully implemented in C++ to locate the minimum key by traversing to the leftmost leaf node.

