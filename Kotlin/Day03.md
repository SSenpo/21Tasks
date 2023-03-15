### Hello there!

In this project, we will get acquainted with several interesting themes:

- Generics - classes, which can have type parameters. With their help, we can write a class or a method that will work not with specific, but with arbitrary data types: the type (or types hierarchy) will be defined by a developer in the context of use. At the same time, the tool offers type safety: after specifying a type or a types hierarchy, work with this generic goes only in context of specified type.
- Delegates. It's a very cool mechanism to ask someone else make a job for you :) There are two common ways to do this:
  - Delegation of properties. There are often situations when we implement the same logic for properties (for its getter and setter) in different parts of the project. This is where the guardian of concise code enters the scene - the delegation mechanism, which allows you to implement such properties only once and take them to a convenient and accessible place, for example, a library. There are two standard delegates - `lazy` and `observable`. 
  - Delegation of implementation. Also, the developers supported the ability to delegate the implementation of interfaces, which allows one object to delegate all requests to another object. This implementation of the Delegate architectural pattern is a good alternative to inheritance.
- Functional types: of course, working with them deserves attention. The developers have provided excellent support for this popular tool, and have also added several convenient constructs for performing tasks in the context of an object.
- As official documentation says, “Kotlin is designed with Java interoperability in mind”. It means that Kotlin fully supports Java code calls within its code and vice versa. In most projects which started with Java and later switched to Kotlin, the Java code is considered as legacy. So, the cases, when old Java code is called from Kotlin, are much more often. We’ll take a look at some interaction cases.

## Topics:
- Generics
- Delegates
- Functional types
- Interoperability with Java

