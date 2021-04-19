---
layout: post
title: Garbage Collector for Nodes in C++
description: >
  bbb
hide_image: false
accent_color: '#4fb1ba'
accent_image:
  background: 'linear-gradient(to bottom,#193747 0%,#233e4c 30%,#3c929e 50%,#d5d5d4 70%,#cdccc8 100%)'
  overlay:    true
---

Hey lads, so I've been on working **Data Structures** for quite while & I created some **node structures** as **template classes** like, **Singly & Doubly linked-lists**, etc.

After playing with these structures, I realized that they perform some very expensive operations like **allocation** & **deallocation** of **nodes/memory**. Means each time when user decides to **push** or **pop** a **node**, the **compiler** makes request to **OS (Operating System)** for allocation/deallocation, which makes the process slower on the back-end.

Recently, I found out that **Java** has the concept of **Garbage Collectors** for such scenarios. So, I thought why not implement in **C++**? And then, I added this really cool concept in my node classes. Also, it's really powerful technique to boost your program for long run.

The working Concept is simple. Each time we want to pop a node, we do not deallocate the node/memory. Instead we transfer it to a **static Garbage Collector**. So, later if someone wants to push a **new node**, we can reuse that transferred node from Garbage Collector. In this way, we don't have to deal with extra **OS requests** (I.e. using **new/ delete** keywords).

But, here comes another problem, the program will gradually increase in size as its not releasing nodes/memory on the back-end. So I came with a solution that if size of Garbage Collector increases to **max_capacity** (i.e. variable) then it deallocates the **half of the total nodes** currently present in GC.

**P.S:** In Doubly Linked List class, this Garbage Collector works even more efficiently as each time a **class object** of a type gets destroyed, it nodes are transferred to GC at **O(1)** Complexity, whereas in Singly, its **O(n)**.

[**Source Code Folder Link**](https://github.com/HypertextAssassin0273/Data_Structures_in_Cpp/tree/main/Native_Data_Structures/Contiguous_Structures)