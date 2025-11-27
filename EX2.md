
# Ex.No:2

# Ex.Name: Write the Splay/BST construction module of splay tree in CPP.

## Date: 09/10/2025

## Aim:
To write a C++ module to construct a Splay Tree by inserting nodes using standard Binary Search Tree (BST) insertion followed by splaying the newly inserted node to the root.

## Algorithm:
```
1. Start the insertion process.
2. If the tree is empty, create a new node and set it as root.
3. Insert the new key in the tree following normal **Binary Search Tree (BST)** rules.
4. After insertion, **splay** the newly inserted node by performing appropriate rotations:

   * **Zig Rotation**: Node is child of root.
   * **Zig-Zig Rotation**: Node and parent are both left children or both right children.
   * **Zig-Zag Rotation**: Node is left child of right parent or vice-versa.
5. Continue rotations until the inserted node becomes the **root**.
6. Stop the process.
```




## Program:
```cpp
node *BST(node *root, int key)
{
    if(root==NULL)
    {
        node *newnode = new node;
        newnode->key = key;
        newnode->left = NULL;
        newnode->right = NULL;
        
        return newnode;
    }
    else
    {
        if(root->key > key)
        {
            root->left = BST(root->left,key);
        }
        else
        {
            root->right = BST(root->right,key);
        }
    }
    return root;
}
```


## Output:

<img width="983" height="362" alt="image" src="https://github.com/user-attachments/assets/79f91c3d-82f5-4d6f-9a5e-eccb158a1ebc" />



##  Result:
The module successfully constructs a Splay Tree by performing BST insertion followed by splaying the inserted node to the root using Zig, Zig-Zig, and Zig-Zag rotations.

