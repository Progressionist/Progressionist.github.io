---
title: "week 2"
draft: true
---
### I. Stacks and Queues
#### 1. Stack: Linkedlist Implementation
Stacks and Queues and both represented by either linked-list or array. Below is the linked list class, and linked list 
representation of stack:

    class Node(object):
        def __init__(self, data=None, next_node=None):
            self.data = data
            self.next_node = next_node
    
        def get_data(self):
            return self.data
    
        def get_next(self):
            return self.next_node
    
        def set_next(self, new_next):
            self.next_node = new_next


     class LinkedListStack:
        def __init__(self):
            self.first = Node(None, None)
    
        def push(self, item):
            old_first = copy.deepcopy(self.first)
            self.first = Node(item, None)
            self.first.next_node = old_first
            self.print_stack()
    
        def pop(self):
            self.first = self.first.next_node
            self.print_stack()
    
        def is_empty(self):
            return False if self.first.get_data() else True
    
        def print_stack(self):
            res = ""
            node = copy.deepcopy(self.first)
            while node.get_data():
                res += (node.get_data() + " ")
                node = node.next_node
            print res
            
The key idea of linked list stack is that each time we push one item, it will be the new "first" node, the 
previous first node will now be the "next_node" of the new first node. Whenever we want to pop an item, we just
make the next node of current first node the new first node.

#### 2. Stack: Resizing Array Implementation:
In array implementation, one big draw back is that we have to pre-set the size of the array which is not smart enough.
Therefore, whenever the size of the stack is larger than what we initialized, we increase the size of the array. The method
is we make a new array with new size, and then copy everything in the old array into the new one. The problem with
this approach is that everytime we push one item, we need to make a new array. A better approach is double the size of the
array whenever we reach the limit of the array. Similarly, when we the array is half full, we can shrink the array size
to avoid using too much of the memory. Intuitively, we can halve the size when the array is half full. But the worst case
if we push-pop-push, the array size will be doubling-halving-doubling, which is called "thrashing". This is too expensive.
So instead, we only halve the array size when it's one-quater full. So in summary:

**Resizing:**

1. When array is full, double the size
2. When array is one quater full, halve the size


#### 3. Queue


#### 4. Dijkstra's Two Stack Algorithm

### II. Elementary Sorts

#### 1. Selection Sort

#### 2. 