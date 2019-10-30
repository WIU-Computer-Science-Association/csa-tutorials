# Using PRAW with Flask
Link to Google Slides Version: [Link](https://docs.google.com/presentation/d/1OvNt9Jb6Ws40oBtm-90g90jYna1ARKAS4ZXezwaaTv0/edit#)
Link to Gitlab Repository: [Link](https://gitlab.wiu.edu/aj-kulpa/flask_tutorial)

## Prerequisites
You will need:
  * Python version: 2.7, 3.3, 3.4, 3.5, or 3.6
  * Reddit Account 
  * Client ID,  Client Secret, User Agent
  * PRAW
      * `pip install praw`

You will also need (NEW):
  * Flask
    * `pip install flask`
  * Basic Front-End Web Development understanding

## Overview
  * Python Quick Review
  * Using Reddit API with PRAW Review
  * Add Reddit Bot functions
  * Review Flask 
  * Use functionality in Flask Web-server

## Python Quick Review
### Conditional Statements
```python
If condition:
    # do something
elif condition2:
    # do something else
else:
    # do something else else
```

### Loops
```python
while(condition):
    #do this while condition=true

For x in object:
    #iteratively do something
```

### Variables
```python
Word = ‘string’ 
Word1 = “string”
Words = [“x”,”y”,”z”]
Num = 1
```

### Functions
```python
def main():
    print(“hello world”)
main()
```

### Classes
```python
class exampleClass():
 def __init__(self):
     #initialization (constructor) code
     self.variableExample = ‘something’
 def anotherFunction(self, argument):
    print(argument)
```


## Using Reddit API with PRAW Review
### Steps to get you started again

* Import the python reddit wrapper:
	* `import praw`
* Import your configuration:
	* `From CONFIG import *`
* Setup authentication using constants from config.py.
	* `reddit = praw.Reddit(user_agent = USER_AGENT, client_id = CLIENT_ID, client_secret = CLIENT_SECRET, username = USERNAME, * password = PASSWORD)`
* Add functionalities!
	* `do_something()`

### All Together
```python
import praw ## The library we’re using!
From CONFIG import *


def main():
# setup authentication using constants from CONFIG.
reddit = praw.Reddit(user_agent = ‘LMGTFY (by /u/csa_bot_example)’, client_id = CLIENT_ID, client_secret = CLIENT_SECRET, username = USERNAME, password = PASSWORD)
do_something() ## Your functionalities!

def do_something():
# If printing something, encode it using ‘OBJECT.encode(“utf-8”)

if __name__ == ‘__main__’:
    main()
```

## Add Reddit Bot Functions

## Review Flask

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions.

### Basics of Using Flask
To use it, you must install it.
  * `pip install flask`

Then import it.
  * `from flask import Flask, render_template`

Setup basic Flask components (sample code)
```python
from flask import Flask, render_template # Import Flask and the html template renderer

# “Flask uses the import name ‘__name__’ to know where to look 
#  up resources, templates, static files, instance folder, etc.”
app = Flask(__name__) 

@app.route('/') #example 1, main index using html files
def index(): #Setup function to call when HOST/ visited
    return render_template("FILE.html", KEY = VARIABLE) # Display HTML using Jinja

@app.route('/WEB_PATH') # example 2, using plaintext
def test(): #Setup function to call when HOST/WEB_PATH visited
    return "HTML TEXT HERE!" # Display webpage with only this text

if __name__ == '__main__': # If python running the file as the main program
    app.run(debug = True, host='0.0.0.0') # run the app in debug mode; locally
```

### Basics of Jinja
Basic HTML Structure ( + Jinja)
```html
<html>
 <head>
  <title>WEBSITE TITLE</title>
 </head>
 <body>
  CONTENT
  {% block body_append %}{% endblock %}
 </body>
</html>
```

Basic Jinja Extension
```html
{% extends "layout.html" %}
{% block body %}
  <ul>
  {% for var in vars %}
    <li>
<a href="{{ var.url }}">{{ var.x }}</a>
</li>
  {% endfor %}
  </ul>
{% endblock %}
```


## Use Reddit Bot in Flask

  * Import PRAW bot file:
    * `Import FILE_NAME`
  * Create new web-app route
	```python
		@app.route('/reddit')
		def reddit_bot():
			#FUNCTIONALITIES HERE :)
	```
  * Use PRAW bot functions:
    * `variable = FILE_NAME.function(parameter)`
      * e.g. `submissions = reddit.get_top_100_stocks_submissions()`
  * Pass Variables to Jinja Template:
    * `return render_template('TEMPLATE.html', key = variables)`
      * e.g. `return render_template('reddit.html', submissions = submissions)`

## What's Next?
  * Run it! (`python simple_webserver.py`) ← Link to Gitlab repository
  * Add Functionalities:
    * Sentiment checking (Sentiment140)
    * Filtering for Stock mentions (ftp://ftp.nasdaqtrader.com/symboldirectory)
    * Impact-on-brand rating (Estimates using info from PRAW)
    * Remote web-server access (Ngrok)
    * More social-media crawling (Tweepy)
    * Long-term analysis (via data in database - Pymysql)
    * Exporting into dynamic webpages for each stock (Flask)
    * Easy as setting dynamic paths via:
      * `@app.route(“/stocks/<stock_name>”)`
      * `def stock_report(stock_name)`

