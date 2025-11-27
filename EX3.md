# Ex.No:3

# Ex.Name: Write the fixup module of the red black tree in CPP.

## Date: 09/10/2025
## Aim:
To write a C++ function to perform the Fixup operation of a Red-Black Tree after insertion by applying recoloring and rotations to maintain Red-Black Tree properties.

## Algorithm:
```
1. Start with the newly inserted node `pt`.
2. While `pt` is not the root and both `pt` and its parent are RED:

   * Identify the parent and grandparent nodes.
   * If parent is a left child:

     * If the uncle is RED → recolor parent, uncle, and grandparent.
     * Else if `pt` is the right child → perform **Left Rotate** on parent.
     * Perform **Right Rotate** on grandparent and swap colors.
   * Else if parent is a right child:

     * If uncle is RED → recolor parent, uncle, and grandparent.
     * Else if `pt` is the left child → perform **Right Rotate** on parent.
     * Perform **Left Rotate** on grandparent and swap colors.
3. After all adjustments, set the root color to **BLACK**.
4. Stop.
```
## Program:
```cpp
void fixup(node* root, node* pt)
{
    node* parent_pt = NULL;
    node* grand_parent_pt = NULL;
 
    while ((pt != root) && (pt->c != 0) && (pt->p->c == 1))
    {
        parent_pt = pt->p;
        grand_parent_pt = pt->p->p;
        /*  Case : A Parent of pt is left child of Grand-parent of pt */
        if (parent_pt == grand_parent_pt->l)
        {
            node* uncle_pt = grand_parent_pt->r;
            /* Case : 1 The uncle of pt is also red Only Recoloring required */
            if (uncle_pt != NULL && uncle_pt->c == 1)
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
            else
            {
                /* Case : 2 pt is right child of its parent Left-rotation required */
                if (pt == parent_pt->r) 
                {
                    leftrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
                /* Case : 3 pt is left child of its parent Right-rotation required */
                rightrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
        /* Case : B Parent of pt is right child of Grand-parent of pt */
        else 
        {
            node* uncle_pt = grand_parent_pt->l;
            /*  Case : 1 The uncle of pt is also red Only Recoloring required */
            if ((uncle_pt != NULL) && (uncle_pt->c == 1))
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
            else 
            {
                /* Case : 2 pt is left child of its parent Right-rotation required */
                if (pt == parent_pt->l) 
                {
                    rightrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
                /* Case : 3 pt is right child of its parent Left-rotation required */
                leftrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
    }
    root->c = 0;
}
```



## Output:
<img width="801" height="615" alt="image" src="https://github.com/user-attachments/assets/20abf9a9-c029-4237-a82b-c3624349367d" />



 ## Result:
Thus, the fixup module of the Red-Black Tree was successfully implemented using recoloring and rotation operations to maintain tree balance after insertion.

