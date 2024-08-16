+++
title = "Today I learnt (TIL): Leetcode Mini Bite Heap and Priority Queue "
author = ["Shweta Kadam"]
date = 2023-08-15T21:24:00+05:30
tags = ["til", "leetcode", "priorityqueue","heap","kthlargest","kthsmallest"]
draft = false
+++

I decided to write a blog after a long time of pondering and no ideas to write anything interesting about. So I just decided to write about leetcode today which Im doing.
Some mini tricks I learnt by doing the problem https://leetcode.com/problems/kth-largest-element-in-a-stream/description/
When the problem asks for kth smallest or kth largest, typically it is supposed to be solved using Heap. 
And for Kth largest element the opposite element (which is smallest in this case is on top).
Typically when one says Heap, we usually remember the tree diagram on google. However when in it comes to solving DS leetcode style problem I found out just using a Priority queue is simply enough.
In Priority Queue, you just add the elements and it gives them a priority and sorts it .

In short,
```
Kth largest --> Min heap --> where smallest element is at top --> Uses Priority queue 
Kth smallest --> Max heap --> where the Largest element is at top --> Uses Priority queue in reverse Order
```
Also 
Priority Queue
- add : when an element cannot be added in queue it throws an exception
- offer : when an element cannot be added in queue it returns false


