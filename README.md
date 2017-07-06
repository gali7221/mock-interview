* Full Stack Mock Interview

*** What is the most influential book or blog post you’ve read regarding web development?
- A memorable post about web development, or rather, technology was the pursuit of proficiency. The blog spoke about not to overwhelm yourself with every latest new technology - the technologies keep coming and keep bombarding. You will always have time to learn the technologies, but if you focus on foundations, fundamentals, and the evolution of web development your ability to learn and grow as a developer will speed up exponentially. Technology is an ever expanding and changing, and the ability to keep up will almost certainly be overwhelming. Understand the basis of web development and the purpose it serves. What is its purpose, and what challenges does it face? Of course, there will always be a problem. But as web development expands, the fundamentals never change. I, as a fanatic developer, will be put into a better position if I understand the fundamentals. Picking up the hot new technology will inconvenience me in only implementation. This has totally shifted my perception and approach to learning anything. It has also decreased the stress and overwhelming feeling I get when I find out there is a new framework.

*** Tell me about a web application you have built. Why did you choose to build it? What did you learn? What challenges did you face and how did you overcome them?
- A fascinating project I built was a blogging application built with a Python back-end through the Udacity Full Stack Web Nanodegree. Why I built it was because they told me to build it - my knowledge of developing a back-end project was extremely minimal, and so I dived into an online course I felt had validity. The course was my first taste of the back-end. The course was taught by Steve Huffman, and he gave great detail of where Web Development was, and where it is now. The project wasn’t by any means an especially elegant project, but it did allow me to understand the challenges developers were struck with in the face of large projects - we used no framework. We built a minimal blogging post - along the lines of Medium, where users logged-in/out, created posts, liked posts, and commented. We built the majority of the project with Huffman. Once the course ended our assignment was to build the “Comment” and “Like” functionalities.  It was cool, and it felt wonderful to be out in the wild, so to speak. What I learned - documentation is a beautiful thing.  I took for granted these two very common characteristics of social media applications, and I thought nothing of it. But when you begin working and seeing how the DB relates with the code, you increasingly become overwhelmed and feel haunted. I was at a complete loss, until I took an iterative approach. I broke down what needed to be done, and used everything I knew to slowly build up. I used the forums, I used the Google Cloud documentation, and before I knew it I was completely done and felt I could finally take over the world. I think I might try to do that one day.

*** Write a function in Python that takes a list of strings and returns a single string that is an HTML unordered list (< ul > ... < /ul >) of those strings. You should include a brief explanation of your code. Then, what would you have to consider if the original list was provided by user input?

```
def ulify(list):
  string = "<ul>\n"
  for s in list:
      string += "<li>" + str(s) + "</li>\n"
  string += "</ul>"
  return string
```

So, I first created a string that is set to a "<ul>" and followed by a endline mark.
I then iterate over the list and add to the string with "<li>" + str(s) + "</li>"
-- this will ensure that we will have each item in the list be a list item and on its own line - for readability.
I finally return the string.


If the original list was provided by a user it is important to check if all items inside the list were actually a string. For this I added the str(s) as to ensure proper coercsion.


*** List 2-3 attacks that a web applications are vulnerable to. How do these tasks work?
-  SQLi (sql injection) - "is a code injection technique that exploits a security vulnerability occurring in the database layer of the application”. What this essentially means is that the user(attacker) will inject sql code as user input inside query string. SQLi are very much capable of manipulating data such as the CRUD/corrupt database tables. For example - if user is expected to create a username and a password which is often queried by the database. A classic query would be SELECT ID from users where name = $name AND Password = $password. Instead a users input for his/her username is 1 OR 1 = 1;  When the DB queries it will now look like this - SELECT ID from users where name = 1 OR 1 = 1; -  AND Password = $password. THe user has now entered input that is very similar to a DB Query and will and can have adverse effects on the DB! - In this case the 1 ALWAYS equals 1 and the clause is an OR every row will be displayed to the user. You should also consider if a user were to input something like DROP TABLE users “, - this will delete the entire users db. - To counterattack SQLi it is best to use prepared statements. This allows the DB to know the format of the query
-  XSRF(Cross-site Request Forgery) - considered one of the more easy to create attack vector. As a user navigates to GMAIL (Application A) and leaves the site open while opening a new tab and navigates to another site. What you are now vulnerable to is allowing Application B to fire requests (HTTP request to the gmail servers with the code embedded onto an image tag) towards Application A with your privileges. Of course the longer you stay logged in and navigate to other applications the higher the risk. Any tag which fires a request to an external resource can be used to perform hidden XSRF attack, i.e. - image, tags, links, meta tags,   GET & POST are do not make a difference in the effectiveness of the attack.


*** Expand on the starter code and include a route that simulates rolling two dice and returns the result in JSON. You should include a brief explanation of your code.

```
from flask import Flask, jsonify
app = Flask(__name__)

import random


@app.route('/roll/<int:n>/json/')
def rollDice(n):
    rolls = []
    for i in range(n):
        roll = []
        roll.append(random.randint(1, 6))
        roll.append(random.randint(1, 6))
        rolls.append(roll)
    return jsonify(rolls=rolls)

if __name__ == '__main__':
    app.debug = True
    app.run(host='0.0.0.0', port=5000)
```

# Here I have set an argument to to the number of times a two dice will be rolled.
# Each roll will then be appended to an inner list - each inner array will be portray
# one roll of two dices
# 1. The function first declares an array - this array will hold all of the inner rolls
# 2. We then iterate until the number of rolls specified
# 3. we declare another array at the top of the iteration - this is because we will need to reset the array so we can have a new couple of numbers to display.
# 4. we will append a random number from 1-6 (which is the number of sides of a standard die)
# 5. and then finally append it to the base array
# 6. we return the json of the rolls.
