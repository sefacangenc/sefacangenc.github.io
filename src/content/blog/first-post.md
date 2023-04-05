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

```{python}
class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

```

The Node class has four attributes: key, val, prev, and next. The key and val attributes represent the key and value of the key-value pair that the node is associated with. The prev attribute is a pointer to the previous node in the linked list, and the next attribute is a pointer to the next node in the linked list.

Next, let's implement the LRUCache class:
```{python}

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
```

Now let's move on to the _remove function.

The _remove function is responsible for removing a node from the doubly linked list. It takes in a node as an argument and removes it from the list. Here's the code for the _remove function:

```{python}
def _remove(self, node):
    """
    Remove an existing node from the linked list.
    """
    prev = node.prev
    new = node.next
    prev.next = new
    new.prev = prev
```


The _remove function takes in a node as an argument and assigns its predecessor and successor nodes to prev and new, respectively. It then updates the next and prev pointers of these nodes to remove the node from the list.

Finally, we'll implement the LRUCache class that uses the above functions to implement the LRU cache.

```{python}
class LRUCache:
    def __init__(self, capacity: int):
        """
        Initialize LRUCache.
        """
        self.cache = {}
        self.capacity = capacity
        self.size = 0
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        """
        Retrieve item from provided key. Return -1 if nonexistent.
        """
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add(node)
            return node.value
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        """
        Set the value if the key is not present in the cache. If the cache is at capacity remove the oldest item.
        """
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            node.value = value
            self._add(node)
        else:
            if self.size == self.capacity:
                del self.cache[self.head.next.key]
                self._remove(self.head.next)
                self.size -= 1
            node = Node(key, value)
            self.cache[key] = node
            self._add(node)
            self.size += 1

    def _add(self, node):
        """
        Add new node right after the dummy head.
        """
        p = self.tail.prev
        p.next = node
        node.prev = p
        node.next = self.tail
        self.tail.prev = node

    def _remove(self, node):
        """
        Remove an existing node from the linked list.
        """
        prev = node.prev
        new = node.next
        prev.next = new
        new.prev = prev
```




The LRUCache class has a constructor that initializes the cache with the given capacity. It also initializes an empty cache dictionary, a size variable that keeps track of the current number of nodes in the list, and dummy head and tail nodes that mark the beginning and end of the list.

The get method retrieves the value of a key from the cache, and returns -1 if the key does not exist. If the key exists, it removes the node from its current position in the list and adds it to the end of the list, marking it as the most recently used node.

The put method sets the value of a key in the cache, and removes the least recently used node if the cache is at capacity. If the key already exists in the cache, it removes the node from its current position in the list, updates its value, and adds it to the end of the