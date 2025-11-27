
# Ex.No:1

# Ex.Name: Write the Insert Module of the BPlus Tree in CPP
## Date: 09/10/2025
## Aim:
To write a C++ module to perform insertion of keys into a B+ Tree, ensuring node splitting and proper propagation of keys according to B+ Tree rules.

## Algorithm:
```
1. Start the insertion process.
2. If the tree is empty, create a new leaf node and insert the key.
3. Traverse from the root to the appropriate **leaf node** where the key must be inserted.
4. Insert the key into the leaf node in sorted order.
5. If the leaf node does not overflow, stop.
6. If the leaf node overflows:

   * Split the leaf node into two nodes.
   * Move half of the keys to the new leaf node.
   * Promote the **first key of the new leaf** to the parent internal node.
7. If the parent internal node overflows:

   * Split the internal node.
   * Promote the middle key to the parent node.
8. If splitting reaches the root, create a new root.
9. End the insertion process.
```
## Program:
```cpp
void BPTree::insert(int x)
{
    if (root == NULL) 
    {
        root = new Node;
        root->key[0] = x;
        root->IS_LEAF = true;
        root->size = 1;
    }
    else
    {
        Node *cursor = root;
        Node *parent;
        while (cursor->IS_LEAF == false)
        {
            parent = cursor;
            for (int i = 0; i < cursor->size; i++)
            {
                if (x < cursor->key[i])
                {
                    cursor = cursor->ptr[i];
                    break;
                }
                if (i == cursor->size - 1)
                {
                    cursor = cursor->ptr[i + 1];
                    break;
                }
            }
        }
        if (cursor->size < MAX)
        {
            int i = 0;
            while (x > cursor->key[i] && i < cursor->size)
                i++;
            for (int j = cursor->size; j > i; j--)
            {
                cursor->key[j] = cursor->key[j - 1];
            }
            cursor->key[i] = x;
            cursor->size++;
            cursor->ptr[cursor->size] = cursor->ptr[cursor->size - 1];
            cursor->ptr[cursor->size - 1] = NULL;
        } 
        else
        {
            Node *newLeaf = new Node;
            int virtualNode[MAX + 1];
            for (int i = 0; i < MAX; i++)
            {
                virtualNode[i] = cursor->key[i];
            }
            int i = 0, j;
            while (x > virtualNode[i] && i < MAX)
                i++;
            for (int j = MAX + 1; j > i; j--)
            {
                virtualNode[j] = virtualNode[j - 1];
            }
            virtualNode[i] = x;
            newLeaf->IS_LEAF = true;
            cursor->size = (MAX + 1) / 2;
            newLeaf->size = MAX + 1 - (MAX + 1) / 2;
            cursor->ptr[cursor->size] = newLeaf;
            newLeaf->ptr[newLeaf->size] = cursor->ptr[MAX];
            cursor->ptr[MAX] = NULL;
            for (i = 0; i < cursor->size; i++)
            {
                cursor->key[i] = virtualNode[i];
            }
            for (i = 0, j = cursor->size; i < newLeaf->size; i++, j++)
            {
                newLeaf->key[i] = virtualNode[j];
            }
            if (cursor == root)
            {
                Node *newRoot = new Node;
                newRoot->key[0] = newLeaf->key[0];
                newRoot->ptr[0] = cursor;
                newRoot->ptr[1] = newLeaf;
                newRoot->IS_LEAF = false;
                newRoot->size = 1;
                root = newRoot;
            }
            else
            {
                insertInternal(newLeaf->key[0], parent, newLeaf);
            }
        }
    }
}
```


## Output:
<img width="649" height="445" alt="image" src="https://github.com/user-attachments/assets/baa24511-f5fa-44dd-8cf4-d865ec738b3e" />


## Result:
The C++ module successfully implements the insert operation of a B+ Tree.

