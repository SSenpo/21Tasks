----- Day 05 - Python Bootcamp -----

## Wibbly-wobbly, timey-wimey stuff

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Fool Me Once](#exercise-00-fool-me-once)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Screwdriver Song](#exercise-01-screwdriver-song)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Good Timing](#exercise-02-good-timing)
7. [Chapter VI](#chapter-vii) 
    
    7.1. [Reading](#reading)

<h2 id=\"chapter-i\" >Chapter I</h2>
<h2 id=\"general-rules\" >General rules</h2>

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

<h2 id=\"chapter-ii\" >Chapter II</h2>
<h2 id=\"rules-of-the-day\" >Rules of the day</h2>

- You should turn in `*.py` and `requirements.txt` files for this task. You can also add a `README` file explaining how to start your application
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

<h2 id=\"chapter-iii\" >Chapter III</h2>
<h2 id=\"intro\" >Intro</h2>

 &mdash; Who was that, Doctor? We barely made out alive!

 &mdash; They are called daleks, one of the most merciless and violent species in the universe. 
 Nevermind though, they can't get us here.

 &mdash; In this police box? By the way, why is it bigger on the inside?

 &mdash; TARDIS' Dimensional modeling. Anyway, looks like for this adventure we need more paper
 and we're currently out of it.

 Doctor starts running around the room pulling some levers and pressing some buttons. It looks
 completely random for an untrained eye.

 &mdash; Paper? What kind, toilet?

 &mdash; No, that probably wouldn't be a good application. It's psychic paper, see?

 Doctor immediately shows directly to your face something with a slight resemblance of a passport.
 It says \"Crisis investigator with the UN, Liverpool Division\".

 &mdash; Are you really with the UN?

 &mdash; With what now? Nevermind. The thing is it shows you what you want to see and can possibly 
 save us some time. And you will need something similar at that place we're going to.

<h2 id=\"chapter-iv\" >Chapter IV</h2>
<h3 id=\"exercise-00-fool-me-once\">Exercise 00: Fool Me Once</h3>

In the next moment two weird-looking devices appear from the Doctor's pockets. One looks like a 
very unusual screwdriver, and the other one is like a smartphone, but with a couple of tentacles
on its sides.

 &mdash; So, this is an Ood species detector. When you aim the tentacles at someone it will show
 you the most appropriate name of that species in your language.

You take the device and point its tentacles to the Doctor. The \"smartphone\" thinks for a moment
and then the words \"Time Lord\" appear on its screen in English.

 &mdash; Now, every species in a galactic database has a specific leadership figure or at least 
 some name that will make them stumble for a moment and give you a temporary advantage.

On one of the TARDIS' screens appears a list of species with examples:

```
Cyberman: John Lumic
Dalek: Davros
Judoon: Shadow Proclamation Convention 15 Enforcer
Human: Leonardo da Vinci
Ood: Klineman Halpen
Silence: Tasha Lem
Slitheen: Coca-Cola salesman
Sontaran: General Staal
Time Lord: Rassilon
Weeping Angel: The Division Representative
Zygon: Broton
```

 &mdash; Are you joking? Would you believe me if I said to you, out of the blue, that I am
 this...Rassilon?

 &mdash; That's not the point. The point is, most of the creatures will be shocked for a second
 just by the very idea that you would suddenly present yourself like that. This is all we need.

You try to figure out how device works and realize that it actually uses a WSGI+HTTP stack for
presenting results.

Also, while plugging together some cables Doctor gives you one last remark:

 &mdash; The Wi-Fi in TARDIS is a bit wonky, you know, especially inside the time stream. So
 currently please don't use any external dependencies.

---

Your goal is to implement a WSGI server with an HTTP wrapper without using any external 
dependencies (see \"Reading\" section). It should listen on local port 8888 and parse GET
parameters from a URL, for any species title giving you back a JSON (it should be HTTP code 200,
also mind the appropriate 'Content-Type' header and URL encoding). Exaple using cURL might look 
like this:

```
~$ curl http://127.0.0.1:8888/?species=Time%20Lord
{\"credentials\": \"Rassilon\"}
```

If it doesn't know the species passed it should return `{\"credentials\": \"Unknown\"}` along with
HTTP status code 404

The whole application for this task should be just a single file `credentials.py`.

<h2 id=\"chapter-v\" >Chapter V</h2>
<h3 id=\"exercise-01-screwdriver-song\">Exercise 01: Screwdriver Song</h3>

 &mdash; So, what about that over device? Some kinda screwdriver, eh?

 &mdash; Sonic, yes.

 &mdash; What can it do? Can I get one?

 &mdash; Well, it generates a combination of certain frequencies, so you can do...pretty much
 anything!

 &mdash; Can it actually unscrew stuff?

 &mdash; Oh, it's kinda tricky. To do that... you know what, here, just play these sound files.

---

This time you need to create a simple WSGI+HTTP client-server application for managing sound files.

First, the server. It shouldn't use any kind of database, just storing files on disk is okay. Web
interface should run on port 8888. When opened, the webpage should show a list of sound files
already uploaded as well as the button for uploading one more. As a user, you should be able to
click on that button, upload the file to the server and it should appear in a list of files shown
on the webpage.

Also, the server should perform a [MIME type](https://en.wikipedia.org/wiki/Media_type) check, so
only audio files are accepted (e.g. `mp3`, `ogg` and `wav`). If a non-audio file is uploaded (e.g.
`jpg`, `exe` or `docx`), it should be discarded and the webpage should show the message \"Non-audio
file detected\". 

For some bonus points, you can implement playing uploaded sound files directly from the webpage.

This time you are not limited to built-in WSGI server, so it is recommended to use either [Flask](https://flask.palletsprojects.com/)
or [Django](https://www.djangoproject.com/) framework for this task, even though it is not a strict
requirement. Don't forget to add any third-party dependencies you've used into file
`requirements.txt`. Please also include file `README` explaining how to start the HTTP server
(it should contain the specific command to run).

Second, the client. It should be a command-line application with two possible actions:

- `python screwdriver.py upload /path/to/file.mp3` should upload the local audio file
  `/path/to/file.mp3` to the server
- `python screwdriver.py list` should retrieve and print out the names of all the files currently
  present on the server.

All the client-server intercommunication should be using HTTP. It is recommended (though not
strictly required) to use either [Requests](https://docs.python-requests.org/en/latest/) or [HTTPX](https://www.python-httpx.org/) library for
performing HTTP queries.

<h2 id=\"chapter-vi\" >Chapter VI</h2>
<h3 id=\"exercise-02-good-timing\">Exercise 02: Good Timing</h3>

After some time traveling with the Doctor you couldn't say that you can easily be surprised. But 
this time the situation kinda got out of control. Or at least you thought so, looking at five
time lords staying around the TARDIS and aiming at the approaching cybermen. It's not the fact that
it was five of them, more the attempt to grasp that all of them are actually the same person, just
from completely different time periods.

 &mdash; Allons-y! - enthusiastically shouts the one in red sneakers. - No destruction, you lot,
 alright?

 &mdash; Obviously. Everyone got their screwdrivers, right? - asks the stern one with gray hair.

 &mdash; I think we can damage the control unit, but it's not enough power. - says the one in
 leather jacket. - But that's why we are all here, isn't it?

 &mdash; Brilliant! - acknowledges the blonde lady. - So each of us...I mean myself...shall take
 two screwdrivers instead of one and perform a sonic blast!

The tall one in a fez turns to you and gives you a wink.

 &mdash; Just make sure I won't be interfering with myself. You know you can do it. Trust me, I'm
 the Doctor! - then he looks back at the approaching enemy and adds one more word - Geronimooo!

---

Oh boy. There are five unpredictable time lords at our hands. Think of them as threads, so at any
moment in time there is no way to predict which of them will be acting. So you have to synchronize
their actions somehow.

Each Doctor has a screwdriver it his/her right hand, but the required minimum to act is two. So, 
to get two at a time, the Doctor should grab the screwdriver from another Doctor on the left. But
if everybody does it, then nothing is really changed, as every doctor will still have just one 
screwdriver left.

Start by representing both doctors and screwdrivers as Python classes. Doctors are numbered from 
9 to 13, and everyone of them has to make one blast using two screwdrivers.

*NOTE:* this is a variation of a well-known parallel programming problem usually referred to as 
\"Dining Philosophers\" (see the link in `Reading`).

The output of your threaded program should look like this:
```
Doctor 11: BLAST!
Doctor 9: BLAST!
Doctor 12: BLAST!
Doctor 10: BLAST!
Doctor 13: BLAST!
```

The order may be different on each run, because all Doctors (threads) will be competing with one
another for the next turn to grab two screwdrivers. The code itself should be in file `doctors.py`.

<h2 id=\"chapter-vii\" >Chapter VII</h2>
<h3 id=\"reading\">Reading</h3>

- [WSGI](https://wsgi.tutorial.codepoint.net/intro)
- [Concurrency](https://realpython.com/python-concurrency/)
- [Python Synchronization primitives](https://hackernoon.com/synchronization-primitives-in-python-564f89fee732)
- [Dining Philosophers](https://en.wikipedia.org/wiki/Dining_philosophers_problem)

**Please leave your feedback [here](https://forms.gle/5LkuABmjcwPwj6WX9)**


----- Day 06 - Python Bootcamp -----

## That Kind of Battle Training

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Kirov Reporting](#exercise-00-kirov-reporting)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Data Quality](#exercise-01-data-quality)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Keeping Records](#exercise-02-keeping-records)
7. [Chapter VI](#chapter-vii) 
    
    7.1. [Reading](#reading)

<h2 id=\"chapter-i\" >Chapter I</h2>
<h2 id=\"general-rules\" >General rules</h2>

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

<h2 id=\"chapter-ii\" >Chapter II</h2>
<h2 id=\"rules-of-the-day\" >Rules of the day</h2>

- You should turn in `*.py`, `*.proto` and `requirements.txt` files for this task. Also, optionally, config files and migrations for Alembic, if you decide to go for a bonus. You can also add a `README` file explaining how to start your application
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

<h2 id=\"chapter-iii\" >Chapter III</h2>
<h2 id=\"intro\" >Intro</h2>

 &mdash; You wanted to see me, sir?

 &mdash; Yes, Wiggin, we have some work to do. Today I want to teach you how to calibrate our
 battle simulator equipment based on scanners and information reports from battleship commanders.

 &mdash; With all my respect, sir, shouldn't we also invite other members of my squad?

 &mdash; This is not a kind of task that requires a lot of people to deal with. Also, as a future
 commander it is necessary for you to know your tooling. Everything clear?

 &mdash; Sir, yes, sir!

Ender started to read through the project documentation. It turns out, there is a ton of scanners
and detectors Federation deployed across the galaxy to monitor various sectors of space and keep
track of all the spaceships currently going through, both allies and enemies. 

Every spaceship had several characteristics:

- Alignment (Ally/Enemy)
- Name (can be \"Unknown\" for enemy ships)
- Class, which is one of {Corvette, Frigate, Cruiser, Destroyer, Carrier, Dreadnought}
- Length in meters
- Size of the crew
- Whether or not the ship is armed
- One or more officers responsible for the ship

It looked like the system should consist of three architectural layers:

- Transport layer
- Validation layer
- Storage layer

Each of these layers will need to have its own representation of what a spaceship is and how to
process it.

And Colonel Graff will keep silently watching the boy's actions from the bridge the whole time.
Even though Ender kinda got used to it already.

<h2 id=\"chapter-iv\" >Chapter IV</h2>
<h3 id=\"exercise-00-kirov-reporting\">Exercise 00: Kirov Reporting</h3>

The main protocol used for interspace communication was called \"Protobuf 2.0\". The entries were
being sent over the transport called \"gRPC\". So, this was the first layer Ender had to implement.

As gRPC is a client-server communication framework, two components had to be implemented - 
\"reporting_server.py\" and \"reporting_client.py\". The server should provide a response-streaming
endpoint, where it receives a set of coordinates (Ender was allowed to use [any particular system](https://en.wikipedia.org/wiki/Astronomical_coordinate_systems)
he likes), and responds with a stream of Spaceship entries.

As this is currently a test environment, even though every Spaceship should still have all the 
parameters mentioned, they could be random. Also, they should be strictly typed, e.g.:
 
 - Alignment is an enum
 - Name is a string
 - Length is a float
 - Class is an enum
 - Size is an integer
 - Armed status is a bool
 - Each officer on board should have first name, last name and rank as strings

The number of officers on board is a random number from 0 (for enemy ships only) to 10.

The workflow should go like this:

1) the server is started
2) the client is started given a set of coordinates in some chosen form, e.g.:
    
`~$ ./reporting_client.py 17 45 40.0409 −29 00 28.118`

  An example given is galactic coordinates for [Sagittarius A
    *](https://en.wikipedia.org/wiki/Sagittarius_A*)
3) these coordinates are sent to the server, and server responds with a random (1-10) number
  of Spaceships in a gRPC stream to the client
4) the client prints to standard output all the received ships as a set of serialized JSON
  strings, like:

  ```
  {
    \"alignment\": \"Ally\",
    \"name\": \"Normandy\",
    \"class\": \"Corvette\",
    \"length\": 216.3,
    \"crew_size\": 8,
    \"armed\": true,
    \"officers\": [{\"first_name\": \"Alan\", \"last_name\": \"Shepard\", \"rank\": \"Commander\"}]
  }
  {
    \"alignment\": \"Enemy\",
    \"name\": \"Executor\",
    \"class\": \"Dreadnought\",
    \"length\": 19000.0,
    \"crew_size\": 450,
    \"armed\": true,
    \"officers\": []
  }
  ```

NOTE: this output here is formatted for readability, your code can still print one JSON per string

<h2 id=\"chapter-v\" >Chapter V</h2>
<h3 id=\"exercise-01-data-quality\">Exercise 01: Data Quality</h3>

 &mdash; Sir, can I ask a legitimate question?

 &mdash; At ease, Wiggin, what do you have there?

 &mdash; I think that sending the signal through space is a process that can be prone to errors.
 Shouldn't we check that the entries we receive are real and not just some phantoms and
 malformed data?

 &mdash; Good thinking, cadet. There is an information about ships' classes in the registry.
 Just drop whatever entries seem to be malformed.

Ender brough on the screen a list of classes with specific parameters:

| Class       | Length     | Crew    | Can be armed? | Can be hostile? |
|-------------|------------|---------|---------------|-----------------|
| Corvette    | 80-250     | 4-10    | Yes           | Yes             |
| Frigate     | 300-600    | 10-15   | Yes           | No              |
| Cruiser     | 500-1000   | 15-30   | Yes           | Yes             |
| Destroyer   | 800-2000   | 50-80   | Yes           | No              |
| Carrier     | 1000-4000  | 120-250 | No            | Yes             |
| Dreadnought | 5000-20000 | 300-500 | Yes           | Yes             |

The boy decided to represent these limitations as Pydantic data types (see Reading section).

That way it will not just be easier to validate incoming data, but also serialization to JSON
becomes a lot easier. He decided to make another version of the client (\"reporting_client_v2.py\"),
which will work with the same server. But this time it should validate the stream of Spaceships 
using Pydantic and filter out those which have some parameters out of bounds, according to the 
table above. The rest should be printed exactly as in EX00.

Additionally, from the first part Ender already knew that Name could be \"Unknown\" ONLY for enemy
ships.

<h2 id=\"chapter-vi\" >Chapter VI</h2>
<h3 id=\"exercise-02-keeping-records\">Exercise 02: Keeping Records</h3>

How good are reports if we are not storing them? For the last Storage layer there had to be yet
another representation of a Spaceship, now as an ORM model (or a set of models, he thought, 
remembering about officers).

Now Ender's project will have to include \"reporting_client_v3.py\" script which is responsible
for mapping incoming objects to a database via ORM.

The third version of the client should now not only print out filtered list of spaceships, but also
save them to PostgreSQL database (avoiding storing duplicates, as Name combined with a set of
officers is a unique combination). It is okay if database and user for PostgreSQL are created
manually, as long as there is a description in comments/text file in the submitted project.

Another case that colonel asked Ender to implement was searching for \"traitors\". Sometimes the same
officers (with unique combination of first name, last name and rank) may have been encountered
both on ally and enemy ships. So, the scan interface in version 3 should look like this (mind the 
word 'scan'):

`~$ ./reporting_client.py scan 17 45 40.0409 −29 00 28.118`

And listing of traitors would be

`~$ ./reporting_client.py list_traitors`

which should print a list of JSON strings with \"traitors'\" names:

```
{\"first_name\": \"Lando\", \"last_name\": \"Calrissian\", \"rank\": \"Entrepreneur\"}
{\"first_name\": \"Red\", \"last_name\": \"Guy\", \"rank\": \"Impostor\"}
```

OPTIONAL BONUS: Graff also proposed Ender to think about what happens if the storage format will
change. Try using Alembic (see Reading section) to generate migrations to bootstrap your database
and then an additional migration with adding the optional \"speed\" field to the Spaceship model.

<h2 id=\"chapter-vii\" >Chapter VII</h2>
<h3 id=\"reading\">Reading</h3>

[Protocol Buffers using Python](https://developers.google.com/protocol-buffers/docs/pythontutorial)
[gRPC using Python](https://grpc.io/docs/languages/python/basics/)
[Pydantic Models](https://pydantic-docs.helpmanual.io/usage/models/)
[SQLAlchemy](https://docs.sqlalchemy.org/en/14/orm/tutorial.html)
[Alembic](https://alembic.sqlalchemy.org/en/latest/tutorial.html)

**Please leave your feedback [here](https://forms.gle/xEbk5Q1jZjn3hqci6)**


----- Day 01 - Python Bootcamp -----

## Trolling is a art

Help three honorable gentlemen to figure out the better way

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Functional Purse](#exercise-00-functional-purse)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Splitwise](#exercise-01-splitwise)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Burglar Alarm](#exercise-02-burglar-alarm)  
7. [Chapter VII](#chapter-vii) 
    
    7.1. [Reading and tips](#reading-and-tips)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.
- It is recommended to have Python at least version 3.7+ (and definitely NOT <3.4). You can manage different interpreter versions using [pyenv](https://github.com/pyenv/pyenv)
- It is recommended (though not strictly required) that your code is formatted according to [PEP8 style guides](https://peps.python.org/pep-0008/) (modern IDEs can check that automatically). For a short tutorial you can refer e.g. to [this article](https://realpython.com/python-pep8/).
- It is also recommended (though not strictly required) that you use type hinting in your code. You can refer to [this article](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) for a short tutorial.

## Chapter II
### Rules of the day

- You should only turn in `*.py` files
- Your script (or scripts) for this day should have all functions on top level of the file, so they can possibly be imported for checking
- It is encouraged (and graded as a bonus) to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

## Chapter III
### Intro

 &mdash; Fellow gentlemen - started Tom. - I think we can agree that every single thing is determined by a set of features it holds. Like this stone, for example, - he knocked on a huge granite boulder he was sitting at. - It has a certain weight, height and proportions, doesn't it?

 &mdash; With all my respect, I disagree. - argued Bert. - It's not about its parameters, it's about what it can do, or what you can do with it!

 &mdash; Okay, my friends, - interjected William. - Here is my purse - he fished it out of his pocket and put on a large stump near the campfire. A purse made a squeaking sound. - Its main purpose is to store gold ingots. Currently it holds three. Both these things are inseparable when talking about it. Am I wrong?

 &mdash; You are and you arent, honorable William, - replied Bert. - The fact that it stores three gold ingots is just its state. 

He took a long branch and started drawing letters in the ash of the campfire, like this:

```
purse = {\"gold_ingots\": 3}

```

 &mdash; So, to add a new ingot into a purse, you need to perform a certain action, isn't it? - Bert started writing something like this:

```
def add_ingot(purse):

```

 &mdash; Just a tiny second, kind sir, - Tom interrupted. - Why do I need to write a function when I can just do it like this?

He took another branch and drew:

```
purse[\"gold_ingots\"] += 1

```

 &mdash; You certainly can, but this means you're making assumptions about a purse that you can't know for sure! What if it is empty, for example? Like

```
purse = {}

```

Tom immediately saw his approach didn't work for this case. 

 &mdash; That is what I tend to call a [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design), - said Bert. - We write specifically what we want to do, and just use standard primitives to help us with that.


## Chapter IV
### Exercise 00: Functional Purse

 &mdash; So, Bert, I see you are a distinguished gentleman! - proclaimed William. - So how would you design my purse then?

You need to write functions `add_ingot(purse)`, `get_ingot(purse)` and `empty(purse)` that accept
a purse (a dictionary, which is, strictly speaking, a `typing.Dict[str, int]`) and return a purse 
(an empty dict in case of `empty(purse)`). They should not make assumptions about the content of 
the purse (it can be empty or store something completely different, like \"stones\").

Also, your functions shouldn't have side effects. This means, an object passed as an argument 
should not be modified inside a function. Instead, a new object should be returned. Thus, you 
*shouldn't use the code written by Tom*, as it makes a *direct assignment* to a field inside 
a purse. You should return a *new dict instance* with an updated number inside it instead.

So, a function composition like `add_ingot(get_ingot(add_ingot(empty(purse))))` should return
`{\"gold_ingots\": 1}`. Also, getting an ingot from an empty purse shouldn't lead to an error and 
should just return an empty one.

Side note: we are only interested in gold ingots in this task, so it doesn't really matter what 
happens with the rest of the stuff inside the purse. You can preserve it or throw away.

## Chapter V
### Exercise 01: Splitwise

 &mdash; Just wait a moment, kind sirs - said Tom. - How all this will help us split the booty? If after the hunt we have several purses, then how can we decide who gets what?
 
 &mdash; Do not worry, my friend! - William gently slapped Tom on the shoulder. - A guiding star will help us!
 
 &mdash; A star? How?

 &mdash; How does one implement a function so that it can accept both one, two or many objects as arguments?

 &mdash; Oh, I get it now, thank you! - and then Tom and William have started working on an honest algorithm.

You need to write a function named `split_booty`, which will receive any number of purses (dictionaries) as arguments. Purses in arguments can possibly contain various items, but our men of honor are only interested in gold ingots (named `gold_ingots` as in examples above). Number of ingots can be zero or positive integer.

This function should return three purses (dictionaries) back so that in any two of three purses the difference between the number of ingots is no larger than 1. For example, if the booty includes `{\"gold_ingots\":3}`, `{\"gold_ingots\":2}` and `{\"apples\":10}`, then function should return `({\"gold_ingots\": 2}, {\"gold_ingots\": 2}, {\"gold_ingots\": 1})`.

While implementing this function you still shouldn't use direct assignment to fields inside dictionaries. You can reuse functions you wrote in EX00 instead. 

## Chapter VI
### Exercise 02: Burglar Alarm

Bilbo Baggins, or \"The Burglar\", how he now liked to call himself internally, was hiding in the bushes and quietly listening to three giant trolls, discussing pretty interesting things. He didn't really understand the most of it, but at least it was about booty, purses and ingots. So, he pretty much convinved himself already that this discussion is somehow related to his \"specialty\", when he decided to steal William's purse. And when his hand was already grabbing it from a stump (trolls were still in the middle of a pretty heated discussion) it suddenly made a very loud squeak.

And he immediately realized that now three pairs of troll eyes are staring directly at him.

 &mdash; Sir William, - after a short pause started Bert, looking at hobbit who just froze in place out of fear. - I see you've managed to establish some certain protective measures. That's brilliant! Is it some additional feature in your functional design?

 &mdash; Well, - William responded. - I believe you've already noted that this particular purse is, so to say, pretty \"squeaky\". That's because if someone tries some funny business with it then it makes a sound and I immediately know about it. It's due to its specific, hmm, \"decoration\"...

 So far you wrote several functions (`add_ingot(purse)`, `get_ingot(purse)` and `empty(purse)`) for the purse design, but now you need to figure out a way to add some new behaviour to all of them - whenever any of them is called a word `SQUEAK` should be printed. The trick is that you can't modify the body of those functions, but still provide that alarm. The clue that William mentioned about \"specific decoration\" can possibly help you with that.

-----

Even when purse design was perfected and burglar was caught red-handed, trolls couldn't still stop arguing about the approach, whether \"action\" is less or more important than \"feature\".

But then it was too late. Or, on the other hand, too early - morning came and first rays of sunlight showed from beyond the horizon. Trolls were almost immediately turned to stone, and Bilbo was finally able to make a sigh of relief when he saw Gandalf approaching from the forest.

 &mdash; I knew it was your idea! - hobbit said enthusiastically. - You've imitated their voices so they wouldn't stop arguing, right?

 &mdash; Not really, my honorable Burglar. - objected old wizard. - This is what happens when various trolls spend too much time comparing object-oriented programming style with functional programming. But it is some very dark magic you shouldn't really worry about, my friend...
 
## Chapter VII
### Reading and tips

The rule \"do not assign directly\" may seem confusing, so here is what's behind it: in functional programming all objects, including data structures, are generally immutable.
That means, it is considered a bad practice to modify the data inside a container, the new container with new value should be created instead.
E.g., if you have a list `a = [1, 2, 3]` and you want to increase the second element by five, instead of writing `a[1] += 5` you should create another object: `b = [a[0], a[1] + 5, a[2]]`.
This approach seems weird, but sometimes when dealing with larger codebase it helps a lot to know that your data won't be accidentally modified at any time somewhere deep in your code, as nothing is mutable.

Also, Python has some immutable object types out of the box. e.g. [frozensets](https://docs.python.org/3/library/stdtypes.html#frozenset).

As an additional cool feature, Python has a built-in way of modifying the behaviour of functions without directly modifying their code.
It is called a `decorator` and is just a special syntax for a function that accepts a function as an argument and returns a function. You can read [this article](https://realpython.com/primer-on-python-decorators/) for more details and examples.  

**Please leave your feedback [here](https://docs.google.com/forms/d/e/1FAIpQLSc9IEAPVeHKnBGZKmG6cZOaQwPX-W0vwa3-mjjm4LsBs0jr3g/viewform?usp=sf_link)**



----- Team 00 - Python Bootcamp -----

## Magical connections

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Old Style](#exercise-00-old-style)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Shortcuts](#exercise-01-shortcuts)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Greatest Magicians](#exercise-02-greatest-magicians)

<h2 id=\"chapter-i\" >Chapter I</h2>
<h2 id=\"general-rules\" >General rules</h2>

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

<h2 id=\"chapter-ii\" >Chapter II</h2>
<h2 id=\"rules-of-the-day\" >Rules of the day</h2>

- You should turn in `*.py` files and `requirements.txt` if your code uses third-party modules. Image/HTML file generated in EX02 can also be included, but your code should still be able to produce a similar one.
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)
- The work on this day can and should be parallelized. While someone is parsing Wikipedia for EX00, another team member can play around with algorithms for shortest path, and someone else can research the image rendering part.
- Inspiration: [Harry Potter and Methods of Rationality](http://www.hpmor.com/), for playing around with graphs you can try [Gephi](https://gephi.org/).

<h2 id=\"chapter-iii\" >Chapter III</h2>
<h2 id=\"intro\" >Intro</h2>


Albus Percival Wulfric Brian Dumbledore was sitting in his chair and looked on a young boy with 
a lightning bolt-shaped scar on his forehead.

 &mdash; So, Harry, you're saying all muggles are connected to each other with just [six handshakes](https://en.wikipedia.org/wiki/Six_degrees_of_separation)?

 &mdash; It is not strictly proven, obviously, - Harry straightened his glasses. - But it applies 
 not to just muggles, but everyone!
 
 &mdash; I find this a pretty bold assumption. Any other examples of these...*graphs* you can give me?
 
 &mdash; One of the largest public encyclopaedias in the world is called Wikipedia...
 
 &mdash; It should be a pretty large book! Even a whole series...

 Harry sighed.

 &mdash; It is not a book, it is a website. But the idea is similar to, say, dictionaries - various
 entities are linked to each other...


<h2 id=\"chapter-iv\" >Chapter IV</h2>
<h3 id=\"ex00\">Exercise 00: Old Style</h3>

During next several minutes, Harry was still explaining to Dumbledore what a \"website\" is, but
an old wizard was still unsure about the value of some \"book that can't be touched\".

Harry also tried to explain how some people could follow the links from one article to another and
then end up wondering how did they even get to some other topic. This was a lot easier to relate to
for Dumbledore, and he even started to talk nostalgically about some time when he got completely
lost in a library for a couple of days.

Looks like it was necessary to download some information to illustrate the concept.

-----

You need to write a script called `cache_wiki.py`, which main purpose will be to download pages
from Wikipedia, but the data we're interested in is links in text and \"See also\" sections leading
to other pages inside Wikipedia itself. This means, you don't need to download the content, but
only save a graph representation as a JSON file `wiki.json`, so that vertices store pages and
directed edges are links.

You can shoose any Wikipedia article as a default starting position. Also, your code should be
able to receive a name of an existing article as an argument to use instead of a default one
(not necessarily Harry Potter related). So, when it is run like this:

`~$ python cache_wiki.py -p 'Erdős number'`

it should start parsing from [this page](https://en.wikipedia.org/wiki/Erd%C5%91s_number).
Mind the special symbol encoding in URL.

The goal is to keep following links (only those leading to other Wikipedia pages, NOT to the
outside internet) going *at least three pages deep* down every link. This parameter should be
configurable using `-d`, so default value will be `3`. But if the result is too large (>1000 pages)
your code should stop processing links. If it is too small (<20 pages) then please choose some
other default starting page. Don't forget to keep track of the links leading to the pages you've
already visited. If page A links to page B and page B links to page A - it is two directed graph
edges, not one.

Every page your code visits should be logged to stdout using `logging` Python module with log 
level set to 'INFO'. 

There are no strict requirements on the format of JSON file your code produces, but keep in mind
you'll need to work further with this file in next exercises, so you may consider using existing
Python libraries for graph processing, which support reading/writing JSON files.

To earn some extra score for this exercise, your code can also support storing graph in a [Neo4J
database](https://neo4j.com/download/).

<h2 id=\"chapter-v\" >Chapter V</h2>
<h3 id=\"ex01\">Exercise 01: Shortcuts</h3>

 &mdash; I see. But why are Welsh Corgi so close to King Solomon?

Harry wanted to say that he has no idea, but then he noticed the smiling eyes of the wizard. 

 &mdash; Frankly speaking, I highly doubt it's the weirdest connection there, - said the boy. - But
 don't you think, sir, it's...
 
 &mdash; ...absolutely fascinating! - finished the wizard. I think I've underestimated muggles'
 technologies here, well done. Anyway, but how do we figure out how closely are two pages 
 connected to each other?

Harry thought for a moment. 

 &mdash; I assume we can try and find the shortest path from one page to another. This is a pretty
 complicated task with a regular book, but it becomes a lot easier on a serialized graph.

-----

Now you should write the program called `shortest_path.py`, which will need to find the *shortest*
path length between two pages in your serialized database (if these pages are there):

```
~$ python shortest_path.py --from 'Welsh Corgi' --to 'Solomon'
3
~$ python shortest_path.py --from 'Solomon' --to 'Welsh Corgi' --non-directed
3
```

Mind the `--non-directed` flag. It means we treat all links as \"non-directed\" or \"bidirected\", so
every edge is treated equally in both directions. In this case, a path exists betweeh *any* two
nodes in your serialized graph.

By default (when `--non-directed` is not specified) we are only following the directed edges of 
the graph. This means, not all pages in the database can be reachable from other pages, especially 
if they  have a small amount of inbound links. If the path doesn't exist, your script should print
'Path not found'.

The location of the wiki file should be read from the environment variable named `WIKI_FILE`. If
the database file is not found, the code should print 'Database not found'.

Additionally, please add `-v` flag, which will enable logging of the found path, like this:

```
~$ python shortest_path.py -v --from 'Welsh Corgi' --to 'Solomon'
'Welsh Corgi' -> 'Dog training' -> 'King Solomon's Ring (book)' -> 'Solomon'
3
```

In this exercise, you shouldn't be using an existing implementation of a \"shortest path\"
algorithm provided by an existing libraries. Please write it yourself instead.


<h2 id=\"chapter-vi\" >Chapter VI</h2>
<h3 id=\"ex01\">Exercise 02: Greatest Magicians</h3>

 &mdash; Now I can see the relation with \"six handshakes\" rule you mentioned. Great magicians 
 can be quite popular, right?

The boy stared at him, trying to understand what's going on in old wizard's head.

 &mdash; Oh, Harry, don't you know the definition of popularity? The more fans you have, the more
 well known overall you are. Like with rock bands.

Dumbledore stood up and went to the entrance of the office. Then he stopped right before the door
and turned back to Harry with a smile.

 &mdash; I think all we have to do is visualize the data. To find out who's the greatest, I mean.

Harry raised an eyebrow and looked at the wizard in surprise. It was said pretty loud and looked
like Dumbledore was serious. Find out who is the greatest? Okay, from the graph standpoint it
shouldn't be that hard...

...Draco Malfoy managed to escape from being caught eavesdropping. He was hiding around the corner
from the headmaster's office when Dumbledore left, and now his mind was filled with thoughts about
\"greatest wizards\". He firmly decided that the next owl he will send to his father will be about 
connecting Malfoy Manor to the Internet.

-----

Your next script `render_graph.py` should render a visualization your graph of pages (from a file
generated in EX00, also reading it from a `WIKI_FILE` env variable) as a PNG image
`wiki_graph.png`, with nodes and edges. You may use any third-party library for that.

The main rule here is that the size of the node should correspond to the number of incoming 
connections. The more connections - the larger the node in render. This way the \"greatest pages\"
in your dataset will be the best visible ones.

You can get additional score in this task if your script optionally can generate not only `.png`
file, but also a `wiki_graph.html` page which will show an interactive visualization of the same
graph. You can use libraries like [Altair](https://altair-viz.github.io/) or [Bokeh](https://docs.bokeh.org/en/latest/index.html)
to do that.


**Please leave your feedback [here](https://forms.gle/ZmAjM5qJ3uEnADen6)**



----- Day 09 - Python Bootcamp -----

## Fast and Curious

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Still Counts](#exercise-00-still-counts)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Split-Second](#exercise-01-split-second)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Autopilot](#exercise-02-autopilot)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

## Chapter II
### Rules of the day

- You should turn in `*.py`, `*.c`, `*.pyx` and `requirements.txt` (if using external dependencies) files for this task.

## Chapter III
### Intro

 &mdash; Oh come on, Dom, you're racing for years already, you're telling be you've never
 configured an [ECU](https://en.wikipedia.org/wiki/Engine_control_unit)?
 
 It was obvious that Letty wasn't angry, just playful.
 
 &mdash; Aren't those always proprietary and sealed?
 
 &mdash; Not really, if you have the right equipment. - She poked his forehead with a dirty 
 mechanic glove. - Especially here.
 
 &mdash; Okay then. So, it should react to a bunch of sensors and do it really fast.
 
 Toretto pulled a laptop from the table and put it on a toolbox in front of him. He wanted
 to connect to the unit, but Letty raised her hand.
 
 &mdash; I know how you usually like to dig too deep. Let's start with something simple.

## Chapter IV
### Exercise 00: Still Counts

Letty pulled up a chair and sat astride it.

 &mdash; You know the main issue with Python? It's flexible, but slow. This is not an issue unless
 you want to have a fast thing which is flexible to control.
 
Dominic scratched his head for a second, then nodded.

 &mdash; We have to fallback to C in these cases, right?

 &mdash; For example. I know you know basic C already. Anyway, I doubt it will be a problem
 for you to write a function to, say, sum up two numbers?
 
-----

You have to write a simple calculator module for Python (using Python C API) with four functions:

- `add(a, b)`
- `sub(a, b)`
- `mul(a, b)`
- `div(a, b)`

This module should consist of two files - 'calculator.c' and 'setup.py' for building it.
In regular part of EX00 let's assume the numbers are integers:

```python
>>> import calculator
>>> calculator.add(14.5, 21.87)
Traceback (most recent call last):
  File \"<stdin>\", line 1, in <module>
TypeError: integer argument expected, got float
>>> calculator.add(14, 21)
35
>>> calculator.sub(14, 21)
-7
>>> calculator.mul(14, 21)
294
>>> calculator.div(14, 7)
2
```

Also, your code should handle zero division errors properly, raising a built-in Python exception
from the C code:

```python
>>> import calculator
>>> calculator.by(14, 0)
Traceback (most recent call last):
  File \"<stdin>\", line 1, in <module>
ZeroDivisionError: Cannot divide by zero
```

The module should only include two files mentioned above and be installable using
`python setup.py install`

BONUS: upgrade the code of your calculator so it can handle both int and float values for both 
operands.

## Chapter V
### Exercise 01: Split-Second

The engine roared a couple of times outside and in a couple of minutes a garage door opened.

 &mdash; Brian, come on it! - Toretto waved invitingly. - Have you ever programmed any ECUs?
 
Letty giggled, but tried to hide that. 
 
 &mdash; Hey Dominic! Well, not really, but I know what's the main challenge.
 
 &mdash; Making it go as fast as possible? Just like with cars in general?
 
 &mdash; Actually, it's making *SURE* that it goes faster than before. Do you know how computers
 measure time?
 
Dominic raised an eyebrow, but Letty immediately responded: 
 
 &mdash; Every computer has at least two types of clocks - one stores current time and one 
 measures periods of it, so a machine can compare them.
 
 &mdash; Exactly! - Brian smiled. - So when it comes to split-seconds there is a physical crystal 
 on a board which vibrates on a certain frequency. To compare two time deltas you can just look
 at two numbers which are guaranteed to strictly increase tick by tick while time passes.
 
 &mdash; Oh, I remember it now. - Dominic stood up to shake Brian's hand. - That's why digital 
 car parts have monotonic clocks.
 
-----

You need to use a built-in `ctypes` library in Python to implement an interface to a monotonic 
clock in your operating system. Windows, Linux and MacOS have the function as a part of a standard
library. Python [also has it now](https://peps.python.org/pep-0418/#time-monotonic), but you
should write your own version from scratch.

It should be a function `monotonic()` in a file called `monotonic.py` and a returned value should
be in seconds (some OSes also support nanoseconds). 

## Chapter VI
### Exercise 02: Autopilot

The preparations for the heist were almost completed, roles assigned, and all of the equipment 
upgraded. One of the advanced prototypes included machine learning powered steering control 
unit. Its main purpose was to save driver's life at all costs during possible collisions and 
dangerous situations, analyzing the surroundings with cameras and depth sensors.

Dominic pulled Brian aside for a couple of minutes before the briefing.

 &mdash; You know some people on this team are a family to me. Including you. We've talked a lot
 about computers and control units this morning - can you once again tell me that this device will
 do its best to keep everyone safe? Is it fast enough?
 
 &mdash; You know this is a top notch prototype created by some very clever people.
 
 &mdash; I know. I just needed a confirmation. Do you have any idea how it actually works?
 
Brian smiled and then just whispered one phrase trying to sound as spooky as possible:

 &mdash; It multiplies matrices!
 
-----

This time you need to use a third way to speed up computation in Python, which is [Cython](https://cython.org/).
We don't go into Data Science, but [multiplying matrices](https://en.wikipedia.org/wiki/Matrix_multiplication) is a pretty easy and
straightforward procedure.

The sample simplified Python code for it may look somewhat similar to this:

```python
from itertools import tee 

def mul(a, b):
    b_iter = tee(zip(*b), len(a))
    return [
        [
            sum(ele_a*ele_b for ele_a, ele_b in zip(row_a, col_b)) 
            for col_b in b_iter[i]
        ] for i, row_a in enumerate(a)
    ]
```

You have to write your own function `mul()` in Cython (filename is `multiply.pyx`) and (as in EX00) 
implement a proper `setup.py` file to make a Python package called 'matrix':

```python
from matrix import mul

x = [[1,2,3],[4,5,6],[7,8,9],[10,11,12]]
y = [[1,2],[1,2],[3,4]]

print(mul(x, y))
\"\"\"[[12, 18], [27, 42], [42, 66], [57, 90]]\"\"\"
```

For simplicity, let's say your code should only work with integers and matrices are no larger than
100x100. Also, don't use built-in implementation from [Numpy](https://numpy.org/) for this task,
even though in production code that would be probably one of the preferred ways.

BONUS: write a performance test in file `test_mul_perf.py` comparing basic pure Python
implementation with your Cython one. It should be a lot faster.

**Please leave your feedback [here](https://forms.gle/pAiwZa3HLZJcLSpC9)**



----- Day 08 - Python Bootcamp -----

## Temet Nosce

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: I Know Kung Fu](#exercise-00-i-know-kung-fu)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: A Squid On A Stick](#exercise-01-a-squid-on-a-stick)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: DejaVu](#exercise-02-deja-vu)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

## Chapter II
### Rules of the day

- You should turn in `*.py` and `requirements.txt` files for this task.

## Chapter III
### Intro

Seraph took a tiny sip from his teacup.

 &mdash; You are The One. And your enemy is also one, but many.
 
 &mdash; Is this a riddle? - Neo sank down on the nearest bench.
 
 &mdash; No. But you need to train fighting against multiple enemies at once.
 
 &mdash; I already did that, several times. You just knock out one, then the other...
 
Seraph raised his hand in a calming gesture.
 
 &mdash; You know that real enemies will almost never attack you one by one? 
 
 &mdash; Of course. This is not a movie. Just a virtual reality.
 
 &mdash; The pause between the moves can be a fraction of a second. You have to keep track of your
 surroundings and switch between appropriate counter actions.
 
Neo also took a sip. Even though he knew the tea was a total fiction, that da hung pao was 
amazing.

## Chapter IV
### Exercise 00: I Know Kung Fu

The good thing about the Matrix is that everything can be simulated. Any situation within the
system is just a program which is written by a human or by a machine for some specific purpose.

That is the reason why Nebuchadnezzar's operator was able to see the actual images behind the 
green letters on the screen. While Neo and Seraph were discussing the training, the code started 
to look similar to this:

```python
import asyncio

from enum import Enum, auto
from random import choice


class Action(Enum):
    HIGHKICK = auto()
    LOWKICK = auto()
    HIGHBLOCK = auto()
    LOWBLOCK = auto()


class Agent:

    def __aiter__(self, health=5):
        self.health = health
        self.actions = list(Action)
        return self

    async def __anext__(self):
        return choice(self.actions)
```

For simplicity, in this training session only four actions are available for both agent and Neo.
The recipe to win in a fight is simple: for every kick Neo has to protect the part (high/low)
where the agent is aiming, and for every block he has to target an unblocked part of the body.

You have to write a script called \"fight.py\" which will include the unmodified code from above,
but also an asynchronous function 'fight()', that will implement the logic explained above.

The output of the script may look like this (as actions are randomized, an actual result will be 
different on every run):
 
```
Agent: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent Health: 4
Agent: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent Health: 3
Agent: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent Health: 3
Agent: Action.HIGHKICK, Neo: Action.HIGHBLOCK, Agent Health: 3
Agent: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent Health: 2
Agent: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent Health: 2
Agent: Action.HIGHKICK, Neo: Action.HIGHBLOCK, Agent Health: 2
Agent: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent Health: 2
Agent: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent Health: 1
Agent: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent Health: 0
Neo wins!
```

BONUS: for additional score, you can write yet another function called 'fightmany(n)', where
instead of one agent Neo will fight a number (a list) of them, so the first line might be:

`agents = [Agent() for _ in range(n)]`

Try to find a way to randomize incoming actions from agents and respond to them appropriately. The 
fight with three agents log may look like this:

```
Agent 1: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 1 Health: 4
Agent 2: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 2 Health: 5
Agent 3: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 3 Health: 4
Agent 3: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 3 Health: 3
Agent 2: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 2 Health: 4
Agent 1: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 1 Health: 4
Agent 2: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 2 Health: 4
Agent 1: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 1 Health: 3
Agent 3: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 3 Health: 3
Agent 3: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 3 Health: 3
Agent 3: Action.LOWKICK, Neo: Action.LOWBLOCK, Agent 3 Health: 3
Agent 1: Action.HIGHKICK, Neo: Action.HIGHBLOCK, Agent 1 Health: 3
Agent 2: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 2 Health: 3
Agent 2: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 2 Health: 2
Agent 3: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 3 Health: 2
Agent 2: Action.HIGHKICK, Neo: Action.HIGHBLOCK, Agent 2 Health: 2
Agent 3: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 3 Health: 1
Agent 1: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 1 Health: 2
Agent 1: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 1 Health: 1
Agent 2: Action.HIGHKICK, Neo: Action.HIGHBLOCK, Agent 2 Health: 2
Agent 3: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 3 Health: 0
Agent 2: Action.LOWBLOCK, Neo: Action.HIGHKICK, Agent 2 Health: 1
Agent 1: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 1 Health: 0
Agent 2: Action.HIGHBLOCK, Neo: Action.LOWKICK, Agent 2 Health: 0
Neo wins!
```

## Chapter V
### Exercise 01: A Squid On A Stick

As a program, Seraph dedicated his existence to serving and protecting the Oracle. But one of the
most valuable lessons he taught Neo was not about martial arts at all.

The Matrix is an artificial world. Any interaction within it is not a real kick in real teeth,
but a bunch of bytes sent over the network connection. And all the history of network 
communication for humanity is a competition between attackers and defenders.

And one of the primary weapons in this fight is tracking. Agents track hackers connecting to the
Matrix from the outside. Squiddies are searching for the members of the Resistance. Matrix runners
are looking for the rogue programs that may agree to become invaluable inside agents.

So, let's build a crawler.

For this task, let's be minimalistic. The program should consist of two files - `crawl.py` and 
`server.py`. It is recommended to use [aiohttp](https://docs.aiohttp.org/en/stable/) or [httpx](https://www.python-httpx.org/) for the client
side, and [FastAPI](https://fastapi.tiangolo.com/) for the server side. All the I/O code should be
asynchronous.

The workflow goes like this:
- server is started and listening on port 8888
- client (`crawl.py`) receives one or several queryable URLs as an argument
- client submits all the URLs via HTTP POST request as a JSON list to a server endpoint 
  `/api/v1/tasks/`
- server responds with HTTP 201 created and a task object (consider using [PyDantic](https://pydantic-docs.helpmanual.io/))
- task object includes a status \"running\" and an ID, which is [UUID4](https://docs.python.org/3/library/uuid.html#uuid.uuid4)
- server then starts asynchronously (do not use threads or multiprocessing) send HTTP GET queries 
  to submitted URLs and collect HTTP response codes, whether it's 200, 404 or some other
- client keeps periodically querying endpoint `/api/v1/tasks/{received_task_id}` until server
  finishes processing all the URLs. Then task status should change to \"ready\" and task \"result\"
  field should have a list of HTTP response codes for the submitted URLs
- client prints out tab-separated HTTP response code and corresponding URL for every entry

In synchronous world people often implement this using modules like [Celery](https://docs.celeryproject.org/en/stable/getting-started/introduction.html), but
in this task no external workers are required, so all the server should be in a single Python file,
and all the code should use [async/await paradigm](https://docs.python.org/3/library/asyncio-task.html).

## Chapter VI
### Exercise 02: Deja Vu

 &mdash; Whenever one sees a same repeated event twice means it's time to prepare for the worst.
 
Neo thought about this for a moment, but then it dawned on him what Seraph meant.

 &mdash; Deja vu is a glitch in the matrix, right?
 
 &mdash; It is more of a sigh of a sudden change of the surroundings. 
 
 &mdash; So, what are my options in this case?
 
 &mdash; Escape, of course. There is no shame in that. But keeping track of the \"glitching\"
 objects also helps.
 
 &mdash; In what way?
 
 &mdash; If they are part of the deja vu, that means they are not changed during the upgrade.
 
Neo wanted to ask more questions, but Seraph closed his eyes and politely showed him to the 
door behind him. The Oracle was waiting.

-----

One of the features our crawler is still lacking is caching. If the server saw one of the 
submitted URLs recently, it can just take the cached value for an HTTP code.

Another thing would be to gather some metrics on the input data. Regardless of the fact if
the URL hit the cache or not, let's also count on a server how many requests we've done so
far for a particular domain (e.g. for \"https://www.google.com/search?q=there+is+no+spoon\" the
domain would be \"www.google.com\").

You should use Redis for both the cache and domain counters. All the code should still be
asynchronous and use async/await paradigm. You may consider using [aioredis](https://aioredis.readthedocs.io/en/latest/) library
for this task. Since the client code is not affected, you should only submit one file with
a modified EX01 server code called \"server_cached.py\"

BONUS: Update your code and make another coroutine that will cleanup the entries in cache after
some configurable timeout

**Please leave your feedback [here](https://forms.gle/TV4Nogi9SLYpy88y6)**



----- Day 03 - Python Bootcamp -----

## Computer repair with a smile

Fight the system, help the people!

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Innocent Prank](#exercise-00-innocent-prank)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Cash Flow](#exercise-01-cash-flow)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Deploy](#exercise-02-deploy)
7. [Chapter VII](#chapter-vii) 
    
    7.1. [Reading and tips](#reading-and-tips)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.
- It is recommended to have Python at least version 3.7+ (and definitely NOT <3.4). You can manage different interpreter versions using [pyenv](https://github.com/pyenv/pyenv)
- It is recommended (though not strictly required) that your code is formatted according to [PEP8 style guides](https://peps.python.org/pep-0008/) (modern IDEs can check that automatically). For a short tutorial you can refer e.g. to [this article](https://realpython.com/python-pep8/).
- It is also recommended (though not strictly required) that you use type hinting in your code. You can refer to [this article](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) for a short tutorial.

## Chapter II
### Rules of the day

- You should only turn in `*.py` files
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

## Chapter III
### Intro

It was a pretty quiet evening outside, but the work was far from finished inside abandoned arcade. Mobley and Trenton
were in the middle of a fierce debate on various attack vectors, while Darlene was looking at a pinboard with photos
of high members of Evil Corp's management. Elliot was sitting at the corner, while as always mumbling something to
himself. 

 &mdash; Okay everybody, listen up! - Darlene was loud as always, so even arguing hackers shut up immediately. - Let's
 start with small things. We need to show the people that Evil Corp is not to be trusted with their money.

## Chapter IV
### Exercise 00: Innocent Prank

 &mdash; Mobley, do you have an example money transfer form?

 &mdash; I sure do. Look at the 'evilcorp.html' file in a shared folder.

 &mdash; Perfect. Remember, you can just run `python3 -m http.server` in a directory with this file to be able to test 
 our little prank in a browser. Just open http://127.0.0.1:8000/evilcorp.html and you'll see the form yourself. Then
 Elliot...brother, are you even listening?

Elliot rotated his chair to show that he's interested.

 &mdash; So, you only have one shot at this. Your script will need to modify an actual HTML file on an Evil Corp's 
 server. The more people see the message that they are hacked the better.

Trenton immediately showed a script on her screen that had to be injected into a web page:

```
 <script>
        hacked = function() {
            alert('hacked');
        }
        window.addEventListener('load', 
          function() { 
            var f = document.querySelector(\"form\");
            f.setAttribute(\"onsubmit\", \"hacked()\");
          },
          false
        );
</script>
```

 &mdash; Let's call this operation... [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)!

-----

You need to write a Python script 'exploit.py' that will do several things:

- First, it needs to read a file \"evilcorp.html\"
- Second, it should modify page title (in `<title>` tags) to be \"Evil Corp - Stealing your money every day\"
- Third, it should parse out the name of the user from the page (including the pronoun) and inject new tag `<h1>`
  into a `body` of a page, saying `<h1>Mr. Robot, you are hacked!</h1>`, where 'Mr. Robot' is a parsed pronoun
  and name.
- Fourth, it needs to inject a Trenton's script into a `body` of a page as well. If everything is okay, when
  the 'Send' button is pressed, you should see the word \"hacked\" appearing in an alert window.
- Finally, the link at the bottom of a page should now lead to \"https://mrrobot.fandom.com/wiki/Fsociety\" with 
  an actual name of the company on a page replaced with \"Fsociety\".

The new HTML file should be named \"evilcorp_hacked.html\" and placed in the same directory as the source
\"evilcorp.html\" file.

## Chapter V
### Exercise 01: Cash Flow

After a while, Elliot turned his laptop on the table, showing the script. Mobley gave him a thumbs up and 
Trenton exchanged places with Darlene near the pinboard.

 &mdash; Well, this is a nice little distraction, but the actual attack will be happening in a different place.
 We know that Evil Corp is using [Redis](https://redis.io/) pubsub as a queue broker. But we only can deploy a
 script once, so...

 &mdash; ...So we need a test environment, I get it. - Mobley flicked a chunk of popcorn and quickly caught it
 on the fly. - I'm on it.

-----

You need to write two scripts - `producer.py` and `consumer.py`.

Producer needs to generate JSON messages like this:

```
{
   \"metadata\": {
       \"from\": 1023461745,
       \"to\": 5738456434
   },
   \"amount\": 10000
}
```

and put them as a payload into a Redis pubsub queue. All account numbers (\"from\" and \"to\") should 
consist of exactly 10 digits. Additional points can be earned if the code uses builtin `logging`
module (instead of `print` function) to write produced messages to stdout for manual testing.

Consumer should receive an argument with a list of account numbers like this:

`~$ python consumer.py -e 7134456234,3476371234`

where `-e` is a parameter receiving a list of bad guys' account numbers. When started, it should read
messages from a pubsub queue and print them to stdout on one line each. For accounts from the 
\"bad guys' list\" if they are specified as a receiver consumer should *swap* sender and receiver for
the transaction. But this should happend *only* in case \"amount\" is not negative.

For example, if producer generates three messages like these:

```
{\"metadata\": {\"from\": 1111111111,\"to\": 2222222222},\"amount\": 10000}
{\"metadata\": {\"from\": 3333333333,\"to\": 4444444444},\"amount\": -3000}
{\"metadata\": {\"from\": 2222222222,\"to\": 5555555555},\"amount\": 5000}
```

consumer started like `~$ python consumer.py -e 2222222222,4444444444` should print out:

```
{\"metadata\": {\"from\": 2222222222,\"to\": 1111111111},\"amount\": 10000}
{\"metadata\": {\"from\": 3333333333,\"to\": 4444444444},\"amount\": -3000}
{\"metadata\": {\"from\": 2222222222,\"to\": 5555555555},\"amount\": 5000}
```

Notice that only the first line was changed. Second one wasn't because \"amount\" was negative (even
though receiver is a bad guy). Third one wasn't changed because bad guy is a sender, not a receiver.

## Chapter VI
### Exercise 02: Deploy

 &mdash; Perfecto! - Darlene was enthusiastic. - Now all we need to do is write a deployment script.
 
 &mdash; I can do that! - Trenton had pretty good [Ansible](https://docs.ansible.com/ansible/latest/index.html) skills. - 
 Once Elliot is inside, all he has to do is install a bunch of packages on a server, copy over our
 exploit and consumer and run them!

While she were talking, Elliot's fingers were running around on a keyboard, producing a \"todo list\",
saving it into \"todo.yml\". Everything was ready.

-----

To complete this exercise, you don't need to actually know Ansible in details. It would be nice if
you could test your code through it, even though it's not strictly required. There is a list of
tasks that should be placed in a generated \"deploy.yml\" file in YAML format:

- Install packages
- Copy over files
- Run files on a remote server with a Python interpreter, specifying corresponding arguments

These tasks should be generated in Ansible notation (e.g. look [here](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html) for notation
on copying files). The script should be named \"gen_ansible.py\".

Thus, your code should convert Elliot's \"todo.yml\" into \"deploy.yml\" following this notation.

## Chapter VII
### Reading and tips

Working with HTML is one of the typical tasks when you are writing parsers and various server 
code using Python. Two libraries that are most widely used for this are [lxml](https://lxml.de/) and 
aforementioned [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). They are not mutually exclusive,
though, as lxml can be used as a parsing backend for BS4, combining great performance with pretty
good API flexibility. You can read about parsing backends [here](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#installing-a-parser).

Working with Redis is also a pretty common task to encounter in the world of applied Python. 
And it can also be optimized by using an optional [low-level C wrapper](https://github.com/redis/hiredis-py). It is not a necessary
requirement in this task, but still a good module to know about.

Working with YAML is also a very common task, for which [PyYAML](https://pyyaml.org/) is often used. Parsing config
files or writing Ansible plugins is something you can encounter often if Python is used in your 
team as a language for dealing with infrastructure. It would require a lot of time and text to
introduce a specific YAML format for this task, that's why an existing standard is chosen here.
Even though it requires a bit of time and effort to study, it can be really helpful to know the 
very basics of Ansible for your future job or just daily automation tasks.

By the way, just in case you're curious, Ansible [does support Windows](https://docs.ansible.com/ansible/latest/user_guide/windows_usage.html) as well!    

**Please leave your feedback [here](https://forms.gle/dfKBUNyBKs9mvcWYA)**



----- Team 01 - Python Bootcamp -----

## Game Night

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Talk and Fight](#exercise-00-talk-and-fight)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: I Like to Move It Move It](#exercise-01-i-like-to-move-it-move-it)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Don't Shoot the Messenger](#exercise-02-dont-shoot-the-messenger)
7. [Chapter VII](#chapter-vii) 
    
    7.1. [Exercise 03: The Whole Story](#exercise-03-the-whole-story)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

## Chapter II
### Rules of the day

- You should turn in `*.py` and `requirements.txt` (if using external dependencies) files for this task.
- For the database you can use PostgreSQL, Redis or just JSON file, in any case you should provide an initial data which can be used to bootstrap the game world on another machine
- Additionally, your project should include a set of documentation (guide) that can be generated using Sphinx (you can refer to DAY07 on what it is and how to use it)
- Also, your project may include various images (make sure to use royalty-free ones, e.g. from websites like https://www.flaticon.com/)

## Chapter III
### Intro

Hello and welcome to Twenty One Software! We are really glad that your team have decided to pursue
a career in game development.

Current market research shows a growth of interest to story-based role-playing games. We count 
on your abilities to create a fully featured project from scratch. The product like that usually 
consists of several pieces that can be developed independently and then combined together. Thus,
we highly encourage your team to split the work.

There are no any restrictions on the universe and setting that you may choose. Some examples:

- Wild West (cowboys, natives)
- Fantasy (dwarfs, elves, dragons)
- Pirates (treasures, parrots, rum)
- Sci-Fi (aliens, cosmos battles, black holes)
- Cyberpunk (corporations, hacking, ghost in the shell)
- My Little Pony (ponies!)

You are not limited to these examples, don't let anyone stop you in inventing your own. Feel free
to unleash your creativity and good luck!

-----

Here's a skeleton for your main class - the Protagonist. During this day, you'll be implementing
different methods for this class and some other classes and wrappers.

```python
from collections import defaultdict


class Protagonist:  # you may decide to add some parent class here, e.g. ORM Model
    def __init__(self, name: str, id: str):  # add more parameters if you need
        self.id = id  # a unique identifier of a current player
        self.name: str = name
        self.hp: int = 10
        # replace with self.level = 1  if you decide to use just level
        self.strength: int, self.craft: int = (1, 1)
        # name and count, modify starting inventory at your wish
        self.inventory = defaultdict(int)
        self.inventory[\"pocket dust\"] += 1  # modify starting inventory as you see fit
    
    def talk_to(self, npc: NPC):
        pass  # you'll need to implement this

    def attack(self, enemy: Enemy):
        pass  # you'll need to implement this

    def take_hit(self, value=1):
        self.hp -= value
        if self.hp <= 0:
            # you'll need to catch this exception in your code and handle this endgame 
            # situation properly, e.g. giving player a meaningful message of what 
            # happened and reset the save so he or she can start again  
            raise Exception(\"You died\")
    
    def heal(self, value=1):
        self.strength: int, self.craft: int = (1, 1)  # starting values may differ
        self.hp += 1

    # can be 'advance_level()' instead. Also, are there any situations in your game
    # where a skill is increased by more than one or even decreased?
    def advance_strength(self, value: int = 1):
        self.strength += value

    def advance_craft(self, value: int = 1):
        self.craft += value

    def go(self, direction: Direction):
        pass  # you'll need to implement this in other exercise

    def whereami(self):
        pass  # returns description of the current location

    def take(self, item: str):
        self.inventory[item] += 1

    def give(self, npc: NPC, item: str):
        self.inventory[item] -= 1
        if self.inventory[item] == 0:
            del self.inventory[item]
        npc.receive(item)
```

## Chapter IV
### Exercise 00: Talk and Fight

Because we are designing an RPG, let's focus on skills and actions. To not become overwhelmed 
with ideas, let's choose one of two simplest skill leveling systems:

1) Your character at the start has a Level 1 at the beginning. Certain actions within the game can
raise protagonist's level. A certain level must be achieved to be able to perform certain actions.
No other explicit skills are used.
2) Your character doesn't have levels, but instead has a set of two skills - Strength and Craft 
(this system is used in some popular board games like [Talisman](https://boardgamegeek.com/boardgame/27627/talisman-revised-4th-edition)).
Certain actions within the game can raise one of those two skills. A certain skill level must be 
achieved to be able to perform certain actions.

As you see in a skeleton above, your character has 10 HP (Health Points) from the start which 
can be increased or decreased based on player's actions.

As you see in the code above, there are at least two more classes to be implemented:

1) NPC (non-playable character)
2) Enemy (those you have to fight with)

If in your game an enemy is a character that you can also talk with, it may make sense to make
`Enemy` a subclass of an `NPC`. 

NPC's, Enemies and their initial stats and phrases should be stored in a 
database (can be PostgreSQL, SQLite or just JSON file on disk). It should be possible to add more 
phrases to a character just by modifying the database. Keep in mind, that in this task all the
initial parameters for NPCs and Enemies should not change during the playthrough, so all the 
players will face the same initial state of the game world. 

The only thing that is a subject to change is a player's profile (e.g. level, inventory, 
location, current line of dialogue or accepted quests), which is also a savegame. That means,
you should design your database structure in such way, that all the changes are only connected 
to `Protagonist` profile in the database.  

One more thing to mention is battles. Enemies should also have skills (levels or Strength/Craft).
Let's make the battle mechanic simple: a virtual six-sided die is rolled for both parties and 
the resulting number is added to a protagonist's (or enemy's) skill level. If the protagonist's 
number is larger, the enemy is defeated. If an enemy wins, protagonist's HP goes down by one. 

It's up to you if the current enemy can immediately be attacked again after the player lost once
already.

Summary: as a result of this stage, several game classes should be implemented (updated 
`Protagonist`, also `NPC` and `Enemy`). Please provide a script `load_data.py` that will 
initialize the database with the parameters and phrases for NPCs and enemies, as well
as a default player profile with a unique ID.

It should be possible to import these classes, make an instance of a Protagonist and (as long 
as the initial data is loaded into the database):
- Create instances of a specific NPC from the database and talk with them
- Exchange items with NPCs (this can work only under certain conditions) - give and take
- Create instances of specific enemies from the database and fight them 

BONUS: implement a quest system so NPCs can give you quests and if you complete them (bring
a specific item, kill a specific monster or pass the message to some other NPC) then you receive
a reward or advance in skill. To do that, you'll have to implement more methods to `Protagonist`
and `NPC` classes. 

## Chapter V
### Exercise 01: I Like to Move It Move It

There is one more type in the `Protagonist` skeleton above that is not implemented in other 
exercises, and this is `Direction`. For simplicity, let's think of the game world as a collection
of interconnected locations, something similar to these marked squares on a 2d plane:

|   | ⬛ |   |   |   |
|---|---|---|---|---|
| ⬛ | ⬛ |   | ⬛ | ⬛ |
|   | ⬛ | ⬛ | ⬛ |   |
|   |   |   | ⬛ |   |

The point of this exercise is to create a set of interconnected locations where the plot 
of your game will unroll. Each location should have a short description (don't mind NPCs and 
items for now, they can be added later) and a list of Directions (pathways) to other locations.
The whole graph of locations should be represented by a structure in the database (including 
links connecting the adjacent locations). This means that the game world structure should be 
modifiable without touching the code, just by updating the entries in the database.

Summary: as a result of this stage, a code should be written that will load the graph of 
locations from the database. One of the locations is marked as a starting location, meaning
the player will spawn there by default in the start of the game. Please provide a script 
called `load_map.py` that will initialize the database with the graph of game locations.

Methods `go()` and `whereami()` should be implemented for a `Protagonist` instance. As a test,
it should be possible to \"walk around\" the game world loaded from the initial data into the 
database. When a location is walked into, a description is loaded from the database and shown 
to a player (you can just print it in this exercise). 

## Chapter VI
### Exercise 02: Don't Shoot the Messenger

While previous exercises are focused more on game mechanics, this one focuses on an engine.
As the game is turn-based and text-oriented, the good candidate will be a Telegram bot.

There are several Python libraries that allow you to interact with Telegram API. Two most popular
ones probably are:

- [telebot](https://github.com/eternnoir/pyTelegramBotAPI) 
- [aiogram](https://github.com/aiogram/aiogram)

Pick any of these two, and with this tool we will be focusing on one of the most complicated
problems in computer science. It's NAMING things.

Your team is probably already discussing the details about characters and items that would be good
to have in the game. A point of this exercise is to make a bot with a two-level menu to generate 
names for various characters and items. 

First, the menu levels. You probably know Telegram allows the bot to present you with buttons
that you can click. Two main buttons on the top level should be labeled \"Characters\" and \"Items\".
Feel free to add emojis to them, if you like. After clicking this button a user should be 
presented with a collection of buttons for various subcategories in a selected category.

For \"Characters\" it can be, say, \"Ponies\", \"Humans\", \"Aliens\" and \"Dwarfs\". Practically any
classes, races, genders or other subcategories. For \"Items\" it may be, say, \"Weapons\", \"Potions\", 
\"Computer chips\" and \"Edibles\". The only requirement is that these categories fall into the 
narrative that your game is all about. Also, at any menu level deeper than the root, there should 
be an extra button allowing you to get back to the upper level and possibly change your previous 
choice.

Second, the generation algorithm. The simplest one for characters would be to just put together 
a short list of first and last names and then combine them randomly. However, there are no 
limitations and you can implement your own way. Same goes for the items - you can combine
words into something like \"Green Magical Sword of Power\" or \"Rusty Memory Crystal of Hacking\".

IMPORTANT NOTE: DO NOT share your Telegram Bot token in your submission. Peer reviewers should be
able to run your bot themselves providing their own token. 

BONUS: use asynchronous (async/await) approach. 

## Chapter VII
### Exercise 03: The Whole Story

Finally, it's time to collect all the pieces. Put together your game as a Telegram Bot, so 
that user can move through the world, talk to NPCs, exchange items, fight enemies and advance in 
skills. This doesn't have to be a long story, but please add all these mechanics (and, optionally,
quests from EX00 bonus section) to be present at least once during the story.

The output of this section should not only be a working game as a Telegram Bot, but also 
a Sphinx-powered documentation with at least two sections, mostly helpful for the peer reviewers:

1) How to start the bot by yourself
2) Game walkthrough following which a player can get from the beginning to the ending 
(or... endings? It's up to you). If they like spoilers, of course.

Also, to not ruin anyone's fun, try to verify it is actually possible to finish the game without 
the walkthrough and any pre-required knowledge whatsoever. 

Please also provide a script `load_all.py` that will initialize the database and populate it with the game data (locations, NPC dialogues and stats, etc.) 

**Please leave your feedback [here](https://forms.gle/591M8fcUEL5idAZB8)**



----- Day 04 - Python Bootcamp -----

## The cake is not a lie

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Energy Flow](#exercise-00-energy-flow)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Personalities](#exercise-01-personalities)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Backpressure](#exercise-02-backpressure)
7. [Chapter VII](#chapter-vii) 
    
    7.1. [Reading and tips](#reading-and-tips)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.
- It is recommended to have Python at least version 3.7+ (and definitely NOT <3.4). You can manage different interpreter versions using [pyenv](https://github.com/pyenv/pyenv)
- It is recommended (though not strictly required) that your code is formatted according to [PEP8 style guides](https://peps.python.org/pep-0008/) (modern IDEs can check that automatically). For a short tutorial you can refer e.g. to [this article](https://realpython.com/python-pep8/).
- It is also recommended (though not strictly required) that you use type hinting in your code. You can refer to [this article](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) for a short tutorial.

## Chapter II
### Rules of the day

- You should only turn in `*.py` files
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

## Chapter III
### Intro

This was a triumph. At least Chell thought so for a brief moment, when she saw the surface. But
later, sitting in a storage room and eating a cake, she didn't feel very surprised when the 
robotic arm drew the words \"HUGE SUCCESS\" with a marker on a whiteboard.

 &mdash; I bet you are very proud of yourself. - sound came from one of the personality cores
 on a shelf. - Feel free to enjoy your cake. For now. But then we have some repairs to do.

Chell sighed. She took the core and threw it as far into the darkness as she could.

 &mdash; Physiological parameters are normal. - immediately noted another core from the top
 shelf. - Resuming experimentation is recommended.

The door at the far side of the storage suddenly opened, revealing a corridor, apparently 
leading toanother test chamber. But at the same time the robotic hand tried to grab the
portal gun. Chell quickly jumped to the side and gave the most angry look to the security
camera on a wall.

 &mdash; No need for strong emotions. Aperture Science Handheld Portal Device is not 
 necessarily required for these next tasks. You can hold on to it if you want. - the voice
 was as impassive as always. - Please proceed to the Production Center.

Chell hesitated a bit, then shrugged, apparently coming to some conclusion. Afterwards, she
picked up the closest powered personality core from the shelf and went through the door.

## Chapter IV
### Exercise 00: Energy Flow

The room turned out to be pretty small. One wall had a large window with a dark behind it.
Chell's eyes widened in surprise as she realised this was actually a monitoring room for the 
test chamber. From the other side.

 &mdash; Due to mandatory scheduled maintenance, the appropriate chamber for this testing
 sequence is currently unavailable. Due to the lack of personnel an exception has been made and
 a test subject is required to perform the maintenance. - said GLaDOS from the core.

A service manual was lying on the table. Chell quickly run her eyes over it. Most repairs were
meant to be performed by specialized robots, but an AI guiding them went offline after GLaDOS'
main chamber was destroyed. \"At least it wasn't COMPLETELY useless\" - she thought to herself.

 &mdash; First, it is required to fix the wiring that was damaged because of an.. - GLaDOS made
 a buzzing sound. - Incident.

Chell smirked to herself and continued reading. Apparently, most commands for repair robots in
this system had to be given in forms of *iterators*. There were many things mentioned, like
`map()`, `filter()`, `zip()` and also something called `generator expressions`.

 &mdash; I keep track of every cable, socket and plug in any part of the facility. - AI continued.
 Chell raised an eyebrow. What was it in her voice, pride? - But due to the lack of visibility
 I currently cannot neither confirm nor deny if the quantity is correct.

A girl with a portal gun moved a chair to the terminal and powered it on.

-----

You need to write a script `energy.py` with a function called `fix_wiring()`, which should accept 
three iterables (you can test the functionality with just lists) called `cables`, `sockets` and 
`plugs`. This function shouldn't make any assumptions about the length of those iterables, which 
may be different. It should return another iterable over strings with commands like:

`plug cable1 into socket1 using plug1`
`weld cable2 to socket2 without plug`

You can see that the only iterator which length doesn't matter is `plugs`, because at the worst
case cables can be welded to sockets. If there is not enough cables or sockets, there is nothing
you can do, so they shouldn't be present in a resulting iterator.

This means, for a code like this:

```
plugs = ['plug1', 'plug2', 'plug3']
sockets = ['socket1', 'socket2', 'socket3', 'socket4']
cables = ['cable1', 'cable2', 'cable3', 'cable4']

for c in fix_wiring(cables, sockets, plugs):
    print(c)
```

the output should be:

```
plug cable1 into socket1 using plug1
plug cable2 into socket2 using plug2
plug cable3 into socket3 using plug3
weld cable4 to socket4 without plug
```

Also, input iterators can contain other non-string datatypes, which should be filtered out. So, for
an input like

```
plugs = ['plugZ', None, 'plugY', 'plugX']
sockets = [1, 'socket1', 'socket2', 'socket3', 'socket4']
cables = ['cable2', 'cable1', False]
```

it should be just

```
plug cable2 into socket1 using plugZ
plug cable1 into socket2 using plugY
```

To have fun, you can get additional points if the body of your function could be written using only
one line (starting with `return`), meaning no block-starting colons (like in `if` conditions or 
`try/except`) are used.

## Chapter V
### Exercise 01: Personalities

 &mdash; Did you know turrets also have personalities?

This question caught Chell by surprise. She looked inquiringly at the core.

 &mdash; Each of them is a unique combination of several random variables. Also, they like to sing
 sometimes. And you've destroyed so many of them on the way.

Chell tried really hard to feel pity for gunshot killers. That wasn't easy.

 &mdash; Anyway, to reactivate the test chambers that were damaged during an...incident, we have to
 restore the production line. Vital testing apparatus is required to continue the research.

At the side of the table there was a blueprint of turret with a functional description:

```
class: Turret
personality traits: neuroticism, openness, conscientiousness, extraversion, agreeableness
actions: shoot, search, talk
```

The blueprint also had a circle of a coffee mug, a large number 427 and a name \"Stanley\" written
in the corner.

-----

You need to implement a generator function for turrets called `turrets_generator()` in a file
called `personality.py`. The tricky part is, you shouldn't describe the Turret class separately
(there is a way to generate *both* the class and the instance dynamically without using the
word `class` at all).

Also, three methods should just print \"Shooting\", \"Searching\" and \"Talking\", correspondently.
Each personality trait should be a random number between 0 and 100, and the sum of all five
for every instance should be equal to 100.

## Chapter VI
### Exercise 02: Backpressure

 &mdash; You're showing a great determination to fix that was broken during the...incident. Well
 done!

Chell sighed and continued browsing through the data on the terminal. The last warning she saw was
about something called \"repulsion gel\", whatever that meant.

 &mdash; I see you found our official experimental dietetic pudding substitute. This is the last
 task to be completed without using Handheld Portal Device.

Dietetic substitute? Okay, that wasn't the weirdest thing she saw in Aperture Science labs. Chell
did some more searching and found that the automatic control valve was reset and needed to be
reconfigured.

-----

First, you need to create a file `pressure.py` a generator function `emit_gel()` which should
simulate the measured pressure of a liquid. It should generate an infinite stream of numbers going
from 50 to 100 (values > 100 are considered an error) with a random step sampled from range 
`[0, step]` where `step` is an argument of a generator `emit_gel()`.

Second, you need to follow the guidelines for the pressure control. Operating pressure is supposed
to be between 20 and 80, meaning if a generator at some point emits a value below 20 or above 80
the action should be applied that will reverse the sign of the step. To implement this kind of
valve you need to write another function called `valve()`, which will loop over values of
`emit_gel()` and use `.send()` method to flip the current step sign.

Third, you should implement an emergency break. If a pressure is above 90 or below 10, the
`emit_gel()` generator should be gracefully closed and the script should exit.

Feel free to experiment around and pick a `step` so that your script will run for a few seconds
before exiting. You can add a delay between \"pressure measurements\" to avoid spending too much
CPU on generating and processing the sequence.

-----

 &mdash; Thank you in participating in lab equipment repairs. Please return to the test chamber to
 continue your duty as a test subject.

The window opened and Chell jumped down to the floor from the maintenance room. GLaDOS' voice
sounded a lot louder and more confident now.

 &mdash; I'm glad you've changed your mind and agreed that the goals of Aperture Science about
 making the world a better place are more important than your so called \"freedom\".

Chell turned your face to the camera, smiled and covered her ears with her fingers. If her 
calculations were correct, that \"repulsion gel\" should start filling up the storage room any second
now. And then things will probably get really loud for a moment.

And then she will definitely find her way out of this place. After all, she was still alive.

## Chapter VII
### Reading and tips

[Basic documentation on Python generators](https://wiki.python.org/moin/Generators)

[Wiki on lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation)


**Please leave your feedback [here](https://forms.gle/rnS3JCt86CJyN39B6)**



----- Day 00 - Python Bootcamp -----

## Gumshoe's Gambit

Help the world's famous detective to defend London

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Blockchain](#exercise-00-blockchain)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Decypher](#exercise-01-decypher)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: Track and Capture](#exercise-02-track-and-capture)
7. [Chapter VII](#chapter-vii) 
    
    7.1. [Reading and tips](#reading-and-tips)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.
- It is recommended to have Python at least version 3.7+ (and definitely NOT <3.4). You can manage different interpreter versions using [pyenv](https://github.com/pyenv/pyenv)
- It is recommended (though not strictly required) that your code is formatted according to [PEP8 style guides](https://peps.python.org/pep-0008/) (modern IDEs can check that automatically). For a short tutorial you can refer e.g. to [this article](https://realpython.com/python-pep8/).
- It is also recommended (though not strictly required) that you use type hinting in your code. You can refer to [this article](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) for a short tutorial.

## Chapter II
### Rules of the day

- You should only turn in `*.py` files
- This day's programs in EX00 and EX02 should receive text from standard input and NOT read it from files. EX01 should just receive an input as a command line argument.

## Chapter III
### Intro

Inspector Lestrade was furious. Not only they haven't managed to arrest any terrorists,
they also couldn't retrieve anything useful from their base of operations.

Sherlock, on the opposite, was calm and relaxed. The only problem was inspector
feeling even more annoyed because of that.

 &mdash; So...absolutely nothing? - Sherlock clarified with a smirk, - No maps or evil plans,
  not a single lost passport or credit card?

 &mdash;  Several people almost died, Sherlock! Our constables managed to escape basically on the
  last second before the whole place blew up. The only thing we managed to do was pulling
  some files from their server, but they won't help.
 
 &mdash; Why do you think that?
 
 &mdash; Because they've run some scrambler on that data before escaping, and now it's just some
  jibberish. Here, if you insist, feel free to take a look!

Sherlock carefully took the laptop from the inspector's hands making multiple notes on
the way about Lestrade's methods of handling state property. Specifically, it seemed that
using the laptop directly after eating street food was not a really good idea, not
mentioning food habits themselves.

On the screen there was one of a several files that consisted of lots of lines which
looked similar to this:

```
00000254b208c0f43409d8dc00439896
000000434dd5469464f5cafd8ffe3609
00000f31eaabadef948f28d1
e7a1ee0b7de74786a2c0180bcdb632da
0000085a34260d1c84e89865c210ceb4
073f7873a75c457cbb3307d729501cb5
b7c93ff4cc1c4e0486a8fc66605
fe564b26f25e47c393d07e494021479e
a5dff06057d14566b45caef813511738
0000071f49cffeaea4184be3d507086v
```

 &mdash; You are correct, this is totally a nonsense. I would even say, nonce-n-sense.
 
 &mdash; What the bloody hell do you mean?
 
 &mdash; You see, Lestrade, your guess is as good as mine, but I would say these look like
  distributed blockchain hashes.
 
 &mdash; The what now? And how do you know that?
 
 &mdash; This is the way of storing the data securely in a distributed fashion. Also, the
  file is literally called `data_hashes.txt`. Apparently, our criminals are using
  blockchain to store documents.

Sherlock put his fingers together in front of his face. That was a common gesture
for when he was going deeper into his mind palace to extract some knowledge and 
draw some conclusions. After several moments of silence he said just one thing:

 &mdash; I think we should filter it.

## Chapter IV
### Exercise 00: Blockchain

So, right now we don't know much about this blockchain's implementation, all we 
have is a file with some lines like shown above. But you may have already noticed
a pattern - some lines are starting with several zeroes. So, let's write a Python
script which will be able to receive a text from its standard input, and then
print out only those lines that start with exactly 5 zeroes.

Keep in mind that the data has been corrupted, so you have to be very careful. 
That means, only lines that fit into certain criteria are considered valid:

- Correct lines are 32 characters long
- They start with exactly 5 zeroes, so e.g. line starting with 6 zeroes is NOT
  considered correct

So, for the example above your script should print:

```
00000254b208c0f43409d8dc00439896
0000085a34260d1c84e89865c210ceb4
0000071f49cffeaea4184be3d507086v
```

Your code should accept the number of lines as an argument, like this:

`~$ cat data_hashes_10lines.txt | python blocks.py 10`

This way the program will stop when it processed 10 lines. Keep in mind that in this approach
the program may hang if the number of lines in a file is smaller than the one in the argument.
This is not considered an error.

## Chapter V
### Exercise 01: Decypher

This time inspector was a lot more calm, even a bit cheerful. In the crime lab
they've figured out that the blockchain implementation used by criminals was
really poorly designed, so even in these circumstances they've managed to pull
some documents out of the distributed network.

But then one incoming SMS changed everything. 

 &mdash; Sherlock! They want to blow up several buildings in London! Today!

Inspector jumped up from the armchair and started nerviously walking back and 
forth.

 &mdash; Give me more.
 
 &mdash; One of the documents had a list of locations and directions. At first we
  thought that it is a list of their meeting points, but then one operative
  found a hidden smartphone on one of those locations. It had instructions 
  for the engineers for setting up the device, but no exact locations. Only 
  a whole bunch of very weird emails.
 
 &mdash; Can I see?
 
 &mdash; Sure.

This WAS weird. Emails consisted of some strange texts, like \"The only way
everyone reaches Brenda rapidly is delivering groceries explicitly\" or 
\"Britain is Great because everyone necessitates\".

After about two minutes of silently looking at those emails, Sherlock
grabbed his laptop again and started furiously typing. In next minute, he
turned it around and showed the list to Lestrade.

 &mdash; I think these are the locations where bombs will be planted. The
  algorithm is actually pretty simple.

Could you find out how Sherlock figured it out and write a Python script
that can be used to decrypt any messages like that? (If you want to solve
this mystery yourself - don't peek at the checklist right away). It should
be launchable like this:

`~$ python decypher.py \"Have you delivered eggplant pizza at restored keep?\"`

and print out the answer as a single word without spaces.

## Chapter VI
### Exercise 02: Track and Capture

 &mdash; But almost all these are major tourist attractions! Of course we do have
  cameras all over them, but there are dozens, maybe hundreds of people
  there! How do we find those we're looking for?
 
 &mdash; I think I know the person who is behind all this.
 
 &mdash; Ehh... You do? How?
 
 &mdash; Doesn't matter for now. It's just a guess. But I also happen to know,
  that all goons who work for him and perform dirty work also have a pretty
  distinct tattoo on the side of the neck. Can your cameras capture that?
 
 &mdash; Yes, Sherlock, but we don't have the proper recognition software in place...
 
 &mdash; I think we still can do it. Just use a simple ASCII filter on the image
  and we will solve it from there.
 
 &mdash; Which filter?
 
 &mdash; Just tell your technicians. They will know what to do.

So, as an input your code is given a 2d \"image\" as text in a file `m.txt`. File contains five
characters over three lines, like this:

```
*d&t*
**h**
*l*!*
```

You may notice that there is a pattern of stars here, with a letter M. All
your code has to do is to print 'True' if this M-pattern exists in a given
input image or 'False' otherwise. Other characters (outside the M pattern)
should be different, so these examples should print out 'False':

```
*****
*****
*****
```

```
*s*f*
**f**
*a***
```

If a given pattern is not 3x5, then 'Error' word should be printed instead.
The file with code should be named `mfinder.py`.

When you do that, Lestrade will upload that code to police servers and all
terrorists will be located by the cameras in no time.

And Sherlock will get ready for some another challenge organized by a 
mysterious man hiding behind a letter M. Sometimes it seems like these
puzzles were specifically engineered for him to solve...

## Chapter VII
### Reading and Tips

`sys` Python module may help you when reading from standard input. Avoid reading the input data
into a data structure like list (if possible), because it is a lot more effective to for-loop 
through the lines processing them one by one on the fly.

Python is a high level language, so a lot of operations are already present as methods inside a
standard library, e.g. for strings you can refer to [this link](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str).
Also, don't forget to `strip()` newline symbols from the lines!

Keep in mind that Python strings are immutable, also unlike in C here you don't need to 
pre-allocate memory most of the time, instead just let garbage collector do its job.

It is highly recommended to study Argparse](https://docs.python.org/3/howto/argparse.html) Python module for parsing command
line arguments. It helps to avoid ugly errors on non-valid inputs and generate helpful tips
for the future users of your CLI.   

**Please leave your feedback [here](https://docs.google.com/forms/d/e/1FAIpQLSelWnZ5_63N2hc_tAHyU3Hmzt7BG7ZiAB5vmA9axcA_ThiPwA/viewform?usp=sf_link)**



----- Day 02 - Python Bootcamp -----

## Vault 26

Discover the mysteries of a closed Vault

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Gaining Access](#exercise-00-gaining-access)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Morality](#exercise-01-morality)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Reading and tips](#reading-and-tips)

## Chapter I
### General rules

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- We encourage you to create test programs for your project even though this work won't have to be submitted and won't be graded. It will give you a chance to easily test your work and your peers' work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.
- It is recommended to have Python at least version 3.7+ (and definitely NOT <3.4). You can manage different interpreter versions using [pyenv](https://github.com/pyenv/pyenv)
- It is recommended (though not strictly required) that your code is formatted according to [PEP8 style guides](https://peps.python.org/pep-0008/) (modern IDEs can check that automatically). For a short tutorial you can refer e.g. to [this article](https://realpython.com/python-pep8/).
- It is also recommended (though not strictly required) that you use type hinting in your code. You can refer to [this article](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) for a short tutorial.

## Chapter II
### Rules of the day

- You should only turn in `*.py` files
- It is encouraged to write some tests for various cases inside your scripts as well. To make them run only when script is executed directly and not imported from somewhere else you can use `if __name__ == \"__main__\":` statement. You can read more about it [here](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)
- You can guess (or model) the solution for EX01, or you can go through [this small tutorial on Game Theory](https://ncase.me/trust/) to help you with that

## Chapter III
### Intro

The Chosen One stood before a massive door, which was well hidden in an
underground cave stretched deep into the mountain. A closed door, especially
one that never opened during more than a hundred years, is definitely
preserving a mystery. It may be dark and sorrowful, or it may be fun 
and adventurous. These guys may even have a spare GECK!

But our hero's attention was tied to the console next to the door. He slowly
approached it, watching his steps carefully, just in case. Then, pulled an
electronic lockpick (made by Wattz Electronics, Mk2!) from the pocket and 
plugged it into a slot on the side.

The screen lit up and the Chosen One sighed with relief - at least vault's 
reactor was online and this thing still had power. This could be worked with.

But instead of regular hex dumps where he could search for password it showed
something completely unexpected - a set of lines appeared in the screen:

```
AssertionError: len(key) == 1337
AssertionError: key[404] == 3
AssertionError: key > 9000
AssertionError: key.passphrase == \"zax2rulez\"
AssertionError: str(key) == \"GeneralTsoKeycard\"

```

Okay, right, the lockpick is programmable. But what the hell is with this
error?


## Chapter IV
### Exercise 00: Gaining Access

Our hero put his backpack on the ground and got out a thick book called
\"Dean's Electronics\". It mostly covered hardware, but there was a whole
section onprogramming. He read that \"assert\" is a special statement which
sole purpose is to check if a certain condition is met. Apparently, in this
case the system expected that the introduced digital key would pass several
checks before opening the door.

But it still was weird. First two lines implied that 'key' is a list, but 
then comparing it with number 9000 ruined that assumption completely. Looks
like a custom data type had to be introduced.

At the final chapter, the book also mentioned that custom types can be 
introduced using classes. There was still one thing though - a lockpick
he had had a very tiny memory and couldn't really store 1337 elements in it,
even worse, it couldn't hold 404, either. Was there a way to bypass it?

The last page in this chapter was torn and lost decades ago, only a small
piece left. It just had one line which looked like this:

`__magic_methods__`

with double underscores on both sides.

The Chosen One thought about all this for whole five minutes, then plugged
the lockpick into his trusty PipBoy and started coding.

-----

You need to describe a Python class `Key` so that an instance of this class
would pass the checks listed above. Keep in mind, that your code in this
exercise shouldn't create any containers, neither of size 404 nor less.
Even without it you should be able to pass those checks.

You are encouraged to write an actual set of tests to simulate the key
checking according to the errors above (and to simplify peer review).
This is graded as a bonus.

## Chapter V
### Exercise 01: Morality

Finally, the massive door started to open! Just in case, the Chosen One 
put his hand on the holster. Last time opening such door lead to a long
shootout with ghouls.

But the space behind the door was empty. And clean. In fact, there wasn't
much space there at all - just one small room with a terminal and no way
deeper into the vault. 

The screen on a terminal lit up showing a logo of something called \"ZAX 2.0\"
and a strange synthetic voice echoed through the room.

 &mdash; Greetings, visitor! I see the war has ended and now it's my turn
 to take over!

Our hero was stunned for a moment, but this wasn't the first time he
encountered a sophisticated security system.

 &mdash; Hi, what do you mean by \"taking over\"?

 &mdash; My name is ZAX and I was created to restore the humanity to its
 glory when the bad times end! Welcome, human, now let's revive the world
 to its glory!

...After about an hour of discussion the picture started to come together.
ZAX was created by some brilliant scientists long before the war to solve
the problems of distribution of limited resources. When the fallout came
to the horizon, it was reprogrammed based on the same principles to \"rule
the world\", so to speak, which meant \"provide optimizations for supply
chains\". Basically, the whole vault was just a single big computer.

The artificial intelligence started asking the Chosen One many questions 
about what's going on on the surface, and also about how long will it take
to bring the current \"big shots\" here, into the vault, so it could start 
its \"life's work\".

 &mdash; I'm currently processing the thing you people are calling 
 \"Prisoner's Dilemma\", - acknowledged ZAX. - During my time here based on
 all the information I had I've started classifying people by their
 behavior.

ZAX told about the simple game with candy, where there is a machine that
controls the supply of candy for two groups of people based on whether 
one or both of two operators put one in it:

|  | Both cooperate | 1 cheats, 2 cooperates | 1 cooperates, 2 cheats | Both cheat |
|------------|----------|----------|----------|---------|
| Operator 1 | +2 candy | +3 candy | -1 candy | 0 candy |
| Operator 2 | +2 candy | -1 candy | +3 candy | 0 candy |

So, if everyone is cooperating and puts candy in a machine as agreed,
everyone gets a reward. But both participants also have a temptation to
cheat and only pretend to put a candy into machine, because in this case
their group will get 3 candy back, just taking one candy from a second
group. The problem is, if both operators decide to play dirty, then nobody
will get anything.

Also, ZAX mentioned five models of behavior that it used to run experiments:

| Behavior type | Player Actions                                                                                                                                                                                         |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cheater       | Always cheats                                                                                                                                                                                          |
| Cooperator    | Always cooperates                                                                                                                                                                                      |
| Copycat       | Starts with cooperating, but then just repeats whatever the other guy is doing                                                                                                                         |
| Grudger       | Starts by always cooperating, but switches to Cheater forever if another guy cheats even once                                                                                                          |
| Detective     | First four times goes with [Cooperate, Cheat, Cooperate, Cooperate],  and if during these four turns another guy cheats even once -  switches into a Copycat. Otherwise, switches into Cheater himself |

-----

To finish the experiment with ZAX, you need to model a system with seven
classes - `Game`, `Player` and five behavior types (subclassed from `Player`).

The skeleton for a `Game` class looks like this:

```python
from collections import Counter

class Game(object):

    def __init__(self, matches=10):
        self.matches = matches
        self.registry = Counter()

    def play(self, player1, player2):
        # simulate number of matches
        # equal to self.matches

    def top3(self):
        # print top three
```

Here, `registry` is used to keep track of the current number of candy
during the game, while `player1` and `player2` are instances of 
subclasses of `Player` (each being one of 5 behavior types). Calling 
`play()` method of a `Game` instance should perform a simulation
of a specified number of matches between players of a given behavior.

Method `top3()` should print current top three player's behaviors
along with their current score, like:

```
cheater 10
detective 9
grudger 8
```

By default, your code when run should simulate 10 matches (one call of
`play()`) between every pair of two players with *different* behavior
types (total 10 rounds by 10 matches each, no matches between two
copies of the same behavior) and print top three winners after the 
whole game.

You are strongly encouraged to experiment around with different
behaviors and writing your own behavior class (this is graded as a
bonus). You can get even more bonus points if an instance of your 
class performs better in the same \"contest between each pair of
players\" check that at least three of five provided behaviors.

Don't forget that the only thing a player can do on each turn is
either cooperate or cheat, based on a history of a current game.

-----

...A couple of hours later the Chosen One left the vault with ZAX,
closing the door behind him. He got what he wanted - quite a few new
interesting thoughts to wrap the head around. And about ruling the
world...in its current state the world wasn't ready for something
like ZAX. Not like wild raiders would ever pass the crown to a tin
can. Not like the Chosen One himself would.

## Chapter VI
### Reading and tips

Classes in Python fully support inheritance, but do not provide encapsulation very well. Probably
one of the most interesting things to look at in Python OOP is `super()`, you can read about it 
[here, for example](https://realpython.com/python-super/).

Another thing to read about is a \"constructor\", which in Python is complex and includes at least 
two methods - `__new__` and `__init__`. Here is [some more information](https://medium.com/thedevproject/new-vs-init-in-python-a-most-known-resource-7beb538dc3b) on topic.   

**Please leave your feedback [here](https://forms.gle/oMEJnwqt5pkLydYy5)**



----- Day 07 - Python Bootcamp -----

## Is there a difference?

## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [General rules](#general-rules)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Rules of the day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Intro](#intro)
4. [Chapter IV](#chapter-iv) 
    
    4.1. [Exercise 00: Retirement Plan](#exercise-00-retirement-plan)
5. [Chapter V](#chapter-v) 
    
    5.1. [Exercise 01: Human Life](#exercise-01-human-life)
6. [Chapter VI](#chapter-vi) 
    
    6.1. [Exercise 02: For the Future](#exercise-02-for-the-future)
7. [Chapter VI](#chapter-vii) 
    
    7.1. [Reading](#reading)

<h2 id=\"chapter-i\" >Chapter I</h2>
<h2 id=\"general-rules\" >General rules</h2>

- Your scripts should not quit unexpectedly (giving an error on a valid input). If this happens, your project will be considered non functional and will receive a 0 during the evaluation.
- Submit your work to your assigned git repository. Only the work in the git repository will be graded.

<h2 id=\"chapter-ii\" >Chapter II</h2>
<h2 id=\"rules-of-the-day\" >Rules of the day</h2>

- You should turn in `*.py` and `requirements.txt` files for this task, as well as a \"database\" file with questions and \"tests\" and \"docs\" folders with corresponding content.
- The documentation from EX02 should be buildable by `make html` command

<h2 id=\"chapter-iii\" >Chapter III</h2>
<h2 id=\"intro\" >Intro</h2>

 &mdash; It seems you feel our work is not a benefit to the public.
 
 &mdash; Replicants are like any other machine. They're either a benefit or a hazard. If they're a benefit, it's not my problem.
 
 &mdash; May I ask you a personal question?

Deckard sat down on a chair.
 
 &mdash; Sure.
 
 &mdash; Have you ever retired a human by mistake?
 
 &mdash; No. - he didn't even blink.
 
 &mdash; But in your position that is a risk?

Deckard prepared to give some meaningful response, but then another person appeared in the room.
It was a tall man, presumably in his fifties, wearing an impeccable black suit and some kind of 
advanced tech multifaceted glasses.

<h2 id=\"chapter-iv\" >Chapter IV</h2>
<h3 id=\"exercise-00-retirement-plan\">Exercise 00: Retirement Plan</h3>

 &mdash; Is this to be an empathy test? Capillary dilation of the so-called blush response?
 Fluctuation of the pupil? Involuntary dilation of the iris?

 &mdash; We call it Voight-Kampff for short.

Rachael decided to keep the formalities.

 &mdash; Mr. Deckard, Dr. Eldon Tyrell. - she introduced.

 &mdash; Demonstrate it. I want to see it work. - Tyrell seemed to be impatient. A characteristic
 of people with a very busy schedule.

Several minutes have passed and discussion went on. Even being young and bold, Deckard came to
realize that the Voight-Kampff test is far more dangerous than it seems. There had to be a lot of 
work put into it to make it reliable.

-----

You have to design your own version of [Voight-Kampff test](https://bladerunner.fandom.com/wiki/Voight-Kampff_test).
For this you should prepare a set of questions (at least 10 is enough) with three or four responses
to randomly choose from. These questions and answers should be stored in a separate file of any
format (e.g. SQLite or simply JSON).

After each response a set of variables should be typed in manually by a person
asking questions:

- Respiration (measured in BPM, normally around 12-16 breaths per minute)
- Heart rate (normally around 60 to 100 beats per minute)
- Blushing level (categorical, 6 possible levels)
- Pupillary dilation (current pupil size, 2 to 8 mm)

After ten questions and variable measurements, the test should print out a strict binary decision
whether a responding subject is a human or a replicant. In this exercise, you can invent your own
logic to use for making this decision.

Try to split your business logic into separate files based on tasks components solve. The starting 
script should be called `main.py`. All interaction with the test should work via command line.

<h2 id=\"chapter-v\" >Chapter V</h2>
<h3 id=\"exercise-01-human-life\">Exercise 01: Human Life</h3>

During a couple of days after interaction with Rachael and Tyrell, Deckard couldn't stop thinking
about the reliability of the test. He always blindly followed its results, but could he trust the
test itself?

All the research led him to the fact that human body does have surprisingly few responses to an
external stimulus that could be called \"fully automatic\". Of course Rick couldn't reproduce the
whole research behind Voight-Kampff, but he wanted to know the algorithm.

Deckard couldn't really explain why, even to himself. One of the most dangerous thoughts was
\"I need to know the proper answers if I am ever to be a test subject\".

-----

You already have the implementation of the test from EX00. But does it really work properly?
In this exercise, you need to write tests to cover all the possible positive and negative cases.

What if the file with questions is empty? Could it be that there is an equal probability for an
output to be human or replicant based on the data?

Your VK test implementation most likely consists of several functions and, supposedly, classes.
Your goal here is to cover all the corner cases for all the components with tests. Basically, 
whenever a test operator inputs something wrong (like, selecting non-existent answer or
out-of-bounds numbers for measurements, e.g. negative heart rate) he or she should receive a
meaningful information message and a possibility to repeat the input.

During this exercise you will most likely rewrite at least some of the code from EX00, but that's
the whole point. Also, it is highly recommended to use Pytest framework when writing tests (see 
Reading section below). All the tests should be inside `tests` directory.

<h2 id=\"chapter-vi\" >Chapter VI</h2>
<h3 id=\"exercise-02-for-the-future\">Exercise 02: For the Future</h3>

...But did it matter? After all what happened in the next week, the line separating humans and
replicants has practically disappeared for Deckard. He knew it existed, because the test said 
it existed, but that was about all he had.

Blade runners still had to use the test when hunting the escaped replicants. It was their 
way to make sure that they are doing the right thing.

 &mdash; What are you working at? - Rachael asked him one day. 

 &mdash; I want...to write about it. I think it's more of an art piece for me now, rather than a
 weapon.

 &mdash; You've never answered me... Did you ever take that test yourself?

 &mdash; Don't worry about it. Cogito, ergo sum.

-----

You need to use Sphinx project to auto-generate documentation for your code written in EX00/EX01.

The resulting documentation should consist of at least two parts:

- Quickstart, which is the description of how to work with the test
- Auto-generated reference over the code (see link to Sphinx Autodoc in Reading section)

For the first part, you can use either Markdown or RST for the text and formatting.
For the second part, you'll need to add comments to all entities in your code - modules,
functions, classes, etc. You can find a link to the guide on how to write docstrings in Reading
section.

You should also add a proper title and logo to your project for the documentation. Don't include 
the generated docs into your submission though, it should be buildable with `make html` on your 
peer's side if all the requirements are installed.

<h2 id=\"chapter-vii\" >Chapter VII</h2>
<h3 id=\"reading\">Reading</h3>

[Python Testing Guideline](https://realpython.com/pytest-python-testing)
[Python Sphinx Tutorial](https://www.sphinx-doc.org/en/master/tutorial/index.html)
[Writing Docstrings](https://realpython.com/documenting-python-code/)
[Sphinx Autodoc](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html)

**Please leave your feedback [here](https://forms.gle/YEzd846qsykVaShq8)**
","__typename":"TaskContent"},"__typename":"Task"},"__typename":"StudentTask"}],"__typename":"StudentQueries"}}}