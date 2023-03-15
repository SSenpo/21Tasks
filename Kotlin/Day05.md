### Hello, dear student!  
Today we’ll speak about high-intensive computations and lengthy requests and how to handle them without harm to a program or user. It’s a common case, when a program has such computations and requests, but if we handle them in the main program thread, we’ll interrupt the main program algorithm and get terrifying UI freezes. Let’s resolve this problem with a very important and interesting feature of Kotlin - coroutines. This is a tool for implementing asynchronous and parallel computing, providing the ability to avoid blocking of main program thread by using a cheaper and more manageable operation: suspending a coroutine.

## Topics:
- coroutines

### Project: add coroutines to the Smart Calculator app

Coroutines play an important role in working with UI. In Android, all UI work happens on the main thread, and blocking it with calculations and lengthy requests will result in screen freezes and a nasty ANR (Application Not Responding) error. To prevent this, we will modernize our project and handle its computation operations by coroutines.

**Advice!** The idea of coroutines is not new, but Kotlin is for sure one of languages where this feature is implemented on excellent level. Also, this theme is deep and not easy for understanding. We'll get acquainted with basic use cases of coroutines, which you can find probably in each Kotlin project: asynchronous computations, requests for data to repositories (DB, network), special scopes for android (viewModelScope). You should approach the issue from different angles: with the official docs, with articles on different resources, with blogs of Kotlin coroutines developers (e.g. Roman Elizarov). You'll find there such important terms, as `suspend` keyword, scopes and coroutine builders, dispatchers, jobs, Deferred and others - try to find information about them from different sources in different words. It might make the theme easier for understanding. 

## Exercises

**Requirement!** Please, make each exercise in a separate project. For example, `Day05/src/exercise1`, `Day05/src/exercise2`, `Day05/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 0: Try coroutines
This is not an obligatory task, but it's very important introduction for better understanding of the topic. In the official Kotlin coroutines documentation, there are a lot of code samples, literally on each term or feature. They are small and work as is. 
- Add coroutines to the android project
- Create a kotlin file and run these samples for entry themes: coroutine basics, cancellation and timeouts, context and dispatchers, 
- Log an every important step to the console - it'll make processes more clear.

### Exercise 1: Smart calculator with coroutines
- Perform all calculations in tools from the project team00 (multi-module app) using coroutines
- For a better understanding, add logging for all actions (inside and outside coroutines) using the Logging module from the team00

### Exercise 2: High intensive calculations
As we get acquainted with coroutines, we can add more highly loaded tasks to our calculator. Let's add a tool that will make for the entered number following calculations:
- Factorial. Starts with a separate button.
- Square and cube root. Both calculations are started with one button and must be performed in parallel using async. The screen displays the result of both calculations at once.
- Logarithms lg and ln. Both calculations are started with one button and must be performed in parallel using async. The screen displays the result of both calculations at once.
- Squaring and cube. Both calculations are started with one button and must be performed in parallel using async. The screen displays the result of both calculations at once.
- Simplicity test. Starts with a separate button.

This tool is a module with its own screen.

**Also:**
- In this task, we will also log all actions.
- There is a button to run all calculations at once (with async construction)
- Calculations can be interrupted at any time. During the calculation, the corresponding button’s text must be changed from “Run” to “Cancel”
- For the simplicity test, add a timeout (there is a suitable mechanism in coroutines) of 1 sec. In case of the timeout error, a dialog \"An error has occurred. Please try again.\" should be displayed

💡 [Tap here](https://forms.gle/pMtRGjqNwKdVrEaC8) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.

