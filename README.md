# Linked Lists
This is a collection of different linked lists data structures for use in other C++ projects

### General documentation:
- ```empty()```: Returns true when there are no nodes in the list, ```O(1)```
- ```size()```: Returns the number of nodes in the list, ```O(1)```
- All lists deallocate memory when they go out of scope, or have an element remove, so there will be no memory leaks

Below is documentation for each of the included data structures

## CLinkedList
Circularly Linked List: the last node in the list points to the first node.

definition for individual CNodes:
```
template <typename T>
struct CNode
{
    CNode<T> *next = nullptr;
    T elem;
};
```

For all of the below functions except for ```clear()```: O(n) complexity is in reference to the passed argument. For instance, runtime of ```at(i)``` will be proportional to ```i```. The complexity of ```at(0)``` would be O(1). The complexity of all methods are independent of the size of the list, except for ```clear()```.

```cursor``` in this context refers to the current position in the list, and ```front``` refers to 'cursor->next'. 

- ```insert(CNode<T> *node, const int& i)```: Inserts a new node i nodes in front of the cursor, O(n)
    - insert(node, 0) would make 'node->next' become 'cursor->next', and 'cursor->next' would become 'node'
    - if the list is empty, this will make 'cursor = node', for any value of i
    - since the list is circular, i can be any value, even greater than the list's size. This will just insert the node at 'i % size'.

- ```insert(const T& elem, const int& i)```: Creates a new CNode whose element is 'elem', inserts the node at i, O(n)

- ```insert_front(CNode<T> *node)```: calls 'insert(node, 0)', O(1)
- ```insert_front(const T& elem)``` calls 'insert(elem, 0), O(1)

- ```set(const int& i, const T& elem) const```: Sets the element of the node i spaces away from the front to the given element, O(n)
    - The list is circular, so i can be any positive value, even greater than the list's size. The modified node will be at ```i % size```.
    - set(elem, 0) will make 'cursor->next->elem = elem'

- ```remove(CNode<T> *node)```: removes a given node from the list, and deallocates the node's memory O(1)
    - If there is only one node in the list, makes the list empty
    - removes the node FOLLOWING the specified node; ```remove(cursor)``` would remove 'cursor->next' from the list.
    - calling this function with a nullptr, or a node where 'next == nullptr' will cause a segmentation fault.

- ```remove(const int& i)```: finds the node i nodes from the front, and calls 'remove(node)', O(n)
    - calling this function on an empty list will cause a segmentation fault

- ```remove_front()```: calls 'remove(0)', O(1)
    - calling this function on an empty list will cause a segmentation fault

- ```at(const int& i) const```: returns a pointer to the node i nodes away form the front, O(n)
    - The list is circular, so i can be any value, the returned pointer will be at ```i % size```
    - calling this function on an empty list will cause a segmentation fault

- ```front() const```: returns the element at the front of the list, calls 'at(0)->elem', O(1)

- ```operator[](const int& i)```: Use the '[]' operator as you would for an array, it will return the element i nodes form the front. Returns 'at(i)->elem'. O(n)
    - calling this function on an empty list will cause a segmentation fault

- ```clear()```: removes all nodes from the list, and deallocates their memory, O(n)

- ```advance(const int& i = 1)```: advances the cursor by i nodes, O(n)
    - calling this function with no parameters will make 'cursor = cursor->next', essentially advancing the 'front' of the list by one node O(1).
    - setting i to any non-negative int will make 'cursor = cursor->next' i times.
    - calling this function on an empty list will cause a segmentation fault