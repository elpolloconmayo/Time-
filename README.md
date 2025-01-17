# Time travel, Advanced Data Structure

The Time Travel problem in the context of data structures refers to the ability to modify and query the state of a data structure at different points in time, both in the past and in the present. This problem is addressed by retroactive data structures, which allow operations to be performed that affect not only the current state of the structure, but also its history of operations.

Persistence looks like:

![Persistence.](https://github.com/elpolloconmayo/Time-Travel-Queue/blob/main/images/persistent.png)

Retroactive Data structures allow to add, remove, or modify operations that were performed in the past, and the structure will automatically update to reflect these changes. In this case, we allow that by storing separatedly different actions and get the values combining these.

## Current implementation (WIP)

In this implementation, we merge the implementation of Erik Demaine at https://youtu.be/WqCWghETNDc?si=tRViaFba89L1pA3o and the implementation shown by Mitko Nikov at https://youtu.be/m2yRawZGYXk?feature=shared .

Disclaimer: this was made purely to have fun and isn't complete.

"Queue" is a Fully retroactive data structure that supports the following operations:
- Insert an element at a given time.
- Delete an element at a given time.
- Get the element at a given time.
- Get the size of the structure at a given time.
- Get the size of the structure at the current time.
- Undo a operation at a given time. (if it is possible) WIP

![implementation.](https://github.com/elpolloconmayo/Time-Travel-Queue/blob/main/images/curr_implementation.png)

To make this possible, we use a OST as a base to work, in this case the OST is a RB Tree, but can be any tree, The OST is modified according to it's use:
- adding, this OST only contains the operation of adding an element at a given index, stores index and value.
- deleting, this OST only contains the operation of deleting an element at a given index, only stores the index.
- consistency, this OST contains all the operations of adding and deleting elements, and is used to check the consistency of the structure. (stores index, +1 for adding and -1 for deleting)

## Future Work

- to check consistency we make a fully traversal of the tree, this **CAN'T be optimized by storing the size of the tree in each node** as the check should be _inorder_, due to this, a better approach could be to implement a 4th structure that only point's to bridges (like a simple list that stores indexes), or maybe another structure for the consistency tree, like a skiplist would work.
- **fix the undo operation** (in tested enviroment looks fine, with random values there's some bug that I couldn't find)
- benchmark in a better way pop, front and undo operations
- better OST implementation, this one isn't a mess but could be better, AA tree could be a good choice, Tango Tree would be an astonishing choice.

## some questionable benchmarks

![push.](https://github.com/elpolloconmayo/Time-Travel-Queue/blob/main/images/push.png)

![pop.](https://github.com/elpolloconmayo/Time-Travel-Queue/blob/main/images/pop.png)

push seems linear, pop may be N*log(N)?

## some scribble notes

before coding, I made a notebook to try to understand the problem, here it is

![implementation.](https://github.com/elpolloconmayo/Time-Travel-Queue/blob/main/images/notes.png)
