s21_memory

Developing an implementation of the memory management library.  

The russian version of the task can be found in the repository.


## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [Introduction](#introduction)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Information](#information)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Part 1](#part-1-implementation-of-the-s21_memory-library) 
    
    3.2. [Part 2](#part-2-bonus-search-by-free-cells) 
    
    3.3. [Part 3](#part-3-bonus-defragmentation) 

## Chapter I  

![s21_memory](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/70c42e13-8da0-324b-91ad-fb433c59487f.JPG)

There was only one thing left to do before being promoted to the position of a Middle Developer: to implement a small project that replicated the behavior of the standard memory library in the C language, so dearly loved by Eve. When Bob gave her the task, she couldn't believe her luck. She was familiar with malloc and free implementations since reading Kernighan and Ritchie's book. So no wonder Eve immediately rushed to her desk, even though she had plenty of time to do the task.

Walking down the corridors of SIS Head Office, Eve couldn't help but note to herself that all departments were working hard and the company was vibrant. For example, the PR department in the meeting room was loudly developing an advertising strategy for the window-washing robot.  Another SIS innovation that must have had everyone lined up for it, from glass skyscraper owners to housewives who collect a line of smart helpers that are used, at best, a couple of times a year. The \"freedom development\" department, as it is called jokingly among the employees, has been actively working on the latest hinges that would improve durability. The finance department... monitored and multiplied the company's finances. The information security ran back and forth through the corridors and floors of the office. In the last few weeks the amount of their work has increased rapidly.

Not far from the reception hung a myriad of diplomas and awards that the company's products had won: \"Best Robot Vacuum Cleaner of the Year,\" or \"Smartest Clothes Dryer,\" or simply \"Refrigerator of the Year\". SIS, which gained its popularity a couple of decades ago partly due to high-quality and cheap home appliances, today created everything you can possibly imagine, with the prefix \"smart\", which was unconditionally bought up by its loyal customer base. For young minds like Eve, SIS was an opportunity to become a skilled employee and gain invaluable experience, even though the company has changed a lot since its heyday.

After leaning back in her chair and reflecting for a while, Eve came back to reality and moved quickly to the task.

## Introduction

In this project you will learn the algorithms for allocating and freeing memory and write your own implementation of the *malloc*, *calloc*, *realloc* and *free* functions.


## Chapter II

## Information

### Memory blocks

Usually in higher-level programming languages we deal with objects that have structure, fields, methods, etc.

However, from a memory allocator perspective, which works at a lower level, an object is represented simply as a block of memory. All we know is that this block has a certain size, and its contents, being opaque, are treated as a raw sequence of bytes. At runtime this memory block can be casted to a needed type, and its logical layout may differ based on this casting.

Memory allocation is always accompanied by the memory alignment, and creation of an object header. The header stores meta-information related to each object, and which serves the purposes of an allocator, and collector.

The memory block will combine the object header, and the actual payload pointer, which points to the address of the user data. This pointer is returned to the user on allocation request.

The header tracks the size of an object, and whether this block is currently allocated — the used flag. On allocation it’s set to `true`, and on the free operation it’s reset back to `false`, so can be reused in the future requests.
In addition, the linked list of all available blocks has fields pointing to the next and previous blocks. 

Here is a picture of how the blocks look in memory (but there is no pointer to the previous block):

![Memory_Blocks](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/274a120d-e098-34d3-b0fe-37d172f43bd6.png)

The objects A, and C are in use, and the block B is currently not used.

Since this is a linked list, there must be variables tracking the start and the end (the top) of the heap.

### Memory alignment

As mentioned, when allocating a memory, we don’t make any commitment about the logical layout of the objects, and instead work with the size of the block.

For faster access, a memory block should be aligned, and usually by the size of the machine word.

Here is the picture of how an aligned block with an object header looks like:

![Alignment-Header](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/e5bdf7ee-54e5-3781-bbbe-8d87d8da8d4d.png)

It means that if a user requests to allocate, say, 6 bytes, we actually allocate 8 bytes. Allocating 4 bytes can result either to 4 bytes — on 32-bit architecture, or to 8 bytes — on x64 machine.

### Blocks splitting

Simply using a block of the appropriate size may not be effective if a found block is much larger than the requested one.

We will now implement a procedure of splitting a larger free block, taking from it only a smaller chunk, which is requested. The other part stays free, and can be used in further allocation requests.

Here is an example:

![Block-split](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/e77c5567-2a35-3f19-8814-f0573859a923.png)

### Blocks coalescing

If we have two adjacent blocks in the heap of size 8, and a user requests a block of size 16, we can’t satisfy an allocation request. Let’s take a look at another optimization for that case.

On freeing the objects, we can do the opposite to splitting operation, and coalesce two (or more) adjacent blocks to a larger one.

Here is an example:

![Blocks-coalescing](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/eb911ed9-32c8-357f-b8b3-bc547004df42.png)

### Function description

| № | Function | Description |
| ------ | ----------------------------------------------------- | ------ |
| 1 | `void *malloc (size_t size)` | The `malloc` function allocates a `size` byte memory block and returns a pointer to the beginning of the block. The contents of the allocated memory block are not initialized; they remain with undefined values. If it fails, it returns a null pointer. | 
| 2 | `void *calloc (size_t num, size_t size)` | The `calloc` function allocates a block of memory to an array of `num` elements, where each element is of `size` bytes, and initializes all its bits with zeros. As a result, a block of `num * size` bytes is allocated, and the whole block is filled with zeros. It returns a pointer to the beginning of the block; if it fails, it returns a null pointer. |
| 3 | `void *realloc(void *ptr, size_t size)` | The `realloc` function reallocates memory blocks. The size of the memory block pointed to by the `ptr` is changed to `size` bytes. A memory block can decrease or increase in size. This function can move the memory block to a new location, in which case the function returns a pointer to the new memory location. The contents of the memory block are maintained even if the new block is smaller than the old one. Only the data that does not fit into the new block is discarded. If the new `size` value is larger than the old one, the contents of the newly allocated memory will be undefined. Returns a pointer to the beginning of the block, with the original `ptr` pointer becoming invalid and any access to it being undefined behavior. In case of an error it returns a null pointer and the original `ptr` pointer remains valid. |
| 4 | `void free (void* ptr)` | The `free` function frees the memory space. A block of memory previously allocated by calling `malloc`, `calloc` or `realloc` is released. That means that the freed memory can be further used by programs or the OS. Note that this function leaves the value of `ptr` unchanged, so it still points to the same memory block and not to a null pointer. |
### Explicit free-list

The easiest way to find free cells is a linear search, i.e. the analysis of each block, one by one.
A more efficient algorithm would be using an explicit free-list, which links only free blocks.

![Explicit-free-list](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356291/7fe34ac6-4626-3f99-988f-1d9a352e9526.png)

This might be a significant performance improvement, when the heap is getting larger, and one needs to traverse a lot of objects in the basic algorithms.

Such a list can be implemented directly in the object header. For this the `next`, and `prev` pointers would point to the free blocks. Procedures of splitting and coalescing should be updated accordingly, since `next`, and `prev` won’t be pointing to adjacent blocks anymore.
Alternatively, you can create a separate additional free-list.

### Fragmentation

Fragmentation happens when free blocks in the heap are not on adjacent positions.
In this situation, it will not be possible to allocate more memory than the size of each of the free blocks, even if their total size is sufficient.

Defragmentation is reallocation of blocks in the heap, as a result of which data is overwritten in a continuous area.
In this way all free blocks are merged into one, the size of which is equal to the sum of their sizes.

## Chapter III

## Part 1. Implementation of the s21_memory library

You need to implement the functions of the stdlib.h library described [above](#function-description):
- The program must be developed in C++ language of C++17 standard 
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Do not use outdated language constructs and libraries
- Use the prefix s21_ for each function
- Make it as a static library (with a s21_memory.h header file)
- Copying the implementation of the standard library is forbidden
- Provide a Makefile for building the library and tests (with targets all, clean, tests, s21_memory.a)
- Take into account memory alignment, block splitting and coalescing, and possible error situations when implementing functions
- Your functions must not work with the system memory, but with the memory allocated to the heap in the program itself. For this purpose, a dynamic array is created in the program, the memory for which is allocated by the standard function `malloc`.
- A console interface must be implemented that allows the user to:
    - Initialize a heap of size _N_ bytes (the current heap, if there is one, is freed)
    - Call functions `s21_malloc`, `s21_calloc`, `s21_realloc`, `s21_free` with corresponding parameters (displaying the addresses returned by the functions)
    - Write the value in the address specified by the user. In this case the user specifies:
        - Address for writing the value
        - Data type (Only `int`, `double` and `char` are considered)
        - If the value is an array
        - The value itself (in the case of an array, its length and elements)
        - *To be able to display the written value on the screen, create a field in the memory block into which you are writing. That field should contain the data type of the current value.  In cells where type hasn’t yet been specified, consider it as `char` array*
    - Output the current state of the heap (address, contents, size and state (free or occupied) of each block).
Output format:
```
0x2f7b1a0
    Content: [15, 25, -401]
    Size: 16
    State: 1
0x2f7b1b0
    Content: 4.44
    Size: 8
    State: 0
0x2f7b1b8
    Content: [-1024, 127]
    Size: 8
    State: 1
0x2f7b1c0
    Content: ['a', 'a', 'a', 'b', 'a', 'a', 'a', 'o', 'o', 'a', 'a', 'a', 'b', 'a', 'a', 'a']
    Size: 16
    State: 0
```
 
## Part 2. Bonus. Search by free cells

You need to write functions `s21_malloc_onlyfree`, `s21_calloc_onlyfree`, `s21_realloc_onlyfree`, `s21_free_onlyfree` that search for a suitable block only by free blocks.
Add to the interface a research option to optimize the search for free blocks:
1. Two heaps of 1,000,000 bytes are allocated for the research
2. All calls of `s21_malloc` and `s21_malloc_onlyfree` functions occur with a parameter of 10 bytes
3. Call the `s21_malloc` function for the first heap 100,000 times, i.e. the heap should consist entirely of occupied blocks.
4. Call the `s21_malloc_onlyfree` function for the 2nd heap 100,000 times, i.e. the heap should consist entirely of occupied blocks
5. The user sets the number (in percent) of free blocks in the heap
6. In both heaps, random cells are freed so that the number of free cells becomes equal to the user-specified one
7. Measure the time it takes to fill the first heap completely with occupied blocks again by successive calls of the `s21_malloc` function
8. Measure the time it takes to fill the second heap completely with occupied blocks again with successive calls of the `s21_malloc_onlyfree` function
9. Display the results on the screen
 
## Part 3. Bonus. Defragmentation
 
Write a `s21_defragmentation` function that defragments the current heap:
- Add the ability for the user to call this function

💡 [Tap here](https://forms.yandex.ru/u/635aae8beb61461bfd7defae/) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
