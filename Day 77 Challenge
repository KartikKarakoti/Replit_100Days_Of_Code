from flask import Flask, redirect

app = Flask(__name__, static_url_path="/static")


@app.route('/')
def index():
    page = ""
    return page

@app.route("/blog/hello")
def hr():
  return redirect("/hello")

@app.route("/blog/bye")
def br():
  return redirect("/bye")

@app.route('/hello')
def hello():
    title = "Hello World"
    date = "October 25th"
    text = "Here is my first blog entry."
    page = ""
    f = open("template/blog.html", "r")
    page = f.read()
    f.close()
    page = page.replace("{title}", title)
    page = page.replace("{date}", date)
    page = page.replace("{text}", text)
  
    return page

@app.route('/bye')
def bye():
    title = "Bye World"
    date = "October 25th"
    text = "Here is my last blog entry."
    page = ""
    f = open("template/blog.html", "r")
    page = f.read()
    f.close()
    page = page.replace("{title}", title)
    page = page.replace("{date}", date)
    page = page.replace("{text}", text)
  
    return page
  
app.run(host='0.0.0.0', port=81)
