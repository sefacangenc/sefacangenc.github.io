---
title: "Implementing a Least Recently Used (LRU) Cache in Python"
description: "This blog post explains the LRU cache replacement policy and provides a step-by-step guide on how to implement it in Python. The post is aimed at developers who want to learn more about caching and LRU cache implementation in Python. By the end of the post, readers will have a clear understanding of LRU cache and be able to apply this knowledge to their own projects."
pubDate: "Apr 06 2023"
heroImage: "/LRU-cache.png"
---


In this post, we will be implementing an LRU cache in Python. We will use a doubly linked list to keep track of the order in which the keys were accessed, and we will use a hash table to provide O(1) access to the key-value pairs.

Designing the LRU Cache Class
First, let's design the LRU cache class. We will name it LRUCache, and it will have the following methods:

- __init__(self, capacity): Initializes the LRU cache with a positive size capacity.
* get(self, key): Returns the value of the key if it exists in the cache, otherwise returns -1.
+ put(self, key, value): Updates the value of the key if it exists in the cache. Otherwise, adds the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evicts the least recently used key.
To implement the LRU cache, we will use a hash table to provide O(1) access to the key-value pairs. We will also use a doubly linked list to keep track of the order in which the keys were accessed. The head of the linked list will represent the least recently used node, and the tail of the linked list will represent the most recently used node.

Here is the code for the Node class that we will use to represent each node in the linked list:

```python
class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

```

The Node class has four attributes: key, val, prev, and next. The key and val attributes represent the key and value of the key-value pair that the node is associated with. The prev attribute is a pointer to the previous node in the linked list, and the next attribute is a pointer to the next node in the linked list.

Next, let's implement the LRUCache class:
```python

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        node = self.cache[key]
        self._remove(node)
        self._add(node)
        return node.val

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            node = self.cache[key]
            node.val = value
            self._remove(node)
            self._add(node)
        else:
            if len(self.cache) == self.capacity:
                del self.cache[self.head.next.key]
                self._remove(self.head.next)
            node = Node(key, value)
            self.cache[key] = node
            self._add(node)

    def _remove(self, node):
        prev = node.prev
        next = node.next
        prev.next = next
        next.prev = prev

    def _add(self, node):
        p = self.tail.prev
        p.next = node
        node.prev = p
        node.next = self.tail
        self.tail.prev = node
        
```

The _add and _remove functions are private helper methods of the LRUCache class that are used to manipulate the doubly linked list that maintains the order of the keys in the cache.

The _add function adds a given node to the end of the linked list. Here's how it works:

1. Get the previous node (p) of the tail node (self.tail).
2. Set the next pointer of the previous node (p.next) to the new node.
3. Set the prev pointer of the new node (node.prev) to the previous node (p).
4. Set the next pointer of the new node (node.next) to the tail node (self.tail).
5. Set the prev pointer of the tail node (self.tail.prev) to the new node.
6. Here's the code for the _add function:

```python
def _add(self, node):
    p = self.tail.prev
    p.next = node
    node.prev = p
    node.next = self.tail
    self.tail.prev = node
```

The _remove function removes a given node from the linked list. Here's how it works:

1. Get the previous node (p) and the next node (n) of the given node.
2. Set the next pointer of the previous node (p.next) to the next node (n).
3. Set the prev pointer of the next node (n.prev) to the previous node (p).
4. Here's the code for the _remove function:

```python
def _remove(self, node):
    p = node.prev
    n = node.next
    p.next = n
    n.prev = p
```

Together, the _add and _remove functions allow us to maintain the order of the keys in the cache by efficiently adding and removing nodes from the doubly linked list.


Finally, we'll implement the LRUCache class that uses the above functions to implement the LRU cache.

```python
class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add(node)
            return node.value
        return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
        node = Node(key, value)
        self.cache[key] = node
        self._add(node)
        if len(self.cache) > self.capacity:
            node = self.head.next
            self._remove(node)
            del self.cache[node.key]

    def _add(self, node):
        p = self.tail.prev
        p.next = node
        node.prev = p
        node.next = self.tail
        self.tail.prev = node

    def _remove(self, node):
        p = node.prev
        n = node.next
        p.next = n
        n.prev = p

class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None
```
The LRUCache class has a constructor that initializes the cache with the given capacity. It also initializes an empty cache dictionary, a size variable that keeps track of the current number of nodes in the list, and dummy head and tail nodes that mark the beginning and end of the list.

The get method retrieves the value of a key from the cache, and returns -1 if the key does not exist. If the key exists, it removes the node from its current position in the list and adds it to the end of the list, marking it as the most recently used node.

The put method sets the value of a key in the cache, and removes the least recently used node if the cache is at capacity. If the key already exists in the cache, it removes the node from its current position in the list, updates its value, and adds it to the end of the

