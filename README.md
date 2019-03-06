# Data Structures and Algorithims

## Node chains
```c#
public class Node
{
    public int Value { get; set; }
    public Node Next { get; set; }
}

Node first = new Node { Value = 3 };
Node middle = new Node { Value = 5};
first.Next = middle;

Node last = new Node { Value = 7 };
middle.Next = last;
```
[3] => [5] => [7] 

## Linked List 
- Single chain of nodes
- Enumerates single direction
- Head pointer
- Tail pointer 
- Operations
  * Add
  * Remove
  * Find
  * Enumerate

### Doubly Linked List
- Single chain of nodes
- Enumerates both directions of list
- Can improve performance characteristics of certain operations

#### Linked List Node
```c#
namespace LinkedList
{
    /// <summary>
    /// A node in the LinkedList
    /// </summary>
    /// <typeparam name="T"></typeparam>
    public class LinkedListNode<T>
    {
        /// <summary>
        /// Constructs a new node with the specified value.
        /// </summary>
        /// <param name="value"></param>
        public LinkedListNode(T value)
        {
            Value = value;
        }

        /// <summary>
        /// The node value
        /// </summary>
        public T Value { get; set; }

        /// <summary>
        /// The next node in the linked list (null if last node)
        /// </summary>
        public LinkedListNode<T> Next { get; set; }
    }
}
```

### Modern Implementations
#### .NET Framework
```c#
using System;
using System.Collections.Generic;

namespace NetFxLinkedList
{
    class Program
    {
        static void Main(string[] args)
        {
            LinkedList<int> list = new LinkedList<int>();
            list.AddLast(3);
            list.AddLast(5);
            list.AddLast(7);

            foreach (int value in last)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```
- `System.Collections.Generic`
- Doubly Linked list
- Common Operations
  * `AddFirst`, `AddLast`
  * `RemoveFirst`, `RemoveLast`
  * `Find`, `FindLast`

#### C++
```c++
#include <iostream>
#include <algorithm>
#include <list>

int main()
{
    std::list<int> list;
    list.push_back(3);
    list.push_back(5);
    list.push_back(7);

    std::for_each(list.begin(), list.end(), [](int value) {
        std:cout << value << std::end1;
    })
}
```
- `#include <list>`
- Doubly Linked list
- Common Operations
  * `push_front`, `push_back`
  * `pop_front`, `pop_back`
  * iterators

#### pros and cons
- Pros
  * No hard size (depth) limit
  * East to implemnt
    * no bounds checking
    * Empty list = Empty stack

## Stacks - Last In, First Out (LIFO)
A stack is a collection in which data is added and removed in the last in first out order (LIFO)

### Modern Implemntations
#### C#
```c#
Stack<int> values = new Stack<int>();

values.Push(10);
values.Push(20);

int twenty = values.Pop()
int ten = values.Pop()
```
- `Stack<T>`
- `Push`, `Peek`, `Pop`
- Items stored in array
#### C++
```c++
std::stack<int> values;

values.push(10);
values.push(20);

int twenty = values.top();
values.pop();

int ten = values.top();
values.pop();
```
- `std::stack<T>`
- `push`, `top`, `pop`
- Items stored in array

## Queue - First In, First Out (FIFO)

#### Queue Array
Cons
- Can be more complicated to implmenet then linked list queues
- Array growth overhead is what makes the implmentation that much more complicated then linked list implmentations

Pros
- Data locality
- Performance gains
- Reducing the overall number of alocations
- Increace enqueue and dequeue times when an allocation is not taking place.

#### Priority Queue
- Highest priority items Dequeued first
  * Not first in, first out
- Allows for prioritization of queued data 

#### Modern Implmentations
- C#
  * Queue<T>
  * Enqueue, Dequeue
  * Implmented as Array
```c#
Queue<int> q = new Queue<int>();

for (int i = 0; i < 10; i++)
{
    q.Enqueue(i);
}

while (q.Count > 0)
{
    Console.WriteLine(q.Dequeue());
}
```
- C++
  * std::queue
  * push, pop, front
  * srd::priority_queue
```c++
std::queue<int> q;

for (int i = 0; i < 10; i++)
{
    q.push(i);
}

while (!q.empty())
{
    std::cout << q.front() << std::end1;
    q.pop();
}
```

## Trees
Top Node Or Head Node Or Root Or Parent
Child Nodes Or Children
Leaf Nodes Or Terminal Nodes

- Any node is capable if linking itself to any arbitrary number of children
- Each node has exactly one parent
- Exactly one node from Top Node to any one child
- In the reverse its a single path from any one child to the Top Node of the tree

### Binary Tree
- Hirarchy of Data
- A Root Node
- 0-2 Children
- Left Child
- Right Child
- Each child is itself a tree
  * Left Child
  * Right Child
- Binary tress have at most two children hence the name Binary Tree

#### Binary Search Tree
- Sorted Hierarchy of Data
- A Root Node
- Left Child
  * Less then parent
- Right Child
  * Greater then parent
- All children follow the same rules

```
        4
       / \
      2    6
     / \  / \
    1  3  5  7

```

#### Adding Data + Searching 
Adding data
- Recursive Algorithm is used when adding data
- In this structure data will align as children on either the left or right path of the parent node depending on value.
- Lower values fall left and higher values fall right

Searching
- Searching in a Binary Tree will allow for more rapid searching and lower resource usage when compared to a linked list
- In a the example above, A search for `8` would check only three nodes using the left or right principle
- Look left for lower values or look right for higher values.

#### Removing Data
Remove
- Find the node toe be deleted
  * If the node does not exist, exit
- Left (terminal) node
  *  Remove parent's pointer to deleted node
- Non-Leaf node
  * Find the child to replace the deleted node
  * Three scenarios

Remove: Case One
- Removed node has no right child
  * Left child replace removed element
  *  The lack of a right child on the removed element indicates that there is no higher value then the parent of the deleted node which will fall between the left node of the deleted node

Remove: Case Two
- Removed Node has right child, that right child has no left child.
  * Right child of removed node take the place of removed node. 
  * Right child that replaced will now become the parent to the left node of the original removed node if exists
  * The data strucutre which enforces left lower right higher

Remove: Case Three
- Removed right child has left child
  * Use the removed right childs left most value as a replacement for the removed value
  * The invariant strucutre will ensure that he lower leftmost value in the tree is the lowest value in the tree. 