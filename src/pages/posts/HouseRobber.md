---
title: "House Robber Leetcode "
description: "This tutorial is about solving the House Robber Problem using Dynamic Programming."
pubDate: "July 31 2023"
heroImage: "/posts-jpg/houserobber.jpg"
layout: ../../layouts/BlogPost.astro

---

## **Solving the House Robber Problem using Dynamic Programming**
<br>

## **Introduction**
<br>


The House Robber problem is a classic dynamic programming problem where a thief aims to maximize the amount of money they can rob from a row of houses without robbing adjacent houses due to a security system. In this blog post, we'll explore an efficient solution to this problem using dynamic programming and Python.

## **Understanding the Solution**

### **Step 1: Function Signature**
<br>


```python
class Solution:
    def rob(self, nums):
        # Function implementation here
```
<br>

### **Step 2: Initialize Variables**  

<br>

```python
rob1, rob2 = 0, 0
```
<br>

We begin by initializing two variables, **rob1** and **rob2**, to keep track of the maximum loot obtained after robbing the previous and current houses, respectively.

### **Step 3: Dynamic Programming Loop**  
<br>


```python
for n in nums:
    temp = max(rob1 + num, rob2)
    rob1 = rob2
    rob2 = temp
```
<br>

Next, we use a loop to iterate through the input list **nums**, representing the amount of money in each house. At each step, we calculate the maximum loot that can be obtained by either robbing the current house (**n**) along with the loot obtained after robbing the house before the previous one (**rob1**) or skipping the current house and taking the loot from the previous house (**rob2**).

### **Step 4: Dynamic Programming Update**
<br>

```python
temp = max(rob1 + num, rob2)
rob1 = rob2
rob2 = temp
```
<br>

To update **rob1** and **rob2**, we use a temporary variable **temp** to hold the maximum loot value. We calculate **temp** as the maximum between robbing the current house (**rob1 + num**) and not robbing it (**rob2**). After the update, **rob1** is set to the previous value of **rob2**, and **rob2** is set to the value of **temp**.
<br>

### **Step 5: Return the Result**
<br>

```python
return rob2
```

Finally, after the loop finishes, we return the value of **rob2**, which holds the maximum loot that the thief can obtain by robbing the houses in a non-adjacent manner.
<br>

## **Conclusion**
<br>

In this blog post, we've explored an efficient solution to the House Robber problem using dynamic programming. By keeping track of the maximum loot obtained after robbing each house, we can find the maximum amount of money that the thief can rob without breaking any security rules. The solution has a time complexity of O(n) and a space complexity of O(1), making it an optimal and scalable approach for this problem.
<br>

**Note:** Remember to initialize **rob1** and **rob2** to zero before starting the loop and update **rob1** and **rob2** appropriately within the loop to obtain the correct result. The solution has been implemented in Python for ease of understanding and readability.