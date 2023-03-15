### Hi!
Today we’ll continue our job search project development. In this project, we’ll create the android client application and connect it to our server! We are going to create a resume and find a job using modern network and DI technologies for android. Like on the server side, we’ll use the REST API on the network layer.   
As for DI, it stands for Dependency Injection, the design pattern which allows the creation of dependent objects outside classes and inject them in different ways wherever they are needed. It’s very useful and allows us to keep program code readable, testable, expandable and reusable.  
Also, we'll use some architecture principles we've spoken about on Team00 and Day06. The Android app architecture uses SOLID and Clean Architecture ideas, but there are some framework-based interpretations of them. Read the official Android documentation about app architecture, find some articles about Clean Architecture in Android. Get familiar with the terms of Repository, View, Presenter, etc.

## Topics:
- Network: android Retrofit2
- Dependency Injection: Dagger2
- The architecture of the application

### Project: android client application for job searching. 
The application will have two tabs - campaigns and vacancies, screens of their details and a screen for editing resumes.

## Exercises:

**Requirement!** Please, make each exercise in a separate project. For example, `Day07/src/exercise1`, `Day07/src/exercise2`, `Day07/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 1: The list of companies
Let’s create our project and add a list of companies.
- Create android application project
- To work with data, add the Retrofit2 library
- Connect HTTP client to the project. Use Dagger2 to implement DI in the project, starting with the HTTP client. See an example in the Code Samples directory.
- Add a logger and timeouts to the HTTP client
- Add entities to the model to work with a list of companies
- Add a screen with two tabs: \"Companies\" and \"Vacancies\". Add a list of companies to the \"Companies\" tab. The \"Vacancies\" tab is empty. List items must represent a name and a field of activity of a company
- Add the <YourAPI> realization to get the data needed for the company list screen. You should get acquainted with a term “Repository” in android to write your model code accurately.
  
**Check the results:**
- When entering the application, there is a screen with two tabs. The first tab \"Companies\" is opened by default
- The \"Companies\" tab should display a list of companies received from our server (written in the previous day)

### Exercise 2: Company details
Now we’ll add a company details screen
- Add entities to the model to work with company details
- Create a screen with company details. On the screen, in addition to information about the company, there should be a list of vacancies in this company (for now is empty)
- From the list of companies, navigate to the details of a specific company
- Add an API realization to get the data needed for the company details screen

**Check the results:** click on an item in the list of companies to open a screen with the details of this company (including a list of its vacancies)

### Exercise 3: The list of vacancies
Here we’ll add a list of vacancies screen
- Add entities to the model to display a list of all vacancies
- On the main screen, in the \"Vacancies\" tab, add a list of vacancies. List items must represent vacancy title, candidate level, salary level, and company name
- Add an API realization to get the data needed for the list screen of all vacancies

**Check the results:** on the main screen, when you tap on the \"Vacancies\" tab, a list of all vacancies should be displayed

### Exercise 4: Vacancy details
Now we’ll develop a vacancy details screen.
- Add entities to the model to work with vacancy details
- Create a screen with vacancy details.
- On the screen, in addition to information about the vacancy, there should be a link to the company, navigating to the company details.
- From the list of vacancies tab navigate to the details of this vacancy
- From the list of vacancies in company details, navigate to the details of this vacancy
- Add an API realization to get the data needed for the vacancy details screen

**Check the results:** 
- in vacancy details click on a link with the name of a company to open this company details
- click on an item in the list of vacancies tab to open a screen with the details of this vacancy
- click on an item in the list of vacancies in company details to open a screen with the details of this vacancy

### Bonus exercise 5: Resume
Finally, we’ll add a Resume screen  

**Create the \"Resume\" screen:**
- The screen has an app bar
- The screen has 2 modes: a View mode (default) and an Edit mode. The modes are changing with icons:
  - In the View mode there are two icons in app bar: \"Edit\" (something like a pencil) and a \"Back\" arrow. If you press the \"Back\" button, you'll go back to the main screen of the app (with tabs). If you press the \"Edit\" button, the View mode changes to the Edit mode
  - In the Edit mode, the app bar icons are changed with two another: \"Save\" (something like a diskette) and \"Undo\" (something like a cross). If you press the \"Undo\" button, the Edit mode changes to the View mode without any changes to the resume. If you press the \"Save\" button, the changes in the fields will be saved on our server, and the screen Mode will be changed to the View mode.
- There are text blocks on the screen. According to the mode, they are editable or not
- In addition to resume blocks, a block with tags is displayed. You can't edit it in both modes

**API:**
- When you enter to the \"Resume\" screen (there is the View mode by default), a GET request is sent to our server. It returns a resume saved on the server (it can be with empty fields if there is no resume yet). It also returns a collection of tags if exists  
- When you press the \"Save\" button, the changes in the fields will are saved on our server with our POST request. Then you'll go back to the View mode and a GET resume request'll be sent again

**Integrate the \"Resume\" screen into the app:**
- On the main screen, add an app bar
- Add a \"Sidebar\" icon to the app bar (something like a menu icon). Add a sidebar menu which opens when a \"Sidebar\" icon is clicked
- In the sidebar menu, add a button \"My resume\". When \"My resume\" is clicked, the \"Resume\" screen should open

**Check the results:** create a new resume and save it. After saving, a tag block should be filled with the analyzed tags. Go back to the main screen and enter the \"Resume\" screen again - you should see your resume in View Mode.

💡 [Tap here](https://forms.gle/3J7aRNcar555hcbz5) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
