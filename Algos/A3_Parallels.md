Parallels

Implementation of the Parallels project.

The russian version of the task can be found in the repository.


## Contents

1. [Chapter I](#chapter-i) 
    
   1.1. [Introduction](#introduction)
2. [Chapter II](#chapter-ii) 
    
   2.1. [Multithreading](#multithreading) 
    
   2.2. [Mutexes](#mutexes) 
    
   2.3. [Pipeline parallelism](#pipeline-parallelism)
3. [Chapter III](#chapter-iii) 
    
   3.1. [Part 1](#part-1-ant-colony-optimization-algorithm-(ACO))  
    
   3.2. [Part 2](#part-2-solving-systems-of-linear-equations-(SLE))  
    
   3.3. [Part 3](#part-3-winograd-algorithm)


## Chapter I  

![Parallels](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/649023/71083190-7095-36a9-863d-6e80446f0aa6.JPG)

Chuck sat down at the table with such force that the coffee almost spilled out of the cup.

`-` \"You won't believe what I just heard from the IS guy,\" he began, looking around for a waiter. This cafe was a spot that the two of them had been fond of since college. Not crowded, with delicious coffee and desserts. And most importantly, it was always quiet and peaceful there. Perfect for doing your thing, working, or studying, something Eve was doing right now. She was interested in multithreading and paralleling algorithms for a long time.  And now, she had finally found the time to study it properly.

`-` \"So, our \"geniuses\" above managed to lose some dangerous supersmart artificial intelligence,\" Chuck began to whisper. \"I don't know what kind of assassin vacuum cleaner they were making it for, but everyone seems to be in panic. I heard Bob's not himself.\"

`-` \"Sounds serious,\" said Eve, breaking away from her tasks. \"I overheard something like that, too, but Bob didn't seem too frightened. And how do you lose artificial intelligence? It's not like it dropped out of the pocket.\"

`-` \"God knows. What if it ran away on its own? Anyway, it all looks very dirty.  Have you seen our financial reports? I work with it. And things aren't so good there to invest in some innovative robots. I'm telling you, they're secretly building the Terminator.\"

`-` \"Oh, come on,\" said Eve thoughtfully.

`-` \"You'll see,\" Chuck replied distractedly. \"So, what did you order? Mmm, smells good...\"

## Introduction

In this project, you will learn the basic approaches to parallelism, and implement some algorithms applying it.


## Chapter II

### Multithreading

**Synchronous programming** is a programming model where each thread has a set of tasks. All tasks within the thread are executed sequentially, and when one task is completed, it is possible to do another one. In this model you can’t stop the execution of a task in order to perform another one in between.

A special case of synchronous programming is *single-threading*. If there are several tasks to be executed, and the current system provides one thread that can handle all the tasks, then it takes one by one, and the process looks like this:

![singlethreaded](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/649023/0c85fbdb-8afc-33be-a28e-b3d968afae4f.png)

Here you can see that there is a thread and 4 tasks to be executed. The thread starts to execute them one by one and eventually completes them all.

In cases where the order in which the tasks are executed does not affect the result of the program, *Multithreading* can be applied.

Multithreading is another case of the synchronous programming in which there are many threads that can take tasks and start working on them, i.e. we have thread pools and many tasks. 
    
So, multithreading can work like this:

![multithreaded](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/649023/3de208fe-e0c3-3d81-aac6-1462686d8f26.png)

Here you can see that we have 4 threads and just as many tasks to execute, and each thread starts working on them. This is a perfect case, but under normal conditions more tasks are used than the number of available threads, so the freed thread gets another task. 
    
Creating new threads each time is unadvisable, because it requires using additional system resources such as CPU time and memory. So, the initial number of threads should be set in advance.

### Mutexes

When writing multithreaded applications, it is almost always necessary to work with shared data, which can lead to very unpleasant consequences if they are changed at the same time.
To lock shared data from simultaneous access, you need to use *synchronization objects*.

**Mutex** is a mutually exclusive synchronization object. This means that the thread can only receive it one at a time. Mutex is designed for situations where a shared resource can only be used in one of the threads at a time.
Say that the system log is being shared among several processes, but only one of them can save data to the log file at any given time. Mutex is perfect for synchronizing these processes.

Only one bit is needed to describe a mutex, although more often an integer variable is used, where 0 means the unlocked state and all other values correspond to the locked state.

The mutex value is set by two procedures: acquire and release.

1. If a thread is about to enter a critical section, it calls the acquire procedure
2. If the mutex is unlocked, the request is executed, and the calling thread can get into the critical section.
3. If mutex is locked, the thread trying to enter the critical section is locked.
4. If the thread is about to exit the critical section, it calls the release procedure.

The principles of working with mutexes differ between Windows and Linux, but we can highlight the following general steps:
- Create/Describe
- Open/Initialize
- Acquire and wait
- Release

### Pipeline parallelism

The classic way to apply multithreading, in the case when you need to solve the same problem for some *N* sets of input data, is to run the entire algorithm in one thread.  
In this approach, each thread executes the algorithm for *N/(number_of_threads)* sets of input data.

**Pipelining** is generally based on dividing the algorithm to be executed into smaller parts, called stages, and allocating a separate thread to each of them. So the processing of any set of data can be divided into several stages, organizing the transfer of data from one stage to the next. The performance in this case increases due to the fact that at different stages (in different threads) of the pipeline at the same time different sets of data are processed.

An example of the pipeline's work organization:

![pipeline](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/649023/56990344-5441-36e2-84ec-59ebe0863c28.png)

The example is the algorithm for finding the largest number in a string.
The input is an array of strings, for each of which we need to search.
The first thread will split the string into words, the second will convert the words to a numeric data type, and the third will search for the largest among the numbers.
The work process will look like this:
1. The first thread processes the first string in the array. The rest are waiting for their turn.
2. The array of words obtained after processing the 1st string goes to the 2nd thread. Since the first thread is free, it receives the 2nd string for processing.
3. Then the switch between threads 2 and 3 is done in the same way as between threads 1 and 2.
4. If the 2nd string is processed in the 1st thread faster than the 1st string in the 2nd thread, the 2nd string enters the queue waiting for the 2nd thread to release. In the meantime, since the first thread is free, it receives the 3rd string for processing.


## Chapter III

## Part 1. Ant colony optimization algorithm (ACO)

You need to implement an ACO algorithm to solve the traveling salesman problem from the *A2_SimpleNavigator* project with and without parallel computing:
- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Do not use outdated language constructs and libraries
- Provide a Makefile for building the program (with targets all, clean, ant)
- The program must have a console interface
- The user sets the matrix for the traveling salesman problem
- The user sets the number of executions *N*
- Display the results of each of the algorithms for the specified matrix
- Measure the time it takes to execute *N* times an ACO algorithm applying parallelism for a user-defined matrix
- Measure the time it takes to execute *N* times the usual ant algorithm for a user-defined matrix
- Display the obtained time
- Use mutexes to lock access to data for parallel implementation

## Part 2. Solving systems of linear equations (SLE)

You need to implement the usual and parallel algorithms to solve the SLE using the Gaussian elimination method:
- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Do not use outdated language constructs and libraries
- Add to an existing Makefile target called \"gauss\" for building the program
- The program must have a console interface
- The user sets the matrix describing the SLE
- The user sets the number of executions *N*
- Display the results of each of the algorithms for the specified SLE
- Measure the time it takes to execute *N* times a parallel algorithm for solving a user-defined SLE
- Measure the time it takes to execute *N* times the usual algorithm for solving a user-defined SLE
- Display the obtained time
- Use mutexes to lock access to data for parallel implementation

## Part 3. Winograd algorithm

You need to implement the Winograd algorithm of matrix multiplication without using parallelism, as well as using pipeline and classical methods of parallelism:
- The program must be developed in C++ language of C++17 standard
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Do not use outdated language constructs and libraries
- Add to an existing Makefile target called \"winograd\" for building the program
- There should be four stages of the pipeline work
- The program must have a console interface
- There should be two ways of entering:
    - The user sets both matrices for multiplication
    - The user sets dimensions of the matrices, which are then filled into the program randomly
- The user sets the number of executions *N*
- Display the results of each of the algorithms as well as the generated matrices
- Measure the time it takes to execute *N* times matrix multiplication without using parallelism
- Measure the time it takes to execute *N* times matrix multiplication using classical parallelism with the number of threads equal to 2, 4, 8, ..., 4 * (number of logical computer processors)
- Measure the time it takes to execute *N* times matrix multiplication using pipeline parallelism
- Display the obtained time
- Use mutexes to lock access to data for parallel implementation


💡 [Tap here](https://forms.yandex.ru/u/635aa91ac769f120b3a81f17/) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
