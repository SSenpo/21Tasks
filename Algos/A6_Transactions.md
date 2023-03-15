Transactions

Implementation of in-memory key-value store for storing various financial transaction data.

## Contents

1. [Chapter I](#chapter-i) 
    
   1.1. [Introduction](#introduction)
2. [Chapter II](#chapter-ii) 
    
   2.1. [Information](#information)
3. [Chapter III](#chapter-iii) 
    
   3.1. [Part 1](#part-1-implementation-of-in-memory-key-value-store-based-on-a-hash-table)  
   3.2. [Part 2](#part-2-implementation-of-in-memory-key-value-store-based-on-self-balancing-binary-search-tree)  
   3.3. [Part 3](#part-3-implementation-of-the-console-interface)  
   3.4. [Part 4](#part-4-bonus-implementation-of-in-memory-key-value-store-based-on-b-trees)  
   3.5. [Part 5](#part-5-bonus-research-on-temporal-characteristics)

## Chapter I  

![Transactions](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/368087/9a59e644-0057-37ee-be24-476c536354cf.JPG)

It was unusually crowded in the kitchen, as if the entire floor had come to celebrate a colleague’s birthday. Or at
least just to get their piece of the pie. Even Bob was here with his favorite mug. 
    
Eve timidly congratulated the birthday boy, picked up a small plate of apple pie, and hurried back to her desk. She
urgently had to finish a small project on implementing a fast and lightweight data store for the finance department. Bob
kept saying that they didn't have enough people there. So Eve was called to at least partially make up for this
shortage. And while everyone is having fun in the kitchen, she can work in peace and quiet.

`-` \"Bob, I don't even want to think about what happened a year ago,\" an unknown voice suddenly interrupted the silence.

`-` \"So much nerve and money went into putting this incident behind us, and now I find out that we could get something
  worse.\"

`-` \"The ones responsible were punished then and are punished now. We're actively working on the recovery work,\" it was
a familiar voice of the boss. They clearly didn't know that they were not alone. Eve didn't give herself away, too, and
decided to eavesdrop on how the conversation would end.

`-` \"Apparently your punishments have no effect, since history is repeating itself.\"

`-` \"The situation is a little different, after all...\"

`-` \"A little? That's an understatement. So far, it sounds much worse. If last time we got a zombified family that did
whatever the crazy algorithm wanted, what will happen now? I mean, if it only made them buying, say, \"certain\" products,
that's fine, but what did it do? Decided to organize its own \"cult\"?!\"

`-` \"I understand your concern, but this time it's much more under control...\" The sound of voices gradually faded away
towards Bob's office, and it became harder and harder to understand the words. Eve continued to sit still and hardly
breathed even as the voices fell silent, and her colleagues began to return to their desks after a delicious break. She
still had to fully realize what she had just heard...

## Introduction

In this project, you will need to recall and learn more about such data structures as hash tables and self-balancing
binary trees, and implement a key-value store based on them.

## Chapter II

## Information

A key–value store is designed for storing, retrieving, and managing associative arrays. Such a store is implemented in
many programming languages as a container class *dictionary*. Dictionaries contain a collection of objects, or records,
which in turn have many different fields within them, each containing data. These records are stored and retrieved using
a key that uniquely identifies the record, and is used to quickly find the data within the database.

Many NoSQL databases such as Redis, Memcached, Tarantool and many, many others also implement the idea of such store due
to high read and write speeds. Key-value pairs databases support high separability and provide unprecedented horizontal
scaling unattainable with many other types of databases.

![key-value-store](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/368087/2ade4db8-dd66-3cf2-bf5d-ede3ec2f7cb4.png)

Hash tables or search trees are mostly used to implement key-value stores.

#### Hash table

A **hash table** is a data structure that is used when you need to quickly perform insert/delete/find operations. The
speed at which these operations are performed is determined by the hash table structure. They are based on a hashing
function that calculates an index value based on the key passed to it.

Thanks to this function, locating an element in a table by its key is generally performed with complexity O(1), which
does not depend on the size of the hash table itself. The process of obtaining an index by the key is called **hashing**
.

![hash-table](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/368087/6d9b8a88-cb4b-31b3-9d4c-520b50926073.png)

When a hash function generates the same index for several different keys, there is a conflict: it is unclear which value
should be stored in this index. Such situations are called **collisions**.

There are several methods of handling collisions:

- Separate chaining
- Open addressing: Linear probing, Quadratic probing, Double hashing.

Hash tables are used to implement key-value container classes in many programming languages, for example:

* *C#*: Dictionary, ConcurrentDictionary, HashMap
* *Python*: set, map
* *JavaScript*: Map

### Binary search trees

**A binary tree** is a hierarchical data structure in which each node has a value and links to its left and right child.

The highest node (which is not a child of anyone else) is called the root. Nodes that have no children (both children of
which are `NULL`) are called leaves.

**A Binary search tree** is a binary tree with additional properties:

* both subtrees, left and right, are binary search trees
* all nodes in the left subtree of arbitrary node X have key values lesser than the key value of node X itself
* all nodes in the right subtree of arbitrary node X have key values greater than or equal to the key value of node X
  itself.

![binary-tree](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/368087/7e5e3d09-155a-3a39-858d-16a96cf1bf52.png)

As a result, the data in the binary search tree is stored in a sorted order. Each time a new node is inserted, or an
existing node is deleted, the sorted tree order is saved. This makes it possible to formalize the algorithm for
searching items in a binary tree:

* Searching is done by purposeful movement along the tree branches
* If the search key is equal to that of the root, then the key is found, and the value of the node can be returned
* If the search key is less than that of the root, the search proceeds by examining the left subtree, otherwise the
  right one
* If at the next node it is impossible to move further (the pointer is `NULL`), it means that the key you are looking
  for is not in the tree

The maximum search length in this case is equal to the height of the tree.

**Balanced binary search tree** is a binary search tree with logarithmic height. It is used when it is necessary to
perform a quick search for items, alternating with the insertion of new items and the deletion of existing ones. In such
trees, the heights of the two subtrees differ by not more than 1. Examples of self-balancing search trees are the *
red-black trees* or *AVL trees*.

Red-black search trees are used in the data structures of different programming languages, for example:

* *Java*: java.util.TreeMap | java.util.TreeSet
* *C++ STL*: map, multimap, multiset.
* *Linux kernel*: completely fair scheduler, linux/rbtree.h

### B-tree

Main operations in trees are performed in time proportional to its height.

Balanced trees minimize their height (for example, the height of a binary balanced tree with _n_ nodes is _log n_).

What is the problem with these standard search trees? Let's examine a huge database represented in the form of one of
the above-mentioned trees. It is obvious that we can't keep the whole tree in RAM, so we keep only part of the
information in it. The rest is stored on a different medium (say, a hard disk, which is much slower to access). Trees
like red-black or AVL will require _log n_ calls to that medium. If _n_ is large, this is a lot. B-trees are designed to
solve exactly this problem!

B-trees are also balanced trees, so the execution time of standard operations in them is proportional to the height. But
unlike the other trees, they are designed specifically for the efficient use of disk memory, by minimizing the number of
read or write accesses to the disk.

B-trees are used in key-value stores:

* Apache Ignite
* Tokyo Cabinet

### Data structure description

In the key-value store the key will be **strings** and values (data) will be records of School 21 students in the
following form:

* Last name
* First name
* Year of birth
* City
* Number of current coins

### Description of key-value store functions

### SET

This command is used to set the key and its value. In the example below, the key is the string `foo`, and the value is
the structure described above. The values of the new record fields are entered in the order they are described in the
structure. `EX` is used as an optional parameter to specify the lifetime of the record you are creating. If the optional
field is not specified, the record lifetime is not limited by default.

Description of the `SET` command parameters:

```
SET <key> <Last name> <First name> <Year of birth> <City> <Number of current coins> EX <time in seconds>
```

An example of using the `SET` command to create a record with no time limit:

```
SET foo Vasilev Ivan 2000 Moscow 55 
> OK
SET foo Vasilev 123 aaaaa Moscow 55 
> ERROR: unable to cast value \"aaaa\" to type int 
```

An example of using the `SET` command to create a record with a time limit. The record will exist for 10 seconds, and
then it will be automatically deleted:

```
SET foo Vasilev Ivan 2000 Moscow 55 EX 10 
> OK
```

### GET

This command is used to get the value associated with the key. If there is no such record, `(null)` will be returned:

```
GET foo
> Vasilev Ivan 2000  Moscow   55 
GET unknownkey
> (null)
```

### EXISTS

This command checks if a record with the given key exists. It returns `true` if the object exists or `false` if it
doesn't:

```
EXISTS foo
> true
```

### DEL

This command deletes the key and the corresponding value, then returns `true` if the record was successfully deleted,
otherwise `false`:

```
DEL foo
> true
```

### UPDATE

This command updates the value by the corresponding key if such a key exists:

```
SET foo Vas I 20 Mos 5 
> OK
UPDATE foo Vasilev Ivan 2000 Moscow 55 
> OK

GET foo
> Vasilev Ivan 2000 Moscow 55
```

If there is a field that is not planned to change, it is replaced by a dash \"-\":

```
SET foo Vas I 20 Mos 5 
> OK
UPDATE foo Vasilev - - - 55
> OK

GET foo
> Vasilev I 20 Mos 55 
```

### KEYS

Returns all the keys that are in the store:

```
KEYS
1) boo
2) foo
3) bar
```

### RENAME

This command is used to rename keys:

```
RENAME foo foo2
> OK

GET foo
> (null)

GET foo2
> Vasilev I 20 Mos 55
```

### TTL

When the key is set with the time limit, this command can be used to view the remaining time. If there is no record with
the given key, `(null)` will be returned:

```
SET Vasilev Ivan 2000 Moscow 55 EX
10
> OK
TTL foo
> 6
TTL foo
> 5
TTL foo
> 4
TTL foo
> (null)
```

### FIND

This command is used to restore the key (or keys) according to a given value. Similarly to the `UPDATE` command, you
don’t have to specify all the values from the structure of the School 21 students. If any fields will not be searched,
it is replaced by a dash \"-\".

An example of using the `FIND` command to search through all fields of a student structure:

```
FIND Vasilev Ivan 2000 Moscow 55 
> 1) foo
FIND Vasilev Anton 1997 Tver 55
> 1) boo
```

An example of using the `FIND` command to search by last name and number of coins:

```
FIND Vasilev - - - 55
> 1) foo
> 2) boo
```

### SHOWALL

This command is used for getting all records that are in the key-value store at the moment:

```
SHOWALL
> № | Last name |   First name   | Year |  City   | Number of coins |
> 1   \"Vasilev\"       \"Ivan\"       2000  \"Moscow\"         55 
> 2   \"Ivanov\"       \"Vasily\"      2000  \"Moscow\"         55 
```

### UPLOAD

This command is used to upload data from a file. The file contains a list of uploaded data in the format:

```
key1 \"Vasilev\" \"Ivan\" 2001 \" Rostov\" 55
key2 \"Ivanov\" \"Vasiliy\" 2000 \"Москва\" 55 
...
key101 \" Sidorov\" \"Sergei\" 1847 \"Suzdal\" 12312313 
```

Command call:

```
UPLOAD ~/Desktop/TestData/file.dat
> OK 101
```

After the `OK` the number of strings uploaded from the file is displayed.

### EXPORT

This command is used to export the data that are currently in the key-value store to a file. The output of the file must
contain a list of data in the format:

```
key1 \"Vasilev\" \"Ivan\" 2001 \" Rostov\" 55
key2 \"Ivanov\" \"Vasiliy\" 2000 \"Москва\" 55 
...
key101 \" Sidorov\" \"Sergei\" 1847 \"Suzdal\" 12312313 
```

Command call:

```
EXPORT ~/Desktop/TestData/export.dat
> OK 101
```

After the `OK` the number of strings exported from the file is displayed.

## Chapter III

## Part 1. Implementation of in-memory key-value store based on a hash table

You need to implement an in-memory key-value store based on a hash table:

- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Classes must be implemented within the `s21` namespace
- Do not use outdated language constructs and libraries
- Make it as a static library (with a hash_table.h header file)
- The library must be represented as a `HashTable` class, which stores the information in a hash table and contains all
  the necessary methods to implement the functionality described [above] (#description-of-key-value-store-functions). It
  is up to you which hash function and collision resolution method to choose.
- `HashTable` class must be inherited from a base abstract class containing all the methods described [above] (
  # description-of-key-value-store-functions )
- Provide a Makefile for building the library and tests (with targets all, clean, tests, hash_table.a)
- Prepare full coverage of `HashTable` class methods with unit-tests

## Part 2. Implementation of in-memory key-value store based on self-balancing binary search tree

You need to implement an in-memory key-value store based on self-balancing binary search tree:

- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Classes must be implemented within the `s21` namespace
- Do not use outdated language constructs and libraries
- Make it as a static library (with a self_balancing_binary_search_tree.h header file)
- The library must be represented as a `SelfBalancingBinarySearchTree` class, which stores information in the form of a
  self-balancing binary search tree and contains all the necessary methods to implement the functionality
  described [above] (#description-of-key-value-store-functions). It is up to you which type of self-balancing binary
  search tree to choose.
- `SelfBalancingBinarySearchTree` class must be inherited from the same base abstract class as
  in [Part 1](#part-1-implementation-of-in-memory-key-value-store-based-on-a-hash-table), containing all the methods
  described [above](#description-of-key-value-store-functions)
- Add to an existing Makefile target called \"self_balancing_binary_search_tree.a\" for building the library 
- Prepare full coverage of `self_balancing_binary_search_tree.a` class methods with unit-tests

## Part 3. Implementation of the console interface

A console interface must be implemented that provides the user with the following options:

- Initial selection of the store type to be used in the process of running the program:
    - hash table
    - self-balancing binary search tree
- Ability to enter commands described [above](#description-of-key-value-store-functions)

## Part 4. Bonus. Implementation of in-memory key-value store based on B+ trees

You need to implement an in-memory key-value store based on a self-balancing binary search tree:

- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Classes must be implemented within the `s21` namespace
- Do not use outdated language constructs and libraries
- Make it as a static library (with a b_plus_tree.h header file)
- The library must be represented as a `BPlusTree` class, which stores information in the form of a B+ tree and contains
  all the necessary methods to implement the functionality described [above] (#description-of-key-value-store-functions)
  .
- `BPlusTree` class must be inherited from the same base abstract class as
  in [Part 1](#part-1-implementation-of-in-memory-key-value-store-based-on-a-hash-table)
  and [Part 2](#part-2-implementation-of-in-memory-key-value-store-based-on-self-balancing-binary-search-tree),
  containing all the methods described [above](#description-of-key-value-store-functions)
- Add to an existing Makefile target called \"b_plus_tree.a\" for building the library
- Prepare full coverage of `BPlusTree` class methods with unit-tests
- Add to the console interface described in [Part 3](#part-3-implementation-of-the-console-interface) the ability to
  select the B+ tree as the in-memory key-value store

## Part 5. Bonus. Research on temporal characteristics.

Research on temporal characteristics of in-memory key-value store implementations based on a hash table and also a
binary search tree.

- The user sets the number of items in the store
- Data in the store is randomly generated
- The user sets the number of iterations of one operation
- Perform each operation listed below the number of times specified by the user, and then display the average running
  time among the obtained values
- Measure the time for the following operations by both types of stores:
    - Getting an arbitrary item
    - Adding an item
    - Deleting an item
    - Getting a list of all elements in the dictionary
    - Finding the item key by value
- Be prepared to explain the obtained results


💡 [Tap here](https://forms.yandex.ru/u/635ab06ad04688219d2c1920/) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
