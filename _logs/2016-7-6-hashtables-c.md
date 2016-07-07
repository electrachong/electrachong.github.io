---
layout: post
section: devlog
title: Hashtables (in C)
---

Last time I wrote about being excited to work on load balancing, but that was actually the project last week that I didn't end up finishing. I was concerned about getting the content to sync using GlusterFS since my server has more than a single repository of code hosted on it, but I ran into a networking issue while trying to get GlusterFS to work. I tried to look into other services and use csync instead, but couldn't seem to satisfy one of the dependencies. I didn't even get to the load balancing part! But I had to move on since we had new projects coming in with the new week. If I have a chance to catch up on missed projects, I might end up going with a classmate's suggestion to use Capistrano (which I already use to deploy code) to deploy to multiple servers at once.

This week we have a new project on hashtables, and were introduced to our new group project at Holberton. The group project involves working in teams of two to make an AirBnB clone. Why AirBnB? Mostly, because it was a convenient service that involves a lot of modules that would be useful for us to learn. Our higher-level track designer, Guillaume, put together a schematic of what we'll be tasked with creating in 8 weeks:

![airbnb clone schematic](https://raw.githubusercontent.com/electrachong/electrachong.github.io/master/images/2016-7-6-hashtables-c/airbnb-clone-schematic.png)

One twist is that we'll be working with features built by other teams, to simulate a start-up environment when you rarely build the entire project yourself. That is, we'll build some features, and other teams will end up using our features, while we are given theirs to build on top of.

Originally, the plan was for us to pitch our own product ideas, and build it in teams of 4-5. There were some tricky aspects to this, but I did like the fact that we were building our own ideas and working in larger teams -- I had a foreboding sense that it would be difficult, but definitely a useful experience to learn from and to talk about when interviewing or meeting recruiters. So, I'm less excited that we are building another clone project (we had done a twitter clone earlier), but I do think we are going to learn some very useful concepts in the process. Apparently, the schematic above is a very typical structure start-ups follow to create apps.

For the hashtables project, I watched [this video](https://www.youtube.com/watch?v=MfhjkfocRR0) recommended by classmates. The low-level programming intern from France, Alex, also put on a brainstorming session, but I wasn't able to absorb much because I was tired from getting up early to make mochi and trying to adjust to a better sleeping schedule. My sister helped catch me up on what I had missed -- it seems like hashtables are used often instead of dictionaries/hashes because instead of having to check every index of the associative array, a hash function is used to determine the exact index a key will be stored at.

So far I've worked on C functions to create a new hashtable and to add a new element (key-value pair contained in a List struct) to the table -- we're not expected to create our own hash function yet, but one was provided as an example. Some little things I ran into:

1) When added nodes to the linked lists, which we are using as suggested by the video to handle collisions, I wasn't actually changing the List pointers in the array to point to the new node. I used some form of `head = new_node` which was effectively just changing the local variable. In the end, I had to pass a pointer to the pointer `(List **head)` so I could dereference and change the address contained in the pointer, e.g. `*head = new_node`. Ah, pointers.

2) One of the tasks was to make sure if the key provided has already been stored in our array of linked lists that we would replace the value with the new one. I was trying to do this by checking `if (current_node->key == key)`, but [you can't really compare strings like that](http://stackoverflow.com/questions/8004237/how-do-i-properly-compare-strings-in-c) in C. We had built strcmp or strncmp ourselves before but that hadn't really clicked for me. I ended up building an is_identical function instead since I'm not really concerned about anything beyond whether the functions or identical (return 1) or not (return 0).

The code I've written for hashtables is viewable here: [https://github.com/electrachong/holbertonschool-low_level_programming/tree/master/hash_tables](https://github.com/electrachong/holbertonschool-low_level_programming/tree/master/hash_tables)