**Advice!** These themes are usually not too easy for understanding. It would be better to start with articles on them, where people describe these features in simpler words, then in official documentation. For example, there are a lot of good articles about generics in Java - you can start with them just to catch an idea of this mechanism, then read about it in Kotlin (also you'll see all common things and differences between generics in these two languages)

### Project: classes and utils for the video game

## Exercises:

**Requirement!** Please, make each exercise in a separate project. For example, `Day03/src/exercise1`, `Day03/src/exercise2`, `Day03/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 1: Revolver drum
We'll start with creating of a generic data structure. Write a class that represents a data structure of a revolving type
- The structure can hold up to 6 elements
- You can add one element to the nearest free cell. On successful addition the method returns true, else - false
- It is possible to add missing elements. This function takes another collection as a source, pops elements from it and adds to the drum. If there are not enough elements in the source, as many as there are filled in. If it's empty at all, false is returned.
- The structure has a pointer. After the addition, it points on the last added element. You can get the pointer's position, it'll return current element
- You can delete (\"shoot\") items one by one. The deletion starts at the element under pointer, then the pointer moves to the next cell. The deletion returns if an element in this cell was deleted. If a cell is empty, it returns null and moves the pointer
- You can extract (\"unload\") a current element or all elements at once. The extraction returns an element or a list of all elements.
- You can \"scroll\" the drum by setting the pointer to a random element
- Add a method that returns the number of elements in the structure
- The class must work with objects and their descendants (the wildcards feature)
- The class must have a correct `toString()` realization to be able to print the info about itself and its elements. The info about elements prints starting from the current pointer's position 
- Override the `equals` method. Structures are equal if in each of them there are the same order sequences of elements (starting from any element and including nulls) of the same type. See an example below

**Check the result:** write a demo program to show how the structure works
1. Create a structure object, fill it with elements within a loop. Print this structure and its pointer position. The printed structure info should start with the same element, as pointer's position returns 
2. Call the scroll method and print the structure - the printed structure should start with another element (but it can be the same). The order of other elements must be the same
3. Delete 4 elements one by one. Print the structure and compare with the previous print. It should start with fifth element from the previous print, have next element in the same order and then 4 nulls.
4. Create a supply collection of elements with the same type. Add 8 elements to it. Add elements to our revolver structure with this collection, print both and compare. There should be full revolver and 4 elements in supply collection
5. Extract all elements from our structure (it'll return a list of them), print the list size and the structure size (should be 6 and 0)
6. Add elements from our supply collections to the revolver, print the revolver size and the supply collection size (should be 4 and 0)
7. Create a new structure and fill it in an arbitrary way. Compare it with our first revolver, check the result

_Example of output_
```
1. Adding elements
Structure: RevolverDrum<Int> 
Objects: [3, 54, 7, 2, 56, 4]
Pointer: 3

2. Scroll
Structure: RevolverDrum<Int> 
Objects: [7, 2, 56, 4, 3, 54]
Pointer: 7

3. Deletion
Structure: RevolverDrum<Int> 
Objects: [3, 54, null, null, null, null]
Pointer: 3

4. Supply collection
Before:
Supply collection: [4, 6, 3, 22, 77, 43, 76, 5]

Structure: RevolverDrum<Int> 
Objects: [3, 54, null, null, null, null]
Pointer: 3

After add operation performed:
Supply collection: [77, 43, 76, 5]

Structure: RevolverDrum<Int> 
Objects: [22, 54, 6, 4, 3, 54]
Pointer: 22

5. Extraction
The extracted list: [22, 54, 6, 4, 3, 54]
size: 6

Structure: RevolverDrum<Int> 
Objects: [null, null, null, null, null, null]
Pointer: null
size: 0

4. Supply collection 2
Before:
Supply collection: [77, 43, 76, 5]

Structure: RevolverDrum<Int> 
Objects: [null, null, null, null, null, null]
Pointer: null

After add operation performed:
Supply collection: []

Structure: RevolverDrum<Int> 
Objects: [5, 76, 43, 77, null, null]
Pointer: 5

6. Equals
Structure: RevolverDrum<Int> 
Objects: [null, 5, 76, 43, 77, null]
Pointer: null

Structure: RevolverDrum<Int> 
Objects: [null, null, 5, 76, 43, 77]
Pointer: null

Result: equals
```

### Exercise 2: Java bullets and structure improvements
**Bullets:**
- Create an abstract java bullet class
- This class has `shoot()` method, which has no realization
- Also, there is a field describes a condition of a bullet - if it's damp

**Bullet types:**
- Create java classes describing bullets of a certain caliber using Java classes:
  - TwentyTwo
  - ThreeEighty
  - FortyFive
- Each class has its own `shoot()` realization with its own \"Bang\" and caliber info

**Update the revolver structure:**
- Make the revolver structure work only with bullets. You can't load bullets of different caliber in one drum
- The structure \"delete\" method now, besides common behavior, should call `shoot()` method from the bullet
- If you try to delete from an empty cell, it prints \"Click\"

**Implement the following logic for our structure and bullets:** 
  - one bullet can be only in one drum. If you're trying to add it to different drums, the add method must return false and print that you're wrong. Also, if there is such bullet somehow in a bunch of adding bullets, it must be ignored (with log), but the others must be added
  - one bullet can be shot only once. You're able to add it to a revolver drum again, but it'll not shoot. The structure doesn't call shoot method but prints \"Click\", just like on empty cell, but with corresponding log (e.g. \"A shot one\")
  - if the bullet is damp, it can't be shot and when the structure \"shoots\". The structure doesn't call shoot method but prints \"Click\", just like on empty cell, but with corresponding log (e.g. \"A damp one\")

**Advice!** To indicate that bullet is shot, damp or already loaded, you can use something like a flag in bullets class. The logic that changes this flag can be implemented in the revolver structure

**Check the result:** do the same checks, as in previous exercise, but fill different drums with different bullets. 
- Check that normal bullets shoot and damp not.
- Try to add one bullet to different drums. The first addition should return true, the second - false 
- Try to add one bullet to different collections, and then add it to different drums 
- Try to shoot with a damp and shot bullets. The output should be \"A damp one\" and \"A shot one\"

### Exercise 3: Utilities training
Create two kotlin files for utilities

**Abstract utilities:**
1. Write a function that compares 2 arbitrary objects by type (returns Boolean)
2. Write an abstract mapper class:
  - declare an abstract method that converts an element of type A to an element of type B
  - add a method that converts List of type A to List of type B
3. Write a function that extends any class and checks if an object is of a certain type
4. Write a delegate that replaces all spaces in a string with underscores
5. Write a delegate that logs all calls of the field to the console
6. Write addition, subtraction, multiplication and division functions for numbers of arbitrary type. Create an Enum with keys of these actions. Write a function that takes an action key and returns the action

**Utilities for out classes:**
7. Write an extension to our revolver drum, that rearranges its bullets: if there is more than one gap between bullets, they'll be replaced in sequence without gaps
8. Extend the drum class with a function that scrolls the drum and shoots
9. Extend the drum with a function that takes the current element. If it is not null - it extracts the bullet and creates a new drum with this bullet (all transformations must be in the same chain)

**Check the results:**
1. Call the function for String and Int, should return false. For String, String - true
2. Write a realization to convert data class First(val name: String) into data class Second(val name: String). Add a list of First and convert it. Print both lists.
3. Write an Animal class. Inherit a Dog and a Cat. Create variable animal and initialize it with a Dog. Check with extension, if it is a Dog, a Cat, an Animal. Results: true, false, true
4. Create a class and a var property \"description\" of String. Create a String \"The delegate will replace all spaces with underscores\". Print it, assign to the description and print description. The result: \"The_delegate_will_replace_all_spaces_with_underscores\"
5. Create a var String property, add a logging delegate to it. Assign \"Hello\" to the property. Assign the property to a new property. The logger should print both get and set events. 
6. Pass SUBTRACTION for subtraction and pass (10, 5), and print the result
7. Create a drum and fill it with numbers, add two nulls in the middle, print the drum. Call the function and print the result
8. Print the initial, the scrolled drums and the drum after shoot
9. Print the initial and the result drums

_Example_
```
1. 
String, Int - false
String, String - true

2.
Map List<Int>: [First(name=Alex), First(name=John), First(name=Peter)]
to List<String>: [Second(name=Alex), Second(name=John), Second(name=Peter)]

3.
true
false
true

4.
Before: \"The delegate will replace all spaces with underscores\"
After: \"The_delegate_will_replace_all_spaces_with_underscores\"

5.
A property was assigned \"Hello\"
A property \"Hello\" was readed 

6.
The result of subtraction is 5

7.
Before:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), null, null, FortyFive(...), FortyFive(...)]
Pointer: FortyFive(...)

After:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), null, null]
Pointer: FortyFive(...)

8.
Scrolled:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...)]
Pointer: FortyFive(...)

Shot:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), null]
Pointer: FortyFive(...)

9.
Before:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), null]
Pointer: FortyFive(...)

After:
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), FortyFive(...), FortyFive(...), FortyFive(...), null, null]
Pointer: FortyFive(...)

New drum: 
Structure: RevolverDrum<FortyFive> 
Objects: [FortyFive(...), null, null, null, null, null]
Pointer: FortyFive(...)

```

### Exercise 4: The wildest hand in the wild west
**Modify the bullets:** add two classes: PistolBullet and RifleBullet. They should be inherited from the Bullet class, and the classes TwentyTwo, ThreeEighty, FortyFive - from the Pistol Bullet.

**Create a Player class:**
The player has an inventory. It stores:
- A collection of TwentyTwo (10)
- A collection of ThreeEighty (7)
- A collection of FortyFive (44)
- A collection of RifleBullet (12)
- A revolver (one of three pistol calibers)
- A rifle (of RifleBullet)

An inventory has a generic method `reload`, which:
- Takes a caliber as a parameter and returns a collection of corresponding ammo, if it exists in the inventory (or null if not)
- Ejects all shot or damp bullets and add elements from the ammo collection

**Check the result:** 
- Load the rifle with appropriate ammo and shoot! Do it until the player is out of rifle ammo
- Then load the revolver and shoot! Do it until the player is out of pistol ammo (only one caliber)

### Bonus exercise 5: Platform fighting 
Add a Weapon type that has subtypes
- Pistol, SniperRifle - implement Firearm interface, SilencedPistol - implement Firearm and Silent interfaces
- Shuriken, Katana - implement Cold and Silent interfaces
- C4, Grenade - implement Explosive interface 
- Weapons have an interaction method, which prints a type of a gun, its interfaces and interaction sound

Add generic types to describe characters
- Rambo can interact with any weapon
- Sniper can interact with weapons like Firearm
- Ninja can only interact with certain Cold and Silent weapons
- Characters can attack with their weapons, calling the \"interact\" method

**Advice!** Use a mechanism allows generics to use classes which implement certain interfaces

**Check the result:** create each of the characters in program and give them weapons. Attack with each character. You should see something like:
```
Rambo attacks with a Grenade (Explosive) - KA-BOOOM!!!!!!
Ninja attacks with a Shuriken (Cold, Silent) - SPLASH!
```

💡 [Tap here](https://forms.gle/dFB3YDYeVmWs6hKm6) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
