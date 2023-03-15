 ### Hola, dear student!

Welcome to the next project! It is also a part of our job searching service, and today we’ll implement data storage features using databases. We’ll use databases both on the server and on the client sides of our application.

## Topics: Databases
- Exposed + H2 on server side
- Room + SQLite in android application

### Project: Add databases to storage data within the job searching platform server and the android application.

## Exercises:

**Requirement!** Please, make each exercise in a separate project. For example, `Day08/src/exercise1`, `Day08/src/exercise2`, `Day08/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 1: The server side database
Let’s add a DB and to our backend project and implement the following things to store our data:
- Add to the Ktor project the Exposed SQL library and the H2 Database
- Organize the tables structure for Companies, Vacancies, Resume, Tags and related entities which were hardcoded in previous version of project
- Write an implementation for the storage layer. If the GET request is made and there is no resume in the DB, an empty resume will be created in DB and returned in the response

**Advice!** Now you can see how it’s convenient to have an interface and an implementation: while implementations can be different, the interface is still the same, and you don’t need to change any logic depends on it
  
**Check the result:** after you’ve created a tables scheme, fill your database with different objects (you can move here hardcoded objects) and try to interact with your backend via our client application or Postman.

### Exercise 2: A Local resume editing
Let’s develop a new feature for our client. It allows a user to keep resume changes locally and resume edition after the app suddenly closes or changes its configuration (e.g. screen rotation).
- Add the Room library to the android project
- Initialize the database. Use the Dagger2 DI mechanism to inject required objects. See some sample code in Code Samples directory.
- Add a mechanism that allows you to save resume changes to the app DB when an editing screen stops or app changes its configuration. You can read about android activity/fragment lifecycles and configuration changes in Android official documentation.
  - If the configuration change happened, or you closed your app during edition of a resume, when you back to the resume screen, you’ll see a dialog with the text “Would you like to resume editing?” and yes/no buttons. If yes, the resume screen will be filled with the edited copy of resume from the app DB and editing Mode will be turned on. If no, the copy in the app DB will be deleted, and you’ll see unchanged resume in read mode (returned within the GET request)
- When a user during editing of a resume presses the back button, the app should ask if you want to keep changes locally and resume editing later. When user goes back to the resume, a dialog from the previous point should appear

### Bonus exercise 3: Cache
Add a light cache mechanism to our android app. It does the following:
- The data we obtain from the server is saved within a local database
- When we do the first request to the server (a corresponding local db table is empty), we wait until our data is loaded and show a loader
- When requesting data next time, the mechanism first returns data from the database, and then executes a request to the backend. It helps us to improve UX, always showing some data on the screen, while loading the most fresh bunch

### Bonus exercise 4: Migration
It’s a common case, when during the development we change DB model entities. If we don't write a mapping migration (from old to a new version of an entity), we’ll get an error from the table associated with this entity and all the data in this table will be lost.      
Let's try to handle such case on the client local DB. We have a local cache table where the vacations are stored
- Add a boolean field \"isFavourite\" to the Vacancy entity
- Write a migration for this entity, adding this field to the DB with the default value `false`
- Add a button (a heart or a star) to the vacancy details to mark a vacancy as favorite. It'll change the corresponding parameter in a local DB
- 
**Advice!** Read about SQLite migrations with room in official Android documentation.

**Check the results:**
- After the exercise code is written, create a separate file, where you'll store the new code adding the field and the migration. It's needed to show how it works to the reviewer
- You'll install an app with a previous version of the project (from the exercise 3). Then you'll copy the code adding the field and the migration. Finally, you'll try to install a new version of an app (the migration will run automatically), and there shouldn't be any errors from the DB


💡 [Tap here](https://forms.gle/X9a8oKU7wzCxJdWu8) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
