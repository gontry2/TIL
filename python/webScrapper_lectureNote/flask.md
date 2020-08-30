# Flask

> scrapper를 webserver에 넣는 작업

* micro-framwork



```python
from flask import Flask

app = Flask("SuperScrapper")

@app.route("/")
def home():
    return "<h1>Job Search</h1><form><input placeholder='What job do you want?'required/><button>Search</button></form>"

#@app.route("/<username>")
#def contact(username):
#    return f"Hello {username} how are you doing"

# on repl.it 
app.run(host="0.0.0.0")

```



```html
<!-- templates/home.html -->
<!DOCTYPE html>
<html>
    <head>
        <title>Job Search</title>
    </head>
    <body>
        <h1>
            Job Search
        </h1>
        <form action="/report" method="get">
            <!-- query argument -->
            <input placeholder="Search for a job" required name="word"/>
            <button>
                Search
            </button>	
        </form>
    </body>
</html>
```



```python
from flask import Flask, render_template, request, redirect

app = Flask("SuperScrapper")

@app.route("/")
def home():
    return render_template("home.html")

@app.route("/report")
def report():
    word = request.args.get('word')
    if word:
        word = word.lower()
    else:
        return redirect("/")
    return render_template("report.html", searchingBy=word)

# on repl.it 
app.run(host="0.0.0.0")

```



```html
<!-- templates/report.html -->
<!DOCTYPE html>
<html>
    <head>
        <title>Job Search</title>
    </head>
    <body>
        <h1>
            Search Results
        </h1>
        <h3>
            You are looking for {{ searchingBy }}
        </h3>
    </body>
</html>
```



```python
# main.py
from flask import Flask, render_template, request, redirect, send_file
from scrapper import get_jobs
from exporter import save_to_file

app = Flask("SuperScrapper")

# make scrapper fast(fake db)
# server mamory
db = {}

@app.route("/")
def home():
    return render_template("home.html")

@app.route("/report")
def report():
    word = request.args.get('word')
    if word:
        word = word.lower()
        existingJobs = db.get(word)
        if existingJobs:
            jobs = existingJobs
        else:
        	jobs = get_jobs(word)
        	db[word] = jobs
    else:
        return redirect("/")
    return render_template("report.html", searchingBy=word, resultNumber=len(jobs), jobs=jobs)

@app.route("/export"):
    try:
    	word = request.args.get('word')
        if not word:
            raise Exception
         word = word.lower()
         existingJobs = db.get(word)
         if not existingJobs:
            raise Exception
         save_to_file(existingJobs)
         return send_file("jobs.csv")   		            
    except:
        return redirect("/")
        

# on repl.it 
app.run(host="0.0.0.0")

```



```html
<!-- templates/report.html -->
<!DOCTYPE html>
<html>
    <head>
        <title>Job Search</title>
    	<style>
            section {
                display: grid;
                gap: 20px;
                grid-template-column: repeat(4, 1fr);
            }
        </style>
    </head>
    <body>
        <h1>
            Search Results
        </h1>
        <h3>
            Found {{ resultNumber }} results for: {{ searchingBy }}
        </h3>
        <a href="/export?word={{ searchingBy }}">Export to CSV</a>
        <section>
        	<h4>Title</h4>
            <h4>Company</h4>
            <h4>Location</h4>
            <h4>Link</h4>
            {% for job in jobs%}
                <span>{{ job.title }}</span>
                <span>{{ job.company }}</span>
                <span>{{ job.location }}</span>
                <span><a href="{{ job.link }}" target="_blank">Apply</a></span>
            {% endfor %}
        </section>
    </body>
</html>
```



출처: [노마드 아카데미(Python으로 웹 스크래퍼 만들기)](https://nomadcoders.co/python-for-beginners/lobby)

