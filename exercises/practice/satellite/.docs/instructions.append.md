# Instructions append

## Post-order

`TREE_NODE` also needs an iterator, `postorder!`, that yields the tree's values in post-order: the left subtree in post-order, then the right subtree in post-order, and then the node's own value.

For the tree above, `postorder!` yields `i`, `f`, `r`, `x`, `a`.

An iterator may call itself.
Inside `postorder!`, `l.postorder!` walks the left subtree, and `loop yield l.postorder! end` passes each value it yields on to the loop that called the outer `postorder!`.
