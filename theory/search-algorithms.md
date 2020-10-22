# Search algorithms

## Sequential/linear search

* easiest seach algorithm
* we go through each element in the list until the wanted element is found
* the effort grows linear to the amount of elements in the list

## Binary search

* a **sorted** list is necessary
* the middle element is taken and the list is split in two, then we decide if we need to look into the first list or the second list
* this operation is repeated until the lement is found

## Binary search tree

* tree whose internal nodes each store a key greater than all the keys in the node's left subtree and less than those in its right subtree
* we begin by examining the root node (if the tree is null, the key we are searching for does not exist in the tree). If the key is **equal** the the root, we have already found the element we need. If the key is less than the root, we search the left subtree, if it is greater, we search the the right subtree.
* this is repeated until the key is found or the remaining subtree is ```null```. If the searched key is not found after a ```null``` subtree is reached, then the key is not present in the tree.