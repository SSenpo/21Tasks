## Hello!   

Glad to see you on our next project! You worked hard, learnt a lot of interesting things about Kotlin, and now you are ready to develop a real client-server application! We’ll implement our ideas of the job search project in a mobile app with a server side. So, let’s start! Today we will learn how to write a simple server-side part with a Ktor framework.

We'll also get acquainted with some important architecture principles (remember Team00 day, there were a few words about them). The most widely spread architecture principles in projects of different purpose (server, mobile, etc.) are SOLID and Clean Architecture.  
SOLID is an acronym for design principles. Using them helps to make an application more clear, flexible and maintainable.  
Clean Architecture unites ideas of architecture approaches standing for division of application by layers necessity of an app to be testable. One of these principles is the Dependency Rule, which says that internal layers mustn't depend on external. It means that our business and core logic mustn't depend on UI, Databases, libraries and frameworks. It also helps the code base to be more clean and flexible, allowing reusing logic and replacing external layer mechanisms without logic changes.  
You'll use the layers architecture in this project to divide data, domain and networking layers. You'll see how useful it is, as today we won't add realization of data storage mechanism (Database), but do it later in easy way, without domain logic changes.  

## Topics:
- Ktor framework
- HTTP
- The architecture of the application

### Project: we will develop a backend for a job search service
We will create a data model by analogy with the Day02 project.  

## Exercises:

**Requirement!** The project must be developed in accordance with the principles of clean architecture (remember the Team00)  
**Requirement!** You should use Ktor feature modules structure (e.g. Vacancies and Resume modules).
**Requirement!** Please, make each exercise in a separate project. For example, `Day06/src/exercise1`, `Day06/src/exercise2`, `Day06/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 0: Preparations
- First of all, check the Ktor documentation and get acquainted how to create a Ktor project with IntelliJ IDEA
- Install Postman. With this simple and useful app you'll make requests to our Ktor backend and check its responses

### Exercise 1: Companies list
Let's start with an important concept of our app - the company.

- Add an entity describing a company to the project. As in the third day’s project, we are interested in the following information:
  - Name
  - Field of activity (IT, Banking, Public services)
  - Description
  - List of vacancies (for now, let's make a stub here, without specifying the Vacancy class)
  - Contacts
- The data layer must be implemented in such a way that the logic is not tied to a specific implementation of the storage mechanism. At the moment, from this layer we will return a hardcoded collection with company objects.
- Add entities to display a list of companies on the client. To ease the load on the network, the list items should have a simple structure, the minimum necessary to display the list in the desired form. We need to display the name and the field of activity of a company
- Add an http endpoint to get a list of all companies.
- Describe the logic of request processing.

**Check the result**: start the server, make a request to the new endpoint with postman, check the response with the hardcoded companies. If everything works right, you'll see company objects in the Postman BODY tab

### Exercise 2: Company details
When the client selects a company from the list, the client asks our server for detailed information about this company.
- Add an http endpoint to get details about the company by the company ID (the list of vacancies is still empty)
- If a passed company id doesn't exist in the collection, the endpoint returns empty body. For simplicity. Normally it should return an error
- Describe the request processing logic

**Check the result**: check the company details endpoint with Postman, like in previous exercise

### Exercise 3: Vacancies list
The data model for the list of vacancies:
- Add the necessary entities to the project to describe vacancies. We are interested in information about the profession (Developer, QA, Project Manager, Analyst, Designer), the candidate level (junior, senior, middle) and the proposed salary level. Also, we need some description of the vacancy.
- The data layer, as earlier, needs to be made independent of the implementation. At the moment, from this layer we will return a collection with vacancy objects pre-filled in the code.
- Add entities to display a list of vacancies on the client. Here we need a job title, a candidate level, a salary level and a company name
- Add an http endpoint to get a list of all vacancies.
- Describe the logic of request processing.

**Check the result**: check the endpoint with Postman

### Exercise 4: Vacancies details
We have added the ability to receive a list of vacancies. When the user decides to get acquainted with one of them, our server will give the client more detailed data.
- Add an endpoint to get vacancy details

**Check the result**: check the endpoint with Postman

### Exercise 5: Working with resumes
Now we will support a feature of working with resumes for our site. Suppose that the client has a resume form that matches the template from the Day02 project.
- Add the necessary entities to store the resume to the project
- The data layer also needs to be made independent of the implementation. For now, we will be returning a hardcoded resume from this layer.
- Add http endpoints that allow:
  - GET a resume
  - Save changes to the resume with an id (for now, we won't save it anywhere, just print the resume to the console)

**Check the result**:
- Check the get resume endpoint, receive a hardcoded resume with Postman
- To test the mechanism of saving changes, create a request in Postman with data from the resume, and on the server side you should see this resume printed in the console

### Bonus exercise 6: Text analysis
Implement resume text processing logic from the Day02 project.
- It should process the resume between the save endpoint being triggered and the resume being saved (thus, on the logic layer).
- The result of analysis is in new tags. Later they'll be saved in corresponding DB table. Now they won't be saved anywhere.
- Add logging of created tags to the analysis logic
- Add a list of tags to the resume get request class. Hardcode a collection of tags. When a client triggers the get resume endpoint, our server also gives a resume tags collection. There, a resume object should be separate with the collection of tags.
- Add an endpoint that returns the tags list for the resume. It'll be used later. 

**Check the result**:
- Make a request to save a resume with postman. You should see logging of created tags
- Check the get resume endpoint, receive the hardcoded resume and tags with Postman
- Check the get tags endpoint, receive the hardcoded tags

💡 [Tap here](https://forms.gle/QKw7mAuvx9gyBk6k6) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.

