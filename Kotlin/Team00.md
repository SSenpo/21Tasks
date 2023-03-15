### Hi, people!
Today we’ll work in small teams developing a multi-module application.  
By the multi-module architecture we'll understand a project with multiply Gradle modules. The idea implies separation by a purpose of the application code into loosely coupled and self-sufficient parts called modules. It helps to make a code base more clear, maintainable and reduce its complexity.  
As an example we'll take an Android platform.

**Advice!** Read about modularization in android on the official android documentation resource.

In the documentation about modules you can find a mark telling us that before you start it's important to get familiar with the app architecture principles and guidelines. You may read some articles about SOLID and Clean Architecture principles, and then about Android architecture principles to be familiar with, but don't spend much time on it, we'll touch these topics later.  

**Advice!** There are different ways to divide an app into modules: by feature and by architecture layer (you can read about it with reference to architecture principles). Sometimes, the mixed variant is used. Today we'll develop different feature modules and combine them into an Android app.

In the Day00 project, we wrote some features for the Smart Calculator project. Now it's time to move our developments in a real application that a user can interact with. Also, it can be easily decomposed into the feature modules and developed in parallel.

## Topics:
- Modularization of the application

### Project: The Smart Calculator on the android platform.

## Exercises:

**Advice!** Read the documentation about navigation between modules on the Android developers resource.

### Exercise 0. Create a new android project

### Exercise 1. Develop the app module
- There we have our main app logic. The app must have a main screen with buttons navigate to the tools

### Exercise 2. Develop the feature modules
- The app must have feature modules for the tools: Circles (Circles-2), Prime numbers, Thermometer (Thermohydrometer).
- For each module consider UI input and output. It must be implemented using standard android components (input fields, checkboxes, text fields, buttons) and be within the corresponding tool screen

### Exercise 3. Develop core modules
- Create a logger module

### Exercise 4. Come together!
- Merge all modules together. There should be the app module, feature modules and core modules
- Setup navigation between main module and feature modules
- Use the logging module to log the main operations of features. Also, you can add logs to the Android framework events to get better acquainted with it (e.g. activity/fragment lifecycle) 

### Bonus exercise 5: More features
- The Smart Calculator now is a very-easy-to-extend application. Decide with you team, what functionality do you want to add next and write a new module/a couple of modules
- New modules can be of different types: a new feature, a new module with core functionality

