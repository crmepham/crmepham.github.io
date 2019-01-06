---
ID: 85
post_title: 'OCAJP revision: What is Garbage Collection?'
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/certification/ocajp/ocajp-revision-what-is-garbage-collection/
published: true
post_date: 2015-05-04 16:29:38
---
Garbage collection (or a garbage collector) is an automatic memory management program that exists as part of .Net's CLR (Common Language Runtime) and Java's Java Virtual Machine (JVM). It's sole purpose is to optimise a programs memory by deleting unreferenced objects and contiguously compacting the remaining objects to enable quick allocation of memory to newly instantiated objects.

In older programming languages, such as C++, garbage collection had to be done manually by the programmer calling an API when they wanted to remove unreferenced objects. This would have been time consuming and the potential for mistakes large, because the developer had to make sure to include a call to a collector each time an object was going out of scope. Also a programmer may manually delete an object when there are other references to it in the program, causing a pointer error, meaning other references to the object exist elsewhere in the program when the memory, previously allocated to this object, has been reallocated.

Garbage collection enables a developer to focus more on developing the features of a program rather than its maintenance. Without the benefit of a garbage collector the chances of a memory leak occuring greatly increase. Memory leaks occur when unreferenced objects are not collected and available memory is gradually limited to the point where it will impact the running and eventual failure of the program when new objects can not be instantiated due to insufficient memory being available.

The first time a minor garbage collection runs, all objects are automatically entered in to the "Eden space". Garbage collection will then check for any unreferenced objects and delete them, it will then add any remaining objects to the first "From" survivor space (S0) and give these objects a number to identify their "age" or the number of times they have survived garbage collection. The next time a minor garbage collection occurs the same process happens with new objects in the "Eden" space but also garbage collection will occur in S0 to check if any unreferenced objects need to be deleted there. Any surviving objects from both Eden and S0 are copied to S1 ("To" Survivor space 2) and aged accordingly.

Garbage collection will continue in this fashion until the referenced objects reach a threshold age, at which point these objects will be copied to the "Tenured" space, or the "old" generation (or generation 2 in .Net). The survivor spaces being the "new" generation, and Eden being the initially allocated space. This is similar to the CLR's 3 generation approach. Eventually major garbage collection will occur which will check for unreferenced objects in all spaces/generations including the Tenured space.

The CLR and JVM both run a collector in a similar way using Generational garbage collection.

The reason for this generational approach to garbage collection is primarily to reduce the time it takes to perform the garbage collection and therefore limit the processing resources necessary when performing garbage collection.

It is assumed that the older the objects the less likely they are to need collecting so they are placed in an older generation/space where they are checked less frequently.

Generally the younger generation objects will be objects created within methods that go out of scope very quickly, and so collected frequently, whereas older generation objects will be static or global objects accessed by the entire program, usually for the entire time the program runs.

A couple of disadvantages to Garbage collection are:

1. The garbage collector will run at random intervals, even if the developer specifically calls the garbage collector it won't necessarily run at that precise time. This unpredictability could mean stalls could occur at inconvenient times which would not be acceptable for real-time applications, such as transactions.

2. The processing overhead that a system must use when garbage collection runs and decides which objects to delete and compacting existing objects to free up memory. A developer must consider the resources necessary to perform efficient garbage collection and ensure optimal performance for general running of the program.

&nbsp;

&nbsp;