# Ex.No:5

# Ex.Name: Write the search module of B Tree and find out if the given char is present in the tree or not.

## Date:09/10/2025

## Aim:
To write a C++ function to search a given character in a B-Tree node structure and determine whether it is present in the tree or not.

## Algorithm:
```
1. Start from the root node.
2. Initialize an index `i = 0`.
3. Move through the keys of the node until:

   * `i < n` **and**
   * `key > keys[i]`
4. If `keys[i] == key`, return **true** (key found).
5. If the node is a **leaf**, return **false** (key not present).
6. Else, recursively search in the appropriate child:

   * `child[i]`
7. Continue the above steps until the key is found or a leaf is reached.
```





## Program:
```cpp
void search(char val, int *pos, BTreeNode *myNode) 
{
    if (!myNode) 
    {
    return;
    }

    if (val < myNode->val[1]) 
    {
        *pos = 0;
    }
    else
    {
        for (*pos = myNode->count;(val < myNode->val[*pos] && *pos > 1); (*pos)--);
        if (val == myNode->val[*pos]) 
        {
            cout<<val<<" is found";
            return;
        }
    }
    search(val, pos, myNode->link[*pos]);
    return;
}
```



## Output:
<img width="455" height="259" alt="image" src="https://github.com/user-attachments/assets/8f2142c0-8316-4668-8b78-9637fcc3cebb" />



 ## Result:
Thus, the search() module of the B-Tree was successfully implemented in C++ to check whether a given character is present in the tree or not.

