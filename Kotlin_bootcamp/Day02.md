### Good day!  

It's time to get to know the different collections and their transformations better. The developers of Kotlin did their best to make working with data in collections as convenient as possible. Particularly pleased with the large number of different methods, the ability to make it even larger due to extensions, data classes, perfect for working with collections.  
Also, let's pay a little attention to reading / writing from files.

## Topics:
- Collections
- In/out: files

**Advice!** In the `codesamples` folder there are some examples of Collections transformations. Use them to complete exercises.

### Project: today we will work on features for a job search application

There is a common case when a user needs to display data taken from different sources/entities. To do this, the presentation layer usually has special entities that have the fields and properties necessary for display, which are filled with data before display. At the same time, the transformation of some entities into others should not change the original values in any way (the principle of immutability).

## Exercises

**Requirement!** Please, make each exercise in a separate project. For example, `Day02/src/exercise1`, `Day02/src/exercise2`, `Day02/src/bonusexercise3`, etc. If the previous exercise is needed for the next one, just copy a project from the previous to the next folder and continue development within the next one.

### Exercise 1: List of companies
A simple example of such object transformations is a preview list containing partial information about an object.  

Create a collection of companies, each is described as follows:
- Name
- Field of activity (IT, Banking, Public services)
- Description
- A list of vacancies, each contains information about the profession (Developer, QA, Project Manager, Analyst, Designer), level (junior, middle, senior) and the proposed salary level
- Contacts

There must be at least 10 companies, with different fields of activity, professions, candidate levels and salary levels. For simplicity, hardcode them.

**Input:** in the console, a user selects the following filters sequentially: field of activity, profession, level for the candidate and salary level (several forks). At each stage there is an option \"all\". The user selects a number of chosen option. On an incorrect input, the program prints \"It doesn't look like a correct input.\" and repeats an option.  

**Output:** depending on selected options, print to the console a list of vacancy preview items

```
Select a field of activity:
1. IT
2. Banking
3. Public services
4. All
2

Banking. Select a profession:
1. Developer
2. QA
3. Project Manager
4. Analyst
5. Designer
6. All
4

Banking. Analyst. Select the level of a candidate:
1. Junior 
2. Middle
3. Senior
4. All
1

Banking. Analyst. Junior. Select a salary level:
1. < 50000
2. 50000 - 100000
3. > 100000
4. All
3

Banking. Analyst. Junior. > 100000
The list of suitable vacancies:

1.
Junior Analyst     ---      from 100000
  OOO \"SuperPay\"
  Banking
---------------------------------------

2. 
Junior Analyst     ---      from 100000
  MMM
  Banking
---------------------------------------

3.
Junior Analyst     ---      from 100000
  CryptoSuperGo
  Banking
---------------------------------------
```

### Exercise 2: A resume with tags
Let's write a mechanism that allows you to analyze a resume and generate tags based on it.   

A resume has a template:
- Candidate information block
  - Full name
  - Profession (the list of professions is same with one from the previous exercise)
  - Sex
  - Date of Birth
  - Contacts (phone, e-mail)
  - Willingness to travel and relocate
- Block with information about education. For each educational institution:
    - Type of education
    - Years of education
    - Description
- Block with job experience. For each:
    - Dates of work
    - Company name and (if available) contacts
    - Description
- Block for some words in free form

Our tool recognizes template blocks and creates the corresponding objects filled with data from the resume
- Text is parsed by words, which are matched against a tag cloud
- There is a resume export mechanism
  
**Input:**   
Add files to `src/files`
  - _resume.txt_ - it must be filled in accordance with the resume template
  - _tags.txt_ - it must be filled with the initial set of tags
  - _export.txt_
  - _analysis.txt_

**Output:**  
Checking the correct operation of the program: 
- To the _export.txt_ file, export data from objects according to the resume template. 
- After that, the _resume.txt_ and _export.txt_ files must match (can be checked in online editors)  

Output to the _analysis.txt_ file:
- A section with each word from the text (once) with the number of repetitions in the format: \"developer - 42\", in descending order by number
- A section with words that match words from the _tags.txt_ file (there must be at least 3 of them)

Example files - [resume.txt](datasamples/resume.txt), [tags.txt](datasamples/tags.txt), [analysis.txt](datasamples/analysis.txt) are in data-samples folder

### Bonus exercise 3: Seniority
To the candidate levels from the exercise 1, add seniority (in years): junior (0), middle (1), senior (3)  
Output in a section in _analysis.txt_ a list of vacancies suitable for the profession and seniority of the candidate, counted by sum of job experience years (there must be at least 3 of them)  

An example for [analysis.txt](datasamples/analysis.txt) is in data-samples folder

### Bonus exercise 4: Analytics
Let's create the simplest analytics mechanism:
- Add a file _notATag.txt_ to `src/files`, which will store conjunctions, pronouns and other words that are not tags (add, for example, 12-20 words from the resume).
- Based on this file, filter the resume by sending words that don't match either words from _tags.txt_ or words from _notATag.txt_ to the _analysis.txt_ file, section \"Possible tags\"

Examples for [notATag.txt](datasamples/notATag.txt) and [analysis.txt](datasamples/analysis.txt) is in data-samples folder

### Bonus exercise 5: A text comparator
Add a mechanism that compares the texts of the imported and exported resumes  
**Output:** in console output the result of comparison

_Example:_
```
Text comparator: resumes are identical
```

💡 [Tap here](https://forms.gle/ZTzuepYrgDpm2yhd8) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
