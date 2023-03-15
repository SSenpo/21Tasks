### Hola, dear student, welcome to your first Kotlin project!

Here we have to get acquainted with the main features of this wonderful language, which was released quite recently and has already conquered the whole world of mobile development!

**Kotlin** is a statically typed, multi-paradigm programming language and, as conceived by the authors, it is more type-safe and concise than Java. At the same time, it has a number of interesting solutions and a sea of syntactic sugar to facilitate the development and support of projects.

The most interesting features of Kotlin are **Null-safety**, **Extensions** and **Coroutines**. You will have time to work with each of them in the learning process.
Every year, Kotlin finds more and more widespread use and penetrates into various areas of commercial and scientific activities. For example:
- Kotlin is commonly used in the development of applications for the Android platform which was declared as Kotlin-first by Google in 2019 (before there was Java).
- Language developers decided not to stop at one mobile platform and are developing Kotlin Multiplatform technology to create cross-platform projects (Android, iOS, Web).
- Kotlin can be found on the server side
- It is used in Data Science
- Can be transpiled to JavaScript
  And wherever possible... But at the moment it is primarily a mobile :)

# Themes
Right now we will get acquainted with the basics of the language, recall how the common things work and stretch our fingers. Main topics are:
- Data types
- Operators, loops, conditions
- Using program arguments

**Advice!** Read about these topics the official Kotlin documentation. It's a good handbook, but not too wordy, and if you need a better explanation in simpler terms, search for articles written by developers on different media resources

In the Code samples folder you can find a primitive Kotlin project, generated with a new project constructor in IntelliJ Idea (File -> New -> New Project, choose Kotlin language).

### Project: Smart calculator 
Let's consider the basic capabilities of the language using the example of a simple monolithic project, which is a set of tools for solving various applied problems.

# Exercises

**Requirement!** Please, make each exercise in a separate project. For example, `Day00/src/exercise1`, `Day00/src/exercise2`, `Day00/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one. 

### Exercise 0: New project
In IntelliJ Idea, start creating a new project: 
- Choose Kotlin language
- Choose Gradle build system
- Choose a JDK or if none exist click \"Download\" and choose the one of version 18
- The project mustn't contain sample code

**Advice!** In our projects we'll use Gradle build system. You should read some articles about different build systems and the official documentation about Gradle.

### Exercise 1: Circles
Develop a mathematical module that determines if two given circles intersect or not.
- There are two circles on the coordinate plane: the first one is centered at the point (x1, y1) with radius r1, the second one is centered at the point (x2, y2) with radius r2.
- The program reads coordinates and radius for both circles one by one, see an example below
- The program works with floating point numbers
- The program determines if these circles intersect, touch or do not intersect and outputs it as the result. In the case of absorption of one circle by another, it outputs \"One circle is inside another\". _See an example below_
- The program doesn't fail on incorrect input. It writes \"Couldn't parse a number. Please, try again\" and repeats input for the failed parameter

_Example:_
  ```
  Input x1:
  0
  Input y1:
  0
  Input r1:
  3
  Input x2:
  4
  Input y2:
  4
  Input r2: 
  3
  Result: the circles intersect
  ```

### Exercise 2: Prime numbers
Develop a prime numbers module that works with the given number consisting of an arbitrary amount of digits. It has to receive a number and create a set of numbers out of it according to the following rules:
- The first number is equal to the units digit
- The second is made up of the units and tens digits
- Hundreds are added to the third
- Etc. For example, 4835 can give us a set of numbers: 5, 53, 538 and 5384.  

Then the module has to do the primality test for each in this set of numbers:
- Starting from the highest order (4, 48, 483, 4835)
- Starting from the lowest level
- Grouping order is specified in the program arguments (lower by default)  

The program works with integers and fails on a wrong input. It should throw any exception to stop, e.g. `throw Exception(\"message\")`

_Example:_
```
The grouping order is: lower
Enter a number:
352

Result: 
3 - prime
35
352
```

### Exercise 3: Thermometer
The most comfortable temperature for a person is from 22 to 25 ˚C in summer and from 20 to 22 ˚C in winter. Write a module that receives the season and temperature and determines whether the temperature is comfortable.
- The temperature sensor (input temperature) works with a Celsius scale. The input number can be with floating point
- The program can output info in three modes: Kelvin, Celsius and Fahrenheit. The unit is specified in the program arguments (Celsius by default). But input still has to be in Celsius only
- The program doesn't fail on incorrect input. It writes the corresponding message and suggests to try again, like \"Incorrect input. Enter a temperature:\"
- In addition, the program advices you to decrease or increase a temperature to make it comfortable if it isn’t.  

_Example:_
```
Output mode: Celsius
Enter a season - (W)inter or (S)ummer:
W
Enter a temperature:
17

The temperature is 17 ˚C
The comfortable temperature is from 22 to 25 ˚C. 
Please, make it warmer by 5 degrees.
```

### Bonus exercise 4: Thermohydrometer
The comfortable humidity for a person is from 30% to 60% in summer and from 30% to 45% in winter. In exercise 4, for both seasons add comfortable humidity parameters. Input it after temperature and output whether it is comfortable or not (if not, advice to decrease or increase it by a certain number of units)  

_Example:_
```
Output mode: Celsius
Enter a season - (W)inter or (S)ummer:
W
Enter a temperature:
17
Enter humidity:
35

The temperature is 17 ˚C
The comfortable temperature is from 22 to 25 ˚C 
Please, make it warmer by 5 degrees

The comfortable humidity is from 30% to 45%
The humidity is comfortable
```

### Bonus exercise 5: Circles-2
In exercise 2, if the circles intersect/touch, output the coordinates of the intersection/tangency points

### Bonus exercise 6: Speech module
As a child, everyone who loved science fiction and various kinds of mechanisms dreamed of a device that could understand words, receive voice commands and carry out appropriate tasks. Now voice control has become a familiar format for communicating with a computer, making our life easier and making this communication more natural. Our smart calculator certainly needs an intermediary module that translates the recognized speech into a language understandable to the computer.
Develop a speech module that reads integer numbers in digital format and translates them into numbers in words
- The module must accept numbers up to a billion inclusive (positive and negative)
- The module receives an integer number in digital format and prints it in words. In words means a set of words, separated by a space, makes up a number. Example: one hundred fifty-two
- The number input-print process repeats until user prints \"exit\"
- At start the module prints \"The program is running. Enter a number or type \"exit\" to stop:\" before input
- On the second number and further the module prints \"Enter a number:\" before input
- Every 5th iteration, the module prints \"Enter a number or type \"exit\" to stop:\" before input
- If an input is incorrect (a word, a symbol or an unsupported number), the module prints \"Incorrect format, try again.\
Enter a number:\" or \"The number is out of bounds, try again.\
Enter a number:\" and listens to another input

_Example_
```
The program is running. Enter a number or type \"exit\" to stop:
yes
Incorrect format, try again

Enter a number:
34
Thirty-four

Enter a number:
exit

Bye!
```

💡 [Tap here](https://forms.gle/4LxkKv2KoPP5aCgN9) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
